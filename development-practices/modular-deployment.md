# Modular Deployment

Typically, version control repository for Salesforce is organized by components classified by each metadata type. For example, the following image shows all the apex classes in the org are placed under the 'classes' directory.

![All classes in the org placed in a single 'classes' folder](<../.gitbook/assets/image (48) (1).png>)

Propagating a change from a repository organized by components can either done by deploying all the components in the repository or by doing a selective deployment of the changed components. A full deployment of repository is not feasible once the size of the repository grows beyond 10,000 files as Salesforce has a limit on the number of files that can be deployed in one deployment, and this will result in considerable waste of time as your entire repository is deployed.

This can be optimized by two approaches

#### 1. Selective Deployment of Changed Components

A selective deployment of only the changed components, the selection could be automated by utilizing diffs between git commits or by using change sets.

This model has the following issues on a large repository:

* Increased complexity of automation, as each deployment unit is a dynamic and unique (depending on the changed components), scripts need to probe the components inside the unit to determine whether to trigger an automation or not.
* Rollback complexity is increased, as rolling back to an earlier release is not possible using the last deployed unit i.e. each deployment unit is unique, and components gets only included in the deployment unit if it is changed
* Deprecating or removing components is typically handled as an out of process activity that needs a different workflow outside a CI/CD pipeline and reduces the overall velocity
* Managing lifecycle of individual components is a complex affair, this results in components that are not deprecated
* Full Local Unit Tests have to be triggered on every deployment or selective tests need to be identified that helps with deployment of changes

#### 2. Deployment of Modules

A module, be it second generation [unlocked package](types-of-packaging/unlocked-packages.md),[ org dependent unlocked package](types-of-packaging/unlocked-packages.md) or [source package](types-of-packaging/source-packages.md) is an alternate approach for selective deployment. A module is a collection of metadata types that are grouped together in terms of the functionality provided. For example, a logging framework as a module will consist of the apex classes, objects, or any other automation that pertains to logging. A module is deployed in its entirety and the lifecycle of a module is maintained as opposed to individual components.

A modular deployment provides the following benefits:

* Enhanced capabilities around lifecycle management, components that are no longer part of the module can be automatically removed from the org
* Rollbacks are much more feasible, as each deployment unit of the module has the entire components required for it to be functional
* A pre-validated module such as an Unlocked package can be installed in any org without triggering unit tests
* Can be propagated to multiple orgs with strong dependency management

It is often seen that **Option 1** is adopted across Salesforce ecosystem as it provides an immediately perceived increase in deployment velocity, but selective deployment without organizing into functional blocks over a longer time slows the development/deployment velocity **by increasing the cognitive overhead on development, testing and release management teams.**, think 1000 apex classes in a single folder!

The modules should be aligned with various domains and functionality the org caters to. This will also allow one to achieve the following benefits:

* Utilize a release management which is centred around versioned modules as opposed to components, ensuring faster deployments that are traceable to versioned artifacts.
* Validate each module individually and promote a validated module through the path to production, reducing further testing cycles
* Reduce cognitive overhead for developers making a change
