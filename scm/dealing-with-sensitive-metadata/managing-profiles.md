# Managing Profiles

Profiles in Salesforce need a special emphasis, as they are org-specific metadata and need to be version controlled. As mentioned in the [repo structure](../repository-structure.md), profiles need to be placed in src-access-management. DX@Scale's tooling provides support for version controlling profiles. Please read the following article to gain a quick intro how the tools work.  


{% page-ref page="../../media-library/knowledge-articles/version-controlling-profiles-and-why-it-makes-sense-for-deployments.md" %}

While using a scratch org based development, there is no specific need to use sfpowerkit command such as retrieve as normal sfdx push/pull would be suffice. sfpowerscripts automatically does a reconcile against the target org when the profile is deployed. 



