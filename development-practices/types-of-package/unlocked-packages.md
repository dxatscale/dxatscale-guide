---
description: All the details about unlocked package
---

# Unlocked Packages

### Introduction

There is a huge amount of documentation on unlocked packages. Rather than repeating all the information here, a curated list of links are provide which every DX@Scale practitioner should be well versed with  
  
_**The Basics**_

Package Development Model : [https://trailhead.salesforce.com/content/learn/modules/sfdx\_dev\_model](https://trailhead.salesforce.com/content/learn/modules/sfdx_dev_model)  
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
* Don’t package the metadata merely because it is supported by Unlocked Packaging.There are many scenarios where if a particular metadata is cross cutting across different packages \(say layouts\) and packaging them might result in too many dependendencies
* **Custom Labels:** Group and manage custom labels for each package separately to ensure they don't cause deployment  errors. sfpowerkit provides some tooling around to work with maintaining custom labels. Check the command [here](https://github.com/Accenture/sfpowerkit#sfpowerkitsourcecustomlabelcreate) and [here](https://github.com/Accenture/sfpowerkit#sfpowerkitsourcecustomlabelreconcile). Ensure you use sfpowerkit's label create command to create these labels.  **Please ensure you use custom label's for its intended purpose as in for support texts in a multilingual app, do not use it to store constants etc.**
* Care must be taken when dealing with  the following metadata. Most often, they must be placed in a source package in the respective domain, or if its a cross cutting concern, move it to global packages such as src-access-managements/src-ui  
  * Proiles
  * Permission Sets
  * Layouts    
* **Workflows and ProcessBuilders** need to be placed in the same unlocked package that contains the parent object defintion. This is a restriction of this particular metadata component, In these scenarios rather than building  automation using workflows and process builders, it is better to use apex or flow

### Unlocked Package and Test Coverage



### Managing Version Numbers of Unlocked Package

### Deprecating an Unlocked Package

\*\*\*\*

