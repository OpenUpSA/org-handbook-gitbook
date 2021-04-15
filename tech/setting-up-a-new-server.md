# Setting up a new server

1. [Select a hosting provider](preferred-tech-stack.md)
2. Provision the server
   1. Set up a low CPU credit alarm if it's a t-series server on AWS
3. Configure a hostname for the server
4. [Configure operating system users on the server](https://github.com/OpenUpSA/ansible-config/#managing-admin-access-to-servers)
5. [Configure dokku if it's an application server](https://github.com/OpenUpSA/ansible-config/#install-dokku)
6. Configure port monitoring for the server

## Server hostname convention

```text
{{ project short name }}{{ server number }}-{{ provider name}}.{{ apex domain }}
```

* Project short name: e.g. `idp` for IDP Guide
* Server number: The iteration of server for that project on that hosting provider, e.g. the first idp server on aws is 1,  the second on aws is 2, then the next server could be set up on hetzner and have number 1 again
* Provider name: usually `aws` or `hetzner`
* Apex domain
  * OpenUp projects are definitely subdomains of `openup.org.za`
  * If we control the client's domain, then we put their servers on their domain as well, e.g. `pmg.org.za`
  * If we don't, then we fall back to subdomains of `openup.org.za`

Examples

* muni-portal-aws1.openup.org.za
* muni-portal-aws2.openup.org.za
* pmg1-hetzner.openup.org.za
* aws1.keepthereceipt.org.za
* idp1-aws.openup.org.za
* pmg1-aws.pmg.org.za
* justice1-hetzner.openup.org.za

