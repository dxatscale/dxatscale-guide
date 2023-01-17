# GitHub Setup

## Getting Started

The following getting started guide will enable you to configure and setup CI/CD using GitHub and DX@Scale for Salesforce. Assuming you have reviewed and completed the prerequisite account setup and software tool installations, this guide will walk you through the initial setup process in Salesforce and GitHub using the [template](https://github.com/dxatscale/dxatscale-template) provided. Along the way, additional general tips and best practices will be highlighted to help you understand the template provided and enable you to customize as needed.

As always, we welcome any feedback from the community to continuously improve this user guide. Please [contact us](https://docs.dxatscale.io/about-us/contact-us) with any questions or concerns.

{% embed url="https://www.youtube.com/watch?v=TH73diX57w8" %}

## A. Clone Repo

Go to the repo: [https://github.com/dxatscale/dxatscale-template](https://github.com/dxatscale/dxatscale-template)

Click on **Use this template**

![](../../.gitbook/assets/screen-shot-2021-09-09-at-10.09.06-am.png)

Enter in a **Repository name**, set your repo to **Private** and click **Create repository from template**

![](../../.gitbook/assets/screen-shot-2021-09-09-at-10.09.25-am.png)

## B. Setup your Secrets

Follow instructions in[ 2.F](getting-started.md#f-authenticate-to-lower-sandbox-environments-via-cli) to fetch all the authURL for each environment.

1. On GitHub, navigate to the main page of the repository.
2. Under your repository name, click on the "Settings" tab.
3. In the left sidebar, click Secrets.
4. On the right bar, click on "New repository secret"

![](../../.gitbook/assets/screen-shot-2021-09-09-at-10.35.06-am.png)

Under **Name** type in `DEVHUB_SFDX_AUTH_URL` and under **Value**, copy and paste the `sfdxAuthUrl` from `authfile.json`

![](../../.gitbook/assets/screen-shot-2021-09-09-at-10.45.34-am.png)

{% hint style="info" %}
Once you have done that repeat this step for all other orgs you have for your organisation such as SIT, QA, STAGING, PROD and so on. this is important when we go through the release stage of the pipelines. e.g. PROD\_SFDX\_AUTH\_URL
{% endhint %}

## C. Test your pipelines

![](../../.gitbook/assets/screen-shot-2021-09-09-at-10.50.57-am.png)

It is recommended to test your pipelines by triggering the CI Pipeline - Auto triggered by triggering it manually. Monitor the pipeline till it produces a set of packages and publishes to GitHub Packages. If this stage is successful, you can proceed to step 5

## D. Configure Scratch Org Pools

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
        "scope": "MY_PROJECT_NAME",
        "npmtag": "main"
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
          "scope": "MY_PROJECT_NAME",
          "npmtag": "main"
        }
      }

}
```

{% hint style="info" %}
Update the "**scope**" value for "**npm**" from the default "**@org-name**" to your defined scope in the previous project variables section. (eg. **@dxatscale-poc**)
{% endhint %}

{% hint style="info" %}
To get an in-depth understanding of the options available to you for configuration refer to this link [here](https://docs.dxatscale.io/sfpowerscripts/prepare/scratch-org-pool-configuration).
{% endhint %}

## E. Scratch Org Definition File

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

## F. Project Configuration File

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
Updates and additions to the project configuration file can be done gradually as you test your pipeline in GitHub. **No changes** are needed to perform initial CI/CD tests across your environments as it will install the core package containing an AccountNumber field on the Account object as an example.
{% endhint %}

## G. Release Definition File

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

## H. Change Log

[Change Logs](https://sfpowerscripts.dxatscale.io/commands/release#changelog) are created to the **changelog** branch in the repository if the release is successful. This is configured in the template using the `--generatechangelog` and `--branchname changelog` in the [orchestrator release](https://sfpowerscripts.dxatscale.io/commands/release) commands in sfpowerscripts.

**No changes** to this command is required unless you want to change the branch name to something different than **changelog**.

## I. Build Initial Package Artifacts

Prior to creating the scratch org pools, an initial version of artifacts should be created in the Package Registry by sfpowerscripts based on the project configuration file. In the dxatscale-template, the initial **core package** will be generated once the pipeline is executed for the first time and the build stage is completed and has published to the Package Registry.

1. Commit changes to trigger pipeline (eg. Edit **AccountNumber\_\_c** field description)
2. Navigate to **Package & Registries > Package Registry**
3. Verify that the latest **core** artifact has been created and tagged with **main** label.

#### J. Fetch Provisioned Developer Scratch Org from Pool

Once the **schedule-prepare-dev-pool** has been completed successfully, a pool of active/unused developer scratch orgs tagged to the pool name **dev** will be available to be fetched and used to build new features.

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

## K. Pull Requests and Merge to Main

1. Make changes
2. Commit
3. Raise a Merge Request
4. Confirm validation pipeline passes

## L. Add New Packages

1. Update project configuration files
2. Update **validate.yml** configuration file for the **analyze-pmd** and **validate-package jobs** for new packages
3. Save and validate

### Dashboard Integration

#### A. New Relic Configurations

Within your repo there is a folder called `dashboards/NewRelic`

To set up your NewRelic dashboard you will need to:

* Replace with your NewRelic account id, in your cicd-dashboard.json
* Goto NewRelic, and Click on Import and import dashboard to NewRelic
* Set your pipelines environment variables with the following

```
   SFPOWERSCRIPTS_NEWRELIC='true'
   SFPOWERSCRIPTS_NEWRELIC_API_KEY='${{ secrets.NEWRELIC_INSIGHT_INSERT_KEYS }}'
```

* Check the templates for further examples

#### B. Data Dog Configuration

To set up your Data Dog dashboard simply go to each of the pipelines and you will notice a commented out snippet

```
#Set the environment variables for tracking metrics
#env:
  #SFPOWERSCRIPTS_DATADOG: 'true'
  #SFPOWERSCRIPTS_DATADOG_HOST: '${{ secrets.DATADOG_HOST }}'
  #SFPOWERSCRIPTS_DATADOG_API_KEY: '${{ secrets.DATADOG_API_KEY }}'
```

Create the following secrets:

* `DATADOG_HOST`
* `DATADOG_API_KEY`

{% hint style="info" %}
If you haven't created an API key from data dog yet refer to this [link](https://docs.datadoghq.com/account\_management/api-app-keys/)
{% endhint %}

Uncomment all env jobs on all pipelines and it should look like this:

```yaml
#Set the environment variables for tracking metrics
env:
  SFPOWERSCRIPTS_DATADOG: 'true'
  SFPOWERSCRIPTS_DATADOG_HOST: '${{ secrets.DATADOG_HOST }}'
  SFPOWERSCRIPTS_DATADOG_API_KEY: '${{ secrets.DATADOG_API_KEY }}'
```

### Final Words

Congratulations! you have gone through the Github Actions pipeline journey and made it to the end.

I hope you have learned a great deal through this. as for where you go from here this is not the end but just the beginning:

Want to ask more about any of these practices, ask the team directly on [Slack](https://dxatscale.slack.com), Click [here](https://launchpass.com/dxatscale) to get an invite.

And to discuss and contribute to our open-source projects [here](https://docs.dxatscale.io/about-us/contact-us#discussions)
