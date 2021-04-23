# Build your package

### **Learning Objectives**

* What does it mean to 'build' a package 
* What are the differences between the 'build' and 'quickbuild' orchestrator commands
* How does the command determine the packages to be built? 
* How to use the build command correctly 

**Time to complete:** 40 minutes

### Building Packages 

To build a package means to bundle up all your code in a neat little virtual box, ready to be used and 'unpacked' into environments as needed. When you build a package, you can use this package as many times and in as many environments as needed. 

In later modules we will also refer to a package build as an 'artifact'. A package is an artifact that is used in pipelines, but all artifacts are not necessarily packages as there can be many different types of artifacts. 

### Build commands

The Orchestrator provides two types of build commands. **Build** and **quickbuild**. 

The **build** command builds all packages in order of dependencies and generates the artifacts to a supplied directory.  

![](../.gitbook/assets/image%20%2847%29.png)

The **quickbuild** command does almost the same thing as the build command, but it ignores the validation of any dependencies and code coverage. You would use this command before deploying to a developer sandbox to validate code before attempting a build. 

![](../.gitbook/assets/image%20%2846%29.png)

### Steps

#### Create your packages 

* Clone the repo to your local machine 
* Create all of the Easy Spaces packages using the [package create](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_force_package.htm) command: 

```text
   $ sfdx force:package:create -n YourPackageName -t Unlocked -r force-app -v YourDevHubAlias
```

{% hint style="info" %}
Use your project-sfdx.json to find the values for the package names
{% endhint %}

* After you have created all four packages, look at your project-sfdx.json file and notice how the package Aliases have been updates 
* Push the project-sfdx.json file back into your repo
* In your command line or terminal use the `sfdx force:package:list -v devhub@example.com` command to verify that the packages have been created and are installed in your DevHub

#### Create your QuickBuild file 

* Create a new 'Action' in GitHub Actions called 'quickbuild-deploy' 
* Use 





