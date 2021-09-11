# Getting Started

The following getting started guide will enable you to configure and setup CI/CD using GitLab and DX@Scale for Salesforce.  Assuming you have reviewed and completed the prerequisite account setup and software tool installations, this guide will walk you through the initial setup process in Salesforce and GitLab using the [template](https://github.com/dxatscale/dxatscale-template) provided.  Along the way, additional general tips and best practices will be highlighted to help you understand the template provided and enable you to customize as needed.

As always, we welcome any feedback from the community to continuously improve this user guide. Please [contact us](https://docs.dxatscale.io/about-us/contact-us) for any questions or concerns.

## 1. Developer Workstation

In order to successfully troubleshoot and interact with GitHub and Salesforce using the CLI, the following commands should be executed on your computer to validate you have the tools configured correctly.  Depending on your operating system \(eg. **Mac OS, Windows, Linux**\), there may be some variation in the commands and outputs below on your terminal window.

###  Git

```bash
git version
> git version 2.32.0
```

### SFDX CLI

```bash
sfdx version
> sfdx-cli/7.110.0 darwin-x64 node-v16.6.0
```

### SFDX Plugins

```bash
sfdx plugins
> @dxatscale/sfpowerscripts 8.2.1
  sfdmu 4.4.5
  sfpowerkit 3.2.2
```

### Visual Studio Code

```bash
code --version
> 1.60.0
e7d7e9a9348e6a8cc8c03f877d39cb72e5dfb1ff
x64
```

### NPM

```bash
npm --version
> 7.19.1
```

## 2. Salesforce

To enable modular package development, there are a few configurations in Salesforce as a System Administrator that needs to be turned on to be able to create Scratch Orgs and Unlock Packages.

### A. Enable Dev Hub

[Enable Dev Hub](https://help.salesforce.com/s/articleView?id=sf.sfdx_setup_enable_devhub.htm&type=5) in your Salesforce org so you can create and manage scratch orgs and second-generation packages. Scratch orgs are disposable Salesforce orgs to support development and testing.

1. Navigate to the **Setup** menu
2. Go to **Development &gt; Dev Hub**
3. Toggle the button to on for **Enable Dev Hub**

![](../../../.gitbook/assets/image%20%283%29.png)

### B. Enable Unlocked Packages and Second-Generation Managed Packages

[Unlocked packages](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_unlocked_pkg_intro.htm) help organize your existing metadata, package an app, extend an app that you’ve purchased from AppExchange, or package new metadata.

1. Navigate to the **Setup** menu
2. Go to **Development &gt; Dev Hub**
3. Toggle the button to on for **Enable Unlocked Packages and Second-Generation Managed Packages**

![](../../../.gitbook/assets/image%20%281%29.png)

### C. Authenticate to DevHub via CLI

Authorize your production instance and/or Developer Edition Org using the [web login flow](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_auth_web.htm).  The example below uses "**DevHub**" as the alias for the instance where you will use to create Unlock Packages and manage Scratch Orgs.

```bash
sfdx auth:web:login -a DevHub -r https://login.salesforce.com
```

### D. Install sfpowerscripts Scratch Org Pooling Unlocked Package in DevHub

The [Scratch Org Pooling Unlocked Package](https://github.com/Accenture/sfpowerscripts/tree/develop/prerequisites/scratchorgpool) adds additional custom fields, validation rule, and workflow to the standard object "**ScratchOrgInfo**" in the the DevHub to enable associated scratch org pool commands to work for the pipeline.

```bash
sfdx force:package:install -p 04t1P000000gOqzQAE -u DevHub -r -a package -s AdminsOnly -w 30
```

### E. Install sfpowerscripts-artifact Unlocked Package in DevHub and Lower Existing Sandboxes

The [sfpowerscripts-artifact package](https://github.com/Accenture/sfpowerscripts/tree/develop/prerequisites/sfpowerscripts-artifact) is a lightweight unlocked package consisting of a custom setting **SfpowerscriptsArtifact2\_\_c** that is used to keep record of the artifacts that have been installed in the org. This enables package installation, using sfpowerscripts, to be skipped if the same artifact version already exists in the org.

```bash
sfdx force:package:install --package 04t1P000000ka9mQAA -u <OrgAlias> --securitytype=AdminsOnly --wait=120
```

### F. Authenticate to Lower Sandbox Environments via CLI

The template assumes you are following the environment strategy defined in our DX@Scale Guide.  The following sandboxes are recommended to be created and [authenticated](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_auth_web.htm) first prior to running the pipeline.  

* SHAREDDEV \(Shared Development\)
* ST \(System Test\)
* SIT \(System Integration Test\)
* UAT \(User Acceptance Test\)
* PROD \(Production\)

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

### G. Generate SFDX auth URL for Pipeline Authentication

In order for the GitHub pipeline to authenticate to the DevHub and other environments, [SFDX auth URL](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_auth_sfdxurl.htm) is the preferred method over [JWT Bearer Flow](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_auth_jwt_flow.htm).  For each environment, execute the following command on a previously authenticated environment and save the sfdxAuthUrl for use in future pipeline configuration steps.

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

## 3. GitHub

### A. Clone Repo

Go to the repo: [https://github.com/dxatscale/dxatscale-template](https://github.com/dxatscale/dxatscale-template)

Click on **Use this template**

![](../../../.gitbook/assets/screen-shot-2021-09-09-at-10.09.06-am.png)

Enter in a **Repository name**, set your repo to **Private** and click **Create repository from template**

![](../../../.gitbook/assets/screen-shot-2021-09-09-at-10.09.25-am.png)

### B. Setup your Secrets

Follow instructions in[ 2.F](getting-started.md#f-authenticate-to-lower-sandbox-environments-via-cli) to fetch all the authURL for each environment.

1. On GitHub, navigate to the main page of the repository.
2. Under your repository name, click on the "Settings" tab.
3. In the left sidebar, click Secrets.
4. On the right bar, click on "New repository secret"

![](../../../.gitbook/assets/screen-shot-2021-09-09-at-10.35.06-am.png)

Under **Name** type in `DEVHUB_SFDX_AUTH_URL` and under **Value**, copy and paste the `sfdxAuthUrl` from `authfile.json`

![](../../../.gitbook/assets/screen-shot-2021-09-09-at-10.45.34-am.png)

{% hint style="info" %}
Once you have done that repeat this step for all other orgs you have for your organisation such as SIT, QA, STAGING, PROD and so on. this is important when we go through the release stage of the pipelines. e.g. PROD\_SFDX_\__AUTH\_URL
{% endhint %}

## 4. Test your pipelines

![](../../../.gitbook/assets/screen-shot-2021-09-09-at-10.50.57-am.png)

It is recommended to test your pipelines by triggering the CI Pipeline - Auto triggered by triggering it manually. Monitor the pipeline till it produces a set of packages and publishes to GitHub Packages.  If this stage is successful, you can proceed to step 5

## 5. Configure Scratch Org Pools

In your repo, there is a folder called config, in that folder, you can see there are two JSON files

* `project-ci-pool-def.json`
* `project-dev-pool-def.json`

As an overview Scratch Pools help development teams save the time taken to spin up scratch orgs allowing more time to be spent on development, installing all dependencies, and having it ready for development; in conjunction, we also use CI Pools.

To configure the time expiry and the number of orgs to be created and more, here are the file paths to the following scratch org definition YAML Files:

```text
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
To get an in-depth understanding of the options available to you for configuration refer to this link [here](https://sfpowerscripts.dxatscale.io/commands/prepare/scratch-org-pool-configuration).
{% endhint %}

