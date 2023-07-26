# Developer Workstation



In order to successfully troubleshoot and interact with Salesforce and your preferred CI/CD Tooling Platform using the CLI, the following commands should be executed on your computer to validate you have the tools configured correctly. Depending on your operating system (eg. **Mac OS, Windows, Linux**), there may be some variation in the commands and outputs below on your terminal window.&#x20;

### Git

```bash
git version

> git version 2.37.2
```

### SFDX CLI

```bash
npm i --global @salesforce/cli

> sf version
 @salesforce/cli/2.1.7 darwin-arm64 node-v20.3.1
```

### sfpowerscripts

```bash
npm i --global @dxatscale/sfpowerscripts

> sfp version
  @dxatscale/sfpowerscripts/22.6.1 darwin-arm64 node-v20.3.1
```

### Other required plugins

```bash
sfdx plugins:install sfdmu
sfdx plugins:install sfdx-browserforce-plugin

> sfdx plugins 
  sfdmu 4.29.4
  sfdx-browserforce-plugin 2.11.0
```

###

