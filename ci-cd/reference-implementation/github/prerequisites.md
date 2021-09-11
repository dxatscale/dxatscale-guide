# Prerequisites



The following lists of items are required to setup your end-to-end pipeline using [GitHub](https://github.com/) and [Salesforce](https://www.salesforce.com/).‌

#### DevOps Platform <a id="devops-platform"></a>

* [ ] ​[GitHub Account​](https://github.com/join)

#### Salesforce <a id="salesforce"></a>

* [ ] ​[System Administrator Account](https://help.salesforce.com/s/articleView?id=How-to-change-Administrators-1327365222554&language=en_US&r=https%3A%2F%2Fwww.google.com%2F&type=1)​
* [ ] ​[Enable DevHub](https://help.salesforce.com/s/articleView?id=sf.sfdx_setup_enable_devhub.htm&type=5)​
* [ ] Create **Salesforce Service Account** in your DevHub that can be utilized create scratch orgs and deploy packages executing as the [CI Service Account](https://sfpowerscripts.dxatscale.io/getting-started/prerequisites#create-a-ci-service-user-in-production) using [AuthURL](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_auth_sfdxurl.htm)​
* [ ] Create [Permission Sets](https://developer.salesforce.com/docs/atlas.en-us.securityImplGuide.meta/securityImplGuide/perm_sets_overview.htm#:~:text=A%20permission%20set%20is%20a,access%20without%20changing%20their%20profiles.&text=Users%20can%20have%20only%20one,can%20have%20multiple%20permission%20sets.) and [Sharing Groups](https://sfpowerscripts.dxatscale.io/getting-started/prerequisites#grant-developers-access-to-scratch-org-pools) for Developers on DevHub to [fetch scratch orgs](https://github.com/Accenture/sfpowerkit/wiki/Getting-started-with-ScratchOrg-Pooling#4-fetch-scratch-org-from-a-pool) and work with Salesforce DX
* [ ] Assign [Permission Sets](https://developer.salesforce.com/docs/atlas.en-us.securityImplGuide.meta/securityImplGuide/perm_sets_overview.htm#:~:text=A%20permission%20set%20is%20a,access%20without%20changing%20their%20profiles.&text=Users%20can%20have%20only%20one,can%20have%20multiple%20permission%20sets.) created above to Developers to ensure Object-Level Security \(OLS\) and Field Level Security \(FLS\) is available on [ScratchOrgInfo](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_scratchorginfo.htm)​
* [ ] Install sfpowerscripts [Scratch Org Pooling](https://github.com/Accenture/sfpowerscripts/tree/develop/prerequisites/scratchorgpool) unlocked package in DevHub
* [ ] Install [sfpowerscripts-artifact](https://github.com/Accenture/sfpowerscripts/tree/develop/prerequisites/sfpowerscripts-artifact) unlocked package in DevHub and existing lower existing sandboxes

#### Developer Tools <a id="developer-tools"></a>

* [ ] ​[Visual Studio Code IDE](https://code.visualstudio.com/download)​
  * [ ] ​[Salesforce Extension Pack](https://marketplace.visualstudio.com/items?itemName=salesforce.salesforcedx-vscode)​
  * [ ] _Optional Extensions_​
    * ​[Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one)​
    * ​[Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)​
    * ​[Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)​
    * ​[Beautify](https://marketplace.visualstudio.com/items?itemName=HookyQR.beautify)
    * [Salesforce Package.xml Generator Extension for VS Code](https://marketplace.visualstudio.com/items?itemName=VignaeshRamA.sfdx-package-xml-generator)​
* [ ] ​[git](https://git-scm.com/)​
* [ ] ​[Salesforce CLI](https://www.npmjs.com/package/sfdx-cli)​
* [ ] ​[sfpowerkit Plugin](https://github.com/dxatscale/sfpowerkit)​
* [ ] ​[sfpowerscripts Plugin](https://github.com/Accenture/sfpowerscripts)​
* [ ] ​[SFDX-Data-Move-Utility \(SFDMU\) Plugin](https://github.com/forcedotcom/SFDX-Data-Move-Utility)​

#### Dashboard Platform <a id="dashboard-platform"></a>

* ​[New Relic Account](https://newrelic.com/signup) _\(Optional\)_
* [Data Dog Account](https://www.datadoghq.com/) \(Optional\)
* Other [StatsD](https://github.com/statsd/statsd) Compatible Monitoring Platform _\(Optional\)_

