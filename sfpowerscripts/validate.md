# Validate

**validate** command helps you to validate a change made to your configuration / code against a scratch org for continuous integration. This command is triggered as part of your Pull Request (PR) or Merge process, to ensure the correctness of configuration/code, before being merged into your **main** branch. validate uses a scratch org from a tagged pool prepared earlier using the [prepare](prepare/)[ ](https://github.com/dxatscale/dxatscale-guide/blob/april-22/projects/sfpowerscripts/orchestrator/broken-reference/README.md)command to speed up the process of Salesforce Deployment Validations and &#x20;

**validate** command runs the following checks with the options to enable additional features such as dependency and impact analysis:

* Checks accuracy of metadata by deploying the metadata to a just-in-time continuous integration (CI) org
* Triggers Apex Tests
* Validate Apex Test Coverage of each package (default: 75%)
* Toggle between different modes for validation
  * Individual
  * Fast Feedback
  * Thorough _(Default)_
  * Fast Feedback Release Config
  * Thorough Release Config
* \[optional] - Validate dependencies between packages for changed components
* \[optional] - Visualize components impacted by changes in pull request
* \[optional] - Do not update information about deployed artifacts to the org
* \[optional] - Disable diff check while validating, this will validate all the packages in the repository
* \[optional] - Disable parallel testing of apex tests, this will validate apex tests of each package in synchronous mode

## Validate Modes

| Mode                         | Description                                                                                                                                                                                                    | Flag                                                                                                |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| Individual                   | Ignore packages installed in scratch org, identify list of changed packages from PR/Merge Request, and validate each of the changed packages (respecting any dependencies) using thorough mode.                | `--mode=individual`                                                                                 |
| Fast Feedback                | Skip package dependencies and code coverage and selective test class executions, install only changed components, and ignore changes in package descriptors                                                    | `--mode=fastfeedback`                                                                               |
| Thorough (Default)           | Include package dependencies, code coverage, all test classes during full package deployments                                                                                                                  | `--mode=thorough`                                                                                   |
| Fast Feedback Release Config | Extension of fast feedback mode but filtered using release configuration file that defines list of packages to validate with only changed packages ending up being used to validate against the scratch org    | <p><code>--mode=ff-release-config</code><br><br><code>--releaseconfig=&#x3C;value></code></p>       |
| Thorough Release Config      | Extension of thorough default mode but filtered using release configuration file that defines list of packages to validate with only changed packages ending up being used to validate against the scratch org | <p><code>--mode=thorough-release-config</code><br><br><code>--releaseconfig=&#x3C;value></code></p> |

## Sequence of Activities

The following are the list of steps that are orchestrated by the **validate** command

* Fetch a scratch org from the provided pools in a sequential manner
* Authenticate to the Scratch org using the [auth URL](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_cli\_reference.meta/sfdx\_cli\_reference/cli\_reference\_auth\_sfdxurl.htm) fetched from the [Scratch Org Info Object](https://developer.salesforce.com/docs/atlas.en-us.object\_reference.meta/object\_reference/sforce\_api\_objects\_scratchorginfo.htm)
* Build packages that are changed by comparing the tags in your repo against the packages installed in scratch org
*   For each of the packages (internally calls the Deploy Command)\
    \
    **Thorough Mode (Default)**\


    * Deploy all the built packages as [source packages](types-of-packaging/source-packages.md) / [data packages](types-of-packaging/data-packages.md) (unlocked packages are installed as source package)
    * Trigger Apex Tests if there are any apex test in the package
    * Validate test coverage of the package depending on the type of the package (source packages: each class needs to have 75% or more, unlocked packages: packages as whole need to have 75% or more)

    \
    **Fast Feedback Mode**\


    * Deploy only changed metadata components for built packages as [source packages](types-of-packaging/source-packages.md) / [data packages](types-of-packaging/data-packages.md)
    * Trigger selective Apex Tests based on impact analysis of the changes in the package
    * Skip coverage calculations
    * Skip deployment of package if the descriptor is changed
    * Skip deployment of top level packages direct dependency on the package containing changed components



    **Individual Mode**\


    * Ignore packages that are installed in the scratch org (basically eliminate the requirement of using a pooled org)
    * Compute changed packages by observing the diff of Pull/Merge Request
    * Validate each of the changed packages (install any dependencies) using Thorough Mode

    \
    **Fast Feedback Release Config Mode**\


    * Inherit Fast Feedback Mode Features but filtered using a release configuration file containing list of packages to focus validation on
    * Deploy only change packages in the list by comparing against what is installed in the org



    **Thorough Release Config Mode**\


    * Inherit Thorough Mode Features but filtered using a release configuration file containing list of packages to focus validation on
    * Deploy only change packages in the list by comparing against what is installed in the org

{% hint style="info" %}
Use of default "thorough" mode is still recommended in the pipeline with fast feedback to ensure coverage computation and scripts added to the descriptor files are correctly working and deployable in an empty org.
{% endhint %}

{% hint style="info" %}
By default, all the apex tests are triggered in parallel, with an automated retry, where any tests that fail to execute due to SOQL locks etc are retried synchronously. You can override this behaviour using `--disableparalleltesting` which will trigger tests every time in synchronous mode.
{% endhint %}



## &#x20;Using Release Config file for Fast Feedback Release Config Mode / Thorough Release Config Mode&#x20;

A sample release config such as shown below is required for these modes. You can read more about release config file and and its schema [here](release/#automated-generation-of-release-definition)&#x20;

```
// Sample release config file

---
​skipIfAlreadyInstalled: true
skipIfAlreadyInstalled: true
includeOnlyArtifacts:
  - src-env-specific-pre
  - src-env-specific-alias-pre
  - core-crm
  - telephony-service
excludePackageDependencies:
  - Genesys Cloud for Salesforce
  - Marketing Cloud
releasedefinitionProperties:
  changelog:
    workItemFilters:
      -  BRO-[0-9]{3,4}
    workItemUrl: https://bro.atlassian.net/browse
    limit: 30

```

## Evolution of Validate Command

The evolution of additional modes and logic during apex test execution for the **validate** command was due to inputs from the community to automate retry apex testing, enable faster feedback during PR/Merge requests, and isolate selective packages to validate against scratch orgs.  As the community embraced more modular design in their mono repo, the need for additional flexibility during validation was required prevent long queues for PR requests and improve developer experience.

Details about the context and problem statement and resulting decision for each enhancement can reviewed below.

### Decision Records

* [001 - Automated Retry Apex Testing in Synchronous Mode](https://github.com/dxatscale/sfpowerscripts/blob/develop/decision%20records/validate/001-automated-apex-testing-retry.md)
* [002 - Provide Faster Feedback During Validate](https://github.com/dxatscale/sfpowerscripts/blob/develop/decision%20records/validate/002-fast-feedback.md)
* [003 - Individual Validation Mode](https://github.com/dxatscale/sfpowerscripts/blob/develop/decision%20records/validate/003-individual-validation-mode.md)
* [004- Restrict Validation of Packages Validated by Release Config](https://github.com/dxatscale/sfpowerscripts/blob/develop/decision%20records/validate/004-validate-by-release-config.md)

## Validate Against an Existing Org

While validate command works against a scratch org fetched from the Scratch Org Pool (created by [prepare](prepare/) command), there might be instances where you need to validate against an Org where you have more data or control over (as in to write more scripts). This is where a variant of the command **validateAgainstOrg** comes into play. You could provide a target org and sfpowerscripts will try to validate the incoming changes against that org. To make a diff based validation work, please ensure the org has '[sfpowerscripts\_artifact](https://github.com/Accenture/sfpowerscripts/tree/main/prerequisites/sfpowerscripts-artifact)' installed and the records populated with packages that it already has.\
\
**validateAgainstOrg** has a default behaviour for ignoring diffCheck, which means all the packages in the repository will be deployed for validation. To achieve similar behaviour of validate, one could use `diffCheck` flag to ensure only changed packages (compared against what is in the org) need to be built and validated

When **validateAgainstOrg** is used in long running CI environments such as sandboxes, for refactoring purposes, using a Pull Request/Merge Request based approach for validating can result in packages being built on the tip of the temporary PR/MR branch to be installed in the org and then recorded to the org. This will then impact other PRs as these packages will become unreachable since they may never been approved and merged. There is an additional parameters `disableArtifactUpdateFlag` which can be used to let sfpowerscripts know that information about packages should not be written to sfpowerscripts artifact records.

## Common Queries

### My metadata looks intact, but validate is failing on deployment of some packages? Why is that and what should be done?

We have noticed specific instances where a change is not compatible with a scratch org fetched with the pool. Most notorious are changes to picklists, causing checks to fail. We recommend you always create a pool, without **installall** flag, and design your pipelines in a way (through an environment variable / or through a commit message hook) to switch to a pool which only has the dependent packages for your repo to validate your changes.

### I have some issues with some apex test on a particular package and I need to disable it temporarily. What are my options?

You can disable the testing on a particular package by adding the following descriptor to the packages that need to be skipped testing

```
"skipTesting":<boolean> //default:false, skip apex testing during installation of source package to a sandbox
```

### I am not able to get the coverage quite right for a source package and validation is failing. What are my options?

Source packages have a more stringent validation (for an optimized deployment, as each class in the package need to have 75% or more). There will be situations when you need to just go on temporarily (though we don't recommend it), you could use the below descriptor on the package

```
"skipCoverageValidation":<boolean> //default:false, skip apex coverage validation during validation phase,
```

### I am getting "bad object:xxxyyy" error during validate command, What am I doing wrong?

Validate commands compare the incoming commit, with what is installed in the scratch org, and what is in the repos to figure out which packages are to be built and validated in the scratch org. CI Build systems especially like **GitHub Actions** by default only do a fetch of the tip of the Pull Request branch, and hence validate command will not be able to reach out the ancestors to do a diff. We recommend you to check the CI/CD platform docs to do a more deeper fetch of the repo. Here is how is it in GitHub

```
# Checkout the code in the pull request
- name: 'Checkout source code'
  uses: actions/checkout@v2
  with:
        fetch-depth: 0
```
