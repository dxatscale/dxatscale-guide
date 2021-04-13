# Scratch Org Pooling Part 2 \(prepare\)

### **Learning Objectives**

* Why is scratch org pooling important in continuous integration? 
* How do I use Scratch Org pooling for validation?
* How do I use the prepare command? 

**Time to complete:** 30 minutes

### Prepare Command

The prepare command, which is apart of the orchestrator functionality of sfpowerscripts was introduced in 2020 and provides scratch org pooling, specifically tailored for use in your CICD platform. 

Prepare command helps you to build a pool of prebuilt scratch orgs which include managed packages as well as packages in your repository. This process allows you to considerably cut down time in re-creating a scratch org during validation process when a scratch org is used as Just-in-time CI environment.

### Steps

Good news! If you completed [Scratch Org Pooling Part 1](scratch-org-pooling.md) you have already completed the installation steps required. If you haven't, follow the instructions under the steps '**Install the prerequisite fields'**. 

#### Create a Pool Config File 

We will begin by creating another pool config file. We won't be recapping the creation steps here, as we have already covered it in part 1. The schema we are going to use is below. 

```text
{
  "pool": {
        "expiry": 1,
        "tag":"preparepool",
        "max_allocation": 10,
        "config_file_path": "config/project-scratch-def.json",
        "relax_all_ip_ranges": true,  
    }
  ]
}
```

#### Create a 'prepare' yaml file 



