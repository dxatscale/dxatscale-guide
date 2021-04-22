# Validating your changes

### **Learning Objectives**

* How DX@Scale has combined SFDX and Continuous Integration 
* How to validate changes using the 'validate' command 

**Time to complete:** 20 minutes

### Validate Command

**Validate** command helps you to validate a change made to your configuration / code. This command is triggered as part of your pull request process, to ensure the correctness of configuration/code, before being merged into your **main** branch. validate simplifies setting up and speeding up the process by using a scratch org prepared earlier using the [prepare ](scratch-org-pooling-part-2-prepare.md)command.

**validate** command runs the following checks

* Checks accuracy of metadata by deploying the metadata to a Just-in-time CI org
* Triggers Apex Tests
* Validate Apex Test coverage of each package

Options available for the validate command are here: 

![](../.gitbook/assets/image%20%2844%29.png)

You can also use the command below in the terminal to get more information

```text
sfdx sfpowerscripts:orchestrator:validate --help
```

### Steps 

1. Create a new 'action' on GitHub as done on the previous module
2. Create the action using the examples here: [https://github.com/dxatscale/easy-spaces-lwc/tree/develop/.azure-pipelines](https://github.com/dxatscale/easy-spaces-lwc/tree/develop/.azure-pipelines) \(Hint: Make sure you align the validate command with the prepare command from the previous module\)
3. Run your new workflow 

{% hint style="danger" %}
If you validation command fails, replace your sfdx-project.json file with the contents here: [https://github.com/dxatscale/easy-spaces-lwc/blob/develop/sfdx-project.json](https://github.com/dxatscale/easy-spaces-lwc/blob/develop/sfdx-project.json) 
{% endhint %}

### Recap

This is a short module, as it reuses the concepts learned in prepare. Well done, you now know how to simply validate your changes. You can now see how you can have this set up to be triggered on every pull request to your main or develop branches. 



