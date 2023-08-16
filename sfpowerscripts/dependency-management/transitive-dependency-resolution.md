# Transitive Dependency Resolution

This feature is by default activated whenever build/quickbuild  even in implicit scenarios such as validate, prepare etc, which might result in building packages.

Let's consider the following sfdx-project.json to explain how this feature works.

```
{
    "packageDirectories": [
       {
            "path": "./src/frameworks/sfdc-logging",
            "package": "sfdc-logging",
            "versionName": "Version 1.0.2",
            "versionNumber": "1.0.2.NEXT"
        },
        {
            "path": "./src/frameworks/feature-mgmt",
            "package": "feature-mgmt",
            "versionName": "Version 1.0.6",
            "versionNumber": "1.0.6.NEXT",
            "dependencies": [
                {
                    "package": "sfdc-logging".
                    "versionNumber": "1.0.2.LATEST"
                }
            ]
        },
       c
      
    ],
    "namespace": "",
    "sfdcLoginUrl": "https://login.salesforce.com",
    "sourceApiVersion": "52.0",
    "packageAliases": {
        "feature-mgmt": "0Ho5f000000GmkrCAC",
        "sfdc-logging": "0Ho5f000000GmerCAC",
        "core-crm": "0Ho5f000000Amz7CAC"
    },
    "plugins": {}
}
```

The above project manifest (sfdx-project.json) describes three packages, **sfdc-logging, feature-mgmt., core-crm .**  Each package are defined with dependencies as described below

<table><thead><tr><th width="218">Package</th><th>Incorrectly Defined Dependencies</th></tr></thead><tbody><tr><td>sfdc-logging</td><td>None</td></tr><tr><td>feature-mgmt</td><td>sfdc-logging</td></tr><tr><td>core-crm</td><td>feature-mgmt</td></tr></tbody></table>

As you might have noticed, this is an incorrect representation, as per the definitions of unlocked package, the package 'core-crm' should be explicitly defining all its dependencies. This means it should be as described below.&#x20;

<table><thead><tr><th width="218">Package</th><th>Correctly Defined Dependencies</th></tr></thead><tbody><tr><td>sfdc-logging</td><td>None</td></tr><tr><td>feature-mgmt</td><td>sfdc-logging</td></tr><tr><td>core-crm</td><td>sfdc-logging, feature-mgmt</td></tr></tbody></table>

To successfully create a version of core-crm , both sfdc-logging and feature-mgmt. should be defined as an explicit dependency in the sfdx-project.json

As the number of packages grow in your project, it is often seen developers might accidentally miss declaring dependencies or the sfdx-project.json has become so large due to large amount of repetition of dependencies between packages.  This condition would result in build stage often failing with missing dependencies.

sfpowerscripts features a transitive dependency resolution which can **autofill** the dependencies of the package by inferring the dependencies from sfdx-project.json, so the above package descriptor of core-crm will be resolved correctly to \


```
 {
            "path": "./src/core-crm",
            "package": "core-crm",
            "versionName": "Version 1.0.6",
            "versionNumber": "1.0.6.NEXT",
            "dependencies": [
                  {
                    "package": "sfdc-logging".
                    "versionNumber": "1.0.2.LATEST"
                },
                {
                    "package": "feature-mgmt",
                    "versionNumber": "1.0.6.LATEST"
                }
            ]
        },
```

Please note, in the current iteration, it will autofill dependency information from the current sfdx-project.json and doesn't consider variations among previous versions.&#x20;

&#x20;For dependencies outside of the sfdx-project.json, one could define an externalDependencyMap as shown below&#x20;

````
```json
 "plugins": {
        "sfpowerscripts": {
            "disableTransitiveDependencyResolver": true,
            "ignoreFiles": {
                "prepare": ".forceignore",
                "validate": ".forceignore",
                "quickbuild": "forceignores/.quickbuildignore",
                "build": "forceignores/.buildignore"
            },
            "externalDependencyMap": {
                "trigger-framework": [
                    {
                        "package": "0H1000XRTCam",
                        "versionNumber": "1.0.3.LATEST"
                    }
                ],
          }
      }
}
````

If you need to disable this feature and have stringent dependency management rules, utilize the following in your sfdx-project.json

{% hint style="info" %}
An external dependency is a package that is not defined within the current repositories sfdx-project.json. Managed packages and unlocked packages built from other repositories fall into 'external dependency' bucket.  IDs of External packages have to be defined explicitly in the **packageAliases** section.
{% endhint %}

```json
"plugins": {
        "sfpowerscripts": {
            "disableTransitiveDependencyResolver": true,
        }
    }
```

