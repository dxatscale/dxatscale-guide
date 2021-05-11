---
description: All the details about unlocked package
---

# Unlocked Packages

### Introduction

There is a huge amount of documentation on unlocked packages. Rather than repeating all the information here, a curated list of links are provided which every DX@Scale practitioner should be well versed with  
  
_**The Basics**_

Package Development Model: [https://trailhead.salesforce.com/content/learn/modules/sfdx\_dev\_model](https://trailhead.salesforce.com/content/learn/modules/sfdx_dev_model)  
Unlocked Package for Customers: [https://trailhead.salesforce.com/content/learn/modules/unlocked-packages-for-customers](https://trailhead.salesforce.com/content/learn/modules/unlocked-packages-for-customers)  
Successfully Creating Unlocked Package: [https://www.youtube.com/watch?v=xJNmHOtIgO0](https://www.youtube.com/watch?v=xJNmHOtIgO0)  
Salesforce Developer Guide to Unlocked Package: [https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_unlocked\_pkg\_intro.htm](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_unlocked_pkg_intro.htm)  
Unlocked Package FAQ: [https://sfdc-db-gmail.github.io/unlocked-packages/faq-unlocked-pkgs.html](https://sfdc-db-gmail.github.io/unlocked-packages/faq-unlocked-pkgs.html)

_**Advanced Materials**_

Anti Patterns in Package Dependency Design: [https://medium.com/salesforce-architects/5-anti-patterns-in-package-dependency-design-and-how-to-avoid-them-87bb50331cb8](https://medium.com/salesforce-architects/5-anti-patterns-in-package-dependency-design-and-how-to-avoid-them-87bb50331cb8)

The following sections deal with items that are particular to DX@Scale or more emphasis is required in large scale programs

### Placing  metadata components in Unlocked Package

* Don’t package the metadata that is not supported by **Metadata API**. Always check [Metadata coverage](https://developer.salesforce.com/docs/metadata-coverage/). Ensure you run the following command during Pull Request Validation / Locally using the following command.

```text
                 sfdx sfpowerkit:package:valid -n <name_of_package> 
```

* If you have the following scenarios, it may be a good idea to put them in **domain specific packages**.
  * A group of related code and customization
  * Independent from other components and can be called from other packages
  * Standalone and released independently
* Don’t package the metadata merely because it is supported by Unlocked Packaging. There are many scenarios where if  particular metadata is cross-cutting across different packages \(say layouts\) and packaging them might result in too many dependencies
* **Custom Labels:** Group and manage custom labels for each package separately to ensure they don't cause deployment errors. sfpowerkit provides some tooling around to work with maintaining custom labels. Check the command [here](https://github.com/Accenture/sfpowerkit#sfpowerkitsourcecustomlabelcreate) and [here](https://github.com/Accenture/sfpowerkit#sfpowerkitsourcecustomlabelreconcile). Ensure you use[ sfpowerkit label create ](https://github.com/Accenture/sfpowerkit#sfpowerkitsourcecustomlabelcreate)command to create these labels.  **Please ensure you use custom label's for its intended purpose as in for support texts in a multilingual app, do not use it to store constants etc.**
* Care must be taken when dealing with the following metadata. Most often, they must be placed in a source package in the respective domain, or if its a cross-cutting concern, move it to global packages such as src-access-managements/src-ui  
  * Profiles
  * Permission Sets
  * Layouts    
* **Workflows and ProcessBuilders** need to be placed in the same unlocked package that contains the parent object definition. This is a restriction of this particular metadata component, In these scenarios rather than building  automation using workflows and process builders, it is better to use apex or flow

### Unlocked Package and Test Coverage

Unlocked Packages, excluding Org-Dependent unlocked packages have mandatory test coverage requirements. Each package should have minimum of 75% coverage requirement.  A validated build \(or [build command ](https://dxatscale.gitbook.io/sfpowerscripts/commands/build-and-quickbuild)in sfpowerscripts\) validates the coverage of package during the build phase. To enable the feedback earlier in the process, sfpowerscripts provide you functionality to validate test coverage of a package during the Pull Request Validation process.

{% hint style="info" %}
Please note that during pull request validation, all apex tests in a package are triggered in parallel and test cases must be written to ensure the guidelines mentioned in the link below  
[https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/langCon\_apex\_locking\_records.htm](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/langCon_apex_locking_records.htm)
{% endhint %}

### Managing Version Numbers of Unlocked Package

For unlocked packages, we ask our practitioners to follow a semantic versioning of packages. You can read more about semantic version at this [link](https://semver.org/).

{% hint style="info" %}
Please note Salesforce packages do not support the concept of PreRelease/BuildMetadata. The last segment of a version number is a build number. We recommend to utilize the auto increment functionality provided by salesforce rather than rolling out your own build number substitution \( Use  'NEXT' while describing the build version of the package and 'LATEST' to the build number where the package is used as a dependency\)
{% endhint %}

### Deprecating components from an  Unlocked Package

Unlocked packages provide traceability in the org by locking down the metadata components to the package that introduces it. This feature which is the main benefit of unlocked package can also create issues when you want to refactor components from one package to another. Let's look at  some scenarios and common strategies that need to be applied

For a project that has two packages, Package A and Package B, and Package B is dependent on Package A  
  
 **Scenario 1:  Remove a component from Package A, provided the component has no dependency** 

Create a new version of package A with the metadata component being removed and install the package

 **Scenario 2:  Move a metadata component from Package A to Package B**  
  
This scenario is pretty straight forward, one can remove the metadata component from Package A and move that to Package B.  When ****a new version of Package A gets installed, the following things happen  
- If the deployment of the unlocked package is set to mixed, and no other metadata component is dependent on the component, the component gets deleted \( [https://help.salesforce.com/articleView?id=sf.fields\_managing\_deleted\_fields.htm&type=5](https://help.salesforce.com/articleView?id=sf.fields_managing_deleted_fields.htm&type=5)\). On subsequent install of Package B, package B restores the field and takes  ownership of the component  
  
 **Scenario 3:  Move a metadata component from Package B to Package A, where the component currently has other dependencies in Package B** 

In this scenario, one can move the component to Package A and get the packages built. However during deployment to an org, Package A will fail with an error this component exists in Package B. To mitigate this one should do the following  
 - Deploy a version of Package B which removes the lock on the metadata component using deprecate mode. Some times this needs extensive refactoring to other components to break the dependencies. So evaluate whether the approach will work. If not, you can goto the UI \(**Setup --&gt; Packaging --&gt; Installed Packages --&gt; &lt;name of package&gt; --&gt; View Components  and Remove** \)  and remove the lock for a package.

\*\*\*\*

