---
description: The DX@Scale CI/CD Orchestrator
---

# Overview

An end-to-end build and deployment orchestrator for modular development on Salesforce that can be implemented in any CI/CD platform of choice.&#x20;

## **Key Features**

* Utilizes sfdx-project.json ([Salesforce DX Project Configuration](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_ws\_config.htm)) as the source of truth for driving the build system, ensuring minimal maintenance on projects and programs often dealing with multiple number of packages
* Builds packages in parallel by respecting dependencies
* Ability to selectively build changed packages in a [mono repo](https://en.wikipedia.org/wiki/Monorepo)
* Ability to deploy only packages that are changed in a mono repo
* Ability to toggle between package validation modes during pull-requests (PRs) against scratch org prepared earlier in pool.
  * **Individual -** ignore packages installed in scratch org, identify list of changed packages from PR/Merge Request, and validate each of the changed packages (respecting any dependencies) using **thorough** mode.
  * **Fast Feedback -** skip package dependencies and code coverage and selective test class executions, install only changed components, and ignore changes in package descriptors  **** &#x20;
  * **Thorough (default)** - include package dependencies, code coverage, all test classes during full package deployments
  * **Fast Feedback Release Config** - extension of fast feedback mode but filtered using release configuration file that defines list of packages to validate with only changed packages ending up being used to validate against the scratch org
  * **Thorough Release Config** -  extension of thorough default mode but filtered using release configuration file that defines list of packages to validate with only changed packages ending up being used to validate against the scratch org
* Pooling commands to prepare a pool of scratch orgs with packages pre-installed for optimized Pull/Merge Request Validation
* Artifacts Driven, all create commands produce an artifact or operate on an artifact
* Integrate with any CI/CD system of choice
  * Templates currently supported are GitHub, GitLab, and Azure DevOps
* Generate Change Logs for each release
* All commands are instrumented providing metrics about various aspects of your CI/CD

sfpowerscripts is built with these key principles to align with the vision of DX@Scale

## Ease of Use

The tasks or commands should be easy to use. You don't need to resort to complex scripts to build a pipeline. A knowledge of what you need to achieve from a pipeline and Salesforce development (such as [Salesforce DX](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_intro.htm), [Unlocked Package](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_unlocked\_pkg\_intro.htm)/[Org Based Deployment Model](https://trailhead.salesforce.com/content/learn/modules/org-development-model) or a Hybrid where you combine both\*) should be enough to get you going.

We will also strive to provide sample pipelines to quickly get you started. **For sample pipelines checkout this** [**repo**](https://github.com/dxatscale/dxatscale-template)\*\*\*\*

\*If you need a refresher on Salesforce DX, Unlocked Packages or Org Based Deployment, checkout some of the available trailhead modules [here](https://trailhead.salesforce.com/en/users/dxatscale/trailmixes/sfdx-devops-starter-pack).

## Everything is a Package

sfpowerscripts is built on the concept of generating artifacts for package creation tasks, unlocked or not, which then could be versioned, uploaded into an artifact provider or utilized in subsequent release stages for consistent deployment across environments.

The following package creation commands shows this in action

* Create Source Package
* Create Unlocked Package (including Org-dependent Unlocked Packages)
* Create Data Package, for Records Based Configuration, such as Vlocity datapacks

![](<../.gitbook/assets/image (11) (2).png>)

These commands create an artifact named`<package_name>_sfpowerscripts_artifact_<ver>.zip`. This zip file contains the following items

| Item                      | Description                                                               |
| ------------------------- | ------------------------------------------------------------------------- |
| artifact\_metatadata.json | A JSON based manifest that contains information about the package         |
| changelog.json            | A JSON based schema that carries all commit description about the package |
| source                    | A directory containing the metadata in source format                      |

## Optimized for Speed Without Hampering Traceability

One of the frequent questions that is often asked to us is:

_**Does deploying packages compared to selective/git diff deployments (deploys only what is changed between two commits or a range of commits) make the overall deployment slower?**_

As packages are always deployed in its entirety, this is an understood fact, read more about it [here](../development-practices/modular-deployment.md). sfpowerscripts will always be built with features to optimize for speed but still ensuring the org is traceable compared to the traditional happy soup model most organizations are burdened with today.

Features currently enabling this principle include:

* All sfpowerscripts package creation commands feature a diff check, which builds the package only if it detects a change
* Packages will only be installed in the org, if the given package is not installed in the org
* Support for mono repository, while working with multiple packages reduces overhead and overall complexity

Of course, the onus is on developers to granulize packages and understand how their feature fits into the overall solution and will be stored in the mono-repository.  Tools are available but developers must commit to the new modular development best practices. &#x20;

The following sections provide further details into the commands and usage of sfpowerscripts.

