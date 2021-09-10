# Getting Started

The following getting started guide will enable you to configure and setup CI/CD using GitLab and DX@Scale for Salesforce.  Assuming you have reviewed and completed the prerequisite account setup and software tool installations, this guide will walk you through the initial setup process in Salesforce and GitLab using the [template](https://github.com/dxatscale/dxatscale-template) provided.  Along the way, additional general tips and best practices will be highlighted to help you understand the template provided and enable you to customize as needed.

As always, we welcome any feedback from the community to continuously improve upon this user guide so please [contact us](https://docs.dxatscale.io/about-us/contact-us) for any questions or concerns.

## Developer Workstation

In order to successfully troubleshoot and interact with GitLab and Salesforce using the CLI, the following commands should be executed on your computer to validate you have the tools configured correctly.  Depending on your workstation operating system \(eg. **Mac OS, Windows, Linux**\), there may be some variation in the commands and outputs below on your terminal window.

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

## Salesforce

To enable modular package development, there are a few configurations in Salesforce as a System Administrator that needs to be enabled to create Scratch Orgs and Unlock Packages.

### A. Enable Dev Hub

[Enable Dev Hub](https://help.salesforce.com/s/articleView?id=sf.sfdx_setup_enable_devhub.htm&type=5) features in your Salesforce org so you can create and manage scratch orgs, create and manage second-generation packages. Scratch orgs are disposable Salesforce orgs to support development and testing.

1. Navigate to the **Setup** menu
2. Go to **Development &gt; Dev Hub**
3. Toggle the button to on for **Enable Dev Hub**

![](../../../.gitbook/assets/image%20%282%29.png)

### B. Enable Unlocked Packages and Second-Generation Managed Packages

[Unlocked packages](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_unlocked_pkg_intro.htm) help organize your existing metadata, package an app, extend an app that you’ve purchased from AppExchange, or package new metadata.

1. Navigate to the **Setup** menu
2. Go to **Development &gt; Dev Hub**
3. Toggle the button to on for **Enable Unlocked Packages and Second-Generation Managed Packages**

![](../../../.gitbook/assets/image.png)

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

The [sfpowerscripts-artifact package](https://github.com/Accenture/sfpowerscripts/tree/develop/prerequisites/sfpowerscripts-artifact) is a lightweight unlocked package consisting of a custom setting SfpowerscriptsArtifact2\_\_c that is used to keep record of the artifacts that have been installed in the org. This enables package installation, using sfpowerscripts, to be skipped if the same artifact version already exists in the org.

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
Assuming that Production is also your Dev Hub, we recommend that you still create multiple CLI connections to segregate the environments.
{% endhint %}

Additional environments and customization can be made once you are familiar with the scripts.  

```bash
sfdx auth:web:login -a <orgAlias> -r https://test.salesforce.com
```



## GitLab: Part I

### A. Create New Project

Most work in GitLab is done in a [project](https://docs.gitlab.com/ee/user/project/working_with_projects.html). Files and code are saved in projects, and most features are in the scope of projects.

1. From the **GitLab Menu**, click on **Projects &gt; Create new project**
2. Select **Create blank project**
3. Enter **dxatscale-poc** for the **Project name**
4. Select your correct **Project URL**
5. Enter a **Project description \(optional\)** as needed
6. Leave **Visibility Level** to default **Private** with **README** to be initialized into the repository
7. Click on the **Create project** button

![](../../../.gitbook/assets/image%20%283%29.png)

![](../../../.gitbook/assets/image%20%287%29.png)

![](../../../.gitbook/assets/image%20%2810%29.png)

### B. Create Project Access Token

[Project access tokens](https://docs.gitlab.com/ee/user/project/settings/project_access_tokens.html) are similar to personal access tokens except they are attached to a project rather than a user. For the template, the Project Access Token is used to enable pushing git tags and change logs to the repository. 

{% hint style="info" %}
Project Access Tokens are only supported on self-managed instances on Free tier and above and GitLab SaaS Premium and above.
{% endhint %}

1. From the **Project Menu**, click on **Settings &gt; Access Tokens**
2. Enter in **PROJECT\_ACCESS\_TOKEN** for the **Token name**
3. Set the **Expiration date** to a preferred date
4. Leave the default role to **Maintainer**
5. For the **Select scopes**, check the **api** option
6. Click on the **Create project access token** button
7. Save the **project access token value** to be used in subsequent steps in the project variable steps.

![](../../../.gitbook/assets/image%20%281%29.png)

![](../../../.gitbook/assets/image%20%286%29.png)

### C. Create Project Variables

[Project access tokens](https://docs.gitlab.com/ee/user/project/settings/project_access_tokens.html) are simila

## Repository

A. Clone Repository



## GitLab: Part II



```
$ give me super-powers
```

{% hint style="info" %}
 Super-powers are granted randomly so please submit an issue if you're not happy with yours.
{% endhint %}

Once you're strong enough, save the world:

{% code title="hello.sh" %}
```bash
# Ain't no code for that yet, sorry
echo 'You got to trust me on this, I saved the world'
```
{% endcode %}



## Closing Thoughts

Good luck on your journey.

