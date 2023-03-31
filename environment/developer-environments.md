# Developer Environments

Scratch orgs are one of the best features that Salesforce released, where they re-imagined the developer experience on the platform. Scratch orgs are ephemeral orgs that can be provisioned as a just-in-time environment, which can be populated with metadata and data from source control repository. This allows one to be in control of the metadata and data that needs to be provisioned in the orgs as opposed to sandboxes (which are either a clone of another sandbox or created from production).

Scratch orgs helps to create environments at any specific point in time in your version control, and results in an interesting side effect, i.e. significant reduction in manual steps, as the whole objective is to get an org ready for development just from code



{% embed url="https://twitter.com/dxatscale/status/1485701086878961664?s=20&t=evQTq447ilXDZYHotw_www" %}

{% hint style="info" %}
DX@Scale utilizes scratch org's as preferred mechanism for developer environments, with a scratch org being utilized for each individual work item. Sandboxes with source tracking could be utilized in a similar fashion, However there is limited tooling support.
{% endhint %}
