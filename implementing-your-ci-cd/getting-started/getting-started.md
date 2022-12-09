# Developer Workstation



In order to successfully troubleshoot and interact with Salesforce and your preferred CI/CD Tooling Platform using the CLI, the following commands should be executed on your computer to validate you have the tools configured correctly. Depending on your operating system (eg. **Mac OS, Windows, Linux**), there may be some variation in the commands and outputs below on your terminal window.&#x20;

### Git

```bash
git version
> git version 2.33.1
```

### SFDX CLI

```bash
sfdx version
> sfdx-cli/7.176.1 darwin-x64 node-v18.7.0
```

### sfp-cli

```
npm i -g @dxatscale/sfp-cli
```

### sfpowerscripts

```
sfdx plugins:install @dxatscale/sfpowerscripts
```

### Other required plugins

```bash
sfdx plugins:install sfpowerkit
sfdx plugins:install sfdmu
sfdx plugins:install sfdx-browserforce-plugin
```

### Visual Studio Code

```bash
code --version
> 1.72.2
d045a5eda657f4d7b676dedbfa7aab8207f8a075
x64
```

### NPM

```bash
npm --version
> 8.15.0
```

