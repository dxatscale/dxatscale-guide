# Dependency Management

sfpowerscripts features commands and functionality that helps in dealing with complexity of defining dependency of unlocked packages. These functionalities are designed considering aspects of a dx@scale project, such as the predominant use of mono repositories in the context of a non-ISV scenarios.

Package dependencies are defined in the sfdx-project.json (Project Manifest). More information on defining package dependencies can be found in the Salesforce [docs](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev2gp\_config\_file.htm).

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

