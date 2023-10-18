---
description: '@dxatscale/sfpowerscripts/23.4.2 darwin-arm64 node-v20.3.1'
---

# Command Glossary

To list all the commands for sfpowerscripts, enter the following in your terminal:

```bash
> sfp
> sfp --help

> sfpowerscripts
> sfpowerscripts --help

DX@Scale Toolkit

VERSION
  @dxatscale/sfpowerscripts/23.4.2 darwin-arm64 node-v20.3.1

USAGE
  $ @dxatscale/sfpowerscripts [COMMAND]

TOPICS
  apextests          Trigger Apex Tests and validate apex tests in a package
  artifacts          Fetch artifacts from an artifact registry that is either NPM compatible or supports universal artifacts
  changelog          Track your artifacts & user stories as they progress through different environments, with release changelogs
  dependency         Commands to help with dependency management of a project
  metrics            Report a custom metric to any sfpowerscripts supported metric provider
  orchestrator       Orchestrate packages from a monorepo through its lifecycle, driven by descriptors in your sfdx-project.json
  package            Work with various types of packages such as unlocked/source/data/delta individually
  pool               Manage the pooled orgs created by the sfpowerscripts orchestrator in prepare stage
  profile            This command is used in the lower environments such as ScratchOrgs , Development / System Testing Sandboxes, where a retrieved profile from production has to be cleaned up only
                     for the metadata that is contained in the environment or  base it only as per the metadata that is contained in the packaging directory.
  releasedefinition  Commands around release definition
  repo               Commands to help with maintaing repository
```

| Topics                                                    | Command                                                                                         | Description                                                                                                                                                                                                                                                                                                              |
| --------------------------------------------------------- | ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| apextests                                                 |                                                                                                 | Trigger Apex Tests and validate apex tests in a package                                                                                                                                                                                                                                                                  |
|                                                           | [apextests:trigger](command-glossary.md#sfp-apextests-trigger-help)                             | Triggers Apex unit test in an org. Supports test level RunAllTestsInPackage, which optionally allows validation of individual class code coverage                                                                                                                                                                        |
| artifacts                                                 |                                                                                                 | Fetch artifacts from an artifact registry that is either NPM compatible or supports universal artifacts                                                                                                                                                                                                                  |
|                                                           | [artifacts:fetch](command-glossary.md#sfp-artifacts-fetch-help)                                 | Fetch artifacts from an artifact registry that is either NPM compatible or supports universal artifacts                                                                                                                                                                                                                  |
|                                                           | [artifacts:query](command-glossary.md#sfp-artifacts-query-help)                                 | Fetch details about artifacts installed in a target org                                                                                                                                                                                                                                                                  |
| changelog                                                 |                                                                                                 | Track your artifacts & user stories as they progress through different environments, with release changelogs                                                                                                                                                                                                             |
|                                                           | [changelog:generate](command-glossary.md#sfp-changelog-generate-help)                           | Generates release changelog, providing a summary of artifact versions, work items and commits introduced in a release. Creates a release definition based on artifacts contained in the artifact directory, and compares it to previous release definition in changelog stored on a source repository                    |
| dependency                                                |                                                                                                 | Commands to help with dependency management of a project                                                                                                                                                                                                                                                                 |
|                                                           | [dependency:expand](command-glossary.md#sfp-dependency-expand-help)                             | Expand the dependency list in sfdx-project.json file for each package, fix the gap of dependencies from its dependent packages                                                                                                                                                                                           |
|                                                           | [dependency:install](command-glossary.md#sfp-dependency-install-help)                           | Install all the external dependencies of a given project                                                                                                                                                                                                                                                                 |
|                                                           | [dependency:shrink](command-glossary.md#sfp-dependency-shrink-help)                             | Shrink the dependency list in sfdx-project.json file for each package, remove duplicate dependencies that already exist in its dependent packages                                                                                                                                                                        |
| metrics                                                   |                                                                                                 | Report a custom metric to any sfpowerscripts supported metric provider                                                                                                                                                                                                                                                   |
|                                                           | [metrics:report](command-glossary.md#sfp-metrics-report-help)                                   | Report a custom metric to any sfpowerscripts supported metric provider                                                                                                                                                                                                                                                   |
| orchestrator                                              |                                                                                                 | Orchestrate packages from a monorepo through its lifecycle, driven by descriptors in your sfdx-project.json                                                                                                                                                                                                              |
|                                                           | [orchestrator:build](command-glossary.md#sfp-orchestrator-build-help)                           | Build all packages (unlocked/source/data) in a repo in parallel, respecting the dependency of each packages and generate artifacts to a provided directory                                                                                                                                                               |
|                                                           | [orchestrator:deploy](command-glossary.md#sfp-orchestrator-deploy-help)                         | Deploy packages from the provided aritfact directory, to a given org, using the order and configurable flags provided in sfdx-project.json                                                                                                                                                                               |
|                                                           | [orchestrator:prepare](command-glossary.md#sfp-orchestrator-prepare-help)                       | Prepare a pool of scratchorgs with all the packages upfront, so that any incoming change can be validated in an optimized manner                                                                                                                                                                                         |
|                                                           | [orchestrator:promote](command-glossary.md#sfp-orchestrator-promote-help)                       | Promotes validated unlocked packages with code coverage greater than 75%                                                                                                                                                                                                                                                 |
|                                                           | [orchestrator:publish](command-glossary.md#sfp-orchestrator-publish-help)                       | Publish packages to an artifact registry, using a user-provided script that is responsible for authenticating & uploading to the registry.                                                                                                                                                                               |
|                                                           | [orchestrator:quickbuild](command-glossary.md#sfp-orchestrator-quickbuild-help)                 | Build packages (unlocked/source/data) in a repo in parallel, without validating depenencies or coverage in the case of unlocked packages                                                                                                                                                                                 |
|                                                           | [orchestrator:release](command-glossary.md#sfp-orchestrator-release-help)                       | Release a collection of artifacts as defined in the release definition file                                                                                                                                                                                                                                              |
|                                                           | [orchestrator:validate](command-glossary.md#sfp-orchestrator-validate-help)                     | Validate the incoming change against an earlier prepared scratchorg                                                                                                                                                                                                                                                      |
|                                                           | [orchestrator:validateAgainstOrg](command-glossary.md#sfp-orchestrator-validateagainstorg-help) | Validate the incoming change against target org                                                                                                                                                                                                                                                                          |
| package                                                   |                                                                                                 | Work with various types of packages such as unlocked/source/data/delta individually                                                                                                                                                                                                                                      |
|                                                           | [package:data](command-glossary.md#sfp-package-data-help)                                       | Commands to create and install data packages (sfdmu)                                                                                                                                                                                                                                                                     |
|                                                           | [package:source](command-glossary.md#sfp-package-source-help)                                   | Commands to create and install sfpowerscripts source packages                                                                                                                                                                                                                                                            |
|                                                           | [package:unlocked](command-glossary.md#sfp-package-unlocked-help)                               | Commands to create and install unlocked packages                                                                                                                                                                                                                                                                         |
|                                                           | [package:install](command-glossary.md#sfp-package-install-help)                                 | Unified command to install any sfpowerscripts  packages/artifacts                                                                                                                                                                                                                                                        |
| pool                                                      |                                                                                                 | Manage the pooled orgs created by the sfpowerscripts orchestrator in prepare stage                                                                                                                                                                                                                                       |
| [pool:metrics](command-glossary.md#sfp-pool-metrics-help) |                                                                                                 | Publish metrics about scratch org pools to your observability platform, via StatsD or direct APIs for supported platforms                                                                                                                                                                                                |
|                                                           | [pool:metrics:publish](command-glossary.md#sfp-pool-metrics-publish-help)                       | Publish metrics about scratch org pools to your observability platform, via StatsD or direct APIs for supported platforms                                                                                                                                                                                                |
| pool:org                                                  |                                                                                                 | Deletes a particular scratch org in the pool, This command is to be used in a pipeline with correct permissions to delete any active scratch org record or to be used by an administrator                                                                                                                                |
|                                                           | [pool:org:delete](command-glossary.md#sfp-pool-org-delete-help)                                 | Deletes a particular scratch org in the pool, This command is to be used in a pipeline with correct permissions to delete any active scratch org record or to be used by an administrator                                                                                                                                |
| pool                                                      |                                                                                                 | Manage the pooled orgs created by the sfpowerscripts orchestrator in prepare stage                                                                                                                                                                                                                                       |
|                                                           | [pool:delete](command-glossary.md#sfp-pool-delete-help)                                         | Deletes the pooled scratch orgs from the Scratch Org Pool                                                                                                                                                                                                                                                                |
|                                                           | [pool:fetch](command-glossary.md#sfp-pool-fetch-help)                                           | Gets an active/unused scratch org from the scratch org pool                                                                                                                                                                                                                                                              |
|                                                           | [pool:list](command-glossary.md#sfp-pool-list-help)                                             | Retrieves a list of active scratch org and details from any pool. If this command is run with -m\|--mypool, the command will retrieve the passwords for the pool created by the user who is executing the command.                                                                                                       |
| profile                                                   |                                                                                                 | This command is used in the lower environments such as ScratchOrgs , Development / System Testing Sandboxes, where a retrieved profile from production has to be cleaned up only for the metadata that is contained in the environment or base it only as per the metadata that is contained in the packaging directory. |
|                                                           | [profile:reconcile](command-glossary.md#sfp-profile-reconcile-help)                             | This command is used in the lower environments such as ScratchOrgs , Development / System Testing Sandboxes, where a retrieved profile from production has to be cleaned up only for the metadata that is contained in the environment or base it only as per the metadata that is contained in the packaging directory. |
| releasedefinition                                         |                                                                                                 | Commands around release definition                                                                                                                                                                                                                                                                                       |
|                                                           | [releasedefinition:generate](command-glossary.md#sfp-releasedefinition-generate-help)           | Generates release defintion based on the artifacts installed from a commit reference                                                                                                                                                                                                                                     |
| repo                                                      |                                                                                                 | Commands to help with maintaining repository                                                                                                                                                                                                                                                                             |
|                                                           | [repo:patch](command-glossary.md#sfp-repo-patch-help)                                           | \[Alpha] Patch a branch in the repository as per the release definition and create a new branch                                                                                                                                                                                                                          |



## `sfp apextests:trigger --help`

Triggers Apex unit test in an org. Supports test level RunAllTestsInPackage, which optionally allows validation of individual class code coverage

```
USAGE
  $ @dxatscale/sfpowerscripts apextests:trigger -u <value> [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL] [--apiversion <value>] [-l
    RunSpecifiedTests|RunApexTestSuite|RunLocalTests|RunAllTestsInOrg|RunAllTestsInPackage] [-n <value>] [-c] [--validatepackagecoverage] [--specifiedtests <value>] [--apextestsuite <value>] [-p
    <value>] [-w <value>]

FLAGS
  -c, --validateindividualclasscoverage  Validate that individual classes have a coverage greater than the minimum required percentage coverage, only available when test level is
                                         RunAllTestsInPackage
  -l, --testlevel=<option>               [default: RunLocalTests] The test level of the test that need to be executed when the code is to be deployed
                                         <options: RunSpecifiedTests|RunApexTestSuite|RunLocalTests|RunAllTestsInOrg|RunAllTestsInPackage>
  -n, --package=<value>                  Name of the package to run tests. Required when test level is RunAllTestsInPackage
  -p, --coveragepercent=<value>          [default: 75] Minimum required percentage coverage, when validating code coverage
  -u, --targetusername=<value>           (required) Username or alias of the target org.
  -w, --waittime=<value>                 [default: 60] wait time for command to finish in minutes
  --apextestsuite=<value>                comma-separated list of Apex test suite names to run
  --apiversion=<value>                   Override the api version used for api requests made by this command
  --loglevel=<option>                    [default: info] logging level for this command invocation
                                         <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>
  --specifiedtests=<value>               comma-separated list of Apex test class names or IDs and, if applicable, test methods to run
  --validatepackagecoverage              Validate that the package coverage is greater than the minimum required percentage coverage, only available when test level is RunAllTestsInPackage

DESCRIPTION
  Triggers Apex unit test in an org. Supports test level RunAllTestsInPackage, which optionally allows validation of individual class code coverage

EXAMPLES
  $ sfp apextests:trigger -u scratchorg -l RunLocalTests -s

  $ sfp apextests:trigger -u scratchorg -l RunAllTestsInPackage -n <mypackage> -c
```

## `sfp` artifacts:fetch `--help`

Fetch artifacts from an artifact registry that is either NPM compatible or supports universal artifacts

```
USAGE
  $ @dxatscale/sfpowerscripts artifacts:fetch -d <value> [-p <value>] [--scope <value> [--npm | -f <value>]] [--npmrcpath <value> ] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -d, --artifactdir=<value>        (required) [default: artifacts] Directory to save downloaded artifacts
  -f, --scriptpath=<value>         (Optional: no-NPM) Path to script that authenticates and downloads artifacts from the registry
  -p, --releasedefinition=<value>  Path to YAML file containing map of packages and package versions to download
  --loglevel=<option>              [default: info] logging level for this command invocation
                                   <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>
  --npm                            Download artifacts from a pre-authenticated private npm registry
  --npmrcpath=<value>              Path to .npmrc file used for authentication to registry. If left blank, defaults to home directory
  --scope=<value>                  (required for NPM) User or Organisation scope of the NPM package

DESCRIPTION
  Fetch artifacts from an artifact registry that is either NPM compatible or supports universal artifacts

EXAMPLES
  $ sfp artifacts:fetch -p myreleasedefinition.yaml -f myscript.sh

  $ sfp artifacts:fetch -p myreleasedefinition.yaml --npm --scope myscope --npmrcpath path/to/.npmrc
```

## `sfp` artifacts:query `--help`

Fetch details about artifacts installed in a target org.

```
USAGE
  $ @dxatscale/sfpowerscripts artifacts:query -u <value> [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -u, --targetusername=<value>  (required) Username or alias of the target org.
  --loglevel=<option>           [default: info] logging level for this command invocation
                                <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>

GLOBAL FLAGS
  --json  Format output as json.

DESCRIPTION
  Fetch details about artifacts installed in a target org

EXAMPLES
  $ sfp artifacts:query -u <target_org>
```

## `sfp` changelog:generate `--help`

Generates release changelog, providing a summary of artifact versions, work items and commits introduced in a release. Creates a release definition based on artifacts contained in the artifact directory, and compares it to previous release definition in changelog stored on a source repository

```
USAGE
  $ @dxatscale/sfpowerscripts changelog:generate -d <value> -n <value> -w <value> [--limit <value>] [--workitemurl <value>] [-r <value>] [--directory <value>] (--nopush -b <value>)
    [--showallartifacts] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -b, --branchname=<value>      (required) Repository branch in which the changelog files are located
  -d, --artifactdir=<value>     (required) [default: artifacts] Directory containing sfpowerscripts artifacts
  -n, --releasename=<value>     (required) Name of the release for which to generate changelog
  -r, --repourl=<value>         Repository in which the changelog files are located. Assumes user is already authenticated.
  -w, --workitemfilter=<value>  (required) Regular expression used to search for work items (user stories) introduced in release
  --directory=<value>           Relative path to directory to which the release defintion file should be generated, if the directory doesnt exist, it will be created
  --limit=<value>               limit the number of releases to display in changelog markdown
  --loglevel=<option>           [default: info] logging level for this command invocation
                                <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>
  --nopush                      Do not push the changelog to a repository to the provided branch
  --showallartifacts            Show all artifacts in changelog markdown, including those that have not changed in the release
  --workitemurl=<value>         Generic URL for work items. Each work item ID will be appended to the URL, providing quick access to work items

DESCRIPTION
  Generates release changelog, providing a summary of artifact versions, work items and commits introduced in a release. Creates a release definition based on artifacts contained in the artifact
  directory, and compares it to previous release definition in changelog stored on a source repository

EXAMPLES
  $ sfpowerscripts changelog:generate -n <releaseName> -d path/to/artifact/directory -w <regexp> -r <repoURL> -b <branchName>
```

## `sfp` dependency:expand `--help`

Expand the dependency list in sfdx-project.json file for each package, fix the gap of dependencies from its dependent packages

```
USAGE
  $ @dxatscale/sfpowerscripts dependency:expand -v <value> [-o] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -o, --overwrite                     Flag to overwrite existing sfdx-project.json file
  -v, --targetdevhubusername=<value>  (required) Username or alias of the Dev Hub org.
  --loglevel=<option>                 [default: info] logging level for this command invocation
                                      <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>

DESCRIPTION
  Expand the dependency list in sfdx-project.json file for each package, fix the gap of dependencies from its dependent packages
```

## `sfp` dependency:install `--help`

Install all the external dependencies of a given project

```
USAGE
  $ @dxatscale/sfpowerscripts dependency:install -u <value> -v <value> [-k <value>] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -k, --installationkeys=<value>      Installation key for key-protected packages (format is packagename:key --> core:key nCino:key vlocity:key to allow some packages without installation key)
  -u, --targetusername=<value>        (required) Username or alias of the target org.
  -v, --targetdevhubusername=<value>  (required) Username or alias of the Dev Hub org.
  --loglevel=<option>                 [default: info] logging level for this command invocation
                                      <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>

DESCRIPTION
  Install all the external dependencies of a given project
```

## `sfp` dependency:shrink `--help`

Shrink the dependency list in sfdx-project.json file for each package, remove duplicate dependencies that already exist in its dependent packages

```
USAGE
  $ @dxatscale/sfpowerscripts dependency:shrink -v <value> [-o] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -o, --overwrite                     Flag to overwrite existing sfdx-project.json file
  -v, --targetdevhubusername=<value>  (required) Username or alias of the Dev Hub org.
  --loglevel=<option>                 [default: info] logging level for this command invocation
                                      <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>

DESCRIPTION
  Shrink the dependency list in sfdx-project.json file for each package, remove duplicate dependencies that already exist in its dependent packages
```

## `sfp` metrics:report `--help`

Report a custom metric to any sfpowerscripts supported metric provider

```
USAGE
  $ @dxatscale/sfpowerscripts metrics:report -m <value> -t gauge|counter|timer [-v <value>] [-g <value>] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -g, --tags=<value>    tags for metric
  -m, --metric=<value>  (required) metrics to publish
  -t, --type=<option>   (required) type of metric
                        <options: gauge|counter|timer>
  -v, --value=<value>   value of metric
  --loglevel=<option>   [default: info] logging level for this command invocation
                        <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>

DESCRIPTION
  Report a custom metric to any sfpowerscripts supported metric provider

EXAMPLES
  $ sfpowerscripts metrics:report -m <metric> -t <type> -v <value>
```

## `sfp` orchestrator:build `--help`

Build all packages (unlocked/source/data) in a repo in parallel, respecting the dependency of each packages and generate artifacts to a provided directory

```
USAGE
  $ @dxatscale/sfpowerscripts orchestrator:build -v <value> --branch <value> [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL] [--apiversion <value>] [--diffcheck] [-r
    <value>] [-f <value>] [--artifactdir <value>] [--waittime <value>] [--buildnumber <value>] [--executorcount <value>] [--tag <value>] [--releaseconfig <value>]

FLAGS
  -f, --configfilepath=<value>  [default: config/project-scratch-def.json] Path in the current project directory containing  config file for the packaging org
  -r, --repourl=<value>         Custom source repository URL to use in artifact metadata, overrides origin URL defined in git config
  -v, --devhubalias=<value>     (required) Username or alias of the Dev Hub org.
  --apiversion=<value>          Override the api version used for api requests made by this command
  --artifactdir=<value>         [default: artifacts] The directory where the generated artifact is to be written
  --branch=<value>              (required) The git branch that this build is triggered on, Useful for metrics and general identification purposes
  --buildnumber=<value>         [default: 1] The build number to be used for source packages, Unlocked Packages will be assigned the buildnumber from Saleforce directly if using .NEXT
  --diffcheck                   Only build the packages which have changed by analyzing previous tags
  --executorcount=<value>       [default: 5] Number of parallel package task schedulors
  --loglevel=<option>           [default: info] logging level for this command invocation
                                <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>
  --releaseconfig=<value>       Path to the release config file which determines what packages should be built
  --tag=<value>                 Tag the build with a label, useful to identify in metrics
  --waittime=<value>            [default: 120] Wait time for command to finish in minutes

DESCRIPTION
  Build all packages (unlocked/source/data) in a repo in parallel, respecting the dependency of each packages and generate artifacts to a provided directory
```

## `sfp` orchestrator:deploy `--help`

Deploy packages from the provided aritfact directory, to a given org, using the order and configurable flags provided in sfdx-project.json

```
USAGE
  $ @dxatscale/sfpowerscripts orchestrator:deploy -u <value> [--artifactdir <value>] [--waittime <value>] [-t <value>] [-b <value> --skipifalreadyinstalled] [--releaseconfig <value>]
    [--enablesourcetracking] [-g <value>] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -b, --baselineorg=<value>         The org against which the package skip should be baselined
  -g, --logsgroupsymbol=<value>...  Symbol used by CICD platform to group/collapse logs in the console. Provide an opening group, and an optional closing group symbol.
  -t, --tag=<value>                 Tag the deploy with a label, useful for identification in metrics
  -u, --targetorg=<value>           (required) Username or alias of the target org.
  --artifactdir=<value>             [default: artifacts] The directory containing artifacts to be deployed
  --enablesourcetracking            Enable source tracking on the packages being deployed to an org
  --loglevel=<option>               [default: info] logging level for this command invocation
                                    <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>
  --releaseconfig=<value>           Path to the config file which determines how the packages are deployed based on the filters in release config
  --skipifalreadyinstalled          Skip the package installation if the package is already installed in the org
  --waittime=<value>                [default: 120] Wait time for command to finish in minutes

DESCRIPTION
  Deploy packages from the provided aritfact directory, to a given org, using the order and configurable flags provided in sfdx-project.json

EXAMPLES
  $ sfpowerscripts orchestrator:deploy -u <username>
```

## `sfp` orchestrator:prepare `--help`

Prepare a pool of scratchorgs with all the packages upfront, so that any incoming change can be validated in an optimized manner

```
USAGE
  $ @dxatscale/sfpowerscripts orchestrator:prepare -v <value> [-f <value>] [--npmrcpath <value>] [--keys <value>] [-g <value>] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -f, --poolconfig=<value>            [default: config/poolconfig.json] The path to the configuration file for creating a pool of scratch orgs
  -g, --logsgroupsymbol=<value>...    Symbol used by CICD platform to group/collapse logs in the console. Provide an opening group, and an optional closing group symbol.
  -v, --targetdevhubusername=<value>  (required) Username or alias of the Dev Hub org.
  --keys=<value>                      Keys to be used while installing any managed package dependencies. Required format is a string of key-value pairs separated by spaces e.g. packageA:pw123
                                      packageB:pw123 packageC:pw123
  --loglevel=<option>                 [default: info] logging level for this command invocation
                                      <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>
  --npmrcpath=<value>                 Path to .npmrc file used for authentication to a npm registry when using npm based artifacts. If left blank, defaults to home directory

DESCRIPTION
  Prepare a pool of scratchorgs with all the packages upfront, so that any incoming change can be validated in an optimized manner

EXAMPLES
  $ sfpowerscripts orchestrator:prepare -f config/mypoolconfig.json  -v <devhub>
```

## `sfp` orchestrator:promote `--help`

Promotes validated unlocked packages with code coverage greater than 75%

```
USAGE
  $ @dxatscale/sfpowerscripts orchestrator:promote -v <value> -d <value> [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -d, --artifactdir=<value>           (required) [default: artifacts] The directory where artifacts are located
  -v, --targetdevhubusername=<value>  (required) Username or alias of the Dev Hub org.
  --loglevel=<option>                 [default: info] logging level for this command invocation
                                      <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>

DESCRIPTION
  Promotes validated unlocked packages with code coverage greater than 75%

EXAMPLES
  $ sfpowerscripts orchestrator:promote -d path/to/artifacts -v <org>
```

## `sfp` orchestrator:publish `--help`

Publish packages to an artifact registry, using a user-provided script that is responsible for authenticating & uploading to the registry.

```
USAGE
  $ @dxatscale/sfpowerscripts orchestrator:publish -d <value> [-p -v <value>] [-t <value>] [--gittag] [--gittaglimit <value>] [--gittagage <value>] [--pushgittag] [--scope <value> [--npm | -f
    <value>]] [--npmtag <value> ] [--npmrcpath <value> ] [-g <value>] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -d, --artifactdir=<value>         (required) [default: artifacts] The directory containing artifacts to be published
  -f, --scriptpath=<value>          Path to script that authenticates and uploaded artifacts to the registry
  -g, --logsgroupsymbol=<value>...  Symbol used by CICD platform to group/collapse logs in the console. Provide an opening group, and an optional closing group symbol.
  -p, --publishpromotedonly         Only publish unlocked packages that have been promoted
  -t, --tag=<value>                 Tag the publish with a label, useful for identification in metrics
  -v, --devhubalias=<value>         Username or alias of the Dev Hub org.
  --gittag                          Tag the current commit ID with an annotated tag containing the package name and version - does not push tag
  --gittagage=<value>               Specifies the number of days,for a tag to be retained,any tags older the provided number will be deleted
  --gittaglimit=<value>             Specifies the minimum number of  tags to be retained for a package
  --loglevel=<option>               [default: info] logging level for this command invocation
                                    <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>
  --npm                             Upload artifacts to a pre-authenticated private npm registry
  --npmrcpath=<value>               Path to .npmrc file used for authentication to registry. If left blank, defaults to home directory
  --npmtag=<value>                  Add an optional distribution tag to NPM packages. If not provided, the 'latest' tag is set to the published version.
  --pushgittag                      Pushes the git tags created by this command to the repo, ensure you have access to the repo
  --scope=<value>                   (required for NPM) User or Organisation scope of the NPM package

DESCRIPTION
  Publish packages to an artifact registry, using a user-provided script that is responsible for authenticating & uploading to the registry.

EXAMPLES
  $ sfpowerscripts orchestrator:publish -f path/to/script

  $ sfpowerscripts orchestrator:publish --npm

  $ sfpowerscripts orchestrator:publish -f path/to/script -p -v HubOrg

  $ sfpowerscripts orchestrator:publish -f path/to/script --gittag --pushgittag
```

## `sfp` orchestrator:quickbuild `--help`

Build packages (unlocked/source/data) in a repo in parallel, without validating depenencies or coverage in the case of unlocked packages

```
USAGE
  $ @dxatscale/sfpowerscripts orchestrator:quickbuild -v <value> --branch <value> [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL] [--apiversion <value>] [--diffcheck] [-r
    <value>] [-f <value>] [--artifactdir <value>] [--waittime <value>] [--buildnumber <value>] [--executorcount <value>] [--tag <value>] [--releaseconfig <value>]

FLAGS
  -f, --configfilepath=<value>  [default: config/project-scratch-def.json] Path in the current project directory containing  config file for the packaging org
  -r, --repourl=<value>         Custom source repository URL to use in artifact metadata, overrides origin URL defined in git config
  -v, --devhubalias=<value>     (required) Username or alias of the Dev Hub org.
  --apiversion=<value>          Override the api version used for api requests made by this command
  --artifactdir=<value>         [default: artifacts] The directory where the generated artifact is to be written
  --branch=<value>              (required) The git branch that this build is triggered on, Useful for metrics and general identification purposes
  --buildnumber=<value>         [default: 1] The build number to be used for source packages, Unlocked Packages will be assigned the buildnumber from Saleforce directly if using .NEXT
  --diffcheck                   Only build the packages which have changed by analyzing previous tags
  --executorcount=<value>       [default: 5] Number of parallel package task schedulors
  --loglevel=<option>           [default: info] logging level for this command invocation
                                <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>
  --releaseconfig=<value>       Path to the release config file which determines what packages should be built
  --tag=<value>                 Tag the build with a label, useful to identify in metrics
  --waittime=<value>            [default: 120] Wait time for command to finish in minutes

DESCRIPTION
  Build packages (unlocked/source/data) in a repo in parallel, without validating depenencies or coverage in the case of unlocked packages
```

## `sfp` orchestrator:release `--help`

Release a collection of artifacts as defined in the release definition file

```
USAGE
  $ @dxatscale/sfpowerscripts orchestrator:release -p <value> -u <value> [--scope <value> [--npm | -f <value>]] [--npmrcpath <value> ] [-g <value>] [-t <value>] [--waittime <value>] [--keys <value>]
    [-d <value>] [-b <value> --generatechangelog] [-v <value>] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -b, --branchname=<value>            Repository branch in which the changelog files are located
  -d, --directory=<value>             Relative path to directory to which the changelog should be generated, if the directory doesnt exist, it will be created
  -f, --scriptpath=<value>            (Optional: no-NPM) Path to script that authenticates and downloads artifacts from the registry
  -g, --logsgroupsymbol=<value>...    Symbol used by CICD platform to group/collapse logs in the console. Provide an opening group, and an optional closing group symbol.
  -p, --releasedefinition=<value>...  (required) Path to release definiton yaml, Multiple paths can be seperated by commas
  -t, --tag=<value>                   Tag the release with a label, useful for identification in metrics
  -u, --targetorg=<value>             (required) Username or alias of the target org.
  -v, --devhubalias=<value>           Username or alias of the Dev Hub org.
  --generatechangelog                 Create a release changelog
  --keys=<value>                      Keys to be used while installing any managed package dependencies. Required format is a string of key-value pairs separated by spaces e.g. packageA:pw123
                                      packageB:pw123 packageC:pw123
  --loglevel=<option>                 [default: info] logging level for this command invocation
                                      <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>
  --npm                               Download artifacts from a pre-authenticated private npm registry
  --npmrcpath=<value>                 Path to .npmrc file used for authentication to registry. If left blank, defaults to home directory
  --scope=<value>                     (required for NPM) User or Organisation scope of the NPM package
  --waittime=<value>                  [default: 120] Wait time for package installation

DESCRIPTION
  Release a  collection of artifacts as defined in the release definition file

EXAMPLES
  sfpowerscripts orchestrator:release -p path/to/releasedefinition.yml -u myorg --npm --scope myscope --generatechangelog
```

## `sfp` orchestrator:validate `--help`

Validate the incoming change against an earlier prepared scratchorg

```
USAGE
  $ @dxatscale/sfpowerscripts orchestrator:validate -p <value> -v <value> --mode individual|fastfeedback|thorough|ff-release-config|thorough-release-config [--installdeps] [--releaseconfig <value>]
    [--coveragepercent <value>] [--disablesourcepkgoverride] [-x] [--orginfo] [--keys <value>] [--enableimpactanalysis --basebranch <value>] [--enabledependencyvalidation ] [--tag <value>]
    [--disableparalleltesting] [--disablediffcheck] [--disableartifactupdate] [-g <value>] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -g, --logsgroupsymbol=<value>...    Symbol used by CICD platform to group/collapse logs in the console. Provide an opening group, and an optional closing group symbol.
  -p, --pools=<value>...              (required) Fetch scratch-org validation environment from one of listed pools, sequentially
  -v, --targetdevhubusername=<value>  (required) Username or alias of the Dev Hub org.
  -x, --deletescratchorg              Delete scratch-org validation environment, after the command has finished running
  --basebranch=<value>                The pull request base branch
  --coveragepercent=<value>           [default: 75] Minimum required percentage coverage for validating code coverage of packages with Apex classes
  --disableartifactupdate             Do not update information about deployed artifacts to the org
  --disablediffcheck                  Disables diff check while validating, this will validate all the packages in the repository
  --disableparalleltesting            Disable test execution in parallel, this will execute apex tests in serial
  --disablesourcepkgoverride          Disables overriding unlocked package installation as source package installation during validate
  --enabledependencyvalidation        Validate dependencies between packages for changed components
  --enableimpactanalysis              Visualize components impacted by changes in pull request
  --installdeps                       Install dependencies during fast feedback
  --keys=<value>                      Keys to be used while installing any managed package dependencies. Required format is a string of key-value pairs separated by spaces e.g. packageA:pw123
                                      packageB:pw123 packageC:pw123
  --loglevel=<option>                 [default: info] logging level for this command invocation
                                      <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>
  --mode=<option>                     (required) [default: thorough] validation mode
                                      <options: individual|fastfeedback|thorough|ff-release-config|thorough-release-config>
  --orginfo                           Display info about the org that is used for validation
  --releaseconfig=<value>             (Required if the release modes are ff-relese-config or thorough-release-config), Path to the config file which determines how the release defintion should be
                                      generated
  --tag=<value>                       Tag the build with a label, useful to identify in metrics

DESCRIPTION
  Validate the incoming change against an earlier prepared scratchorg

EXAMPLES
  $ sfp orchestrator:validate -p "POOL_TAG_1,POOL_TAG_2" -v <devHubUsername>
```

## `sfp` orchestrator:validateAgainstOrg `--help`

Validate the incoming change against target org

```
USAGE
  $ @dxatscale/sfpowerscripts orchestrator:validateAgainstOrg -u <value> --mode individual|fastfeedback|thorough|ff-release-config|thorough-release-config [--releaseconfig <value>] [--coveragepercent <value>]
    [--diffcheck] [--disableartifactupdate] [-g <value>] [--basebranch <value>] [--orginfo] [--installdeps] (--disablesourcepkgoverride -v <value>) [--disableparalleltesting] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -g, --logsgroupsymbol=<value>...  Symbol used by CICD platform to group/collapse logs in the console. Provide an opening group, and an optional closing group symbol.
  -u, --targetorg=<value>           (required) Username or alias of the target org.
  -v, --devhubalias=<value>         (required) Username or alias of the Dev Hub org.
  --basebranch=<value>              The pull request base branch
  --coveragepercent=<value>         [default: 75] Minimum required percentage coverage for validating code coverage of packages with Apex classes
  --diffcheck                       Only build the packages which have changed by analyzing previous tags
  --disableartifactupdate           Do not update information about deployed artifacts to the org
  --disableparalleltesting          Disable test execution in parallel, this will execute apex tests in serial
  --disablesourcepkgoverride        Disables overriding unlocked package installation as source package installation during validate
  --installdeps                     Install dependencies during fast feedback
  --loglevel=<option>               [default: info] logging level for this command invocation
                                    <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>
  --mode=<option>                   (required) [default: thorough] validation mode
                                    <options: individual|fastfeedback|thorough|ff-release-config|thorough-release-config>
  --orginfo                         Display info about the org that is used for validation
  --releaseconfig=<value>           (Required if the release modes are ff-relese-config or thorough-release-config), Path to the config file which determines how the release defintion should be
                                    generated

DESCRIPTION
  Validate the incoming change against target org

EXAMPLES
  $ sfpowerscripts orchestrator:validateAgainstOrg -u <targetorg>
```

## `sfp` package:data `--help`

Commands to create and install data packages (sfdmu)

```
USAGE
  $ @dxatscale/sfpowerscripts package:data:COMMAND

COMMANDS
  package:data:create   Creates a versioned artifact from a source directory containing SFDMU-based data (in csv format and export json). The artifact can be consumed by release pipelines, to deploy
                        the data to orgs
  package:data:install  Installs a SFDMU-based data package consisting of csvfiles and export.json to a target org
```

## `sfp` package:source `--help`

Commands to create and install sfpowerscripts source packages

```
USAGE
  $ @dxatscale/sfpowerscripts package:source:COMMAND

COMMANDS
  package:source:create   This task simulates a packaging experience similar to unlocked packaging - creating an artifact that consists of the metadata (e.g. commit Id), source code & an optional
                          destructive manifest. The artifact can then be consumed by release pipelines, to deploy the package
  package:source:install  Installs a sfpowerscripts source package to the target org
```

## `sfp` package:unlocked `--help`

Commands to create and install unlocked packages

```
COMMANDS
  package:unlocked:create   Creates a new package version, and generates an artifact that consists of the metadata (e.g. version Id). The artifact can then be consumed by release pipelines, to
                            install the unlocked package. Utilize this task in a package build for DX Unlocked Package
  package:unlocked:install  Installs an unlocked package using sfpowerscripts metadata
  
```

## `sfp package:install --help`

Unified command to install any type of sfp package individually to a given org

```
Installs a sfpowerscripts artifact to an org

USAGE
  $ @dxatscale/sfpowerscripts package:install -u <value> [-n <value>] [--artifactdir <value>] [--securitytype full|none] [-f] [--upgradetype
    delete-only|deprecate-only|mixed-mode] [-o] [-t] [--waittime <value>] [--publishwaittime <value>] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -f, --skipifalreadyinstalled  Skip the installation if the package is already installed in the org
  -n, --package=<value>         Name of the package to be installed
  -o, --optimizedeployment      (source) Optimize deployment by triggering test classes that are in the package, rather than using the whole
                                tests in the org
  -t, --skiptesting             (source) Skips running test when deploying to a sandbox
  -u, --targetorg=<value>       (required) Username or alias of the target org.
  --artifactdir=<value>         [default: artifacts] The directory where the artifact is located
  --loglevel=<option>           [default: info] logging level for this command invocation
                                <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>
  --publishwaittime=<value>     [default: 10] (unlocked) number of minutes to wait for subscriber package version ID to become available in the
                                target org
  --securitytype=<option>       [default: none] (unlocked) Select the security access for the package installation
                                <options: full|none>
  --upgradetype=<option>        [default: mixed-mode] (unlocked)the upgrade type for the package installation
                                <options: delete-only|deprecate-only|mixed-mode>
  --waittime=<value>            [default: 120] wait time for command to finish in minutes

DESCRIPTION
  Installs a sfpowerscripts artifact to an org

EXAMPLES
  $ sfp package:install -n packagename -u sandboxalias -i
```

##

## `sfp` pool:metrics `--help`

Publish metrics about scratch org pools to your observability platform, via StatsD or direct APIs for supported platforms

```
USAGE
  $ @dxatscale/sfpowerscripts pool:metrics:COMMAND

COMMANDS
  pool:metrics:publish  Publish metrics about scratch org pools to your observability platform, via StatsD or direct APIs for supported platforms
```

## `sfp` pool:metrics:publish `--help`

Publish metrics about scratch org pools to your observability platform, via StatsD or direct APIs for supported platforms

```
USAGE
  $ @dxatscale/sfpowerscripts pool:metrics:publish -v <value> [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -v, --targetdevhubusername=<value>  (required) Username or alias of the Dev Hub org.
  --loglevel=<option>                 [default: info] logging level for this command invocation
                                      <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>

DESCRIPTION
  Publish metrics about scratch org pools to your observability platform, via StatsD or direct APIs for supported platforms

EXAMPLES
  $ sfpowerscripts pool:metrics:publish -v <myDevHub>
```

## `sfp` pool:org `--help`

Deletes a particular scratch org in the pool, This command is to be used in a pipeline with correct permissions to delete any active scratch org record or to be used by an administrator

```
USAGE
  $ @dxatscale/sfpowerscripts pool:org:COMMAND

COMMANDS
  pool:org:delete  Deletes a particular scratch org in the pool, This command is to be used in a pipeline with correct permissions to delete any active scratch org record or to be used by an
                   adminsitrator
```

## `sfp` pool:org:delete `--help`

Deletes a particular scratch org in the pool, This command is to be used in a pipeline with correct permissions to delete any active scratch org record or to be used by an adminsitrator

```
USAGE
  $ @dxatscale/sfpowerscripts pool:org:delete -u <value> -v <value> [--apiversion <value>] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -u, --requiredUserNameFlag=<value>  (required) Username or alias of the target org.
  -v, --targetdevhubusername=<value>  (required) Username or alias of the Dev Hub org.
  --apiversion=<value>                Override the api version used for api requests made by this command
  --loglevel=<option>                 [default: info] logging level for this command invocation
                                      <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>

DESCRIPTION
  Deletes a particular scratch org in the pool, This command is to be used in a pipeline with correct permissions to delete any active scratch org record or to be used by an adminsitrator

EXAMPLES
  $ sfpowerscripts pool:org:delete -u test-xasdasd@example.com -v devhub
```

## `sfp` pool:delete `--help`

Deletes the pooled scratch orgs from the Scratch Org Pool

```
USAGE
  $ @dxatscale/sfpowerscripts pool:delete -v <value> [-t <value>] [-i | -a] [-o] [--apiversion <value>] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -a, --allscratchorgs                Deletes all used and unused Scratch orgs from pool by the tag
  -i, --inprogressonly                Deletes all In Progress Scratch orgs from pool by the tag
  -o, --orphans                       Recovers scratch orgs that were created by salesforce but were not tagged to sfpowerscripts due to timeouts etc.
  -t, --tag=<value>                   tag used to identify the scratch org pool
  -v, --targetdevhubusername=<value>  (required) Username or alias of the Dev Hub org.
  --apiversion=<value>                Override the api version used for api requests made by this command
  --loglevel=<option>                 [default: info] logging level for this command invocation
                                      <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>

DESCRIPTION
  Deletes the pooled scratch orgs from the Scratch Org Pool

EXAMPLES
  $ sfpowerscripts pool:delete -t core

  $ sfpowerscripts pool:delete -t core -v devhub

  $ sfpowerscripts pool:delete --orphans -v devhub
```

## `sfp` pool:fetch `--help`

Gets an active/unused scratch org from the scratch org pool

```
USAGE
  $ @dxatscale/sfpowerscripts pool:fetch -v <value> -t <value> [-a <value>] [-s <value>] [-d] [--nosourcetracking] [--apiversion <value>] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -a, --alias=<value>                 Fetch and set an alias for the org
  -d, --setdefaultusername            set the authenticated org as the default username that all commands run against
  -s, --sendtouser=<value>            Send the credentials of the fetched scratchorg to another DevHub user, Useful for situations when pool is only limited to certain users
  -t, --tag=<value>                   (required) (required) tag used to identify the scratch org pool
  -v, --targetdevhubusername=<value>  (required) Username or alias of the Dev Hub org.
  --apiversion=<value>                Override the api version used for api requests made by this command
  --loglevel=<option>                 [default: info] logging level for this command invocation
                                      <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>
  --nosourcetracking                  Do not set source tracking while fetching the scratch org

DESCRIPTION
  Gets an active/unused scratch org from the scratch org pool

EXAMPLES
  $ sfdx sfpowerkit:pool:fetch -t core

  $ sfdx sfpowerkit:pool:fetch -t core -v devhub

  $ sfdx sfpowerkit:pool:fetch -t core -v devhub -m

  $ sfdx sfpowerkit:pool:fetch -t core -v devhub -s testuser@test.com
```

## `sfp` pool:list `--help`

Retrieves a list of active scratch org and details from any pool. If this command is run with -m|--mypool, the command will retrieve the passwords for the pool created by the user who is executing the command.

```
USAGE
  $ @dxatscale/sfpowerscripts pool:list -v <value> [--json] [--apiversion <value>] [-t <value>] [-m] [-a] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -a, --allscratchorgs                Gets all used and unused Scratch orgs from pool
  -m, --mypool                        Filter the tag for any additions created  by the executor of the command
  -t, --tag=<value>                   tag used to identify the scratch org pool
  -v, --targetdevhubusername=<value>  (required) Username or alias of the Dev Hub org.
  --apiversion=<value>                Override the api version used for api requests made by this command
  --loglevel=<option>                 [default: info] logging level for this command invocation
                                      <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>

GLOBAL FLAGS
  --json  Format output as json.

DESCRIPTION
  Retrieves a list of active scratch org and details from any pool. If this command is run with -m|--mypool, the command will retrieve the passwords for the pool created by the user who is executing
  the command.

EXAMPLES
  $ sfpowerscripts pool:list -t core

  $ sfpowerscripts pool:list -t core -v devhub

  $ sfpowerscripts pool:list -t core -v devhub -m

  $ sfpowerscripts pool:list -t core -v devhub -m -a
```

## `sfp` profile:reconcile `--help`

This command is used in the lower environments such as ScratchOrgs , Development / System Testing Sandboxes, where a retrieved profile from production has to be cleaned up only for the metadata that is contained in the environment or base it only as per the metadata that is contained in the packaging directory.

```
USAGE
  $ @dxatscale/sfpowerscripts profile:reconcile -u <value> [-f <value>] [-n <value>] [-d <value>] [-s] [--apiversion <value>] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -d, --destfolder=<value>      the destination folder for reconciled profiles, if omitted existing profiles will be reconciled and will be rewritten in the current location
  -f, --folder=<value>...       path to the folder which contains the profiles to be reconciled,if project contain multiple package directories, please provide a comma seperated list, if omitted,
                                all the package directories will be checked for profiles
  -n, --profilelist=<value>...  list of profiles to be reconciled. If ommited, all the profiles components will be reconciled.
  -s, --sourceonly              set this flag to reconcile profiles only against component available in the project only. Configure ignored perissions in sfdx-project.json file in the array
                                plugins->sfpowerkit->ignoredPermissions.
  -u, --targetorg=<value>       (required) Username or alias of the target org.
  --apiversion=<value>          Override the api version used for api requests made by this command
  --loglevel=<option>           [default: info] logging level for this command invocation
                                <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>

DESCRIPTION
  This command is used in the lower environments such as ScratchOrgs , Development / System Testing Sandboxes, where a retrieved profile from production has to be cleaned up only for the metadata
  that is contained in the environment or  base it only as per the metadata that is contained in the packaging directory.

EXAMPLES
  $ sfpowerscripts profile:reconcile  --folder force-app -d destfolder -s

  $ sfpowerscripts profile:reconcile  --folder force-app,module2,module3 -u sandbox -d destfolder

  $ sfpowerscripts profile:reconcile  -u myscratchorg -d destfolder
```

## `sfp` releasedefinition:generate `--help`

Generates release definition based on the artifacts installed from a commit reference

```
USAGE
  $ @dxatscale/sfpowerscripts releasedefinition:generate -c <value> -f <value> -n <value> [-b <value>] [-d <value>] [--nopush] [--forcepush ] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -b, --branchname=<value>   Repository branch in which the release defintion files are to be written
  -c, --gitref=<value>       (required) Utilize the tags on the source branch to generate release definiton
  -d, --directory=<value>    Relative path to directory to which the release defintion file should be generated, if the directory doesnt exist, it will be created
  -f, --configfile=<value>   (required) Path to the config file which determines how the release defintion should be generated
  -n, --releasename=<value>  (required) Set a releasename on the release definition file created
  --forcepush                Force push changes to the repository branch
  --loglevel=<option>        [default: info] logging level for this command invocation
                             <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>
  --nopush                   Do not push the changelog to a repository to the provided branch

DESCRIPTION
  Generates release defintion based on the artifacts installed from a commit reference

EXAMPLES
  $ sfpowerscripts releasedefinition:generate -n <releaseName>
```

## `sfp` repo:patch `--help`

\[Alpha] Patch a branch in the repository as per the release definition and create a new branch

```
USAGE
  $ @dxatscale/sfpowerscripts repo:patch -p <value> -s <value> -t <value> [--scope <value> [--npm | -f <value>]] [--npmrcpath <value> ] [-g <value>] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -f, --scriptpath=<value>             (Optional: no-NPM) Path to script that authenticates and downloads artifacts from the registry
  -g, --logsgroupsymbol=<value>...     Symbol used by CICD platform to group/collapse logs in the console. Provide an opening group, and an optional closing group symbol.
  -p, --releasedefinitions=<value>...  (required) Path to release definiton yaml
  -s, --sourcebranchname=<value>       (required) Name of the source branch to be used on which the alignment need to be applied
  -t, --targetbranchname=<value>       (required) Name of the target branch to be created after the alignment
  --loglevel=<option>                  [default: info] logging level for this command invocation
                                       <options: trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL>
  --npm                                Download artifacts from a pre-authenticated private npm registry
  --npmrcpath=<value>                  Path to .npmrc file used for authentication to registry. If left blank, defaults to home directory
  --scope=<value>                      (required for NPM) User or Organisation scope of the NPM package

DESCRIPTION
  [Alpha] Patch a branch in the repository as per the release definition and create a new branch

EXAMPLES
  $ sfpowerscripts repo:patch -n <releaseName>
```
