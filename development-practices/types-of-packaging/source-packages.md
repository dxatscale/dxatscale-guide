# Source Packages

Source Packages is an [sfpowerscripts](https://sfpowerscripts.dxatscale.io) construct which wraps the Salesforce Metadata (in [source format](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_source\_file\_format.htm)), along with [sfdx-project.json](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_ws\_config.htm), some additional metadata information (such as commit id, branch, tag, etc.) in a versioned zip file (artifact), which can be deployed to a Salesforce Org using sfpowerscripts package release command.

Source Packages are metadata deployments from a Salesforce perspective, it is a group of components that are deployed to an org. Unlocked packages are a **First Class** Salesforce deployment construct, where the lifecycle is governed by the org, such as deleting/deprecating metadata and validating versions.

We always recommend using unlocked packages over source packages whenever you can. As a matter of preference, this is our priority of package types

1. [Unlocked Packages](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_unlocked\_pkg\_intro.htm)
2. [Unlocked Packages (Org-Dependent)](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_unlocked\_pkg\_org\_dependent.htm)
3. Source Packages

Source Packages are typically used for application-config (configuring an application delivered by a managed package such as changes to help text/description of fileds ) or when you come across these constraints

* [Metadata not supported by Unlocked Packages](https://developer.salesforce.com/docs/metadata-coverage)
* Facing bugs while deploying the metadata using unlocked packages
* Unlocked Package validation takes too long (still we recommend go org-dependent)
* Dealing with metadata that is global or org-specific in nature (such as queues, profiles, etc or composite UI layouts, which doesn't make sense to be packaged using unlocked package)
* Development teams who are starting to adopt package-based development and want to organize their metadata

## How are Source Packages different from deploying a folder using source:deploy?

Well, no difference, internally sfpowerscripts is using the same command to deploy it into the Salesforce org.

## Why I should be using Source Packages instead of deploying a folder?

We have added some additional enhancements that make it worth taking a look at:

* **Ability to skip the package if already installed:** By keeping a record of the version of the package installed in the target org with the support of an unlocked package, sfpowerscripts can skip installation of source packages if it is already installed in the org
* **Optimized Deployment Mode:** sfpowerscripts package installation commands can auto-detect apex unit tests provided in the package, thus a package can be deployed to an Org by utilizing only the apex test classes provided in the package (provided each class is having a code coverage of 75% or more by the apex classes in the package) thus saving time spend on triggering local tests of all the apex classes in an org for every source packages in your repo
* **Versioned Artifact:** Aligned with sfpowerscripts principle of traceability, every deployment is traceable to a versioned artifact, which is difficult to achieve when you are using a folder to deploy

## How do Source Packages compare against Unlocked Packages?

Source Packages are metadata deployments from a Salesforce perspective, it is a group of components that are deployed to an org. Unlocked packages are a first class Salesforce deployment construct, where the lifecycle is governed by the org, such as deleting/deprecating metadata and validating versions.

## When should I be using Source Packages over Unlocked Packages?

We always recommend using unlocked packages over source packages whenever you can. As a matter of preference, this is our priority of approach packages.

1. [Unlocked Packages](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_unlocked\_pkg\_intro.htm)
2. [Unlocked Packages (Org-Dependent)](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_unlocked\_pkg\_org\_dependent.htm)
3. [Source Packages](https://github.com/dxatscale/dxatscale-guide/blob/april-22/development-practices/types-of-packaging/broken-reference/README.md)
4. [Change Sets](https://help.salesforce.com/articleView?id=changesets.htm\&type=5)

Source Pages are typically used when you come across these constraints

* [Metadata not supported by Unlocked Packages](https://developer.salesforce.com/docs/metadata-coverage)
* Facing bugs while deploying the metadata using unlocked packages
* Unlocked Package validation takes too long (still we recommend go org-dependent,)
* Dealing with metadata that is global or org-specific in nature (such as queues, profiles etc or composite UI layouts., which doesn't make sense to be packaged using unlocked package)

## **What are my options with Source Packages?**

sfpowerscripts source packages support the following exclusive options in addition to other options supported by the orchestrator commands.

All these currently available options that can be enabled for source packaging by adding to the package descriptor in the sfdx-project.json file.

* **Optimized Deployment (`isOptimizedDeployment:<boolean>)`:** Control the behaviour of testing of source packages during deployment, utilize the org's coverage or better have apex unit tests that have 75% or more coverage for each class carried in the source package. Any source packages that do not have apex classes/triggers will be deployed without triggering tests
* **Aliasify (`aliasfy:<boolean>`)** : Aliasify enables deployment of a subfolder in a source package that matches the target org. For example, you have a source package as listed below. During Installation, only the metadata contents of the folder that matches the alias gets deployed.  If the alias is not found, sfpowerscripts will fallback to the '**default**' folder.  If the default folder is not found, an error will be displayed saying default folder or alias is missing.

![source Packages with env-specific-folders](<../../.gitbook/assets/2022-05-26\_10-53-34 (1).png>)

* **Skip Testing ( `skipTesting:<boolean>`)** : Allows you to deploy a source package without triggering test to an Org. Please note, this is only applicable during deployments to sandboxes. Apex tests are mandatory (if your package contains apex classes/triggers) during deployment to production.
* **Reconcile Profiles ( `reconcileProfiles:<boolean>`) :** By default, true, automatically reconcile a profile existing in the source package against the target org. Read more about reconcile option [here](https://github.com/Accenture/sfpowerkit/discussions/410).
* **Apply Destructive Changes ( `destructiveChangePath:<path>)`**: Allows you to deploy a destructive manifest that need to be applied before deploying the package.

```
  {
    "path": "path--to--package",
    "package": "name--of-the-package", //mandatory, when used with sfpowerscripts
    "versionNumber": "X.Y.Z.0", //Pass the build number flag to override zero
    "aliasfy": <boolean>, // Only for source packages, allows to deploy a subfolder whose name matches the alias of the org when using deploy command
    "isOptimizedDeployment": <boolean>  // default:true for source packages, Utilizes the apex classes in the package for deployment,
    "skipTesting":<boolean> //default:false, skip apex testing during installation of source package to a sandbox
    "skipCoverageValidation":<boolean> //default:false, skip apex coverage validation during validation phase,
    "destructiveChangePath:<path> // only for source, if enabled, this will be applied before the package is deployed
    "assignPermSetsPreDeployment: ["","",]
    "assignPermSetsPostDeployment: ["","",]
    "preDeploymentScript":<path> //All Packages
    "postDeploymentScript:<path> // All packages
    "reconcileProfiles:<boolean> //default:true Source Packages 
  }
```

## How do source packages manage to skip installation if it's already deployed in a org?

This functionality only works provided, the target org has sfpowerscripts-artifact' (04t1P000000ka9mQAA) package installed. You need to install the package to every target org (including your production environment). The command for installing this package is as follows

```
sfdx force:package:install --package 04t1P000000ka9mQAA -u <org> -w 10
```

If your prefer to install a package from your own DevHub rather than this package, you could do by building a package from the source provided at the [URL](https://github.com/Accenture/sfpowerscripts/tree/develop/prerequisites/sfpowerscripts-artifact). Once this package is built, you can override sfpowerscripts to use this package by passing in the the environment variable SFPOWERSCRIPTS\_ARTIFACT\_UNLOCKED\_PACKAGE

## **Can I have an entire org composed of Source Packages?**

Of course, you can, you would get traceability in terms of packages in your CI/CD pipelines, and some nice functionality, however, the benefits of validating dependencies and modular development would not be fully realized. There is also associated danger, as there is no locks associated with source packages, so another source package with same metadata component can overwrite a metadata component deployed by another package. For these, reasons, we always prefer unlocked packages.

An example of a common metadata component that typically gets overridden is [Custom Labels](https://developer.salesforce.com/docs/atlas.en-us.api\_meta.meta/api\_meta/meta\_customlabels.htm) which can span across multiple packages.

## How do I delete components deployed through an earlier version of Source Packages?

By utilizing a destructive manifest file, one could delete metadata components during a Source Package Installation. Add the `destructiveChangePath` in the package descriptor by directing to the path to the file that carries information on the component that needs to be uninstalled.

## Can I have dependencies for source packages?

**Short answer no**, source packages assume that dependent metadata is already there in your org before the metadata in the source package is being deployed. That being said, for purposes of development in scratch org, you could add '**unlocked package'** dependencies to a source package, so commands like prepare and validate (in sfpowerscritpts:orchestrator) will install the dependencies to the scratch org.

## Why is the version number for source packages have to end with zero? Doesn't it support .next?

At the moment, it is not supported. So ensure that all your source packages in your repository has '0' as placeholder for the build number which can be replaced by a build number passed as a flag by the build command Make sure to use the right variable name according to your CI/CD system, the sample below describes how to pass the build number using GITLAB CI/CD.

```
sfdx sfpowerscripts:orchestrator:quickbuild --buildnumber ${CI_JOB_ID} --configfilepath config/scratch-org-def.json --diffcheck --branch develop
```
