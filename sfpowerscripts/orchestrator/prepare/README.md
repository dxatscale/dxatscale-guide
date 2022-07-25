---
description: Prepare a pool of just-in-time CI scratch orgs or Development Environments
---

# Prepare

Prepare command helps you to build a pool of pre-built scratch orgs which can include managed packages as well as packages in your repository. This process allows you to cut down time in re-creating a scratch org during validation process when a scratch org is used as just-in-time CI environment or when being used as a developer environment.

## Building a Pool of Scratch Orgs

As you try to automate more of your business processes in Salesforce, you cannot avoid adding third party managed packages as a dependency to your configuration metadata and code in your repository. The time required to spin up a just-in-time CI scratch org or even a developer environment (one need to run data loading scripts, assign permission sets etc.) would increase and the value of scratch org diminishes, as teams find it cumbersome.

This is the primary reason scratch org pools pre-installed with managed packages and your custom configuration and code, along with data from your repository will significantly enhance the developer experience.

{% hint style="info" %}
The Prepare command was built primarily due to the delays from Salesforce to enable **snapshot** feature and make it GA to the public. However, even with snapshot feature, you might need to rebuild the snapshot every day, as we have noticed in a large mono repo scenario (full deployment of metadata also takes long time). We will modify the command as needed when this feature launches to utilize snapshot accordingly.
{% endhint %}

We expect you to build a pool of scratch org's using a pipeline at scheduled intervals, that ensures the pools are always replenished with scratch org's ready for consumption whenever you demand it.  If needed, these scheduled jobs should be able to be triggered manually to replenish the scratch org pools if required.

{% hint style="info" %}
Note that to enable scratch org pooling, you will need to deploy some pre-requisite fields  and metadata to the ScratchOrgInfo Object in Dev Hub. The additional fields determine which pool a scratch org belongs to and also allows the validate and fetch commands to fetch scratch orgs from a pool. Instructions on how to install the pre-requisite package that contains the fields are available [here](https://github.com/dxatscale/sfpower-scratchorg-pool).
{% endhint %}

## Steps undertaken by prepare command

The prepare command does the following sequence of activities:

1. **Calculate the number of scratch orgs to be allocated** (Based on your requested number of scratch orgs and your org limits, we calculate what is the number of scratch orgs to be allocated at this point in time)
2. **Fetch the artifacts from registry if "fetchArtifacts" is defined in config, otherwise build all artifacts**
3. **Create the scratch orgs, and update Allocation\_status\_c of each these orgs to "In Progress"**
4. **On each scratch org, in parallel, do the following activities:**
   * Install SFPOWERSCRIPTS\_ARTIFACT\_PACKAGE (04t1P000000ka9mQAA) for keeping track of all the packages which will be installed in the org. You can set an environment variable SFPOWERSCRIPTS\_ARTIFACT\_PACKAGE to override the installation with your own package id (the source code is available [here](https://github.com/dxatscale/sfpowerscripts-artifact))
   * Install all the dependencies of your packages, such as managed packages that are marked as dependencies in your sfdx-project.json
   * Install all the artifacts that is either built/fetched
   * If `enableSourceTracking` is specified in the configuration, create and deploy "sourceTrackingFiles" using sfpowerscripts artifacts to the scratch org.  To store local source tracking files, we re-create it when fetching a scratch org from a pool, using the [@salesforce/source-tracking](https://github.com/forcedotcom/source-tracking) library. Checkout the commit from which each sfpowerscripts artifact was created, and update the local source tracking using the package directory.  The files are retrieved to the local ".sfdx" directory, when using `sfpowerscripts:pool:fetch` to fetch a scratch org, and allows users to deploy their changes only, through source tracking.  Refer to the [decision log](https://github.com/dxatscale/sfpowerscripts/blob/main/decision%20records/prepare/001-prepare-source-tracking.md) for more details.
5. **Mark each completed scratch org as "Available", depending on the pool config \`succeedOnDeploymentErrors\` is true, else scratch orgs are deleted**

{% hint style="warning" %}
**Ensure that your DevHub is authenticated using** [**SFDX Auth URL**](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_cli\_reference.meta/sfdx\_cli\_reference/cli\_reference\_auth\_sfdxurl.htm) **and the auth URL is stored in a secure place (Key Management System or Secure Storage).**
{% endhint %}

## **Using pre-existing artifacts in Scratch Org Pools**

Building packages from source code during pooling takes a considerable amount of time, and there could be situations where the latest head is broken. Hence we recommend using the last-known successful build from the artifact repository. When the `installall` and `fetchArtifacts` configurations are specified, the user can either use **NPM** to fetch artifacts or define the path to a shell script containing the logic for fetching artifacts from a registry.

{% hint style="info" %}
If the `installall` configuration is specified without`fetchArtifacts`, then new packages will be built, from the checked-out source code, and installed in the scratch orgs. &#x20;
{% endhint %}

## Fetching Scratch Orgs from Pool

While scratch orgs created by prepare command will be automatically fetched by the validate command, for use as just-in-time environments for validating an incoming change. Developers who need a scratch org from the pool must issue the fetch command on their terminal

```javascript
sfdx sfpowerscripts:pool:fetch -t <POOL_NAME> -v <devhub-alias> -a <scratchorg-alias>
```

Developers need sufficient permission in the associated DevHub to fetch a scratch org. Read more about associated permissions [here](../../../implementing-your-ci-cd/github/prerequisites.md).

{% hint style="warning" %}
When [Free Limited Access Licenses](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/dev\_hub\_license.htm) are being utilized, developers will not be able to delete the scratch orgs fetched from the pool (due to permission restrictions). It is recommended to build a pipeline in your CI/CD system that is run with elevated permission and license which could delete these scratch orgs.  Developer Users assigned with the "**Free Limited Access Licenses"** are restricted to "**Limited Access User**" Profiles only.  If standard Salesforce and Salesforce Platform licences are planned, the recommendation is to ensure you assign developers a cloned "**Minimum Access - Salesforce**" Profile to restrict access and grant them permissions to the scratch orgs objects via PermSet and Sharing Rules.&#x20;
{% endhint %}

{% hint style="info" %}
Please check the pre-requisites to learn more about and the steps required to enable pooling in your DevHub
{% endhint %}

## Managing Package Dependencies

The Prepare command utilizes `sfpowerkit:package:dependencies:install` under the hood to orchestrate installation of package dependencies. Package dependencies are defined in the sfdx-project.json. More information on defining package dependencies can be found in the Salesforce [docs](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev2gp\_config\_file.htm).

```javascript
{
  "packageDirectories": [
    {
      "path": "util",
      "default": true,
      "package": "Expense-Manager-Util",
      "versionName": "Winter ‘22",
      "versionDescription": "Welcome to Winter 2022 Release of Expense Manager Util Package",
      "versionNumber": "4.7.0.NEXT"
    },
    {
      "path": "exp-core",
      "default": false,
      "package": "ExpenseManager",
      "versionName": "v 3.2",
      "versionDescription": "Winter 2022 Release",
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
  "sourceApiVersion": "55.0",
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
  * Expense Manager - Util is an unlocked package in your DevHub, identifiable by **0H** in the packageAlias
  * Expense Manager - another unlocked package which is dependent on ' Expense Manager - Util', 'TriggerFramework' and 'External Apex Library - 1.0.0.4'
* External Apex Library is an external dependency, It could be a managed package or any unlocked package released on a different Dev Hub. All external package dependencies have to be defined with a **04t** ID, which can be determined from the installation URL from AppExchange or by contacting your vendor.
* sfpowerscripts parses sfdx-project.json and does the following in order
  * Skips Expense manager - Util as it doesn't have any dependencies
  * For Expense manager
    * Checks whether any of the package is part of the same repo, in this example 'Expense Manager-Util' is part of the same repository and will not be installed as a dependency
    * Installs the latest version of TriggerFramework ( with major, minor and patch versions matching 1.7.0) to the scratch org
    * Install the 'External Apex Library - 1.0.0.4' by utilizing the 04t id provided in the packageAliases

If any of the managed package has keys, it can be provided as an argument to the prepare command. Check the command's flags for more information.

### Key Support for Managed Packages

The format for the 'keys' parameter is a string of key-value pairs separated by spaces - where the key is the name of the package, the value is the protection key of the package, and the key-value pair itself is delimited by a colon .

e.g. `--keys "packageA:12345 packageB:pw356 packageC:pw777"`

{% hint style="warning" %}
The time taken by this command depends on how many managed packages and your packages that need to be installed. Please note, if you are triggering this command in a CI server, ensure proper time outs are provided for this task, as most cloud-based CI providers have time limits on how long a single task can be run.  Explore [multi-stage prepare jobs](https://github.com/dxatscale/sfpowerscripts/blob/main/decision%20records/prepare/002-prepare-daisy-chaining.md) in case this is a blocker for the team.
{% endhint %}

## Handling a change in shape of pooled scratch orgs

For changes to the features and settings in pooled scratch orgs, check out the [validate command's documentation](../validate.md), which has information on how to dynamically update the shape of already created scratch orgs. Otherwise, the existing pool can be deleted and created again.

## Managing the Scratch Org Pool

The `sfpowerscripts:pool` topic contains commands that can be used to manage (list, fetch and delete) the scratch org pools created by prepare command.

## Executing a custom script

User can execute the custom script before dependencies install into a particular org when `preDependencyInstallationScriptPath` configuration is specified or after all the artifacts are deployed into a particular org when `postDeploymentScriptPath` configuration is specified in the pool config file.&#x20;

```
"preDependencyInstallationScriptPath": "scripts/prepare/pre.sh" //Linux or Mac
```

Following arguments will be passed into the script for use in the custom logic.

```
$0: custom script path
$1: scratch org username 
$2: devhub username
#Only applicable for post-deployment script, 
$3 deployment status ("failed" or "succeed")
```

## Package Checkpoints

Package checkpoints allow precise control over which scratch orgs are committed to a pool when there are deployment failures and the `succeedOnDeploymentErrors` configuration is specified. To designate a package as a checkpoint, add the property `checkpointForPrepare: true` to the package in the sfdx-project.json. Only scratch orgs that satisfy at least one checkpoint will be committed to the pool. This provides more consistency in what you can expect from your scratch orgs.

## Using Prepare in Multiple Stages

When you are using prepare in larger repositories with multiple managed packages, the process of preparing a scratch org can be extremely slow, often running above 6 hours. If you are preparing using cloud hosted agents of a CI/CD platform, most of the platforms are designed to timeout within a certain time window. This could result in unavailability of scratch orgs in pools, as most scratch orgs will be in 'IN PROGRESS' state and can only reclaimed by deleting the pool as there are no agents to continue the remaining progress or change the stage of the orgs. This is where you could use prepare in multiple stages.

![Daisy chaining scratch org pools ](<../../../.gitbook/assets/image (54).png>)

In the above image, CI2 Pool is using CI Snapshot pool prepared in an earlier stage or job. The CI2 Pool definition will be utilizing 'snapshotPool' as a property which points to 'CI Snapshot' pool. Any packages that are installed on CI Snapshot pool are skipped while preparing CI2 Pools.

## Using Prepare with Non-NPM Registries

Unlike NPM registries, there is no uniform method for downloading artifacts from a universal registry, so you will need to provide a shell script that calls the relevant API. The path to the shell script should be specified in the pool configuration.

There are multiple parameters available in the shell script. Pass these parameters to the API call, and at runtime they will be substituted with the corresponding values:

1. Artifact name
2. Artifact version
3. Directory to download artifacts

**Eg.** **Fetching from Azure Artifacts using the Az CLI on Linux**

```
#!/bin/bash

# $1 - artifact name
# $2 - artifact version
# $3 - artifact directory 

echo "Downloading Artifact $1 Version $2"

az artifacts universal download --feed myfeed --name $1 --version $2 --path $3 \
    --organization "https://dev.azure.com/myorg/" --project myproject --scope project
```
