# Prerequisites

The following lists of items are required to setup your end-to-end pipeline on either [GitHub](https://github.com/), [GitLab](https://about.gitlab.com/free-trial/) or [Azure DevOps](https://azure.microsoft.com/en-au/services/devops/#overview) and [Salesforce](https://www.salesforce.com). Support for future CI/CD pipeline tools will be added in the future as needed.

## DevOps Platform <a href="#devops-platform" id="devops-platform"></a>

* [ ] ​[GitHub Account​](https://github.com/join)
* [ ] [​GitLab Account​](https://about.gitlab.com/free-trial/)
* [ ] ​[Azure DevOps Account](https://azure.microsoft.com/en-au/services/devops/#overview)

## Salesforce Org <a href="#salesforce" id="salesforce"></a>

A Salesforce Org of the following types that allows for enabling the org as a [DevHub](https://help.salesforce.com/s/articleView?language=en\_US\&type=5\&id=sf.sfdx\_setup\_enable\_devhub.htm) is required. Ensure you have [System Administrator](https://help.salesforce.com/s/articleView?id=How-to-change-Administrators-1327365222554\&language=en\_US\&r=https%3A%2F%2Fwww.google.com%2F\&type=1) access.

{% hint style="info" %}
To setup a proper pipeline, a minimum of 2 orgs will be required to configured in the pipeline to deploy a release. If you do not have access to a Production or Trial Org that can support sandboxes, you will need to have to create multiple developer edition or trailhead playground orgs to configure the pipeline.
{% endhint %}

### No Sandboxes Available

* [ ] [Developer Edition Org](https://developer.salesforce.com/signup)
* [ ] [Trailhead Playground Org](https://trailhead.salesforce.com/content/learn/modules/trailhead\_playground\_management)

### Sandbox Available

* [ ] [Trial Org](https://www.salesforce.com/form/signup/freetrial-sales-ee/)
* [ ] [Production Org](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_auth\_prod\_org.htm)​

## Licenses <a href="#developer-tools" id="developer-tools"></a>

[Free Limited Access Licenses](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/dev\_hub\_license.htm) are available for Production Orgs to enable non-admin users in your production org. This is recommended to be requested to your Salesforce Account Executive to request this free license that will appear in as a new standard profile in your org with the name "**Limited Access User**" and User License "**Salesforce Limited Access - Free**"

* [ ] [Free Limited Access License](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/dev\_hub\_license.htm)

<figure><img src="../.gitbook/assets/image (71).png" alt=""><figcaption><p>Salesforce Limited Access - Free License</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption><p>Profile: Limited Access User</p></figcaption></figure>

{% hint style="info" %}
A maximum of 1 user license of "Salesforce Limited Access - Free" for every 2 scratch org licenses will be provided. Scratch Org [allocations](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_scratch\_orgs\_editions\_and\_allocations.htm) varies depending on your edition.\
\
These will be used for fetching Scratch Orgs from the Scratch Org Pools for your developers.
{% endhint %}

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption><p>Scratch Org Allocations for Dev Hub Editions</p></figcaption></figure>

{% hint style="info" %}
Alternatively, if you are experimenting in a Developer Edition Org or a Production Org that does not have the Free Limited Access License, you can use the "[Minimum Access - Salesforce](https://help.salesforce.com/s/articleView?id=release-notes.rn\_forcecom\_general\_new\_profile.htm\&type=5\&release=226)" as your profile assignment to your developers instead. They will still consume a Salesforce or Salesforce Platform License so factor this into your decision. Best practice is to clone the "Minimum Access - Salesforce" Standard Profile and use the custom version.
{% endhint %}

## Developer Tools <a href="#developer-tools" id="developer-tools"></a>

* [ ] ​[Visual Studio Code IDE](https://code.visualstudio.com/download)​
  * [ ] ​[Salesforce Extension Pack](https://marketplace.visualstudio.com/items?itemName=salesforce.salesforcedx-vscode)
  * [ ] [Salesforce Extension Pack (Expanded)​](https://marketplace.visualstudio.com/items?itemName=salesforce.salesforcedx-vscode-expanded)
  * [ ] **Optional Extensions**
    * [ ] [Salesforce Package.xml Generator Extension for VS Code](https://marketplace.visualstudio.com/items?itemName=VignaeshRamA.sfdx-package-xml-generator)
    * [ ] ​[Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)​
    * [ ] ​[Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)​​
    * [ ] [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one)
    * [ ] [Markdown PDF](https://marketplace.visualstudio.com/items?itemName=yzane.markdown-pdf)​​
* [ ] ​[git](https://git-scm.com)​
* [ ] ​[Salesforce CLI](https://www.npmjs.com/package/sfdx-cli)
* [ ] [Node.js](https://nodejs.org/en/download/)
* [ ] [​sfpowerkit Plugin](https://github.com/dxatscale/sfpowerkit)​
* [ ] [​sfpowerscripts Plugin](https://github.com/dxatscale/sfpowerscripts)​
* [ ] ​[SFDX-Data-Move-Utility (SFDMU) Plugin](https://github.com/forcedotcom/SFDX-Data-Move-Utility)​

## Dashboard Platform (Optional) <a href="#dashboard-platform" id="dashboard-platform"></a>

* ​[New Relic Account](https://newrelic.com/signup) _(Optional)_
* [Data Dog Account](https://www.datadoghq.com) (Optional)
* Other [StatsD](https://github.com/statsd/statsd) Compatible Monitoring Platform _(Optional)_
