# Pooling Scratch Orgs

Scratch Org pools help development teams to solve the time taken to spin up a scratch org, install all dependencies and make it ready for development.  Another use case for Scratch Org Pools is for a just in time CI environment. The following links discuss how DX@Scale's tooling \(sfpowerkit and sfpowerscripts\) enable scratch org pools.

{% page-ref page="../media-library/knowledge-articles/scratch-org-pooling-for-ci.md" %}

{% page-ref page="../media-library/knowledge-articles/scratch-org-pooling-for-development.md" %}

The following sections deal with the typical pool strategies followed by DX@Scale practitioners.

### Number of Pools Required

DX@Scale at the minimum require about 3 pools to be created. These pools serve different purposes and is been detailed below

* **CI/CD pools with full packages installed** This particular pool is the one typically used for validation runs.  This pool will be utilizing source packages of the latest validated packages from the particular repository and optimizes the validation stage to only validate a package that is changed, providing maximum time savings
* **CI/CD pools with only dependencies installed** This is the non-default pool, which will only have managed packages installed and usually utilized only when there are changes that require none of the packages to be pre-installed \(This is mainly needed due to bugs in scratch org, such as the one where picklist value changes always result in validation failures, when it is deployed on top of an existing package\). A switch to this pool is typically handled by using a specific commit message or a pipeline runtime variable.
* **Developer Pool** These are the pools that will be used by developers. This is pretty similar to CI/CD pools with only dependencies installed, however, due to an implementation difference, these scratch orgs have to be provisioned using sfpowerkit instead of sfpowerscripts 

The number of scratch orgs in the pool have to be determined depending on the size of the program and adjusted accordingly.

### Replenishing Pools

Scratch Org pools need to be replenished in the following manner.

* **CI/CD pools with full packages installed** Replenished periodically through out the day, completely deleted at end of the day and recreated in the very early hours of the day to provide a fresh set of pools each day. These pools will have the expiry set to 2 day only.
* **CI/CD pools with only dependencies installed** Replenished periodically through out the day, completely deleted at end of the day and recreated in the very early hours of the day to provide a fresh set of pools each day. These pools will have the expiry set to 2 day only.
* **Developer Pool** Replenished periodically through out the day, never deleted automatically. Scratch orgs are left to expire by itself. The expiry for each org is set to 7 days and developers need to be aware of the expiry and should be encouraged to work on feature/tasks that should be less than these number of days and should fetch a new org from the pool

Pipelines should be built and invoked using a scheduler to replenish the scratch orgs in the pool

### Recreating Pools

There would be situations when pools need to be killed, such as change in shape of the org or due to any other inconsistencies. This involves a significant downtime, as creating pool with full strength could take anywhere between 1-3 hours depending on the number of scratch orgs involved. This should be communicated to all the developers in the team workspace to let them know this is happening.

It is highly recommended to build a delete pool pipeline that could be triggered manually to delete all the pools.

### Monitoring Pools



