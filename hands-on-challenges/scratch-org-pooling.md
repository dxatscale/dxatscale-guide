# Scratch Org Pooling Part 1

### Learning Objectives

* What is a scratch org pool? 
* What are the benefits of using a scratch org pool? 
* What are the different types of scratch org pools?
* How do I set up a scratch org pool? 

**Time to Complete :** 45 Minutes

### What is a Scratch Org Pool? 

We discussed what scratch orgs are in an [earlier](4.-scratch-org-introduction.md) section. While scratch orgs are a great way of developing on the Salesforce platform, the time it takes to spin up an org and install all the dependencies grows with each iteration of development. What DX@Scale has done is taken the scratch org capability and extended it to create a "pool" of scratch orgs available for development or for use as 'Just in time' Continuous Integration environments used for validating changes in your org. 

### Types of Scratch Org Pools

DX@Scale offers two types of scratch org pools 

1. A pool which can be used by developers to work on features. These scratch org pools will typically have a longer duration, and would more actively use the 'user-mode' feature
2. A pool which is used in your validation stage during the Continuous Integration pipeline

We will be discussing type 1 in this module, and will do a "part 2" for scratch orgs in a later module. 

### **Steps**

#### **Install the prerequisite fields** 

In order for scratch org pooling to work, you will need to install the **sfpower-scratchorg-pool** unlocked package into your DevHub

* Log into your DevHub 
* Navigate to [https://login.salesforce.com/packaging/installPackage.apexp?p0=04t1P000000gOqzQAE](https://login.salesforce.com/packaging/installPackage.apexp?p0=04t1P000000gOqzQAE)
* Select 'Install for Admin Only' 

#### Build a Pool Configuration

A pool configuration defines the 'shape' of your scratch org pool. This includes how it is identified, the size and when the pool expires. 

The fields below are exactly what can be specified when defining your pool.

| Field | Type | Description |
| :--- | :--- | :--- |
| expiry | Number | Number of days after which the pooled scratch org will expire |
| tag | String | \(Required\) Identifier for the pool created |
| max\_allocation | Number | \(Required\) Size of the pool, ignored if pool users are specified |
| config\_file\_path | String | \(Required\) Path to the scratch org definition file |
| script\_file\_path | String | Path to a script file to be executed e.g. to install dependencies in scratch orgs. Currently supports batch file or shell scripts which gets executed by cmd or bash respectively. The script will be passed two arguments the scratchorg username and devhub username respectively as %1 and %2 |
| relax\_ip\_ranges | Array | Relax IP address ranges from which clients can access created scratch orgs. |
| relax\_all\_ip\_ranges | Boolean | Relax All IP address ranges from which clients can access created scratch orgs. |
| poolUsers | Array | List of pool users and their min/max scratch org allocation, expiry, email and priority |

**An example schema**

```text
{
  "pool": {
        "expiry": 1,
        "tag":"examplepool",
        "max_allocation": 10,
        "config_file_path": "config/project-scratch-def.json",
        "relax_all_ip_ranges": true,  
    }
  ]
}
```

There are variations of a scratch org pool with either 

* Relaxing all IP ranges vs Relaxing start/end point IP ranges
* User mode vs Tag mode 

**Relaxing IP Ranges**

Relaxation of IP ranges is key in tag mode config files to allow users to access the scratch orgs. In tag mode, the scratch orgs belong to the user who is creating it, \(so the CI user\). By relaxing IP ranges, you disable email-based validation, or you have to ask the CI user to provide you a validation code.

**User Mode vs Tag Mode**

**User mode** allows for a specific user or users to have their own pool available, signified by their username. This is good for scenarios where you have developers using the same amount of scratch orgs in a consistent manner. For example, Johnny uses 3 scratch orgs a month, whereas Amy only uses 1.

**Tag mode** is instead identified by the tag given to the pool. For example, you might be developing in a multi-repo scenario and want to have a certain number of scratch orgs allocated per repo. In this case, each repo would have its own pool config file and your tag could be the name of the repo. In a mono-repo scenario, the tag name could be how your packages are broken down, or by your work groups.

{% hint style="info" %}
**For this module we will be using tag mode with all IP ranges relaxed, as in the example schema above**
{% endhint %}

* Create a **scratchorg-pool-config.json** file in your repo with a file path of **config/scratchorg-pool-config.json**
* Add the above example schema 
* Update the "max\_allocation" tag to 2 
* Make sure the config file path is pointing to your correct project-scratch-def.json location 
* Commit the file to your repo 

#### Create your pool

With all the pre work we have done, the command to create the pool is deceptively simple 

```text
sfdx sfpowerkit:pool:create -f config/scratchorg-pool-config.json -v Devhub
```

#### Fetch a scratch org

Now try to use your scratch org pool by fetching it using this command 

```text
sfdx sfpowerkit:pool:fetch --tag examplepool  -v Devhub
```

The username and password will be outputted from this command which you can use to log in at [https://test.salesforce.com](https://test.salesforce.com/) 

#### Delete the pool 

We don't need the pool for the next modules, so lets clear up your scratch org space using the delete command. 

```text
sfdx sfpowerkit:pool:delete --tag examplepool -v Devhub
```

### Recap

Well done. Scratch org pooling is a big topic to complete. You should now know what a pool is, why you would use one and how to set one up. 

Keep your scratch org pool schema in your repo, we will use it later. 

