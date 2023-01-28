---
description: Orchestrate your builds and deployment with minimal code/config
---

# Orchestrator

## Orchestrator

**sfpowerscripts:orchestrator** is a group of commands (or topic in the CLI parlance) that enables one to work with multiple packages in a mono-repo through the development lifecycle or stages. The current version of the orchestrator features these commands

{% embed url="https://youtu.be/-3_DHysV7os" %}

### Orchestrator commands

1. [**prepare**](https://dxatscale.gitbook.io/sfpowerscripts/faq/orchestrator/prepare) **(sfdx sfpowerscripts:orchestrator:prepare)**: Prepare command helps you to build a pool of prebuilt scratch orgs which include managed packages as well as packages in your repository. This process allows you to considerably cut down time in re-creating a scratch org during a pull request validation process when a scratch org is used as Just-in-time CI environment. In simple terms, it reduces time taken in building a scratch org to validate your changes in an incoming pull or merge request. This command also have an option to pull artifacts from your artifact repository, so that say you can pre-build your validation orgs, say from validated set of packages.
2. ****[**validate**](validate.md) **(sfdx sfpowerscripts:orchestrator:validate)**: This command goes in pair with the prepare command. It fetches a scratch org from the pool already created (by the prepare command) and deploys/unit tests the changed packages.  Different validation mode options exist depending on your requirements for individual, fast feedback, thorough, fast feedback release config, and thorough release config, and leveraging release configuration files.
3. ****[**build**](build-and-quick-build.md) **(sfdx sfpowerscripts:orchestrator:build/quickbuild)** : This command builds all the packages in parallel wherever possible by understanding your manifest and dependency tree. Goodbye to the sequential builds, where you fail in the n-1th package and have to wait for the next hour. This command brings massive savings to your build (package creation) time. Also use the [**quickbuild**](build-and-quick-build.md) variant, which builds unlocked package without dependency check in intermittent stages for faster feedback.
4. ****[**deploy**](deploy.md) **(sfdx sfpowerscripts:orchestrator:deploy)**: So you have built all the packages, now this command takes care of deploying it, by reading the order of installation as you have specified in your sfdx-project.json. Installs it one by one, deciding to trigger tests etc. and provide you with the logs if anything fails
5. ****[**publish**](publish.md) **(sfdx sfpowerscripts:orchestrator:publish)** : Publish lets you publish the built artifacts into an artifact registry during publish stages of your pipeline.
6. ****[**release**](release/) (**sfdx sfpowerscripts:orchestrator:release**) : Release commands orchestrate fetching of artifacts from an artifact repository, deploying to an environment including any external dependencies and generating changelog all driven by a release definition file.

### Controlling Aspects of the Orchestrator

Orchestrator utilizes additional properties mentioned along with each package in your sfdx-project.json which can be used to control what the orchestrator should work with each package.

{% embed url="https://youtu.be/c_E8fBIlFPo" %}

| Modifier                         | Type    | Description                                                                                                                                                                                          | Stages Applied                                                                                                                                             |
| -------------------------------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **aliasfy**                      | Boolean | Deploy a subfolder in a source package that matches the alias of the org                                                                                                                             | **deploy**                                                                                                                                                 |
| **alwaysDeploy**                 | boolean | Deploys package, even if it's installed already in the org. The artifact has to be present in the artifact directory for this particular option to work                                              | <p><strong>deploy,</strong><br><strong>release</strong></p>                                                                                                |
| **assignPermSetsPreDeployment**  | array   | <p>Apply permsets before deploying a package<br><br>Click <a href="orchestrator.md#sample-permission-assignment-configuration-for-packages">here</a> for sample.</p>                                 | <p><strong>prepare,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p>                               |
| **assignPermSetsPostDeployment** | array   | <p>Apply permsets after deploying a package<br><br>Click <a href="orchestrator.md#sample-permission-assignment-configuration-for-packages">here</a> for sample.</p>                                  | <p><strong>prepare,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p>                               |
| **buildCollection**              | array   | Utilize this to build packages in unison, it will build all packages in the collection, even if only one of them changes                                                                             | **build**                                                                                                                                                  |
| **checkpointForPrepare**         | boolean | Prevent a scratch org from being added to pool, if this package is not able to be installed during prepare                                                                                           | **prepare**                                                                                                                                                |
| **destructiveChangePath**        | string  | Apply destructive changes during deployment                                                                                                                                                          | <p><strong>deploy,</strong><br><strong>release</strong></p>                                                                                                |
| **enableFT**                     | boolean | Enable Feed Tracking deployment                                                                                                                                                                      | <p><strong>deploy,</strong><br><strong>release</strong></p>                                                                                                |
| **enableFHT**                    | boolean | Enable Field History Tracking deployment                                                                                                                                                             | <p><strong>deploy,</strong> <br><strong>release</strong></p>                                                                                               |
| **isOptimizedDeployment**        | true    | Detects test classes in a source package automatically and utilizes it to deploy the provided package                                                                                                | <p><strong>deploy,</strong><br><strong>validate,</strong></p><p><strong>release</strong></p>                                                               |
| **ignoreOnStage**                | array   | Ignore this package on a particular stage                                                                                                                                                            | <p><strong>prepare,</strong></p><p><strong>build,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p> |
| **postDeploymentScript**         | string  | <p>Run an executable script after deploying a package. User need to provide a path to the script file<br><br>Read more <a href="orchestrator.md#executing-pre-post-deployment-scripts">here</a></p>  | <p><strong>prepare,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p>                               |
| **preDeploymentScript**          | string  | <p>Run an executable script before deploying a package. User need to provide a path to the script file<br><br>Read more <a href="orchestrator.md#executing-pre-post-deployment-scripts">here</a></p> | <p><strong>prepare,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p>                               |
| **reconcileProfiles**            | boolean | Reconcile Profiles during a deployment of source packages                                                                                                                                            | <p><strong>prepare,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p>                               |
| **type**                         | string  | Denotes the type of the package, accepted values are "source","data"                                                                                                                                 | <p><strong>prepare,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p>                               |
| **skipCoverageValidation**       | boolean | Skip the coverage validation of a package (unlocked/source)                                                                                                                                          | **validate**                                                                                                                                               |
| **skipDeployOnOrgs**             | array   | Skip deployment on a particular org or org(s). Take an array of aliases as the input                                                                                                                 | <p><strong>prepare,</strong></p><p><strong>validate,</strong></p><p><strong>deploy,</strong><br><strong>release</strong></p>                               |
| **skipTesting**                  | boolean | Skip unit testing during validate or deployment (source packages)                                                                                                                                    | <p><strong>deploy,</strong><br><strong>release</strong></p><p><strong>validate</strong></p>                                                                |
| **testSynchronous**              | boolean | Validate apex tests of a package by triggering test synchrounously                                                                                                                                   | **validate**                                                                                                                                               |

### Handling Multiple Ignore Files

Sometimes, due to certain platform errors, some metadata components need to be ignored during **quickbuild** or **validate** or any other stages. sfpowerscripts offer you an easy mechanism which allows to switch .forceignore files depending on the stage.

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

### Executing Pre/Post Deployment Scripts

In some situations, you might need to execute a pre/post deployment script to do manipulate the data before or after being deployed to the org. **sfpowerscripts** allow you to provide a path to a shell script (Mac/Unix) / batch script (on Windows).&#x20;

The scripts are called with the following parameters. In your script you can refer to the parameters using [positional parameters.](https://linuxcommand.org/lc3\_wss0120.php)&#x20;

Please note scripts are copied into the [artifacts](../ci-cd/artifacts.md) and are not executed from version control. sfpowerscripts only copies the script mentioned by this parameter and do not copy any additional files or dependencies. Please ensure pre/post deployment scripts are independent or should be able to download its dependencies



| Position | Value                                                                                                                               |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| 1        | Name of the Package                                                                                                                 |
| 2        | Username of the target org where the package is being deployed                                                                      |
| 3        | Alias of the target org where the package is being deployed                                                                         |
| 4        | Path to the working directory that has the contents of the package                                                                  |
| 5        | Path to the package directory. One would need to combine parameter 4 and 5 to find the absolute path to the contents of the package |

<pre><code><strong># Sample pre/post script
</strong><strong>
</strong><strong># $1 package name
</strong># $2 org
# $3 alias
# $4 working directory
# $5 package directory

sfdx force:apex:execute -f scripts/datascript.apex -u $2
</code></pre>

### Sample Permission Assignment Configuration for Packages

```json
    {
      "path": "src/health-cloud",
      "package": "health-cloud",
      "versionName": "health-cloud-1.0",
      "versionNumber": "1.0.0.0",
      "assignPermSetsPreDeployment": [
        "HealthCloudFoundation",
        "HealthCloudSocialDeterminants",
        "HealthCloudAppointmentManagement",
        "HealthCloudVideoCalls",
        "HealthCloudUtilizationManagement",
        "HealthCloudMemberServices",
        "HealthCloudAdmin",
        "HealthCloudApi",
        "HealthCloudLimited",
        "HealthCloudPermissionSetLicense",
        "HealthCloudStandard",
        "HealthcareAssociatedInfectionDiseaseGroupAccess"
      ]
    },
```
