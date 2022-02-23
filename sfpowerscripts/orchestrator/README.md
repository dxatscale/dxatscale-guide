---
description: Orchestrate your builds and deployment with minimal code/config
---

# Orchestrator

## Orchestrator

**sfpowerscripts:orchestrator** is a group of commands (or topic in the CLI parlance) that enables one to work with multiple packages in a mono-repo through the development lifecycle or stages. The current version of the orchestrator features these commands

{% embed url="https://youtu.be/-3_DHysV7os" %}

### A typical pipeline

To understand the orchestrator, let's look at a typical CI/CD pipeline for a package-based development in a program that has multiple environments. For brevity, prepare and validate states are not discussed.

![](<../../.gitbook/assets/image (52).png>)



Let's dive into the pipeline depicted above, there key stages we wil be&#x20;

*   **CI Pipeline**: A pipeline that gets triggered on every merge to the trunk. During this process, the following stages happen in sequence.

    * [quickbuild](broken-reference) a set of changed packages (packages without validating for dependency or code coverage)&#x20;
    * [deploy](broken-reference) to a Development Sandbox.  This process ensures the upgrade process of a package is accurate and you could also do a quick round of validation of your packages coming in from a scratch org.
    * Once deploy is successful, the pipeline proceed to [build](broken-reference) the set of changed packages (but this time with dependency validation and code coverage check). The same job could then [publish](broken-reference) these validated packages to an artifact repository for deployment into higher environments for further testing.


* **CD Pipeline**:  A Continuous Delivery Pipeline that gets triggered manually or automatically (every day on a scheduled time interval) deploying a set of the latest validated packages to a series of environment. The sequence of stages include
  * Fetch the Artifacts from the artifact repository using the provided release definition
  * Deploy the set of packages say to System Testing environment
  * Upon successful testing, the same set of packages progress to the System Integration Test environment and so forth
  * If the packages are successful in all of the testing, the packages are marked for promotion
  * The promoted packages are then deployed to production.

Take a note of each stage in the pipeline above and the key functionality required, such as build, deploy, release etc, this is typically done by inserting the equivalent sfdx commands into your CI/CD pipeline definition. As your number of packages grow, it not only is hard to maintain but is error prone. This is where sfpowerscripts orchestrator simplifies the pipeline to a one time setup. All the stages are driven by sfdx-project.json, which ensures zero maintenance to the pipelines. Each stage of the above pipeline could be modelled by using equivalent sfpowerscripts orchestrator commands

### Orchestrator commands

1. [**prepare**](https://dxatscale.gitbook.io/sfpowerscripts/faq/orchestrator/prepare) **(sfdx sfpowerscripts:orchestrator:prepare)**:  Prepare command helps you to build a pool of prebuilt scratch orgs which include managed packages as well as packages in your repository. This process allows you to considerably cut down time in re-creating a scratch org during a pull request validation process when a scratch org is used as Just-in-time CI environment. In simple terms, it reduces time taken in building a scratch org to validate your changes in an incoming pull request. This command also have an option to pull artifacts from your artifact repository, so that say you can prebuild your validation orgs, say from validated set of packages.  &#x20;
2. [**validate**](broken-reference) **(sfdx sfpowerscripts:orchestrator:validate)**: This command goes in pair with the prepare command. It fetches a scratch org from the pool already pre prepared (by the prepare command) and deploys/unit tests the changed packages.   &#x20;
3. [**build**](broken-reference) **(sfdx sfpowerscripts:orchestrator:build/quickbuild)** : This command builds all the packages in parallel wherever possible by understanding your manifest and dependency tree. Goodbye to the sequential builds, where you fail in the n-1th package and have to wait for the next hour. This command brings massive savings to your build (package creation) time. Also use the [**quickbuild**](broken-reference) variant, which builds unlocked package without dependency check in intermittent stages for faster feedback.  &#x20;
4. [**deploy**](broken-reference) **(sfdx sfpowerscripts:orchestrator:deploy)**: So you have built all the packages, now this command takes care of deploying it, by reading the order of installation as you have specified in your sfdx-project.json. Installs it one by one, deciding to trigger tests etc. and provide you with the logs if anything fails   &#x20;
5. [**publish**](broken-reference) **(sfdx sfpowerscripts:orchestrator:publish)** :  Publish lets you publish the built artifacts into an artifact registry during publish stages of your pipeline.
6. [**release**](broken-reference) (**sfdx sfpowerscripts:orchestrator:release**) : Release commands orchestrate fetching of artifacts from an artifact repository, deploying to an environment including any external dependencies and generating changelog all driven by a release definition file.

### Controlling Aspects of the Orchestrator

Orchestrator utilizes additional properties mentioned along with each package in your sfdx-project.json which can be used to control what the orchestrator should work with each package.

{% embed url="https://youtu.be/c_E8fBIlFPo" %}

| Modifier                         | Type    | Description                                                                                                                                             | Stages Applied                                                                                                                                             |
| -------------------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **aliasfy**                      | boolean | Deploy a subfolder in a source package that matches the alias of the org                                                                                | **deploy**                                                                                                                                                 |
| **alwaysDeploy**                 | boolean | Deploys package, even if it's installed already in the org. The artifact has to be present in the artifact directory for this particular option to work | <p><strong>deploy,</strong> <br><strong>release</strong></p>                                                                                               |
| **assignPermSetsPreDeployment**  | array   | Apply permsets before deploying a package                                                                                                               | <p><strong>prepare,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong> <br><strong>release</strong></p>                              |
| **assignPermSetsPostDeployment** | array   | Apply permsets after deploying a package                                                                                                                | <p><strong>prepare,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong> <br><strong>release</strong></p>                              |
| **buildCollection**              | array   | Utilize this to build packages in unison, it will build all packages in the collection, even if only one of them changes                                | **build**                                                                                                                                                  |
| **destructiveChangePath**        | string  | Apply destructive changes during deployment                                                                                                             | <p><strong>deploy,</strong><br><strong>release</strong></p>                                                                                                |
| **isOptimizedDeployment**        | true    | Detects test classes in a source package automatically and utilize it to deploy the provided package                                                    | <p><strong>deploy,</strong> <br><strong>validate,</strong></p><p><strong>release</strong></p>                                                              |
| **ignoreOnStage**                | array   | Ignore this package on a particular stage                                                                                                               | <p><strong>prepare,</strong></p><p><strong>build,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p> |
| **postDeploymentScript**         | string  | Run an executable script after deploying a package. User need to provide a path to the script file                                                      | <p><strong>prepare,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p>                               |
| **preDeploymentScript**          | string  | Run an executable script before deploying a package. User need to provide a path to the script file                                                     | <p><strong>prepare,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p>                               |
| **reconcileProfiles**            | boolean | Reconcile Profiles during a deployment of source packages                                                                                               | <p><strong>prepare,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p>                               |
| **type**                         | string  | Denotes the type of the package, accepted values are "source","data"                                                                                    | <p><strong>prepare,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p>                               |
| **skipCoverageValidation**       | boolean | Skip the coverage validation of a package (unlocked/source)                                                                                             | **validate**                                                                                                                                               |
| **skipDeployOnOrgs**             | array   | Skip deployment on a particular org or org(s). Take an array of aliases as the input                                                                    | <p><strong>prepare,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p>                               |
| **skipTesting**                  | boolean | Skip unit testing during validate or deployment (source packages)                                                                                       | <p><strong>deploy,</strong><br><strong>release</strong></p><p><strong>validate</strong></p>                                                                |

### Handling multiple ignore files

Sometimes, due to certain platform errors, some metadata components need to be ignored during **quickbuild** or **validate** or any other stages. sfpowerscripts offer you an easy mechanism, which allows to switch .forceignore files depending on the stage.

Add this entry to your sfdx-project.json and as in the example below, mention the path to different files that need to be used for different stages

```
 "plugins": {
        "sfpowerscripts": {
            "ignoreFiles": {
                "prepare": ".forceignore",
                "validate": ".forceignore",
                "quickbuild": "forceignores/.buildignore",
                "build": "forceignores/.validationignore"
            }
        }
```

### Ignoring a package on any particular stage from being being processed by the orchestrator

Utilize the `ignoreOnStage` descriptor to mark which packages should be skipped by the lifecycle commands.
