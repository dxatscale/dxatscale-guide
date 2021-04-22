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



