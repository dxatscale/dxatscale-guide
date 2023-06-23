# Azure DevOps Setup

## Getting Started

{% hint style="info" %}
Azure DevOps Getting Started guide is a Work in Progress.
{% endhint %}

The following getting started guide will enable you to configure and setup CI/CD using Azure DevOps and DX@Scale for Salesforce. Assuming you have reviewed and completed the prerequisite account setup and software tool installations, this guide will walk you through the initial setup process in Salesforce and Azure DevOps using the [template](https://github.com/dxatscale/dxatscale-template) provided. Along the way, additional general tips and best practices will be highlighted to help you understand the template provided and enable you to customize as needed.

As always, we welcome any feedback from the community to continuously improve this user guide. Please [contact us](https://docs.dxatscale.io/about-us/contact-us) for any questions or concerns.

### 1. Developer Workstation

In order to successfully troubleshoot and interact with GitHub and Salesforce using the CLI, the following commands should be executed on your computer to validate you have the tools configured correctly. Depending on your operating system (eg. **Mac OS, Windows, Linux**), there may be some variation in the commands and outputs below on your terminal window.

#### Git

```bash
git version
> git version 2.33.1
```

#### SFDX CLI

```bash
sfdx version
> sfdx-cli/7.176.1 darwin-x64 node-v18.7.0
```

#### SFDX Plugins

```bash
sfdx plugins
> @dxatscale/sfpowerscripts 19.8.2
  @dxatscale/sfp-cli 3.1.1
  sfdmu 4.17.6
  sfpowerkit 6.0.0
```

#### Visual Studio Code

```bash
code --version
> 1.72.2
d045a5eda657f4d7b676dedbfa7aab8207f8a075
x64
```

#### NPM

```bash
npm --version
> 8.15.0
```

### 2. Salesforce

To enable modular package development, there are a few configurations in Salesforce as a System Administrator that needs to be turned on to be able to create Scratch Orgs and Unlock Packages.

#### A. Enable Dev Hub

[Enable Dev Hub](https://help.salesforce.com/s/articleView?id=sf.sfdx\_setup\_enable\_devhub.htm\&type=5) in your Salesforce org so you can create and manage scratch orgs and second-generation packages. Scratch orgs are disposable Salesforce orgs to support development and testing.

1. Navigate to the **Setup** menu
2. Go to **Development > Dev Hub**
3. Toggle the button to on for **Enable Dev Hub**

![](<../../.gitbook/assets/image (58).png>)

#### B. Enable Unlocked Packages and Second-Generation Managed Packages

[Unlocked packages](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_unlocked\_pkg\_intro.htm) help organize your existing metadata, package an app, extend an app that you’ve purchased from AppExchange, or package new metadata.

1. Navigate to the **Setup** menu
2. Go to **Development > Dev Hub**
3. Toggle the button to on for **Enable Unlocked Packages and Second-Generation Managed Packages**

![](<../../.gitbook/assets/image (1) (1).png>)

#### C. Create Service Account for DevOps

For auditing purposes, it is best practice to create a separate [service account](https://help.salesforce.com/s/articleView?id=000331470\&type=1) to manage deployments to your Salesforce instance. The separation of user owned accounts and service accounts ensures traceability to your metadata and configuration changes.

1. Navigate to the **Setup** menu
2. Go to **Users > Users**
3. Click on **New User** button
4. Enter **CICD** for **First Name** and **User** for **Last Name**
5. Enter in a Email address and Username
6. Set **User License** to **Salesforce**
7. Set **Profile** to **System Administrator**
8. Scroll down and click on **Save**

![](<../../.gitbook/assets/image (18).png>)

{% hint style="info" %}
Only certain [editions](https://help.salesforce.com/s/articleView?id=000326486\&type=1) of Salesforce has API Access. It's best to create a new **Profile** or **Permission Set** and configure the **System Permissions** and enable the **API Enabled** and **Api Only User** permission.
{% endhint %}

#### D. Authenticate to DevHub via CLI

Authorize your production instance and/or Developer Edition Org using the [web login flow](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_cli\_reference.meta/sfdx\_cli\_reference/cli\_reference\_auth\_web.htm). The example below uses "**DevHub**" as the alias for the instance where you will use to create Unlock Packages and manage Scratch Orgs.

```bash
sfdx auth:web:login -a DevHub -r https://login.salesforce.com
```

#### E. Install sfpowerscripts Scratch Org Pooling Unlocked Package in DevHub

The [Scratch Org Pooling Unlocked Package](https://github.com/dxatscale/sfpower-scratchorg-pool) adds additional custom fields, validation rule, and workflow to the standard object "**ScratchOrgInfo**" in the DevHub to enable associated scratch org pool commands to work for the pipeline.

```bash
sfdx force:package:install -p 04t1P000000katQQAQ -u DevHub -r -a package -s AdminsOnly -w 30
```

#### F. Install sfpowerscripts-artifact Unlocked Package in DevHub and Lower Existing Sandboxes

The [sfpowerscripts-artifact package ](https://github.com/dxatscale/sfpowerscripts-artifact)is a lightweight unlocked package consisting of a custom setting **SfpowerscriptsArtifact2\_\_c** that is used to keep record of the artifacts that have been installed in the org. This enables package installation, using sfpowerscripts, to be skipped if the same artifact version already exists in the org.

```bash
sfdx force:package:install --package 04t1P000000ka9mQAA -u <OrgAlias> --securitytype=AdminsOnly --wait=120
```

#### G. Authenticate to Lower Sandbox Environments via CLI

The template assumes you are following the environment strategy defined in our DX@Scale Guide. The following sandboxes are recommended to be created and [authenticated](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_cli\_reference.meta/sfdx\_cli\_reference/cli\_reference\_auth\_web.htm) first prior to running the pipeline.

* SHAREDDEV (Shared Development)
* ST (System Test)
* SIT (System Integration Test)
* UAT (User Acceptance Test)
* PROD (Production)

{% hint style="info" %}
Assuming that Production is also your Dev Hub, we still recommend creating multiple CLI entries to segregate the connections.
{% endhint %}

Additional environments and customization can be made once you are familiar with the scripts.

{% tabs %}
{% tab title="Sandbox" %}
```bash
sfdx auth:web:login -a <orgAlias> -r https://test.salesforce.com
```
{% endtab %}

{% tab title="Production" %}
```
sfdx auth:web:login -a <orgAlias> -r https://login.salesforce.com
```
{% endtab %}
{% endtabs %}

#### H. Generate SFDX auth URL for Pipeline Authentication

In order for the Azure DevOps pipeline to authenticate to the DevHub and other environments, [SFDX auth URL](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_cli\_reference.meta/sfdx\_cli\_reference/cli\_reference\_auth\_sfdxurl.htm) is the preferred method over [JWT Bearer Flow](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_auth\_jwt\_flow.htm). For each environment, execute the following command on a previously authenticated environment and save the sfdxAuthUrl for use in future pipeline configuration steps.

```bash
sfdx force:org:display -u <orgAlias> --verbose --json > authFile.json
cat authFile.json
> {
  "status": 0,
  "result": {
    "id": "XXXXYYY",
    "accessToken": "00D8G0000009g7h!uhuRfGKbvPeubTZKztmFWgrykDuuVdxbffzjjVTqjMyRcV{wb+2JtxsevgKfGiGXRz02jY83uNBsD4CuWHwv.b21KZdFxbTi",
    "instanceUrl": "https://your.salesforce.com",
    "username": "vu.ha@accenture.com.dxatscale.shareddev",
    "clientId": "PlatformCLI",
    "connectedStatus": "Connected",
    "sfdxAuthUrl": "force://PlatformCLI::Cq$QLeQvDxpvUoNKgiDkoTqyVHdeoMupiZvkgHYcdVHsfMaDpqKJNbg#8ZtUpfBuIdVaUD0B21cFav5X2Pzv5X2@yoursalesforce.com",
    "alias": "SharedDev"
  }
}
```

{% hint style="info" %}
Save only the following part of the **sfdxAuthUrl** for each environment

`force://PlatformCLI::Cq$QLeQvDxpvUoNKgiDkoTqyVHdeoMupiZvkgHYcdVHsfMaDpqKJNbg#8ZtUpfBuIdVaUD0B21cFav5X2Pzv5X2@yoursalesforce.com`
{% endhint %}

#### I. Grant developers access to scratch org pools

For developers (who are on limited access license) to access scratch orgs created by the CI service user, for their local development, a sharing setting needs to be created on the ScratchOrgInfo object. The sharing setting should grant read/write access to the ScratchOrgInfo records owned by a public group consisting of the CI service user and a public group consisting of the developer users.

Create two public groups

1. CI Users (Admin users/ CI users who creates scratch orgs in pool)
2. Developers (developers who are allowed to fetch scratch orgs from pool),

Then create a sharing rule that grant read/write access to the ScratchOrgInfos records owned by the CI Users to Developers

The developers must also have object-level and FLS permissions on the ScratchOrgInfo object. One way to achieve this is to assign a permission set that has Read, Create, Edit and Delete access on ScratchOrgInfos, as well as Read and Edit access to the custom fields used for scratch org pooling: `Allocation_status__c`, `Password__c`, `Pooltag__c` and `SfdxAuthUrl__c`

### 3. Azure DevOps

#### A. Download Repo & Set Up

Open your Azure DevOps account click on **New organization**; **once you have created your organisation create a project to get started.**

![](../../.gitbook/assets/screen-shot-2021-09-14-at-2.43.40-pm.png)

Make your way to **Repos** and click on Import. Provide the Clone URL [https://github.com/dxatscale/dxatscale-template](https://github.com/dxatscale/dxatscale-template)

![](../../.gitbook/assets/azuredevops\_import.png)

After a few minutes, your repository will be set up in Azure DevOps.

#### B. Create Variable Groups

[Variable Groups](https://docs.microsoft.com/en-us/azure/devops/pipelines/library/variable-groups?view=azure-devops\&tabs=yaml) store values and secrets that Azure DevOps pipeline uses to authenticate to protected resources etc. The template uses both variables and files in the CI/CD to setup the environment connections, NPM Registry Scope, Project Access Tokens, and optionally metrics dashboard connection details.

![Azure DevOps Variable Group](../../.gitbook/assets/azuredevops\_variable\_group.png)

1. From the **Pipelines** click on **Library** and add a new variable group
2. Click on **+ Variable Group**
3. Name the variable group as CICD and provide some description
4. In the Variables, section, click on **+ Add** and add the following variables
5. Follow instructions in[ 2.F](../github-1/getting-started.md#f-authenticate-to-lower-sandbox-environments-via-cli) to fetch all the authURL for each environment and add this to the variable group

| Name                       | Value          | Protect |
| -------------------------- | -------------- | ------- |
| DEVHUB\_ALIAS              | devhub         | No      |
| DEVHUB\_SFDX\_AUTH\_URL    | \<sfdxAuthUrl> | Yes     |
| PROD\_ALIAS                | prod           | No      |
| PROD\_SFDX\_AUTH\_URL      | \<sfdxAuthUrl> | Yes     |
| SHAREDDEV\_ALIAS           | shareddev      | No      |
| SHAREDDEV\_SFDX\_AUTH\_URL | \<sfdxAuthUrl> | Yes     |
| SIT\_ALIAS                 | sit            | No      |
| SIT\_SFDX\_AUTH\_URL       | \<sfdxAuthUrl> | Yes     |
| ST\_ALIAS                  | st             | No      |
| ST\_SFDX\_AUTH\_URL        | \<sfdxAuthUrl> | Yes     |
| UAT\_ALIAS                 | uat            | No      |
| UAT\_SFDX\_AUTH\_URL       | \<sfdxAuthUrl> | Yes     |
| scope                      | \<scope>       | No      |

#### C. Create New Azure Artifact Feed

1. On ADO, navigate to Artifacts section
2. Create a new feed with a name and choose the right settings depending on your preference

![](../../.gitbook/assets/azuredevops\_feed.png)

1. Click on **Connect to Feed** and navigate to **npm** section.

***

![Connect to feed](../../.gitbook/assets/azuredevops\_connect-to-feed.png)

1. Create a .npmrc file in your system and copy the contents from the 'Connect To Feed'
2. Upload this file as secure files in your library

![](../../.gitbook/assets/screen-shot-2021-09-14-at-3.08.41-pm.png)

#### D. Import your pipelines

Make your way to **Pipelines** and click on **Pipelines**

![](../../.gitbook/assets/screen-shot-2021-09-15-at-9.44.36-am.png)

Click on **Create Pipeline** and select **Azure Repos Git**

![](../../.gitbook/assets/screen-shot-2021-09-15-at-9.59.43-am.png)

Click on **Existing Azure Pipelines YAML file**

![](../../.gitbook/assets/screen-shot-2021-09-15-at-10.08.54-am.png)

On the right side of the screen, you will see **Select an existing YAML file** on Path select the `/.azure-pipelines/env-operations/prepare-ci-pool.yml`

![](../../.gitbook/assets/screen-shot-2021-09-15-at-10.09.51-am.png)

Click on the Dropdown button on **Run** and click **Save**

![](../../.gitbook/assets/screen-shot-2021-09-15-at-10.12.52-am.png)

{% hint style="info" %}
Repeat this step for all pipelines in the `.azure-pipelines` folder.
{% endhint %}

#### E. Test your pipelines

It is recommended to test your pipelines by triggering the CI Pipeline - Auto triggered by triggering it manually. Monitor the pipeline till it produces a set of packages and publishes to Azure Artifacts. If this stage is successful, you can proceed to step 5

#### F. Configure Scratch Org Pools

In your repo, there is a folder called config, in that folder, you can see there are two JSON files

* `project-ci-pool-def.json`
* `project-dev-pool-def.json`

As an overview Scratch Pools help development teams save the time taken to spin up scratch orgs allowing more time to be spent on development, installing all dependencies, and having it ready for development; in conjunction, we also use CI Pools.

To configure the time expiry and the number of orgs to be created and more, here are the file paths to the following scratch org definition YAML Files:

```
YOUR_REPO/config/project-ci-pool-def.json
YOUR_REPO/config/project-dev-pool-def.json
```

Let's get started by looking at CI Pool Definition:

```javascript
{
  "$schema": "https://raw.githubusercontent.com/Accenture/sfpowerscripts/develop/packages/sfpowerscripts-cli/resources/schemas/pooldefinition.schema.json",
  "tag": "ci",
   "maxAllocation": 5,
   "expiry": 2,
   "batchSize": 5,
   "configFilePath": "config/project-scratch-def.json",
   "enableSourceTracking": false,
   "installAll": true,
    "fetchArtifacts": {
      "npm": {
        "scope": "org-name"
      }
    }

 }
```

Let's look at DEV Pool Definition now:

```javascript
{
    "$schema": "https://raw.githubusercontent.com/Accenture/sfpowerscripts/develop/packages/sfpowerscripts-cli/resources/schemas/pooldefinition.schema.json",
    "tag": "dev",
    "maxAllocation": 5,
    "expiry": 10,
    "batchSize": 5,
    "configFilePath": "config/project-scratch-def.json",
    "relaxAllIPRanges": true,
    "enableSourceTracking": true,
    "retryOnFailure": true,
    "succeedOnDeploymentErrors": true,
    "installAll": true,
    "fetchArtifacts": {
        "npm": {
          "scope": "org-name"
        }
      }

}
```

{% hint style="info" %}
Update the "**scope**" value for "**npm**" from the default "**@org-name**" to your defined scope in the previous variables section. (eg. **@dxatscale-poc**). Please ensure your org-name matches the name of your org and it is in 'LOWERCASE'
{% endhint %}

{% hint style="info" %}
To get an in-depth understanding of the options available to you for configuration refer to this link [here](https://sfpowerscripts.dxatscale.io/commands/prepare/scratch-org-pool-configuration).
{% endhint %}

#### G. Scratch Org Definition File

The [project-scratch-def.json](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_scratch\_orgs\_def\_file.htm) is a blueprint for a scratch org. It mimics the shape of an org that you use in the development life cycle, such as sandbox, packaging, or production.

Customize the provided scratch org definition file for your use case and save and commit the file to the repository. If you want to use the file as is to test, **no action** is required.

```bash
{
    "orgName": "DX@Scale Demo Org",
    "edition": "Developer",
    "hasSampleData": false,
    "features": ["Communities", "Walkthroughs", "EnableSetPasswordInApi"],
    "settings": {
        "communitiesSettings": {
            "enableNetworksEnabled": true
        },
        "experienceBundleSettings": {
            "enableExperienceBundleMetadata": true
        },
        "lightningExperienceSettings": {
            "enableS1DesktopEnabled": true
        },
        "mobileSettings": {
            "enableS1EncryptedStoragePref2": false
        },
        "pathAssistantSettings": {
            "pathAssistantEnabled": true
        },
        "userEngagementSettings": {
            "enableOrchestrationInSandbox": true,
            "enableShowSalesforceUserAssist": false
        }
    }
}
```

## Using Scratch Orgs with Org Shape

To take all advantages from DX@Scale and be compliant with your current org, you can use the Org Shape feature, but when you do it you need to add an extra parameter on your scratch-def.json which is the **Security Settings > Password Policies > Minimum Password Lifetime = FALSE**.

The reason behind this need, is because when you spin a Scratch Org with Org Shape that feature will be TRUE (no matter how your source org is configured or not), and it will break your pipeline during the password reset process which DX@Scale uses. This issue is affected only with Org Shape feature.

```bash
{
    "orgName": "DX@Scale Demo Org,
    "sourceOrg": "00DB1230400Ifx5",
    "settings": {
        "securitySettings": {
            "passwordPolicies": {
                "minimumPasswordLifetime": false
            }
        }
    }
}
```

#### H. Project Configuration File

The [project configuration file](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_ws\_config.htm) **sfdx-project.json** indicates that the directory is a Salesforce DX project. The configuration file contains project information and facilitates the authentication of scratch orgs and the creation of second-generation packages. It also tells the CLI where to put files when syncing between the project and scratch org.

The dxatscale-template [project configuration file](https://github.com/dxatscale/dxatscale-template/blob/main/sfdx-project.json) contains initial, pre-defined package directories based on our best practices for [repository structure](https://docs.dxatscale.io/scm/repository-structure) and modularization.

| Package                         | Description                                                                                                                                                                                                                                                                                                   |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **src-env-specific-pre**        | Installed first across all release environments.                                                                                                                                                                                                                                                              |
| **src-env-specific-alias-pre**  | Installed after src-env-specific-pre and is only used when any environment-specific metadata has to be aligned with each environment                                                                                                                                                                          |
| **core**                        | A folder to house all the core model of your org which is shared with all other domains.                                                                                                                                                                                                                      |
| **src-ui**                      | This folder would include page layouts, FlexiPages and Lightning/Classic apps unless we are sure these will only reference the components of a single domain package and its dependencies. In general custom UI components such as LWC, Aura and VisualForce should be included in a relevant domain package. |
| **src-access-management**       | This package is typically one of the packages that is deployed second to last in the deployment order and used to store profiles, permission sets, and permission set groups that are applied across the org.                                                                                                 |
| **src-env-specific-alias-post** | Installed after src-env-specific-pre and is only used when any environment specific metadata has to be aligned with each environments                                                                                                                                                                         |
| **src-temp**                    | This folder is marked as the default folder in sfdx-project.json. This is the landing folder for all metadata and this particular folder doesn't get deployed anywhere other than a developers scratch org. This place is utilized to decide where the new metadata should be placed into.                    |

{% hint style="info" %}
Updates and additions to the project configuration file can be done gradually as you test your pipeline in ADO. **No changes** are needed to perform initial CI/CD tests across your environments as it will install the core package containing an AccountNumber field on the Account object as an example.
{% endhint %}

#### I. Release Definition File

Before triggering a release across environments for DX@Scale, a [release definition file](https://sfpowerscripts.dxatscale.io/commands/release) is required. A release is defined by a YAML file, where you can specify the artifacts to be installed in the org, in addition to other parameters. The release will then be orchestrated based on the configuration of the YAML definition file.

The dxatscale-template [release-1.0.yml](https://github.com/dxatscale/dxatscale-template/blob/main/releasedefinitions/release-1.0.yml) file defines the initial core package artifact to be deployed across environments. As you test out and add/modify existing packages, this file can be modified or a new release definition file can be created.

```bash
release: "Release-1.0"
skipIfAlreadyInstalled: true
artifacts:
  #src-env-specific-alias-pre: main
  core: main
  #src-ui: main
  #src-access-management: main
  #src-env-specific-alias-post: main
changelog:
  workItemFilter: "issues/[0-9]+"
```

{% hint style="info" %}
The release stage in the **release.yml** file across the defined environments is where the release definition file is referenced. As you create new releases, revisit these sections and update the file to the preferred release definition file to deploy.
{% endhint %}

#### J. Change Log

[Change Logs](https://sfpowerscripts.dxatscale.io/commands/release#changelog) are created to the **changelog** branch in the repository if the release is successful. This is configured in the template using the `--generatechangelog` and `--branchname changelog` in the [orchestrator release](https://sfpowerscripts.dxatscale.io/commands/release) commands in sfpowerscripts.

**No changes** to this command is required unless you want to change the branch name to something different than **changelog**.

#### K. Build Initial Package Artifacts

Prior to creating the scratch org pools, an initial version of artifacts should be created in the Package Registry by sfpowerscripts based on the project configuration file. In the dxatscale-template, the initial **core package** will be generated once the pipeline is executed for the first time and the build stage is completed and has published to the Package Registry.

1. Commit changes to trigger pipeline (eg. Edit **AccountNumber\_\_c** field description)
2. Navigate to **Artifacts**
3. Verify that the latest **core** artifact has been created and tagged with **main** label.

#### L. Fetch Provisioned Developer Scratch Org from Pool

Once the **prepare-dev-pool.yml** has been completed successfully, a pool of active/unused developer scratch orgs tagged to the pool name **dev** will be available to be fetched and used to build new features.

```bash
sfp pool:fetch -a <SOAlias> -t dev -v <DevHub>
> ======== Scratch org details ========
KEY          VALUE
───────────  ────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
Id           2SR4t00000001QeGAI
orgId        00D0i0000009VO4
loginURL     https://force-data-6074.cs98.my.salesforce.com/
username     test-uaojizr8cqxi@example.com
password     oy)Lnjphoq7tj
expiryDate   2021-09-11
sfdxAuthUrl  force://PlatformCLI::cUMRoQtoy)Lnjphoq7tj9PXadNVRdeTvCzyhp[FhUNsQsZDesdiVBHjZQjoCukBJUauxagGJgQUng6?gyYwkRmz@force-data-6074.cs98.my.salesforce.com/
status       Assigned
```

#### M. Pull Requests and Merge to Main

1. Make changes
2. Commit
3. Raise a Merge Request
4. Confirm validation pipeline passes

#### N. Add New Packages

1. Update project configuration files
2. Update **validate.yml** configuration file for the **analyze-pmd** and **validate-package jobs** for new packages
3. Save and validate

#### O. Grant developers access to scratch org pools

For developers (who are on limited access license) to access scratch orgs created by the CI service user, for their local development, a sharing setting needs to be created on the ScratchOrgInfo object. The sharing setting should grant read/write access to the ScratchOrgInfo records owned by a public group consisting of the CI service user and a public group consisting of the developer users.

Create two public groups

1. CI Users (Admin users/ CI users who creates scratch orgs in pool)
2. Developers (developers who are allowed to fetch scratch orgs from pool),

Then create a sharing rule that grant read/write access to the ScratchOrgInfos records owned by the CI Users to Developers

The developers must also have object-level and FLS permissions on the ScratchOrgInfo object. One way to achieve this is to assign a permission set that has Read, Create, Edit and Delete access on ScratchOrgInfos, as well as Read and Edit access to the custom fields used for scratch org pooling: `Allocation_status__c`, `Password__c`, `Pooltag__c` and `SfdxAuthUrl__c`
