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

* **User experience is critical:** You probably don't know what's actually usable as well as you think you do.
* \*\*\*\*[**Easy dev**](development-guidelines.md#easy-development-setup)**:** It should be easy to get a project up and running in a development environment.
* \*\*\*\*[**Automate testing**](development-guidelines.md#automated-tests)**:** If a feature is worth implementing, it's worth having automated tests for it
* \*\*\*\*[**Code is intended to be read by humans**](development-guidelines.md#code-is-intended-to-be-read-by-humans): Otherwise we'd keep assembly in git instead of source code.
* \*\*\*\*[**Time boxes**](development-guidelines.md#time-boxes)**:** Don't spend unbounded time on a problem.
* \*\*\*\*[**Tracer bullets**](development-guidelines.md#tracer-bullets)**:** Don't leave the end-to-end functionality for last.
* [**Automate repetition**](development-guidelines.md#automate-repetition)**:** Automate the things you do repetitively.
* **Fail loudly:** Brokenness should be visible.
* \*\*\*\*[**Tend towards best practices**](development-guidelines.md#tend-towards-best-practises)**:** Don't do sweeping dramatic changes that never get finished.

### Easy development setup

### Automate testing

### Code is intended to be read by humans

* Use full versions of command arguments in scripts, e.g. `--tries=5` instead of `-t5`

### Time boxes

### Tracer bullets

### Automate repetition

### Brokenness should be visible

* Never catch and drop exceptions without logging them.
* Ensure shell scripts fail on error instead of running through with undefined behaviour. use `set -eux`  in bash.
* Add uptime monitoring to public services and ensure we get emailed when a service goes down.

### Tend towards best practices



## Further reading

* [The Twelve-Factor App](https://12factor.net/) - Lots of clear, specific best practices for building maintainable services
* [The Pragmatic Programmer](https://pragprog.com/titles/tpp20/the-pragmatic-programmer-20th-anniversary-edition/) - Techniques for productively building software that don't get old
* [Clean Architecture](https://blog.cleancoder.com/uncle-bob/2011/11/22/Clean-Architecture.html) - No, it's not outdated. It's just about separating business logic from data, network, and presentation stuff.





