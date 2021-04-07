---
description: All the details about unlocked package
---

# Unlocked Packages

### Unlocked Package and Test Coverage

### Managing Version Numbers of Unlocked Package

### Deprecating an Unlocked Package

### Utilizing unlocked packages effectively

* Don’t package the metadata that is not supported by **Metadata API**. Always check [Metadata coverage](https://developer.salesforce.com/docs/metadata-coverage/)
* Don’t package the metadata merely because it is supported by Metadata API.There are many scenarios where if your metadata is cross cutting across multiple packages.  It is a good candidate to be placed in a cro \(?\).
* Configuration that is generally **shared across verticals** should be placed in Core \(example is custom Address object and related fields or a Flow for address maintenance\)
* If you have the following scenarios, it may be a good idea to put them in **domain specific packages**.
  * A group of related code and customization
  * Independent from other components and can be called from other packages
  * Standalone and released independently
* Don't move configuration up to core just to manage **cross-vertical dependencies** - do this only where it logically makes sense, otherwise re-factor if possible or move to unpackaged.
* Keep metadata of a shared nature **unpackaged**, eg: 
  * Profiles
  * Permission Sets
  * Dashboards
  * Reports
  * ReportTypes
  * Email Templates
  * Flows, PB and Workflow if Email alert is needed
* If functionality would be useful to future apps or other parts of the org, consider moving it to **base packages**
* **Flow:** Where cross-package dependencies exist \(but it should not be in core as it is functionally aligned to a vertical\) place in unpackaged,
* **Workflow**: Must be packaged alongside its parent object, otherwise move to unpackaged post
* **FlexiPages:** Need to be packaged alongside components included in its metadata \(such as its parent object if it's a record page or any lwc's embedded in the page\) - if this is not possible move to unpackaged post
* **Apex**: All fields referenced in an apex class must exist in your package or a dependent package \(i.e. Core\) - do not create dependencies between vertical packages, instead use dependency injection or platform events
* **Process Builders**: Be aware of the following issues related to Process Builders
  * They generate a blank Workflow metadata file when created, and this needs to be present for the PB to be deployed \(though doesn't need to be in the same package\)
  * If the Process Builder has an email alert, this will create a Workflow Definition file that the PB is dependent on - however as discussed earlier workflows must be packaged alongside their parent object - if this means moving the PB out of a vertical package into core, instead move to unpackaged.
* **Custom Labels:** Group and managed custom labels for each package separately to ensure they don't cause deployment validation errors.

