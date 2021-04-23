# Build and Deploy your package

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

![](../.gitbook/assets/image%20%2848%29.png)

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

#### Create your QuickBuild and Deploy file 

* Create a new 'Action' in GitHub Actions called 'quickbuild-deploy' using the code below

```text
# Unique name for this workflow
name: quick build and deploy

# Definition when the workflow should run
on:
    workflow_dispatch:
    push:
        branches:
            - develop

# Jobs to be executed
jobs:
    quickbuild:
        name: QuickBuild the packages
        runs-on: ubuntu-latest
        container: dxatscale/sfpowerscripts
        steps:
            # Checkout the code
            - name: 'Checkout source code'
              uses: actions/checkout@v2
              with:
                  fetch-depth: 0

            # Authenticate dev hub
            - name: 'Authenticate Dev Hub'
              run: |
                  echo "${SALESFORCE_JWT_SECRET_KEY}" > ./JWT_KEYFILE
                  sfdx auth:jwt:grant -u ${{ secrets.DEVHUB_USERNAME }} -i ${{ secrets.DEVHUB_CLIENT_ID }} -f ./JWT_KEYFILE -a devhub -r https://login.salesforce.com
                  rm -f ./JWT_KEYFILE
              env:
                  SALESFORCE_JWT_SECRET_KEY: ${{ secrets.DEVHUB_SERVER_KEY }}

            # Create all packages
            - name: 'Create packages'
              id: sfpowerscripts-build
              run: |
                  pwd
                  sfdx sfpowerscripts:orchestrator:quickbuild -v devhub --diffcheck
            # Publish artifacts
            - uses: actions/upload-artifact@v2
              with:
                  name: quickbuild-artifacts
                  path: artifacts

    # Simulating a deploy to System Test Environment using a scratch org
    deploy:
        name: Deploy and Validate the packages
        runs-on: ubuntu-latest
        container: dxatscale/sfpowerscripts
        needs: quickbuild
        steps:
            # Checkout the code
            - name: 'Checkout source code'
              uses: actions/checkout@v2
              with:
                  fetch-depth: 0

    #Github Actions are event based and are triggered independently,  There is no currently an option to control concurrency settings
    #on pipelines and in this model, build should be run sequentially
            - name: Wait till previous pipeline has finished this stage
              uses: softprops/turnstyle@v0.1.5
              env:
                GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
              with:
                abort-after-seconds: 1800

              # Download Artifacts
            - name: Download Artifacts
              uses: actions/download-artifact@v2
              with:
                  name: quickbuild-artifacts
                  path: artifacts

            # Authenticate dev hub
            - name: 'Authenticate Dev Hub'
              run: |
                  echo "${SALESFORCE_JWT_SECRET_KEY}" > ./JWT_KEYFILE
                  sfdx auth:jwt:grant -u ${{ secrets.DEVHUB_USERNAME }} -i ${{ secrets.DEVHUB_CLIENT_ID }} -f ./JWT_KEYFILE -a devhub -r https://login.salesforce.com
              env:
                  SALESFORCE_JWT_SECRET_KEY: ${{ secrets.DEVHUB_SERVER_KEY }}

            # Create scratch org
            - name: Create scratch org
              run: sfdx force:org:create -f config/project-scratch-def.json -a scratch-org -s -d 1 -v devhub

            # Install all new packages into scratch org
            - name: 'Install new package versions into scratch org'
              run: 'sfdx sfpowerscripts:orchestrator:deploy -u scratch-org'

            # Housekeeping
            - name: Delete scratch org
              if: always()
              run: sfdx force:org:delete -p -u scratch-org
```

* Run the file, and take a look at what is happening inside the action. 

{% hint style="info" %}
Notice that this command is still deploying, it's just using a scratch org, if you were using an ST sandbox to do testing, you would supply the alias or username of this sandbox in the -u portion of the deploy command 
{% endhint %}

#### Create your Build and Deploy file 

* Create a new action in GitHub actions called 'build - deploy' using the following code

```text
# Unique name for this workflow
name: build and deploy

# Definition when the workflow should run
on:
    workflow_dispatch:
    push:
        branches:
            - develop

# Jobs to be executed
jobs:
    build:
        name: Build Production Ready packages
        runs-on: ubuntu-latest
        container: dxatscale/sfpowerscripts
        steps:
            # Checkout the code
            - name: 'Checkout source code'
              uses: actions/checkout@v2
              with:
                  fetch-depth: 0

              # Authenticate dev hub
            - name: 'Authenticate Dev Hub'
              run: |
                  echo "${SALESFORCE_JWT_SECRET_KEY}" > ./JWT_KEYFILE
                  sfdx auth:jwt:grant -u ${{ secrets.DEVHUB_USERNAME }} -i ${{ secrets.DEVHUB_CLIENT_ID }} -f ./JWT_KEYFILE -a devhub -r https://login.salesforce.com
                  rm -f ./JWT_KEYFILE
              env:
                  SALESFORCE_JWT_SECRET_KEY: ${{ secrets.DEVHUB_SERVER_KEY }}

#Github Actions are event based and are triggered independently,  There is no currently an option to control concurrency settings
#on pipelines and in this model, build should be run sequentially
            - name: Wait till previous pipeline has finished this stage
              uses: softprops/turnstyle@v0.1.5
              env:
                GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
              with:
                abort-after-seconds: 1800

              # Create all packages
            - name: 'Create packages'
              id: sfpowerscripts-build
              run: 'sfdx sfpowerscripts:orchestrator:build -v devhub'

              # Publish artifacts
            - uses: actions/upload-artifact@v2
              with:
                  name: validated-artifacts
                  path: artifacts

    promote:
        runs-on: ubuntu-latest
        container: dxatscale/sfpowerscripts
        needs: build
        name: Promote the packages
        steps:
            # Checkout the code
            - name: 'Checkout source code'
              uses: actions/checkout@v2
              with:
                  fetch-depth: 0

              # Download Artifacts

            - name: Download Artifacts
              uses: actions/download-artifact@v2
              with:
                  name: validated-artifacts
                  path: artifacts

            # Authenticate dev hub
            - name: 'Authenticate Dev Hub'
              run: |
                  echo "${SALESFORCE_JWT_SECRET_KEY}" > ./JWT_KEYFILE
                  sfdx auth:jwt:grant -u ${{ secrets.DEVHUB_USERNAME }} -i ${{ secrets.DEVHUB_CLIENT_ID }} -f ./JWT_KEYFILE -a devhub -r https://login.salesforce.com
                  rm -f ./JWT_KEYFILE
              env:
                  SALESFORCE_JWT_SECRET_KEY: ${{ secrets.DEVHUB_SERVER_KEY }}

            # Promoted all packages
            - name: 'Promote packages'
              id: sfpowerscripts-build
              run: 'sfdx sfpowerscripts:orchestrator:promote -v devhub -o promoted-artifacts'
```

* Run this file and see if you can spot the differences between what happens in quickbuild vs what happens in build. 

{% hint style="danger" %}
Did you spot what we've left out of the build-deploy? 



Yes, we left off the deploy component! 
{% endhint %}

Your **last task** for this module is to use what you have learnt to add in your own deploy stage to this action. 

### Recap 

Hopefully we've learnt a lot in this module! You should now have the basic steps together for how to build and deploy your unlocked packages. 

