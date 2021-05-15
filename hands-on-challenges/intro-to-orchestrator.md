# Intro to sfpowerscripts orchestrator

### **Learning Objectives**

* What is sfpowerscripts?
* How does sfpowerscripts help you in package based development? 

**Time to complete:** 20 minutes

### Background

Orchestrator was introduced as part of the December 2020 sfpowerscripts [Release 18](https://github.com/Accenture/sfpowerscripts/releases/tag/Release_18). Previous to this, the sfpowerscripts structure was based around individual tasks, and putting them together to create a custom CICD pipeline. While you can still individualise your tasks, the sfpowerscripts orchestrator provides you with a set of commands which understand your package structure and 'Orchestrate' your CICD pipeline for you.

The orchestrator commands are built to be used through a CICD platform, but can also be used locally through the command line.

{% embed url="https://youtu.be/-3\_DHysV7os" caption="" %}

### **Steps** 

#### **Install sfpowerscripts** 

The first step is to install sfpowerscripts as a plugin to your sfdx-cli

```text
 echo'y' | sfdx plugins:install sfpowerkit
```

#### **Install the prerequisite fields** 

In order for scratch org pooling to work, you will need to install the **sfpower-scratchorg-pool** unlocked package into your DevHub

* Log into your DevHub 
* Navigate to [https://login.salesforce.com/packaging/installPackage.apexp?p0=04t1P000000gOkXQAU](https://login.salesforce.com/packaging/installPackage.apexp?p0=04t1P000000gOkXQAU)
* Select 'Install for Admin Only' 

