# Validate

**validate** command helps you to validate a change made to your configuration / code against a scratch org . This command is triggered as part of your pull request (PR) or merge process, to ensure the correctness of configuration/code, before being merged into your **main** branch. validate simplifies setting up and speeding up the process by using a scratch org prepared earlier using [prepare](prepare/)[ ](https://github.com/dxatscale/dxatscale-guide/blob/april-22/projects/sfpowerscripts/orchestrator/broken-reference/README.md)command.

**validate** command runs the following checks with the options to enable additional features such as dependency and impact analysis:

* Checks accuracy of metadata by deploying the metadata to a Just-in-Time CI org
* Triggers Apex Tests
* Validate Apex Test Coverage of each package
* Toggle between standard mode and fast feedback mode for validations
* \[optional] - Validate dependencies between packages for changed components
* \[optional] - Visualize components impacted by changes in pull request

{% hint style="success" %}
**May 2022 Release** \
\
validate command introduces a new feature to enable '**fast feedback**' mode for the validate command which will only do selective deployment of changed metadata in packages and selective tests. Benefits for existing teams is a reduction in time required for PR (pull request) validations.  For more information on this feature, you can review the [decision record](https://github.com/Accenture/sfpowerscripts/blob/develop/decision%20records/validate/002-fast-feedback.md) for the feature.
{% endhint %}

## Sequence of Activities

The following are the list of steps that are orchestrated by the **validate** command

1. Fetch a scratch org from the provided pools in a sequential manner
2. Authenticate to the Scratch org using the [auth URL](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_cli\_reference.meta/sfdx\_cli\_reference/cli\_reference\_auth\_sfdxurl.htm) fetched from the [Scratch Org Info Object](https://developer.salesforce.com/docs/atlas.en-us.object\_reference.meta/object\_reference/sforce\_api\_objects\_scratchorginfo.htm)
3. Build packages that are changed by comparing the tags in your repo against the packages installed in scratch org
4.  For each of the packages (internally calls the Deploy Command)\
    \
    **Standard Mode**\
    ****

    * Deploy all the built packages as [source packages](types-of-packaging/source-packages.md) / [data packages](types-of-packaging/data-packages.md) (unlocked packages are installed as source package)
    * Trigger Apex Tests if there are any apex test in the package
    * Validate test coverage of the package depending on the type of the package (source packages: each class needs to have 75% or more, unlocked packages: packages as whole need to have 75% or more)

    \
    **Fast Feedback Mode**\
    ****

    * Deploy only changed metadata components for built packages as [source packages](types-of-packaging/source-packages.md) / [data packages](types-of-packaging/data-packages.md)
    * Trigger selective Apex Tests based on impact analysis of the changes in the package
    * Skip coverage calculations
    * Skip deployment of package if the descriptor is changed
    * Skip deployment of top level packages direct dependency on the package containing changed components

{% hint style="info" %}
Use of standard mode is still recommended in the pipeline with fast feedback to ensure coverage computation and scripts added to the descriptor files are correctly working and deployable in an empty org.
{% endhint %}

## Validate against an existing org

While validate command works against a scratch org fetched from the Scratch Org Pool (created by [prepare](prepare/) command), there might be instances where you need to validate against an Org where you have more data or control over (as in to write more scripts). This is where a variant of the command **validateAgainstOrg** come into play. You could provide a target org and sfpowerscripts will try to validate the incoming changes against that org. To make a diff based validation work, please ensure the org has '[sfpowerscripts\_artifact](https://github.com/Accenture/sfpowerscripts/tree/main/prerequisites/sfpowerscripts-artifact)' installed and the records populated with packages that it already has.\
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

Validate commands compare the incoming commit, with what is installed in the scratch org, and what is in the repos to figure out which packages are to be built and validated in the scratch org. CI Build systems especially like **Github Actions** by default only do a fetch of the tip of the Pull Request branch, and hence validate command will not be able to reach out the ancestors to do a diff. We recommend you to check the CI/CD platform docs to do a more deeper fetch of the repo. Here is how is it in Github

```
            # Checkout the code in the pull request
            - name: 'Checkout source code'
              uses: actions/checkout@v2
              with:
                fetch-depth: 0
```
