# Developer Workstation



In order to successfully troubleshoot and interact with Salesforce and your preferred CI/CD Tooling Platform using the CLI, the following commands should be executed on your computer to validate you have the tools configured correctly. Depending on your operating system (eg. **Mac OS, Windows, Linux**), there may be some variation in the commands and outputs below on your terminal window.&#x20;

### Git

```bash
git version

> git version 2.39.3
```

### SFDX CLI

```bash
npm i --global @salesforce/cli

> sf version
@salesforce/cli/2.17.14 darwin-arm64 node-v20.8.0
```

### sfpowerscripts

```bash
npm i --global @dxatscale/sfpowerscripts

> sfp version
@dxatscale/sfpowerscripts/25.0.6 darwin-arm64 node-v20.8.0
```

### Other required plugins

```bash
sf plugins install sfdmu
sf plugins install sfdx-browserforce-plugin

> sf plugins 
  sfdmu 4.30.0
  sfdx-browserforce-plugin v4.0.0
```

### Troubleshooting Issues

#### Issue #1 - Unable to install sfpowerscripts due to error better-sqlite3 on MacOS

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

#### Issue #2 - Unable to install sfpowerscripts due to error for node-gy and Visual Studio installation on Windows

````
npm i -g @dxatscale/sfpowerscripts

```
npm ERR! code 1
npm ERR! path C:\Users\user.name\AppData\Roaming\npm\node_modules\@dxatscale\sfpowerscripts\node_modules\better-sqlite3
npm ERR! command failed
npm ERR! command C:\WINDOWS\system32\cmd.exe /d /s /c prebuild-install || node-gyp rebuild --release
npm ERR! prebuild-install warn install No prebuilt binaries found (target=20.9.0 runtime=node arch=ia32 libc= platform=win32)
npm ERR! gyp info it worked if it ends with ok
npm ERR! gyp info using node-gyp@9.4.0
npm ERR! gyp info using node@20.9.0 | win32 | ia32
npm ERR! gyp info find Python using Python version 3.11.6 found at "C:\Users\user.name\AppData\Local\Microsoft\WindowsApps\PythonSoftwareFoundation.Python.3.11_qbz5n2kfra8p0\python.exe"
npm ERR! gyp ERR! find VS
npm ERR! gyp ERR! find VS msvs_version not set from command line or npm config
npm ERR! gyp ERR! find VS VCINSTALLDIR not set, not running in VS Command Prompt
npm ERR! gyp ERR! find VS checking VS2019 (16.11.34301.259) found at:
npm ERR! gyp ERR! find VS "C:\Program Files (x86)\Microsoft Visual Studio\2019\BuildTools"
npm ERR! gyp ERR! find VS - found "Visual Studio C++ core features"
npm ERR! gyp ERR! find VS - found VC++ toolset: v142
npm ERR! gyp ERR! find VS - missing any Windows SDK
npm ERR! gyp ERR! find VS could not find a version of Visual Studio 2017 or newer to use
npm ERR! gyp ERR! find VS not looking for VS2015 as it is only supported up to Node.js 18
npm ERR! gyp ERR! find VS not looking for VS2013 as it is only supported up to Node.js 8
npm ERR! gyp ERR! find VS
npm ERR! gyp ERR! find VS **************************************************************
npm ERR! gyp ERR! find VS You need to install the latest version of Visual Studio
npm ERR! gyp ERR! find VS including the "Desktop development with C++" workload.
npm ERR! gyp ERR! find VS For more information consult the documentation at:
npm ERR! gyp ERR! find VS https://github.com/nodejs/node-gyp#on-windows
npm ERR! gyp ERR! find VS **************************************************************
npm ERR! gyp ERR! find VS
npm ERR! gyp ERR! configure error
npm ERR! gyp ERR! stack Error: Could not find any Visual Studio installation to use
npm ERR! gyp ERR! stack     at VisualStudioFinder.fail (C:\Program Files (x86)\nodejs\node_modules\npm\node_modules\node-gyp\lib\find-visualstudio.js:122:47)
npm ERR! gyp ERR! stack     at C:\Program Files (x86)\nodejs\node_modules\npm\node_modules\node-gyp\lib\find-visualstudio.js:75:16
npm ERR! gyp ERR! stack     at VisualStudioFinder.findVisualStudio2013 (C:\Program Files (x86)\nodejs\node_modules\npm\node_modules\node-gyp\lib\find-visualstudio.js:380:14)
npm ERR! gyp ERR! stack     at C:\Program Files (x86)\nodejs\node_modules\npm\node_modules\node-gyp\lib\find-visualstudio.js:71:14
npm ERR! gyp ERR! stack     at VisualStudioFinder.findVisualStudio2015 (C:\Program Files (x86)\nodejs\node_modules\npm\node_modules\node-gyp\lib\find-visualstudio.js:364:14)
npm ERR! gyp ERR! stack     at C:\Program Files (x86)\nodejs\node_modules\npm\node_modules\node-gyp\lib\find-visualstudio.js:67:12
npm ERR! gyp ERR! stack     at VisualStudioFinder.parseData (C:\Program Files (x86)\nodejs\node_modules\npm\node_modules\node-gyp\lib\find-visualstudio.js:237:5)
npm ERR! gyp ERR! stack     at C:\Program Files (x86)\nodejs\node_modules\npm\node_modules\node-gyp\lib\find-visualstudio.js:143:14
npm ERR! gyp ERR! stack     at ChildProcess.exithandler (node:child_process:414:7)
npm ERR! gyp ERR! stack     at ChildProcess.emit (node:events:514:28)
npm ERR! gyp ERR! System Windows_NT 10.0.22621
npm ERR! gyp ERR! command "C:\\Program Files (x86)\\nodejs\\node.exe" "C:\\Program Files (x86)\\nodejs\\node_modules\\npm\\node_modules\\node-gyp\\bin\\node-gyp.js" "rebuild" "--release"
npm ERR! gyp ERR! cwd C:\Users\user.name\AppData\Roaming\npm\node_modules\@dxatscale\sfpowerscripts\node_modules\better-sqlite3
npm ERR! gyp ERR! node -v v20.9.0
npm ERR! gyp ERR! node-gyp -v v9.4.0
npm ERR! gyp ERR! not ok
```
````

