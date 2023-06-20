# Developer Workstation



In order to successfully troubleshoot and interact with Salesforce and your preferred CI/CD Tooling Platform using the CLI, the following commands should be executed on your computer to validate you have the tools configured correctly. Depending on your operating system (eg. **Mac OS, Windows, Linux**), there may be some variation in the commands and outputs below on your terminal window.&#x20;

### Git

```bash
git version
> git version 2.33.1
```

### SFDX CLI

```bash
npm install --global @salesforce/cli
```

### sfpowerscripts

```
npm i --global @dxatscale/sfpowerscripts
```

### Other required plugins

```bash
sfdx plugins:install sfdmu
sfdx plugins:install sfdx-browserforce-plugin
```

###

