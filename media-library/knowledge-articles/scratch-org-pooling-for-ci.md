---
description: 'Published on February 15, 2021 by Caitlyn Mills'
---

# Scratch Org pooling for CI

Scratch orgs have been available in salesforce development for over three years now and have quickly become a ‘tried and true’ way to develop, test and validate implementations, alongside the existing sandbox development method. But what’s new for scratch orgs? There are certainly slight downsides, such as the time taken to deploy packages to a scratch org before use or trying to use a scratch org as an ‘Just-in-time’ Continuous Integration environment for validating new changes. While the Salesforce team does have plans to support scratch org development further such as with the “snapshot” feature, there have been delays, which has prompted the DX@Scale team to extend scratch org features using open source plugins.

Imagine if you could have a “pool” of scratch orgs at your disposal? Pre-prepared with your packages, refreshed as required and available seamlessly? Imagine no more, DX@Scale has your solution and its completely open source.

In part one let’s talk about preparing scratch orgs for use as "just-in-time" **Continous Integration Environments**

sfpowerscripts [December 2020 release](https://github.com/Accenture/sfpowerscripts/releases/tag/Release_18) introduced the “orchestrator:prepare” command which allows you to create a pool of scratch orgs, install all, some or no code in your repo as well as required managed packages to emulate your Production Org. But how? What exactly is happening under the “hood”? Well, the prepare commands works in this way:

1. First it calculates how many scratch orgs to provide based both on how many scratch orgs requested and what your org limits are
2. Then it fetches the packages required, using “ArtifactFetchScript” if specified, alternatively it builds all packages
3. Next it creates the scratch orgs and updates a record which tracks your scratch orgs in production to “In progress”
4. SFPOWERSCRIPTS\_ARTIFACT\_PACKAGE \(04t1P000000ka0fQAA\) is installed in each scratch org which keeps track of all of the packages to be installed
5. All dependencies as marked in the sfdx-project.json file are installed to the scratch org
6. Each scratch org installs all packages that are either built/fetched
7. All scratch orgs are then marked as “available”
8. Any scratch orgs which failed are deleted

And voila, that’s it – if you want to dig more in the nitty gritty of how, the source code is available [here](https://github.com/Accenture/sfpowerscripts/blob/develop/packages/sfpowerscripts-cli/src/commands/sfpowerscripts/orchestrator/prepare.ts) you can also read some FAQ’s [here](https://dxatscale.gitbook.io/sfpowerscripts/faq/orchestrator/prepare).

So, you know what Is happening behind the scenes, but really, you just want to know how do YOU use this?! Well – it can be simple, there are some [prerequisites](https://github.com/Accenture/sfpowerkit/wiki/Getting-started-with-ScratchOrg-Pooling) \(steps 1 and 2\), but it really comes down to your production settings, pool config file and a simple command.

```text
sfdx sfpowerscripts:orchestrator:prepare -t CI_1 -v <devhub>
```

Yes, there are some optional flags in the command to provide you with greater customisation and flexibility, but you can use this command at its most basic as well, which uses default values for the flags which aren’t provided.

What customisation is available?

* Expiry length \(days\) for scratch orgs in the pool
* the size of the scratch org pool to be created
* Install all dependencies
* Install unlocked packages as source packages
* Specific keys to be used when installing managed packaged dependants
* Whether the scratch org should fail if any packages are deployed
* How many scratch orgs can be provisioned in parallel

For example, creating a scratch org pool of **15**, with an expiry length of **3** days, all dependencies installed and being prepared **5** at a time in parallel looks like:

```text
sfdx sfpowerscripts:orchestrator:prepare -t CI_Example -v DevHub -e 3 -m 15 -batchsize 5
```

You have the basics. If you need a further example, see [here](https://github.com/dxatscale/easy-spaces-lwc/blob/develop/.github/workflows/sfpowerscripts-prepare.yml). What do you do with it? Where does this command go?

Well, we recommend running this command at a scheduled time during low development windows. So, if you are an over eager, over organised night owl like…. myself, you \*could\* run this manually through your CLI every morning at 3am. However, we find that a scheduled pipeline in your preferred CI platform works the best. This pool can then be used in the [validate command](https://dxatscale.gitbook.io/sfpowerscripts/faq/orchestrator/validatehttps:/dxatscale.gitbook.io/sfpowerscripts/faq/orchestrator/validate), also released in December 2020.

Stay tuned for Part 2 – Scratch org pooling for development happy pooling.

All opinions are my own, but DX@Scale is the best open source tool for supersizing your DX development. Open-source Salesforce CI doesn’t have to be hard!

