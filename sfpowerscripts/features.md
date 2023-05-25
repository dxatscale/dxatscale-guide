---
description: Learn about all the features in sfpowerscripts
---

# Features

## **Boost your Productivity!**

* Enable Developers to create an org the way they want it utilizing a mono repository, significant gains in productivity removing the need for working across multiple repositories at the same time
* No distinction between package type(s), handle all of them at ease from a single repository
* Simple to use CLI commands that can be operated from your terminal

## **Don’t spend your days fighting YAML/Bash Scripts!**

* Enhance your sfdx-project.json to orchestrate validation, build and deployment, acting as source of truth for everything about a package.
* “Thou shall not leave sfdx-project.json” – Zero intervention required on your pipeline when you add or remove packages

## **Don't wait for a Dev Environment!**&#x20;

* Prepare your scratch orgs with all the packages, data and serve it at an instant with Developer Pools and Source tracking.

## **Instantaneous CI Environments!**

* Prepare a pool of Scratch Org’s to act as a just in time CI orgs, reducing a significant amount of time during the validation phase
* Connect multiple stages to prepare environments to ensure developer environments are created within your CI/CD agent's time limits

## **Shift Left... We got it Right!**

* Ability to validate only changed packages against a pool of pre-prepared scratch org, saves time!
* Ability to validate only changed components from a changed package ensuring quick deployability check
* Detect and trigger tests that are only impacted by the change
* Validate metadata coverage for packaging, only package components what you should\* (sfpowerkit).
* Static Analysis using PMD\* (sfpowerkit)
* Automatically identify test classes within a given package, validate test coverage before a package is being built.

## **Faster Builds... Less slack time!**

* Parallelized Package Builder that steps through building packages by understanding dependencies
* Build packages that are only changed, saving significant amount of time
* Automated resolution of package version numbers of dependencies to ensure packages are built with the right versions during parallel builds
* Handle multiple .forceignore files depending on stage (development vs validation vs build)
* Bundled Package Builds (build a group of package, if any one of them changes)

## **Deploy with confidence!**

* Deploy only packages that are changed
* Ability to deploy a set of packages by comparing against a baseline org
* Always deploy a package if required
* Skip deployment of a package on a particular org
* Reconcile profiles automatically for source packages
* Assign PermSets before or after deployment of a package
* Run pre/post scripts for each package

## **Track like a Boss!**

* Automated Release Notes Generator
* Track Linked Work Items along with commits made to each package
* Automated Release Definition Generator

## **Observability at its Best**

* All functionality instrumented with StatsD, as well as Log Based metrics to build dashboards the way you want it.
* Native integration with DataDog/NewRelic
