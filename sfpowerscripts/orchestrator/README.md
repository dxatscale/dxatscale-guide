---
description: Orchestrate your builds and deployment with minimal code/config
---

# Orchestrator

## Orchestrator

**sfpowerscripts:orchestrator** is a group of commands (or topic in the CLI parlance) that enables one to work with multiple packages in a mono-repo through the development lifecycle or stages. The current version of the orchestrator features these commands

{% embed url="https://youtu.be/-3_DHysV7os" %}

### Orchestrator commands

1. [**prepare**](https://dxatscale.gitbook.io/sfpowerscripts/faq/orchestrator/prepare) **(sfdx sfpowerscripts:orchestrator:prepare)**: Prepare command helps you to build a pool of prebuilt scratch orgs which include managed packages as well as packages in your repository. This process allows you to considerably cut down time in re-creating a scratch org during a pull request validation process when a scratch org is used as Just-in-time CI environment. In simple terms, it reduces time taken in building a scratch org to validate your changes in an incoming pull request. This command also have an option to pull artifacts from your artifact repository, so that say you can prebuild your validation orgs, say from validated set of packages.
2. [**validate**](https://github.com/dxatscale/dxatscale-guide/blob/april-22/projects/sfpowerscripts/orchestrator/broken-reference/README.md) **(sfdx sfpowerscripts:orchestrator:validate)**: This command goes in pair with the prepare command. It fetches a scratch org from the pool already pre prepared (by the prepare command) and deploys/unit tests the changed packages.
3. [**build**](https://github.com/dxatscale/dxatscale-guide/blob/april-22/projects/sfpowerscripts/orchestrator/broken-reference/README.md) **(sfdx sfpowerscripts:orchestrator:build/quickbuild)** : This command builds all the packages in parallel wherever possible by understanding your manifest and dependency tree. Goodbye to the sequential builds, where you fail in the n-1th package and have to wait for the next hour. This command brings massive savings to your build (package creation) time. Also use the [**quickbuild**](https://github.com/dxatscale/dxatscale-guide/blob/april-22/projects/sfpowerscripts/orchestrator/broken-reference/README.md) variant, which builds unlocked package without dependency check in intermittent stages for faster feedback.
4. [**deploy**](https://github.com/dxatscale/dxatscale-guide/blob/april-22/projects/sfpowerscripts/orchestrator/broken-reference/README.md) **(sfdx sfpowerscripts:orchestrator:deploy)**: So you have built all the packages, now this command takes care of deploying it, by reading the order of installation as you have specified in your sfdx-project.json. Installs it one by one, deciding to trigger tests etc. and provide you with the logs if anything fails
5. [**publish**](https://github.com/dxatscale/dxatscale-guide/blob/april-22/projects/sfpowerscripts/orchestrator/broken-reference/README.md) **(sfdx sfpowerscripts:orchestrator:publish)** : Publish lets you publish the built artifacts into an artifact registry during publish stages of your pipeline.
6. [**release**](https://github.com/dxatscale/dxatscale-guide/blob/april-22/projects/sfpowerscripts/orchestrator/broken-reference/README.md) (**sfdx sfpowerscripts:orchestrator:release**) : Release commands orchestrate fetching of artifacts from an artifact repository, deploying to an environment including any external dependencies and generating changelog all driven by a release definition file.

### Controlling Aspects of the Orchestrator

Orchestrator utilizes additional properties mentioned along with each package in your sfdx-project.json which can be used to control what the orchestrator should work with each package.

{% embed url="https://youtu.be/c_E8fBIlFPo" %}

| Modifier                         | Type    | Description                                                                                                                                             | Stages Applied                                                                                                                                             |
| -------------------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **aliasfy**                      | boolean | Deploy a subfolder in a source package that matches the alias of the org                                                                                | **deploy**                                                                                                                                                 |
| **alwaysDeploy**                 | boolean | Deploys package, even if it's installed already in the org. The artifact has to be present in the artifact directory for this particular option to work | <p><strong>deploy,</strong><br><strong>release</strong></p>                                                                                                |
| **assignPermSetsPreDeployment**  | array   | Apply permsets before deploying a package                                                                                                               | <p><strong>prepare,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p>                               |
| **assignPermSetsPostDeployment** | array   | Apply permsets after deploying a package                                                                                                                | <p><strong>prepare,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p>                               |
| **buildCollection**              | array   | Utilize this to build packages in unison, it will build all packages in the collection, even if only one of them changes                                | **build**                                                                                                                                                  |
| **checkpointForPrepare**         | boolean | Prevent a scratch org from being added to pool, if this package is not able to be installed during prepare                                              | **prepare**                                                                                                                                                |
| **destructiveChangePath**        | string  | Apply destructive changes during deployment                                                                                                             | <p><strong>deploy,</strong><br><strong>release</strong></p>                                                                                                |
| **isOptimizedDeployment**        | true    | Detects test classes in a source package automatically and utilize it to deploy the provided package                                                    | <p><strong>deploy,</strong><br><strong>validate,</strong></p><p><strong>release</strong></p>                                                               |
| **ignoreOnStage**                | array   | Ignore this package on a particular stage                                                                                                               | <p><strong>prepare,</strong></p><p><strong>build,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p> |
| **postDeploymentScript**         | string  | Run an executable script after deploying a package. User need to provide a path to the script file                                                      | <p><strong>prepare,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p>                               |
| **preDeploymentScript**          | string  | Run an executable script before deploying a package. User need to provide a path to the script file                                                     | <p><strong>prepare,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p>                               |
| **reconcileProfiles**            | boolean | Reconcile Profiles during a deployment of source packages                                                                                               | <p><strong>prepare,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p>                               |
| **type**                         | string  | Denotes the type of the package, accepted values are "source","data"                                                                                    | <p><strong>prepare,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p>                               |
| **skipCoverageValidation**       | boolean | Skip the coverage validation of a package (unlocked/source)                                                                                             | **validate**                                                                                                                                               |
| **skipDeployOnOrgs**             | array   | Skip deployment on a particular org or org(s). Take an array of aliases as the input                                                                    | <p><strong>prepare,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p>                               |
| **skipTesting**                  | boolean | Skip unit testing during validate or deployment (source packages)                                                                                       | <p><strong>deploy,</strong><br><strong>release</strong></p><p><strong>validate</strong></p>                                                                |
| **testSynchronous**              | boolean | Validate apex tests of a package by triggering test synchrounously                                                                                      | **validate**                                                                                                                                               |

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
