# Managing Profiles

We would recommend profiles to be version controlled, but the approach should ensure permissions configuration provides the level of flexibility required for the organization.

As mentioned in the [repo structure](../scm/repository-structure.md), profiles need to be placed in src-access-mgmt.

DX@Scale's tooling provides support for version controlling profiles. Please read the following article to gain a quick intro how the tools work.

{% content-ref url="../media-library/knowledge-articles/version-controlling-profiles-and-why-it-makes-sense-for-deployments.md" %}
[version-controlling-profiles-and-why-it-makes-sense-for-deployments.md](../media-library/knowledge-articles/version-controlling-profiles-and-why-it-makes-sense-for-deployments.md)
{% endcontent-ref %}

Depending on your permissions strategy, one of the following approaches may be advisable:

* **Admin-managed profiles**. Here profiles are considered under the responsibility of an admin who can make changes without impacting functionality or having these changes overwritten. With this approach profiles are treated as [org-specific metadata](https://docs.dxatscale.io/scm/dealing-with-sensitive-metadata), and settings like IP range restrictions can be added manually in production. This would usually be preferable in a multi-org deployment or an environment where admins should retain flexibility over all aspects of permissions in the org.
* **Source-managed profiles**. Under this approach profiles are treated as core to the application and changes driven from a single [source package](https://docs.dxatscale.io/development-practices/source-packages) definition. It's advisable here to use profiles to control only the minimal settings which cannot be provided through permission sets (e.g. page layout assignments, record type & app defaults and login restrictions) so admins have flexibility to control as much as possible by extending access using permission set combinations. This might be preferable in a single-org deployment where centralized control over permissions is desirable and settings like login IP ranges are static do not need to differ by org.

While using a scratch org based development, there is no specific need to use sfpowerkit command such as retrieve as normal sfdx push/pull would be suffice. sfpowerscripts automatically does a reconcile against the target org when the profile is deployed.
