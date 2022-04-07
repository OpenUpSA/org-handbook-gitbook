# Password management

We prefer **not** using shared accounts where possible. We use shared accounts when the plan we can afford to use of a given service does not allow individual accounts for enough users to be practical for our needs.

You should definitely get a dedicated account for any django/flask app we develop.

{% hint style="info" %}
**Use a password manager.** We recommend that you use bitwarden or your favourite password manager for managing your own passwords of services you use in your work at OpenUp.

A password that is reused between services, or that is a small variation of a password you use in another service, is **not secure**.&#x20;

**We owe it to our beneficiaries, clients and reputation as an organisation that can navigate the world of technology to use secure passwords.**

Secure passwords are complex randomly-generated text which you can't remember (but use a password manager to look up), or unique complex text like the first letter of each word (or the full words!) of a long sentence. **So just use a password manager** and use a long phrase for your password in it.
{% endhint %}

## Sharing passwords

We use BitWarden for shared password management.&#x20;

We organise shared passwords according to:

* unit - for passwords shared with everyone in that unit, e.g. comms, dev, finance
* project - for passwords shared with everyone in the project

Bitwarden can "nest" collections using forward-slashes (`/`) in the name, and creating a collection for each level in the hierarchy.&#x20;

![](../.gitbook/assets/Screenshot\_2022-04-07\_13-23-46.png) ![](../.gitbook/assets/Screenshot\_2022-04-07\_13-25-47.png)

{% hint style="info" %}
**Collection permissions are not inherited.** Collection nesting is just to visually group related collections.&#x20;

Giving someone access to the `projects` collection does not mean they have access to all collections under `projects`.
{% endhint %}

### Credentials used by our software

Developers will need to deploy credentials via Ansible.

Secure Note type items seem to work best for these kinds of credentials. Use a custom text field for the non-sensitive values, and a hidden field for API keys, passwords and other sensitive values.

![](../.gitbook/assets/Screenshot\_2022-04-07\_13-18-20.png) ![](../.gitbook/assets/Screenshot\_2022-04-07\_13-02-18.png)

We usually organise these credentials in an environment collection under the relevant project collection, and named after the service, e.g. under `project/municipal-money` we have `prod`, `staging` and `sandbox` matching the environment names used in the ansible inventory. Ansible can then use this name to select the right credential for each environment.

![](../.gitbook/assets/Screenshot\_2022-04-07\_13-55-28.png)

Make sure the item is named consistently across environments so that the same service can be accessed using only an environment name variable in the collection name.

```
"{{ lookup('bitwarden', 'POSTGRES', field='fields.hostname', collection='project/municipal-money/' ~ env_name) }}"
```

