---
description: The DX@Scale Developer CLI
---

# sfp-cli

## Installation

**Prerequisites**

The sfp-cli is dependent on other modules that must be installed in order for it to work:

* [Salesforce CLI](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_setup.meta/sfdx\_setup/sfdx\_setup\_install\_cli.htm)
* [sfpowerkit](https://github.com/Accenture/sfpowerkit)

**Install sfp-cli**

```
$ npm install -g @dxatscale/sfp-cli
```

## Usage

The sfp-cli may be slightly different than the CLI's that you are accustomed to using. Firstly, the sfp-cli is its own CLI, and _not_ a plugin of the Salesforce CLI, which means that to start using it all you have to type into the terminal is `$ sfp`. The other key difference is that the commands do not accept any flags or arguments. Sfp-cli is designed with an interactive prompt-based UI, which is as simple as following the instruction on the screen. Try it out for yourself by typing `$ sfp [COMMAND]` in the terminal, substituting `[COMMAND]` for one of the commands listed below.

```
$ sfp init
running command...
? Default git branch for this repo? main
? Associate a devhub with this project? Yes
? Create a new scratch org? (y/N)
...
```

### Work Items

The sfp-cli is built around the idea of work items, which are units of work usually defined on an issue tracking system like Jira. Instead of using git directly to create a new branch, in which to do development work, use `$ sfp work` to create or switch between work items, which have their own associated branch as well as development org.

### Syncing changes

The `$ sfp sync` command allows you to effortlessly sync changes between your source repository and development org. It abstracts the nitty-gritty details of git and SFDX commands into simple prompt-driven workflows, while also providing augmented functionality such as moving pulled components into packages and recommendations for packaging.\\
