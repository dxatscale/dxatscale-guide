# Building your packages

### **Learning Objectives**

* What does it mean to 'build' a package 
* What are the differences between the 'build' and 'quickbuild' orchestrator commands
* How do we deploy packages
* How to use the build and deploy commands correctly

**Time to complete:** 40 minutes

### Building Packages 

To build a package means to bundle up all your code in a neat little virtual box, ready to be used and 'unpacked' into environments as needed. When you build a package, you can use this package as many times and in as many environments as needed. 

In later modules we will also refer to a package build as an 'artifact'. A package is an artifact that is used in pipelines, but all artifacts are not necessarily packages as there can be many different types of artifacts. 

The commands in orchestrator follow the order as listed in your sfdx-project.json file to determine the order in which packages are built. The commands also factor in any dependencies and do not commence building a package until dependencies are resolved. More information on how package build order is determined is [here](https://dxatscale.gitbook.io/sfpowerscripts/commands/build-and-quickbuild). 

### Build commands

The Orchestrator provides two types of build commands. **Build** and **quickbuild**. 

The **build** command builds all packages in order of dependencies and generates the artifacts to a supplied directory.  

![](../.gitbook/assets/image%20%2847%29.png)

The **quickbuild** command does almost the same thing as the build command, but it ignores the validation of any dependencies and code coverage. You would use this command before deploying to a developer sandbox to validate code before attempting a build. 

![](../.gitbook/assets/image%20%2846%29.png)

### Deploy command

The deploy command deploys the package to the given alias \(this can be a scratch org, sandbox or devhub org\) 

![](../.gitbook/assets/image%20%2849%29.png)

### Steps

#### Utilize build command to build all packages in the repository

```text
sfdx sfpowerscripts:orchestrator:build -v <devhub> --branch <your branch>
```

Notice how the packages are being built and placed into the artifacts directory.

#### Utilize deploy command to deploy the packages to a new scratch org

1. Create a new scratch org
2. Install sfpowerscripts pre-requisite package into the new scratch org

```text
sfdx force:package:install --package 04t1P000000ka9mQAA -u <so_alias> -w 10
```

3. Use sfpowerscripts deploy command to deploy into the new scratch org

```text
sfdx sfpowerscripts:orchestrator:deploy -u <so_laias>
```

4. Did it fail? Notice the error and try to fix the error using required command

5. Try retriggering Step 3 and notice it sucessfully deployed to the org.

6. Try retriggering deploy one more time and notice how sfpowerscripts automatically skipped all the installed packages in the org.. Isn't it neat?

### Recap 

Hopefully we've learnt a lot in this module! You should now have the basic steps together for how to build and deploy your unlocked packages. 

