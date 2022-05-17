---
description: The DX@Scale CI/CD Orchestrator
---

# sfpowerscripts

sfpowerscripts is an end-to-end build and deployment orchestrator for modular development on Salesforce that can be implemented in any CI/CD platform of choice.&#x20;

## **Key Features**

* Utilises sfdx-project.json ([Salesforce DX Project Configuration](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_ws\_config.htm)) as the source of truth for driving the build system, ensuring incredibly minimal maintenance on projects and programs often dealing with multiple number of packages
* Builds packages in parallel by respecting dependencies
* Ability to selectively build changed packages in a [mono repo](https://en.wikipedia.org/wiki/Monorepo)
* Ability to deploy only packages that are changed in repo
* Pooling commands to prepare a pool of scratch orgs with packages pre-installed for optimized Pull/Merge Request Validation
* Artifacts Driven, all create commands produce an artifact or operate on an [artifact](https://github.com/dxatscale/dxatscale-guide/blob/april-22/ci-cd/broken-reference/README.md)
* Integrate with any CI/CD system of choice
* Generate changelogs for each release
* All commands are instrumented providing [metrics](https://github.com/dxatscale/dxatscale-guide/blob/april-22/ci-cd/broken-reference/README.md) about various aspects of your CI/CD

sfpowerscripts is built with these key principles to align with the vision of DX@Scale

## Ease of use

The tasks or commands should be easy to use. You don't need to resort to complex scripts to build a pipeline. A knowledge of what you need to achieve from a pipeline and Salesforce development (such as [Salesforce DX](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_intro.htm), [Unlocked Package](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_unlocked\_pkg\_intro.htm)/[Org Based Deployment Model](https://trailhead.salesforce.com/content/learn/modules/org-development-model) or a Hybrid where you combine both\*) should be enough to get you going.

We will also strive to provide sample pipelines to quickly get you started. **For sample pipelines checkout this** [**repo**](https://github.com/dxatscale/dxatscale-template)\*\*\*\*

\*If you need a refresher on Salesforce DX, Unlocked Packages or Org Based Deployment, checkout some of the available trailhead modules [here](https://trailhead.salesforce.com/en/users/azlam/trailmixes/salesforce-dx)

## Everything is a package

sfpowerscripts is built on the concept of generating artifacts for package creation tasks, unlocked or not, which then could be versioned, uploaded into an artifact provider or utilised in subsequent release stages for deployment across environments.

The following package creation commands shows this in action

* Create Source Package
* Create Unlocked Package (inluding Org dependent unlocked packages)
* Create Data Package, for Records Based Configuration, such as vlocity datapacks

![](<../.gitbook/assets/image (41).png>)

These commands create an artifact named`<package_name>_sfpowerscripts_artifact_<ver>.zip`. This zip file contains the following items

| Item                      | Description                                                               |
| ------------------------- | ------------------------------------------------------------------------- |
| artifact\_metatadata.json | A JSON based manifest that contains information about the package         |
| changelog.json            | A JSON based schema that carries all commit description about the package |
| source                    | A directory containing the metadata in source format                      |

## Optimised for speed without hampering traceability

One of the frequent questions that is often asked to us is:

_**Does deploying packages compared to delta deployments (deploys only what is changed between two commits or a range of commits) make the overall deployment slower?**_

As packages are always deployed in its entirety, this is an understood fact, read more about it [here](../development-practices/modular-deployment.md). sfpowerscripts will always be built with features to optimize for speed but still ensuring the org is traceable compared to the traditional happy soup model most organisations are burdened with today.

Features currently enabling this principle include

* All sfpowerscripts package creation commands feature a diff check, which builds the package only if it detects a change
* Packages will only be installed in the org, if the given package is not installed in the org
* Support for mono repository, while working with multiple packages reduces overhead and overall complexity

Of course, the onus is on developers to granulize packages, so that this could be achieved, but be assured the tooling is available.

Learn more about sfpowerscripts here

{% content-ref url="../projects/sfpowerscripts/features.md" %}
[features.md](../projects/sfpowerscripts/features.md)
{% endcontent-ref %}
