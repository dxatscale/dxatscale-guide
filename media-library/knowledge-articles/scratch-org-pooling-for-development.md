---
description: Published on February 24, 2021 by Caitlyn Mills
---

# Scratch Org Pooling for Development

In [Part 1](https://www.linkedin.com/pulse/scratch-orgs-scale-part-1-caitlyn-mills/?trackingId=oxGR4J1wcwKpDFQxciU%2FHA%3D%3D) we discussed scratch org pooling for Continuous Integration using the sfpowerscripts orchestrator:prepare command. Today we are going to apply the same concept of a **scratch org pool for development** using [sfpowerkit](https://github.com/Accenture/sfpowerkit).

Let’s dive in - (pun intended)

**Imagine the scenario:** Monday morning you’re assigned ticket for a shiny new development feature, it needs to be done by Friday. You check out the ticket and start spinning up a new scratch org. Scratch org successfully created, and you begin installing the dependent packages you need. Time ticks on, 1 package, 2, 3, 4. By the time you are done, so is half of your day! Sound familiar?

This is where pooling for development comes in. If you have a pool of scratch orgs available for development, there is no need for this set up. This leaves yourself and your developers with more time for working on and perfecting new features for your org!

**Getting Started**

1. First, we are going add required fields/rule to DevHub by cloning the sfpowerkit repo and deploying the [fields and validation rule](https://github.com/Accenture/sfpowerkit/tree/main/src\_saleforce\_packages/scratchorgpool) . If you have already done it for sfpowerscripts, you can skip this step
2. Next we will be building a pool configuration, which defines the shape of our scratch org pool, the [examples](https://github.com/Accenture/sfpowerkit/tree/main/schemas/pool) will get you started, we will discuss the differences between these shortly
3. Now the action starts! You create your pool with this incredible command that looks so simple

```
sfdx sfpowerkit:pool:create -f <config_file_path> -v Devhub 
```

This command should be run in your CI server, with admin permissions to your DevHub, otherwise the fetch commands, detailed below, will not provide the expected results. It should be run on a regular schedule to ensure that your pool is replenished as required.

**What is happening behind the scenes?**

1. Firstly, DevHub gets checked for prerequisite fields (see point 1 above) and quits execution if the fields aren’t available
2. Next the config file gets checked to see if it both exists and is valid, and again execution fails if none is found, or the file is invalid
3. The config file is checked to see if it is a ‘user mode’ or ‘tag mode’ config file. (see below)
4. The amount of scratch orgs to provisioned is checked against the amount available in DevHub, and if a maximum is allocated already, none will be provisioned
5. Scratch orgs are created
6. In each scratch org, any script provided in the ‘script\_file\_path’ parameter of the config file is executed
7. The scratch orgs are then marked as Available, a password is generated and pushed to the records in DevHub

**Config Files**

sfpowerkit allows for two different types of pool config files, User Mode and Tag Mode.

**User mode** allows for a specific user or users to have their own pool available, signified by their username. This is good for scenarios where you have developers using the same amount of scratch orgs in a consistent manner. For example, Johnny uses 3 scratch orgs a month, whereas Amy only uses 1.

**Tag mode** is instead identified by the tag given to the pool. For example, you might be developing in a multi-repo scenario and want to have a certain number of scratch orgs allocated per repo. In this case, each repo would have its own pool config file and your tag could be the name of the repo. In a mono-repo scenario, the tag name could be how your packages are broken down, or by your work groups.

**IP Relaxation**

Relaxation of IP ranges is key in tag mode config files to allow users to access the scratch orgs. In tag mode, the scratch orgs belong to the user who is creating it, (so the CI user). By relaxing IP ranges, you disable email-based validation, or you have to ask the CI user to provide you a validation code. This can be done either by specifying a range to relax:

```
"relax_ip_ranges": [ 

       {

         "start": "49.0.0.0",

         "end": "49.255.255.255"

       },

       {

         "start": "42.0.0.0",

         "end": "42.255.255.255"
       }
```

or by relaxing all IP ranges:

```
"relax_all_ip_ranges": true
```

User mode does not require IP relaxing, as each user gets a verification email.

**Using Scratch orgs**

The fetch command is how scratch orgs can be used/allocated. Only administrators can use the fetch command, due to Scratch Org records only being visible to a user who created them. The recommended method for this is to run the fetch commands through your CI server (with the same admin permission as when the create command was run) and email the end user with the scratch org details. The command is:

```
sfdx sfpowerkit:pool:fetch --tag my_pool --v Devhub -s {username}
```

This is a neat feature which allows your scratch org details to be emailed to the user rather than displayed in a CI server (security issues aside, you don’t know who gets what). Please note this only works provided the username exists in DevHub

There are additional commands such as list and delete, the details of which can be found on the [sfpowerkit github](https://github.com/Accenture/sfpowerkit#sfpowerkitpoolcreate).

Happy pooling!

As before, all opinions are my own, but DX@Scale has the best open-source tooling for supersizing your DX development.
