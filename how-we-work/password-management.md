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

We try to follow the principle of least privilege, meaning you should only have access to passwords you actually need. To avoid creating multiple shared accounts on the same service, please add any accounts that relate to your unit's work to the [Service Accounts](what-do-we-use-for.../#service-accounts) table, and please document when it is the preferred tool for the job in the table above it. Before creating a new account, check if there is an existing account you can get access to and reuse. Duplicate accounts can waste money and effort.

We organise shared passwords according to:

* unit - for passwords shared with everyone in that unit, e.g. comms, dev, finance
* project - for passwords shared with everyone in the project

Bitwarden can "nest" collections using forward-slashes (`/`) in the name, and creating a collection for each level in the hierarchy.&#x20;

![](../.gitbook/assets/Screenshot\_2022-04-07\_13-23-46.png) ![](../.gitbook/assets/Screenshot\_2022-04-07\_13-25-47.png)

{% hint style="info" %}
**Collection permissions are not inherited.** Collection nesting is just to visually group related collections.&#x20;

Giving someone access to the `projects` collection does not mean they have access to all collections under `projects`.
{% endhint %}

### Adding users

Invite new users to the organisation. Once they've accepted, they will have an account and can store passwords for themselves, but they aren't part of the organisation yet.

These users will be listed as `accepted` in the organisation user list. You can accept them into the organisation by confirming their Bitwarden [fingerprint](https://bitwarden.com/help/fingerprint-phrase/) after selecting `Confirm` in the menu next to their name. They can find their fingerprint on their user profile in BitWarden. It is not secret.

![After this, it will ask you to confirm their Bitwarden fingerprint.](../.gitbook/assets/Screenshot\_2022-04-07\_14-16-50.png)

Once they are confirmed, add them to any collections they need access to by clicking on their name and checking the relevant collection boxes.

Everyone should have access to

* project
* unit

and then any specific units and projects they need to access.

![](../.gitbook/assets/Screenshot\_2022-04-07\_14-30-10.png)

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

