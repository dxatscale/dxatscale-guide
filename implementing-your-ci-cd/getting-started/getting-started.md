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

### Troubleshooting Issues

#### Issue - Unable to install sfpowerscripts due to error better-sqlite3 on MacOS

````
npm i -g @dxatscale/sfpowerscripts
npm WARN deprecated @oclif/screen@3.0.4: Deprecated in favor of @oclif/core
npm WARN deprecated request-promise-native@1.0.9: request-promise-native has been deprecated because it extends the now deprecated request package, see https://github.com/request/request/issues/3142
npm WARN deprecated har-validator@5.1.5: this library is no longer supported
npm WARN deprecated @oclif/screen@1.0.4: Deprecated in favor of @oclif/core
npm WARN deprecated uuid@3.4.0: Please upgrade  to version 7 or higher.  Older versions may use Math.random() in certain circumstances, which is known to be problematic.  See https://v8.dev/blog/math-random for details.
npm WARN deprecated @salesforce/command@5.2.43: Package no longer supported. Contact Support at https://www.npmjs.com/support for more info.
npm WARN deprecated request@2.88.2: request has been deprecated, see https://github.com/request/request/issues/3142
npm WARN deprecated vm2@3.9.19: The library contains critical security issues and should not be used for production! The maintenance of the project has been discontinued. Consider migrating your code to isolated-vm.
npm WARN deprecated cli-ux@5.5.1: Package no longer supported. Contact Support at https://www.npmjs.com/support for more info.
npm WARN deprecated puppeteer@19.2.0: < 19.4.0 is no longer supported
npm ERR! code 1
npm ERR! path /usr/local/lib/node_modules/@dxatscale/sfpowerscripts/node_modules/better-sqlite3
npm ERR! command failed
...
```
````

{% hint style="info" %}
Resolution: Ensure that you have installed xcode in your MacOS

```shellscript
xcode-select --install
```
{% endhint %}
