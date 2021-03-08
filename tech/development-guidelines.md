# Development guidelines

OpenUp's context is somewhat different to industry, and in particular our projects are a different scale to typical software industry projects.

* The tech side of our projects is rarely big enough to keep one software developer busy full time for a month
* We can not have a big in-house permanent staff of developers because our projects are very dependent on partners, clients, funding and other opportunities.
* We have multiple projects running at the same time
* The same people often have to be involved in several projects at the same time
* We often have to pause development on a project for a few weeks and then come back to it
* Our project budgets are relatively small, but we are very ambitious about what we want to achieve with the available funding. This should be as quick and easy as possible.

This context means that most industry best practises are even more important to us. Most of our guidelines stem directly from industry best practises. Where we deviate from that, it's even more important to explain why we have a guideline or best practise.

## Guidelines

* **Always deliver something:** Prefer releasing something very basic over ending a sprint with only unreleased partial work.
* \*\*\*\*[**User experience is critical**](development-guidelines.md#user-experience-is-critical)**:** You probably don't know what's actually usable as well as you think you do.
* \*\*\*\*[**Easy dev**](development-guidelines.md#easy-development-setup)**:** It should be easy to get a project up and running in a development environment.
* \*\*\*\*[**Automate testing**](development-guidelines.md#automated-tests)**:** If a feature is worth implementing, it's worth having automated tests for it
* \*\*\*\*[**Code is intended to be read by humans**](development-guidelines.md#code-is-intended-to-be-read-by-humans): Otherwise we'd keep assembly in git instead of source code.
* \*\*\*\*[**Time boxes**](development-guidelines.md#time-boxes)**:** Don't spend unbounded time on a problem.
* \*\*\*\*[**Tracer bullets**](development-guidelines.md#tracer-bullets)**:** Don't leave the end-to-end functionality for last.
* [**Automate repetition**](development-guidelines.md#automate-repetition)**:** Automate the things you do repetitively. Don't automate prematurely.
* \*\*\*\*[**Fail loudly**](development-guidelines.md#fail-loudly-brokenness-should-be-visible)**:** Brokenness should be visible.
* \*\*\*\*[**Tend towards best practices**](development-guidelines.md#tend-towards-best-practises)**:** Avoid attempting sweeping dramatic changes that never get finished.

### User experience is critical

Don't assume just because you know how to use something, a user will know how to use it.

We often develop frontends using Webflow to maximise the flexibility for the designer and make iteration on the user interface as rapid as possible.

See our introductory talk on [our approach using webflow and user-centred design](https://za.pycon.org/talks/25-a-month-in-the-life-of-people-who-sprinkle-tech-webflow-django-and-users/).

### Easy development setup

A developer should be able to clone a repository and have a working site running locally by running a few commands.

#### Frontend

* Backing data from an API should probably default to production, if a production service is available.
* The backing API should be configurable via 
  * environment variable \(semi-permanently e.g. for staging\)
  * user interface \(per use - e.g. for testing a deploy preview against a staging or review app API\)
    * [https://github.com/milafrerichs/dev-tools/](https://github.com/milafrerichs/dev-tools/)
    * [Javascript prompt\(\) and session storage](https://github.com/OpenUpSA/muni-portal-frontend/blob/a8dd961eccc0438520702c8fef3a61f35db17855/src/js/api.js#L6)
    * Do not allow this to be configured by querystring - this risks introducing an injection vulnerability 

#### Backend

Use [our cookiecutter template](https://github.com/OpenUpSA/cookiecutter-django-dokku) for django apps.

* Use docker-compose for development so that database or other backend service dependencies don't make it hard to get up and running.
  * Yes, this adds a layer of indirection. But have you battled with GDAL or wkhtmltopdf version issues? Also, if all our projects are structured this way, moving between projects becomes quick.
  * By following [Twelve Factor Apps](https://12factor.net/), those who really want to run natively just need to provide configuration and it should work.
* Use a seed data fixture for standard data like categories that could be used to seed production.
* Use a demo data fixture for fake data e.g. pages, indicator values, etc.
* Load and smoke-test your fixtures in CI to ensure they are kept functional. 

### Automate testing

### Code is intended to be read by humans

* Use full versions of command arguments in scripts, e.g. `--tries=5` instead of `-t5`
* Consistency and context is more important than personal preference
* Javascript: 
  * We prefer the [AirBnB Javascript style guide](https://github.com/airbnb/javascript/blob/master/README.md)
    * See the [eslint plugin](https://www.npmjs.com/package/eslint-config-airbnb)
* Python:
  * Use [isort](https://pypi.org/project/isort/) for imports, followed by [python-black](https://pypi.org/project/black/) so that black formatting takes precedence 

### Time boxes

### Tracer bullets

### Automate repetition

### Fail loudly \(Brokenness should be visible\)

* Never catch and drop exceptions without logging them.
* Ensure shell scripts fail on error instead of running through with undefined behaviour. use `set -eux`  in bash.
* Add uptime monitoring to public services and ensure we get emailed when a service goes down.
* App startup should fail if required variables are not set, rather than providing a default value that doesn't actually work. e.g. use `env.str("AWS_ACCESS_KEY_ID")` with no default so that the app doesn't start if this environment variable is not set. This means deployment of a new feature/to a new environment fails with a clear indication of the problem, rather than succeeding but with core functionality not being available. This, along with seamless deploys, means a new deployment without the required config won't kill a good working previous deploy.

### Tend towards best practices

Avoid trying to make everything "compliant" with our coding standards at once. It will be more complex than you expect, and you'll get stuck, and all your effort will be wasted because you will run out of time and get nothing merged.

At least don't worsen the quality of the codebase. Discuss extreme circumstances where we might choose to introduce technical debt with the project lead developer.

#### Automated fixes touching the whole codebase

Apply automated fixes like introducing a formatter in one pull request per introduced tool to minimise the time it spends under review, and thus to minimise the merge conflicts with other work in progress. Speak to the rest of the team to coordinate the best time to make these changes.

#### Manual improvements

Apply manual improvements like refactoring and improving test coverage as part of normal business, e.g. adding a feature or fixing a bug. Only improve the code you're touching in this change. This is generally the sweet spot for getting improvements done without causing additional pain. It means improvements get done without scope getting expanded without bound.

Every change is additional effort for the person reviewing your code and risks introducing new bugs. Don't put a task at risk because you're refactoring something totally unrelated.



## Further reading

* [The Twelve-Factor App](https://12factor.net/) - Lots of clear, specific best practices for building maintainable services
* [The Pragmatic Programmer](https://pragprog.com/titles/tpp20/the-pragmatic-programmer-20th-anniversary-edition/) - Techniques for productively building software that don't get old
* [Clean Architecture](https://blog.cleancoder.com/uncle-bob/2011/11/22/Clean-Architecture.html) - No, it's not outdated. It's just about separating business logic from data, network, and presentation stuff.





