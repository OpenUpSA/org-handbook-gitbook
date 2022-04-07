# Password management

We use BitWarden for password management.

We organise passwords according to&#x20;

* unit - for passwords shared with everyone in that unit
* project - for passwords shared with everyone in the project

Bitwarden can "nest" collections using forward-slashes (`/`) in the name, and creating a collection for each level in the hierarchy.&#x20;

![](../.gitbook/assets/Screenshot\_2022-04-07\_13-23-46.png) ![](../.gitbook/assets/Screenshot\_2022-04-07\_13-25-47.png)

{% hint style="info" %}
**Collection permissions are not inherited.** Collection nesting is just to visually group related collections.&#x20;

Giving someone access to the `projects` collection does not mean they have access to all collections under `projects`.
{% endhint %}
