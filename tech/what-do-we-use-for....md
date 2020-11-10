# Preferred tech stack

## Software/web development and hosting

### General

<table>
  <thead>
    <tr>
      <th style="text-align:left">Task</th>
      <th style="text-align:left">Preferred tool</th>
      <th style="text-align:left">Pros</th>
      <th style="text-align:left">Cons</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Domain Registration</td>
      <td style="text-align:left">domains.co.za</td>
      <td style="text-align:left">Local, lots of our domains already there</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">DNS</td>
      <td style="text-align:left">Cloudflare</td>
      <td style="text-align:left">Supports apex domain aliases (Regularly resolves the provded hostname
        to serve an A record as if it&apos;s a CNAME)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Configuration management</td>
      <td style="text-align:left"><a href="https://github.com/OpenUpSA/ansible-config/">Ansible</a>
      </td>
      <td style="text-align:left">One authoritative representation of how an app should currently be deployed.
        Deploying additional instances is trivial</td>
      <td style="text-align:left">It only works if we keep it up to date</td>
    </tr>
    <tr>
      <td style="text-align:left">Secrets management (for things needed when we deploy apps)</td>
      <td style="text-align:left"><a href="https://github.com/OpenUpSA/secrets_store">Passwordstore</a>
      </td>
      <td style="text-align:left">Built on simple principles. Very secure.</td>
      <td style="text-align:left">Not really usable by non-technical people</td>
    </tr>
    <tr>
      <td style="text-align:left">Running apps on servers</td>
      <td style="text-align:left">dokku</td>
      <td style="text-align:left">
        <ul>
          <li>Standardised configuration storage</li>
          <li>Automated HTTP proxy to docker containers</li>
          <li>Seamless deploy with smoke tests</li>
          <li>Easy TLS</li>
        </ul>
      </td>
      <td style="text-align:left">Not suitable for every situation</td>
    </tr>
    <tr>
      <td style="text-align:left">Databases that accept writes at runtime</td>
      <td style="text-align:left">PostgreSQL</td>
      <td style="text-align:left">Has JSONB field types where optional nested fields can be indexed</td>
      <td
      style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Databases that accept writes at data-loading events</td>
      <td style="text-align:left">SQLite</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Website monitoring</td>
      <td style="text-align:left">uptimedoctor.com</td>
      <td style="text-align:left">Most affordable, does the job</td>
      <td style="text-align:left">Apart from the subject line and a basic status, alert emails are not super
        helpful, e.g. don&apos;t include the actual URL checked.</td>
    </tr>
    <tr>
      <td style="text-align:left">Error alerting</td>
      <td style="text-align:left">sentry.io</td>
      <td style="text-align:left">
        <p>Very helpful request and error data capture/presentation,</p>
        <p>Aggregating many instances of the same error (as opposed to 1000 emails
          of the same issue)</p>
        <p>Open Source sponsorship for team account</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### Software/web development stack

Please discuss deviations from our standard stack options in [\#technology-advice-grp](https://openupsa.slack.com/archives/CBL958RME).

See _**Tech to try**_ in our [Tech Infrastructure backlog](https://trello.com/b/3lVjXyzc/tech-infrastructure) for exploring alternatives to these.

| Name | Components | Good for | Bad for | Dev costs | Running costs |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Webflow static site, webflow-hosted | Webflow | Visually appealing sites | Frequent content edits | Webflow designer time | $12/m annual; $15/m monthly |
| Webflow static site, static-hosted | Webflow, static hosting | Visually appealing sites, free hosting | Frequent content edits | Webflow designer time | Free - updates require developer to redeploy \(30 minutes\) |
| Webflow CMS | Webflow | Visually appealing sites, easy content management | more than 2000 data items | Webflow designer time | $16/m annual; $20/m monthly |
| Webflow frontend as Django templates | Webflow, Django | Visually appealing sites, social-sharing metadata, thousands to millions of data items | Hosting has an operations overhead | Webflow designer time, Django developer time, Javascript developer time | ~$5 per month + hosting operations |
| Webflow frontend as Single Page App | Webflow, API backend \(probably Django\) | Visually appealing sites, independence of frontend and backend developer, thousands to millions of data items | Hosting has an operations overhead | Webflow designer time, Django developer time, Javascript developer time | ~$5 per month + hosting operations |

### Django apps

Our preferred way to structure and use django apps is documented and templated using our [Django Cookiecutter](https://github.com/OpenUpSA/cookiecutter-django-dokku)

