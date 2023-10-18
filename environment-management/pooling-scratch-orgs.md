# Pooling Scratch Orgs

Scratch Org pools help development teams to solve the time taken to spin up a scratch org, install all dependencies, load sample data and make it ready for development. Another use case for Scratch Org Pools is for a just in time CI environment. The following links discuss how DX@Scale's tooling enable scratch org pools.

{% embed url="https://medium.com/@dieffrei/introduction-to-salesforce-scratch-org-pools-e1616772499c" %}

{% embed url="https://medium.com/@dieffrei/dx-scale-scratch-org-pools-1dbecfcda8f8" %}

The following sections deal with the typical pool strategies followed by DX@Scale practitioners.

## Number of Pools Required

At the minimum, DX@Scale requires 3 pools to be created. These pools serve different purposes:

*   **CI pools with all packages installed**

    The CI pools are typically used for validation runs. They are pre-installed with the packages from the latest successful build, which allows optimised validations where only the packages that have changed are validated.
*   **CI pools with only dependencies installed**

    Scratch orgs in this pool only have managed packages installed. They are used in special cases where a clean install of all the packages is needed, such as for failures involving picklist value updates. Switching to this pool is handled by pipeline runtime variable or a specific commit message.
* **Developer Pool** These are the scratch orgs that will be used by developers to do their development work. They can either have all of the packages installed or just the dependencies.

The number of scratch orgs in the pool have to be determined depending on the size of the program and adjusted accordingly.

## Replenishing Pools

Scratch Org pools need to be replenished in the following manner.

* **CI/CD pools with full packages installed** Replenished periodically through out the day, completely deleted at end of the day and recreated in the very early hours of the day to provide a fresh set of pools each day. These pools will have the expiry set to 2 day only.
* **CI/CD pools with only dependencies installed** Replenished periodically through out the day, completely deleted at end of the day and recreated in the very early hours of the day to provide a fresh set of pools each day. These pools will have the expiry set to 2 day only.
* **Developer Pool** Replenished periodically through out the day, never deleted automatically. Scratch orgs are left to expire by itself. The expiry for each org is set to 7 days and developers need to be aware of the expiry and should be encouraged to work on feature/tasks that should be less than these number of days and should fetch a new org from the pool

Pipelines should be built and invoked using a scheduler to replenish the scratch orgs in the pool.

## Limiting Packages in Pools

As the number of packages in your repository increases, it would become a significant hurdle to build scratch org pools with all the packages in your repository.  sfpowerscripts provide options to limit the packages installed by using[ Release Config](../sfpowerscripts/release/release-config.md#release-config-file). Release config is available across most sfpowerscripts commands , including [Prepare ](../sfpowerscripts/prepare/)and [Validate](../sfpowerscripts/validate.md) enabling you to build subset of your repositories.

## Recreating Pools

There would be situations when pools need to be killed, such as change in shape of the org or due to any other inconsistencies. This involves a significant downtime, as creating pool with full strength could take anywhere between 1-3 hours depending on the number of scratch orgs involved. This should be communicated to all the developers in the team workspace to let them know this is happening.

It is highly recommended to build a delete pool pipeline that could be triggered manually to delete all the pools.

## Monitoring Pools

Scratch Org Pools can be monitored using an analytic tool like DataDog or New Relic. Check sfpowerscripts documentation to understand the [metrics](../sfpowerscripts/metrics-and-dashboards.md) emitted by sfpowerscripts. A sample dashboard is attached below

![](<../.gitbook/assets/image (84).png>)

To learn more about how to build a pool of scratch orgs using sfpowerscripts, click on the link below:

{% content-ref url="../sfpowerscripts/prepare/" %}
[prepare](../sfpowerscripts/prepare/)
{% endcontent-ref %}
