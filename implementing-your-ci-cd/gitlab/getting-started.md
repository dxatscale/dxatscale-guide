# GitLab Setup

## Getting Started

The following getting started guide will enable you to configure and setup CI/CD using **GitLab** and **DX@Scale** for **Salesforce**. Assuming you have reviewed and completed the prerequisite account setup and software tool installations, this guide will walk you through the initial setup process in Salesforce and GitLab using the [template](https://github.com/dxatscale/dxatscale-template) provided. Along the way, additional general tips and best practices will be highlighted to help you understand the template provided and enable you to customize as needed.

As always, we welcome any feedback from the community to continuously improve this user guide. Please [contact us](https://docs.dxatscale.io/about-us/contact-us) for any questions or concerns.

## Part I - GitLab Project Setup

The following steps will guide you through setting up the initial project, project access tokens, project variables and configuring your SSH keys.

### A. Configure SSH Keys in User Settings

[SSH keys](https://docs.gitlab.com/ee/ssh/index.html#gitlab-and-ssh-keys) allow you to establish a secure connection between your computer and GitLab. To stream line future git interactions with the repository in the GitLab, it recommended to add your SSH Key to the GitLab User Settings

{% hint style="info" %}
To generate an SSH key pair, follow the [instructions](https://docs.gitlab.com/ee/ssh/#generate-an-ssh-key-pair) from the GitLab docs.
{% endhint %}

1. Navigate to **User Settings > SSH Keys**
2. In the **Key** section, paste in the value of your public SSH key
3. **Title** will self-populate
4. Select a date value for **Expires at**
5. Click on the **Add key**

![](<../../.gitbook/assets/image (5) (1).png>)

### B. Create New Project

Most work in GitLab is done in a [project](https://docs.gitlab.com/ee/user/project/working\_with\_projects.html). Files and code are saved in projects, and most features are in the scope of projects.

1. From the **GitLab Menu**, click on **Projects > Create new project**
2. Select **Create blank project**
3. Enter **dxatscale-poc** for the **Project name**
4. Select your correct **Project URL**
5. Select a **"Other hosting service"** for the **Project deployment target (optional).**
6. Leave **Visibility Level** to default **Private** with **README** to be initialized into the repository
7. Click on the **Create project** button

![](<../../.gitbook/assets/image (6) (1).png>)

<figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

![](<../../.gitbook/assets/image (18) (1).png>)

### C. Create Project Access Token

[Project access tokens](https://docs.gitlab.com/ee/user/project/settings/project\_access\_tokens.html) are similar to personal access tokens except they are attached to a project rather than a user. For the template, the Project Access Token is used to enable pushing git tags and change logs to the repository.

{% hint style="info" %}
Project Access Tokens are only supported on self-managed instances on Free Tier and above and GitLab SaaS Premium and above.
{% endhint %}

1. From the **Project Menu**, click on **Settings > Access Tokens**
2. Enter in **PROJECT\_ACCESS\_TOKEN** for the **Token name**
3. Set the **Expiration date** to a preferred date
4. Select the role to **Maintainer** for **"Select a role"**
5. For the **Select scopes**, check the **api** option
6. Click on the **Create project access token** button
7. Save the **project access token value** to be used in subsequent steps in the project variable steps.

![](<../../.gitbook/assets/image (2).png>)

![](<../../.gitbook/assets/image (11) (1).png>)

### D. Create Project Variables

[Project Variables](https://docs.gitlab.com/ee/ci/variables/) are a type of environment variable that will be used to control the behaviour of jobs and pipelines. The template uses both variables and files in the CI/CD to setup the environment connections, NPM Registry Scope, Project Access Tokens, and optionally metrics dashboard connection details.

1. From the **Project Menu**, click on **Settings > CI/CD**
2. Scroll down to **Variables** and click on the **Expand** button
3. Click on **Add variable**
4. Enter **PROJECT\_ACCESS\_TOKEN** for the **Key** field
5. Enter the **Project Access Token Value** from previous steps in the **Value** field
6. In the **Flag** section, enable **Mask Variable** only and uncheck **Protect variable**
7. Leave **Environment Scope** to **All (default)**
8. Click on **Add variable** to save

![](<../../.gitbook/assets/image (47).png>)

![](<../../.gitbook/assets/image (62).png>)

Repeat the steps above and create the following variables below using the sfdxAuthUrl created earlier from the Salesforce CLI.

| Key                        | Value          | Type     | Scope         | Protect | Mask |
| -------------------------- | -------------- | -------- | ------------- | ------- | ---- |
| DEVHUB\_ALIAS              | devhub         | Variable | All (default) | No      | No   |
| DEVHUB\_SFDX\_AUTH\_URL    | \<sfdxAuthUrl> | File     | All (default) | No      | Yes  |
| NPM\_SCOPE                 | @dxatscale-poc | Variable | All (default) | No      | No   |
| PROD\_ALIAS                | prod           | Variable | All (default) | No      | No   |
| PROD\_SFDX\_AUTH\_URL      | \<sfdxAuthUrl> | File     | All (default) | No      | Yes  |
| PROJECT\_ACCESS\_TOKEN     | \<token>       | Variable | All (default) | No      | Yes  |
| SHAREDDEV\_ALIAS           | shareddev      | Variable | All (default) | No      | No   |
| SHAREDDEV\_SFDX\_AUTH\_URL | \<sfdxAuthUrl> | File     | All (default) | No      | Yes  |
| SIT\_ALIAS                 | sit            | Variable | All (default) | No      | No   |
| SIT\_SFDX\_AUTH\_URL       | \<sfdxAuthUrl> | File     | All (default) | No      | Yes  |
| ST\_ALIAS                  | st             | Variable | All (default) | No      | No   |
| ST\_SFDX\_AUTH\_URL        | \<sfdxAuthUrl> | File     | All (default) | No      | Yes  |
| UAT\_ALIAS                 | uat            | Variable | All (default) | No      | No   |
| UAT\_SFDX\_AUTH\_URL       | \<sfdxAuthUrl> | File     | All (default) | No      | Yes  |

![Project Variables](<../../.gitbook/assets/image (79).png>)

{% hint style="info" %}
The NPM\_SCOPE variable should start with the @ character. Read more about npm scope [here](https://docs.npmjs.com/cli/v7/using-npm/scope).
{% endhint %}

## Part II - Repository

### A. Clone Template Repository

The [dxatscale-template](https://github.com/dxatscale/dxatscale-template) repository contains the [.gitlab-ci.yml](https://docs.gitlab.com/ee/ci/yaml/gitlab\_ci\_yaml.html) configuration file for CI/CD jobs for DX@Scale. It exists in the root of of the directory which is the default configuration for GitLab. To start, clone the repository to your computer.

```bash
git clone https://github.com/dxatscale/dxatscale-template.git
```

![](<../../.gitbook/assets/image (79).png>)

### B. Clone Project Repository

1. Navigate to **Repository > Files**
2. Click on the **Clone** button to the right and copy the contents in **Clone with SSH** or **HTTPS**
3. Clone the repository to a folder on your computer

```bash
git clone git@gitlab.com:groupname/dxatscale-poc.git
```

![](<../../.gitbook/assets/image (8).png>)

### C. Copy Template Contents to Project Folder

There are a number of ways to copy the files over. Some sample commands with the cp and rsync commands are provided below or alternatively, you can copy the files manually.

{% hint style="success" %}
Ensure that you copy all hidden files/folders from the template **except** for the following folders **.git**, **.sfdx**, **.azure-pipelines**, **.github.** These are specific to the template git repository and/or templates for other pipelines that DX@Scale supports.

The root directory should contain a **.gitlab-ci.yml**, **.gitignore**, **.forceignores**, and **.forceignore**. The original **.git** from your project repository should be there.
{% endhint %}

#### **Sample Commands**

{% tabs %}
{% tab title="CP" %}
```bash
cp -vR dxatscale-template/* dxatscale-poc
```
{% endtab %}

{% tab title="RSYNC" %}
```
rsync -av dxatscale-template/* dxatscale-poc
```
{% endtab %}
{% endtabs %}

<figure><img src="../../.gitbook/assets/image (33).png" alt=""><figcaption><p>Template Folder Structure</p></figcaption></figure>

### D. Commit Changes to Repository

Once the template files have been copied and verified, you can now stage, commit, and push your changes to the main branch. This will baseline your code in the GitLab Project Remote Repository to get started.

{% hint style="info" %}
Add [**\[skip ci\]**](https://docs.gitlab.com/ee/ci/yaml/#skip-pipeline) to the commit message to ensure the pipeline does not trigger for the initial commit.
{% endhint %}

```bash
git add .
git commit -m "[skip ci] - Initial DX@Scale Template"
git push
```

### E. Validate in GitLab

Once the files have been committed, you can verify the files have been pushed the repository and the initial pipeline has skipped being triggered.

1. Navigate to **Repository > Files**
2. Verify all the files are visible in the repository

![](<../../.gitbook/assets/image (29) (1).png>)

1. Navigate to **CI/CD > Pipelines**
2. Verify the pipeline has been skipped

![](<../../.gitbook/assets/image (28) (1).png>)

## Part III - DX@Scale Setup

In this section, we will review and optionally customize the configuration files in the default template, setup schedule jobs for Scratch Org Pool Creation, and test the pipelines to deploy across your environments using the Package Registry.

### A. Scratch Org Definition File

The [project-scratch-def.json](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_scratch\_orgs\_def\_file.htm) is a blueprint for a scratch org. It mimics the shape of an org that you use in the development life cycle, such as sandbox, packaging, or production.

Customize the provided scratch org definition file for your use case and save and commit the file to repository. If you want to use the file as is to test, **no action** is required.

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

### B. Using Scratch Orgs with Org Shape

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

{% hint style="info" %}
Scratch Org Definition files that use Org Shape, the attribute `"edition": "Enterprise",`needs to be removed as this will generate an error of <mark style="color:red;">"INVALID\_FIELD: When attempting to copy an org's shape, edition cannot be specified."</mark> during Scratch Org Pool Creation.
{% endhint %}

### C. Scratch Org Pool Configuration Files

The [Scratch Org Pool configuration](https://sfpowerscripts.dxatscale.io/commands/prepare/scratch-org-pool-configuration) defines the pool of scratch orgs in sfpowerscripts. The [JSON Schema definition file](https://raw.githubusercontent.com/Accenture/sfpowerscripts/develop/packages/sfpowerscripts-cli/resources/schemas/pooldefinition.schema.json) describes in detail which properties are accepted by the configuration file.

Your Dev Hub org edition determines your scratch org [allocations](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_scratch\_orgs\_editions\_and\_allocations.htm). These allocations determine how many scratch orgs you can create daily, and how many can be active at a given point.

#### Supported Scratch Org Editions

* Developer
* Enterprise
* Group
* Professional

#### Supported Dev Hub Editions and Associated Scratch Org Allocations

| Edition                    | Active Scratch Org Allocation | Daily Scratch Org Allocation |
| -------------------------- | ----------------------------- | ---------------------------- |
| Developer Edition or Trial | 3                             | 6                            |
| Enterprise Edition         | 40                            | 80                           |
| Unlimited Edition          | 100                           | 200                          |
| Performance Edition        | 100                           | 200                          |

{% hint style="info" %}
Depending on your Dev Hub licensing, there are limits on the number of active and daily scratch orgs you can create daily. sfpowerscripts will take this in account if you specify the **maxAllocation** property to a number more than you are allocated by Salesforce.
{% endhint %}

There are two configuration files defined in the template:

**Continuous Integration (CI) Pool** - [project-ci-pool-def.json](https://github.com/dxatscale/dxatscale-template/blob/main/config/project-ci-pool-def.json)

```bash
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
        "scope": "@dxatscale-poc",
      }
    }

 }
```

**Developer Pool** - [project-dev-pool-def.json](https://github.com/dxatscale/dxatscale-template/blob/main/config/project-dev-pool-def.json)

```bash
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
          "scope": "@dxatscale-poc",
        }
      }

}
```

{% hint style="info" %}
Update the "**scope**" value for "**npm**" from the default "**@org-name**" to your defined scope in the previous project variables section. (eg. **@dxatscale-poc**)
{% endhint %}

### D. Project Configuration File

The [project configuration file](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_ws\_config.htm) **sfdx-project.json** indicates that the directory is a Salesforce DX project. The configuration file contains project information and facilitates the authentication of scratch orgs and the creation of second-generation packages. It also tells the CLI where to put files when syncing between the project and scratch org.

The dxatscale-template [project configuration file](https://github.com/dxatscale/dxatscale-template/blob/main/sfdx-project.json) contains initial, pre-defined package directories based on our best practices for [repository structure](https://docs.dxatscale.io/scm/repository-structure) and modularization.

{% hint style="info" %}
When you push the source to the org, the metadata is deployed in the order that you list the package directories in [sfdx-project.json](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_ws\_mpd.htm)
{% endhint %}

| Package                         | Description                                                                                                                                                                                                                                                                                                   |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **src-env-specific-pre**        | Installed first across all release environments.                                                                                                                                                                                                                                                              |
| **src-env-specific-alias-pre**  | Installed after src-env-specific-pre and is only used when any environment specific metadata has to be aligned with each environments                                                                                                                                                                         |
| **src/core-\***                 | A folder to house all the core model of your org which is shared with all other domains.                                                                                                                                                                                                                      |
| **src/frameworks**              | A folder to house all the core model of your org which is shared with all other domains.                                                                                                                                                                                                                      |
| **src-ui**                      | This folder would include page layouts, FlexiPages and Lightning/Classic apps unless we are sure these will only reference the components of a single domain package and its dependencies. In general custom UI components such as LWC, Aura and VisualForce should be included in a relevant domain package. |
| **src-access-management**       | This package is typically one of the packages that is deployed second to last in the deployment order and used to store profiles, permission sets, and permission set groups that are applied across the org.                                                                                                 |
| **src-env-specific-alias-post** | Installed after src-env-specific-pre and is only used when any environment specific metadata has to be aligned with each environments                                                                                                                                                                         |
| **src-temp**                    | This folder is marked as the default folder in sfdx-project.json. This is the landing folder for all metadata and this particular folder doesn't get deployed anywhere other than a developers scratch org. This place is utilized to decide where the new metadata should be placed into.                    |

{% hint style="info" %}
Updates and additions to the project configuration file can be done gradually as you test your pipeline in GitLab. **No changes** are needed to perform initial CI/CD tests across your environments as it will install the core package containing a AccountNumber field on the Account object as an example.
{% endhint %}

### E. Release Definition File

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
promotePackagesBeforeDeploymentToOrg: "SIT"  
changelog:
  workItemFilter: "issues/[0-9]+"
```

{% hint style="info" %}
The release stage in the **.gitlab-ci.yml** file across the defined environments is where the release definition file is referenced. As you create new releases, revisit these sections and update the file to the preferred release definition file to deploy.
{% endhint %}

### F. Change Log

[Change Logs](https://sfpowerscripts.dxatscale.io/commands/release#changelog) are created to the **changelog** branch in the repository if the release is successful. This is configured in the template using the `--generatechangelog` and `--branchname changelog` in the [orchestrator release](https://sfpowerscripts.dxatscale.io/commands/release) commands in sfpowerscripts.

**No changes** to this command is required unless you want to change the branch name to something different than **changelog**.

![](<../../.gitbook/assets/image (34).png>)

### G. Build Initial Package Artifacts

Prior to creating the scratch org pools, an initial version of artifacts should be created in the Package Registry by sfpowerscripts based on the project configuration file. In the dxatscale-template, the initial **core package** will be generated once the pipeline is executed for the first time and the build stage is completed and has published to the Package Registry.

1. Commit changes to trigger pipeline (eg. Edit **AccountNumber\_\_c** field description) to the **Main Branch** directly.
2. Wait for the CI/CD initial jobs to complete the following stages "**quickbuild**, **deploy**, **build**"
3. Navigate to **Package & Registries > Package Registry**
4. Verify that the latest **core** artifact has been created and tagged with **main** label.

![](<../../.gitbook/assets/image (27).png>)

### H. Scheduled Jobs

[Pipeline schedules](https://docs.gitlab.com/ee/ci/pipelines/schedules.html#pipeline-schedules) are used to schedule pipelines at specific intervals. For the dxatscale-template, we leverage scheduled jobs in GitLab to prepare CI and developer scratch org pools, clean pools daily, publish scratch org and DevOps metrics to dashboards, and manually delete fetched developer scratch orgs.

1. Navigate to **CI/CD > Schedules**
2. Click on **New schedule**
3. Enter **schedule-prepare-ci-pool** for **Description**
4. Click on **Custom** for **Interval Pattern** and enter value of **0 23 \* \* \***
5. Update **Cron Timezone** based on your region
6. Leave **Target Branch** to **main**
7. Add **TARGETTASKNAME** for the **Variable Key**.
8. Add **schedule-prepare-ci-pool** for the **Variable Value**
9. Keep **Activated** checked to **Active**
10. Click **Save pipeline schedule**

![](<../../.gitbook/assets/image (40) (1).png>)

Repeat the steps above for all the scheduled jobs below. Interval Pattern should be scheduled during non-peak development windows for your development team to ensure limited disruption.

| Description                   | Interval Pattern | Variable Key   | Variable Value            |
| ----------------------------- | ---------------- | -------------- | ------------------------- |
| **schedule-prepare-ci-pool**  | 0 23 \* \* \*    | TARGETTASKNAME | schedule-prepare-ci-pool  |
| **schedule-prepare-dev-pool** | 0 22 \* \* \*    | TARGETTASKNAME | schedule-prepare-dev-pool |
| **schedule-clean-pool**       | 0 19 \* \* \*    | TARGETTASKNAME | schedule-clean-pool       |
| **schedule-report-so-pool**   | 0 \* \* \* \*    | TARGETTASKNAME | schedule-report-so-pool   |

{% hint style="info" %}
**schedule-report-so-pool** is an optional job to configure if you intend to integrate to a Dashboard Platform such as New Relic and Data Dog. If not, you can skip this configuration.
{% endhint %}

![](<../../.gitbook/assets/image (31).png>)

Once all schedule jobs have been configured, you can trigger the **schedule-prepare-ci-pool** and **schedule-prepare-dev-pool** jobs manually by clicking on the **play button** for each job.

The default tags for the pools are **ci** and **dev** and these can be referenced in future steps to retrieve developer sandboxes.

### I. Fetch Provisioned Developer Scratch Org from Pool

Once the **schedule-prepare-dev-pool** has completed successfully, a pool of active/unused developer scratch orgs tagged to the pool name **dev** will be available to be fetched and used to build new features.

```bash
sfdx sfpowerscripts:pool:fetch -a <SOAlias> -t dev -v <DevHub>
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

### J. Manually Delete Fetched Scratch Org

1. Navigate to **CI/CD > Pipelines**
2. Click on **Run Pipeline**
3. Enter in the username for the developer scratch org (eg. **test-uaojizr8cqxi@example.com**) for the value of **SCRATCH\_ORG\_USERNAME** variable key
4. Enter **manual-delete-fetched-so** value for the **TARGETTASKNAME** variable key
5. Click on **Run pipeline**

![](<../../.gitbook/assets/image (35).png>)

### K. Merge Requests and Merge to Main

1. Make changes
2. Commit
3. Raise a Merge Request
4. Confirm validation pipeline passes

### L. Add New Packages

1. Update project configuration files
2. Update **.gitlab-ci.yml** configuration file for the **analyze-pmd** and **validate-package jobs** for new packages
3. Save and validate

## Troubleshooting Tips

**Release Errors**

\*\*Error: \*\*

* ERROR running auth:sfdxurl:store: ENOENT: no such file or directory, open '\[MASKED]'

**Resolution:**

1. Review the ENV\_SFDX\_AUTH\_URL is configured to "File" Type instead of "Variable".

## Final Words

Congratulations! you have gone through the GitLab pipeline journey and made it to the end.

I hope you have learned a great deal through this. As for where you go from here, this is not the end but just the beginning:

Want to ask more about any of these practices, ask the team directly on [Slack](https://dxatscale.slack.com). Click [here](https://launchpass.com/dxatscale) to get an invite.

And to discuss and contribute to our open-source projects [here](https://docs.dxatscale.io/about-us/contact-us#discussions).
