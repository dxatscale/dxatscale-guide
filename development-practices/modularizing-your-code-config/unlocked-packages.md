---
description: All the details about unlocked package
---

# Unlocked Packages

## Introduction

There is a huge amount of documentation on unlocked packages. Rather than repeating all the information here, a curated list of links are provided which every DX@Scale practitioner should be well versed with

_**The Basics**_

* [Package Development Model](https://trailhead.salesforce.com/content/learn/modules/sfdx_dev_model) 
* [Unlocked Package for Customers](https://trailhead.salesforce.com/content/learn/modules/unlocked-packages-for-customers) 
* [Successfully Creating Unlocked Package](https://www.youtube.com/watch?v=xJNmHOtIgO0)
* [Salesforce Developer Guide to Unlocked Package](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_unlocked_pkg_intro.htm)
* [Unlocked Package FAQ](https://sfdc-db-gmail.github.io/unlocked-packages/faq-unlocked-pkgs.html)

_**Advanced Materials**_

* [Anti Patterns in Package Dependency Design](https://medium.com/salesforce-architects/5-anti-patterns-in-package-dependency-design-and-how-to-avoid-them-87bb50331cb8)

The following sections deal with items that are particular to DX@Scale or more emphasis is required in large scale programs.

## What to Package

* If you have the following scenarios, it may be a good idea to put them in **domain specific packages**.
  * A group of related code and customization
  * Independent from other components and can be called from other packages
  * Standalone and released independently
* Don’t package the metadata merely because it is supported by Unlocked Packaging. Some components \(e.g. profiles\) will need to be managed outside of unlocked packages and it may be preferable to deploy other related metadata using the same mechanism. In other cases, metadata like non-critical reports, email templates etc, may be better to manage outside of source control entirely to allow these to be changed dynamically by end users.
* Metadata acting on components in a package should be scoped where possible to operate within the confines of the package so these can be included too. Examples include:
  * **Permission Sets**, which should be granular and specific to a function, for example **ability to create customers** \(create/edit accounts and contacts\) or **ability to administrate customers** \(delete/view all accounts and contacts\). It's also important that permission sets are composable to reduce the impact of changes - for example including field security for all non-sensitive fields of an object/package in a single permission set simplifies the process of creating a new field, as permissions for this field can be added to just this permission set
  * **Flows**, which should be small and modular
  * **Triggers and Trigger Handler Classes**, which should be implemented through a dependency injection framework, and scoped to be lightweight, calling service classes from common packages where necessary
* **Objects** should ideally be "owned" by one domain specific package which includes the majority of fields, validation rules and other metadata related to this object. This allows for simpler governance around core object changes and ensures that when metadata is added to an object this is pulled by SFDX into the owning package by default.
* **Workflows and Process Builders** need to be placed in the same unlocked package that contains the parent object definition. This is a restriction of this particular metadata component. In these scenarios rather than building  automation using workflows and process builders, it is better to use apex or flow
* **Custom Labels:** Group and manage custom labels for each package separately to ensure they don't cause deployment errors. sfpowerkit provides some tooling around to work with maintaining custom labels. Check the command [here](https://github.com/Accenture/sfpowerkit#sfpowerkitsourcecustomlabelcreate) and [here](https://github.com/Accenture/sfpowerkit#sfpowerkitsourcecustomlabelreconcile). Ensure you use[ sfpowerkit label create ](https://github.com/Accenture/sfpowerkit#sfpowerkitsourcecustomlabelcreate)command to create these labels.  **Custom labels should be used for their intended purpose to support translation and renaming of standard components. Do not use them to store constants and other hard coded values.**
* Usually some metadata will be cross-cutting, and these components should generally be moved to global packages such as src-access-mgmt and src-ui:
  * **Permission Set Groups**, which should collate granular permission sets from multiple packages into a specific access level
  * **Apps**, which include tabs from multiple packages
  * **Layouts**, which can include related lists, buttons and fields referencing metadata outside of the object's package
  * **Flexipages**, which may include components, actions and lists from across packages

## What Not to Package

* Don’t package the metadata that is not supported by **Metadata API**. Always check the latest [Metadata Coverage](https://developer.salesforce.com/docs/metadata-coverage/). Ensure you run the following command during Pull Request Validation / Locally using the following command.

```text
sfdx sfpowerkit:package:valid -n <name_of_package>
```

* **Profiles** should not be included in unlocked packages and need[ special attention](https://docs.dxatscale.io/scm/managing-profiles).
* **Reports** can only be put in an unlocked if
  * They serve a specific purpose within the package, for example: providing behavioural data of some components
  * They serve as a template that admin can clone

## Unlocked Package and Test Coverage

Unlocked Packages, excluding Org-Dependent unlocked packages have mandatory test coverage requirements. Each package should have minimum of 75% coverage requirement. A validated build \(or [build command ](https://dxatscale.gitbook.io/sfpowerscripts/commands/build-and-quickbuild)in sfpowerscripts\) validates the coverage of package during the build phase. To enable the feedback earlier in the process, sfpowerscripts provide you functionality to validate test coverage of a package during the Pull Request Validation process.

{% hint style="info" %}
Please note that during pull request validation, all apex tests in a package are triggered in parallel and test cases must be written to ensure the guidelines mentioned in the [Locking Records](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/langCon_apex_locking_records.htm) developer guide notes.
{% endhint %}

## Managing Version Numbers of Unlocked Package

For unlocked packages, we ask our practitioners to follow a [semantic](https://semver.org/) versioning of packages.

{% hint style="info" %}
Please note Salesforce packages do not support the concept of PreRelease/BuildMetadata. The last segment of a version number is a build number. We recommend to utilize the auto increment functionality provided by Salesforce rather than rolling out your own build number substitution \( Use 'NEXT' while describing the build version of the package and 'LATEST' to the build number where the package is used as a dependency\)
{% endhint %}

Note that an unlocked package must be [promoted](https://sfpowerscripts.dxatscale.io/commands/command-glossary#sfdx-sfpowerscripts-orchestrator-promote) before it can be installed to a production org, and either the major, minor or patch \(not build\) version **must** be higher than the last version of this package which was promoted. These version number changes should be made in the `sfdx-project.json` file before the final package build and promotion.

## Deprecating Components from an Unlocked Package

Unlocked packages provide traceability in the org by locking down the metadata components to the package that introduces it. This feature which is the main benefit of unlocked package can also create issues when you want to refactor components from one package to another. Let's look at some scenarios and common strategies that need to be applied

For a project that has two packages.

* **Package A** and **Package B**
* **Package B** is dependent on **Package A.**

### **Scenario 1:** 

* Remove a component from **Package A**, provided the component has no dependency
* **Solution:** Create a new version of **Package A** with the metadata component being removed and install the package.

### **Scenario 2:** 

* Move a metadata component from **Package A** to **Package B**
* **Solution:** This scenario is pretty straight forward, one can remove the metadata component from **Package A** and move that to **Package B**. When a new version of **Package A** gets installed, the following things happen:
  * If the deployment of the unlocked package is set to mixed, and no other metadata component is dependent on the component, the component gets [deleted](https://help.salesforce.com/articleView?id=sf.fields_managing_deleted_fields.htm&type=5). 
  * On the subsequent install of **Package B**, **Package B** restores the field and takes ownership of the component.  

### **Scenario 3:** 

* Move a metadata component from **Package B** to **Package A**, where the component currently has other dependencies in **Package B**
* **Solution:** In this scenario, one can move the component to **Package A** and get the packages built. However during deployment to an org, **Package A** will fail with an error this component exists in **Package B**. To mitigate this one should do the following:
  * Deploy a version of **Package B** which removes the lock on the metadata component using deprecate mode. Some times this needs extensive refactoring to other components to break the dependencies. So evaluate whether the approach will work. 
  * If not, you can go to the **UI** \(**Setup &gt; Packaging &gt; Installed Packages &gt; &lt;Name of Package&gt; &gt; View Components and Remove**\) and remove the lock for a package.

## Managing Package Dependencies

Package dependencies are defined in the sfdx-project.json. More information on defining package dependencies can be found in the Salesforce [docs](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev2gp_config_file.htm).

```javascript
{
  "packageDirectories": [
    {
      "path": "util",
      "default": true,
      "package": "Expense-Manager-Util",
      "versionName": "Winter ‘20",
      "versionDescription": "Welcome to Winter 2020 Release of Expense Manager Util Package",
      "versionNumber": "4.7.0.NEXT"
    },
    {
      "path": "exp-core",
      "default": false,
      "package": "ExpenseManager",
      "versionName": "v 3.2",
      "versionDescription": "Winter 2020 Release",
      "versionNumber": "3.2.0.NEXT",
      "dependencies": [
        {
          "package": "ExpenseManager-Util",
          "versionNumber": "4.7.0.LATEST"
        },
          {
          "package": "TriggerFramework",
          "versionNumber": "1.7.0.LATEST"
        },
        {
          "package": "External Apex Library - 1.0.0.4"
        }
      ]
    }
  ],
  "sourceApiVersion": "47.0",
  "packageAliases": {
    "TriggerFramework": "0HoB00000004RFpLAM",
    "Expense Manager - Util": "0HoB00000004CFpKAM",
    "External Apex Library@1.0.0.4": "04tB0000000IB1EIAW",
    "Expense Manager": "0HoB00000004CFuKAM"
  }
}
```

Let's unpack the concepts utilizing the above example:

* There are two unlocked packages
  * Expense Manager - Util is an unlocked package in your DevHub, identifiable by 0H in the packageAlias
  * Expense Manager - another unlocked package which is dependent on ' Expense Manager - Util', 'TriggerFramework' and 'External Apex Library - 1.0.0.4'
* External Apex Library is an external dependency, it could be a managed package or any unlocked package released on a different Dev Hub. All external package dependencies must be defined with a 04t ID, which can be determined from the installation URL from AppExchange or by contacting your vendor.

