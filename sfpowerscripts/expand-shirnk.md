---
description: Expand or Shrink package dependency in sfdx-project.json
---

# Expand/Shirnk

It is very often that the sfdx-project.json file can be very large as the number of the packages in the project is keep increasing throughout the project life cycle. And the file becomes extremely hard to maintain and easily missing update package dependencies across all the packages when there is a newly introduced package/dependency.

The expand and shrink commands are used to track those dependencies and fix the missing dependencies when expanding or shrinking the project config file.

When using expand command, you will be able to validate the full dependency list of each packages.&#x20;

Shrink command helps to build a minimal sfdx-project.json file for easy maintenance. And it will also scan the file then create empty entry in the external dependency map for those packages that are not listed in the `packageDirectories`

Shrank project config file will be automatically expanded while the package building process.

External dependency can be defined in plugin section:

```
"plugins": {
      "sfpowerscripts": {
          "disableTransitiveDependencyResolver": false,
              "externalDependencyMap": {
                  "tech-framework@2.0.0.38": [
                      {
                          "package": "sfdc-framework",
                          "versionNumber": "2.3.2.3" 
                      }
                  ]
              }
      }
  }
```



##
