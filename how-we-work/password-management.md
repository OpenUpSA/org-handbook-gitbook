# Password management

We use BitWarden for password management.

We organise passwords according to:

* unit - for passwords shared with everyone in that unit, e.g. comms, dev, finance
* project - for passwords shared with everyone in the project

Bitwarden can "nest" collections using forward-slashes (`/`) in the name, and creating a collection for each level in the hierarchy.&#x20;

![](../.gitbook/assets/Screenshot\_2022-04-07\_13-23-46.png) ![](../.gitbook/assets/Screenshot\_2022-04-07\_13-25-47.png)

{% hint style="info" %}
**Collection permissions are not inherited.** Collection nesting is just to visually group related collections.&#x20;

Giving someone access to the `projects` collection does not mean they have access to all collections under `projects`.
{% endhint %}

## Credentials used by our software

Developers will need to deploy credentials via Ansible.

Secure Note type items seem to work best for these kinds of credentials. Use a custom text field for the non-sensitive values, and a hidden field for API keys, passwords and other sensitive values.

![](../.gitbook/assets/Screenshot\_2022-04-07\_13-18-20.png) ![](../.gitbook/assets/Screenshot\_2022-04-07\_13-02-18.png)

We usually organise these credentials in an environment collection under the relevant project collection, and named after the service, e.g. under `project/municipal-money` we have `prod`, `staging` and `sandbox` matching the environment names used in the ansible inventory. Ansible can then use this name to select the right credential for each environment.

![](../.gitbook/assets/Screenshot\_2022-04-07\_13-55-28.png)

Make sure the item is named consistently across environments so that the same service can be accessed using only an environment name variable in the collection name.

```
"{{ lookup('bitwarden', 'POSTGRES', field='fields.hostname', collection='project/municipal-money/' ~ env_name) }}"
```

