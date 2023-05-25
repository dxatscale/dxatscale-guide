---
description: Commands in sfpowercripts
---

# Command Glossary

* `sfdx sfpowerscripts:analyze:pmd`
* `sfdx sfpowerscripts:apextests:trigger`
* `sfdx sfpowerscripts:apextests:validate`
* `sfdx sfpowerscripts:artifacts:fetch`
* `sfdx sfpowerscripts:artifacts:query`
* `sfdx sfpowerscripts:changelog:generate`
* `sfdx sfpowerscripts:orchestrator:build`
* `sfdx sfpowerscripts:orchestrator:deploy`
* `sfdx sfpowerscripts:orchestrator:prepare`
* `sfdx sfpowerscripts:orchestrator:promote`&#x20;
* `sfdx sfpowerscripts:orchestrator:publish`
* `sfdx sfpowerscripts:orchestrator:quickbuild`
* `sfdx sfpowerscripts:orchestrator:release`
* `sfdx sfpowerscripts:orchestrator:validate`
* `sfdx sfpowerscripts:orchestrator:validateAgainstOrg`
* `sfdx sfpowerscripts:orchestrator:validateAgainstPool`&#x20;
* `sfdx sfpowerscripts:package:data:create`
* `sfdx sfpowerscripts:package:data:install`
* `sfdx sfpowerscripts:package:source:create`
* `sfdx sfpowerscripts:package:source:install`
* `sfdx sfpowerscripts:package:unlocked:create`
* `sfdx sfpowerscripts:package:unlocked:install`&#x20;
* `sfdx sfpowerscripts:package:version:increment`&#x20;
* `sfdx sfpowerscripts:pool:delete`
* `sfdx sfpowerscripts:pool:fetch`
* `sfdx sfpowerscripts:pool:list`
* `sfdx sfpowerscripts:pool:metrics:publish`
* `sfdx sfpowerscripts:pool:org:delete`&#x20;
* `sfdx sfpowerscripts:releasedefinition:generate`
* `sfdx sfpowerscripts:dependency:expand`
* `sfdx sfpowerscripts:dependency:shrink`

## `sfdx sfpowerscripts:analyze:pmd [--sourcedir <string>] [--ruleset <string>] [--rulesetpath <string>] [--format <string>] [-o <string>] [--version <string>] [--threshold <integer>] [-b] [--refname <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

This task is used to run a static analysis of the apex classes and triggers using PMD, Please ensure that the SFDX CLI and sfpowerkit plugin are installed before using this task

```
USAGE
  $ sfdx sfpowerscripts:analyze:pmd [--sourcedir <string>] [--ruleset <string>] [--rulesetpath <string>] [--format <string>] [-o
    <string>] [--version <string>] [--threshold <integer>] [-b] [--refname <string>] [--json] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -b, --istobreakbuild
      Enable this option if the build should be reported as failure if 1 or more critical defects are reported during the
      analysis

  -o, --outputpath=<value>
      The file to which the output for static analysis will be written

  --format=<option>
      [default: text] https://pmd.github.io/latest/pmd_userdocs_cli_reference.html#available-report-formats
      <options: text|textcolor|csv|emacs|summaryhtml|html|xml|xslt|yahtml|vbhtml|textpad|sarif>

  --json
      format output as json

  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)
      [default: info] logging level for this command invocation

  --refname=<value>
      Reference name to be prefixed to output variables

  --ruleset=<option>
      [default: sfpowerkit] Inbuilt is the default ruleset that comes with the task, If you choose custom, please provide
      the path to the ruleset
      <options: sfpowerkit|Custom>

  --rulesetpath=<value>
      The path to the ruleset if you are utilizing your own ruleset

  --sourcedir=<value>
      The directory that is to be analyzed using PMD, If omitted default project directory as mentioned in sfdx-project.json
      will be used

  --threshold=<value>
      [default: 1] Violations with a priority less than or equal to the threshold will cause the command to fail

  --version=<value>
      [default: 6.39.0] The version of PMD to be used for static analysis

DESCRIPTION
  This task is used to run a static analysis of the apex classes and triggers using PMD, Please ensure that the SFDX CLI
  and sfpowerkit plugin are installed before using this task

EXAMPLES
  $ sfdx sfpowerscripts:analyze:pmd --sourcedir <dir>

  Output variable:

  sfpowerscripts_pmd_output_path

  <refname>_sfpowerscripts_pmd_output_path
```

_See code:_ [_src/commands/sfpowerscripts/analyze/pmd.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/analyze/pmd.ts)

## `sfdx sfpowerscripts:apextests:trigger [-l <string>] [-n <string>] [-c] [--validatepackagecoverage] [-s] [--specifiedtests <string>] [--apextestsuite <string>] [-p <integer>] [-w <number>] [-u <string>] [--apiversion <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Triggers Apex unit test in an org. Supports test level RunAllTestsInPackage, which optionally allows validation of individual class code coverage

```
USAGE
  $ sfdx sfpowerscripts:apextests:trigger [-l <string>] [-n <string>] [-c] [--validatepackagecoverage] [-s] [--specifiedtests
    <string>] [--apextestsuite <string>] [-p <integer>] [-w <number>] [-u <string>] [--apiversion <string>] [--json]
    [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -c, --validateindividualclasscoverage
      Validate that individual classes have a coverage greater than the minimum required percentage coverage, only
      available when test level is RunAllTestsInPackage

  -l, --testlevel=<option>
      [default: RunLocalTests] The test level of the test that need to be executed when the code is to be deployed
      <options: RunSpecifiedTests|RunApexTestSuite|RunLocalTests|RunAllTestsInOrg|RunAllTestsInPackage>

  -n, --package=<value>
      Name of the package to run tests. Required when test level is RunAllTestsInPackage

  -p, --coveragepercent=<value>
      [default: 75] Minimum required percentage coverage, when validating code coverage

  -s, --synchronous
      Select an option if the tests are to be run synchronously

  -u, --targetusername=<value>
      username or alias for the target org; overrides default target org

  -w, --waittime=<value>
      [default: 60] wait time for command to finish in minutes

  --apextestsuite=<value>
      comma-separated list of Apex test suite names to run

  --apiversion=<value>
      override the api version used for api requests made by this command

  --json
      format output as json

  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)
      [default: info] logging level for this command invocation

  --specifiedtests=<value>
      comma-separated list of Apex test class names or IDs and, if applicable, test methods to run

  --validatepackagecoverage
      Validate that the package coverage is greater than the minimum required percentage coverage, only available when
      test level is RunAllTestsInPackage

DESCRIPTION
  Triggers Apex unit test in an org. Supports test level RunAllTestsInPackage, which optionally allows validation of
  individual class code coverage

EXAMPLES
  $ sfdx sfpowerscripts:apextests:trigger -u scratchorg -l RunLocalTests -s

  $ sfdx sfpowerscripts:apextests:trigger -u scratchorg -l RunAllTestsInPackage -n <mypackage> -c
```

_See code:_ [_src/commands/sfpowerscripts/apextests/trigger.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/apextests/trigger.ts)

## `sfdx sfpowerscripts:apextests:validate -t <string> [-u <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Validates apex test coverage in the org, Please ensure that the SFDX CLI and sfpowerkit plugin are installed before using this task.

```
USAGE
  $ sfdx sfpowerscripts:apextests:validate -t <string> [-u <string>] [--json] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -t, --testcoverage=<value>                                                        (required) The percentage of test
                                                                                    coverage for apex classes, that
                                                                                    should be as per the last test run
                                                                                    status
  -u, --targetorg=<value>                                                           [default: scratchorg] Alias or
                                                                                    username of the target org
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for
                                                                                    this command invocation

DESCRIPTION
  Validates apex test coverage in the org, Please ensure that the SFDX CLI and sfpowerkit plugin are installed before
  using this task.

EXAMPLES
  $ sfdx sfpowerscripts:apextests:validate -u scratchorg -t 80
```

_See code:_ [_src/commands/sfpowerscripts/apextests/validate.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/apextests/validate.ts)

## `sfdx sfpowerscripts:artifacts:fetch -d <directory> [-p <filepath>] [--scope <string> [--npm | -f <filepath>]] [--npmrcpath <filepath> ] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Fetch artifacts from an artifact registry that is either NPM compatible or supports universal artifacts

```
USAGE
  $ sfdx sfpowerscripts:artifacts:fetch -d <directory> [-p <filepath>] [--scope <string> [--npm | -f <filepath>]] [--npmrcpath
    <filepath> ] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -d, --artifactdir=<value>                                                         (required) [default: artifacts]
                                                                                    Directory to save downloaded
                                                                                    artifacts
  -f, --scriptpath=<value>                                                          (Optional: no-NPM) Path to script
                                                                                    that authenticates and downloads
                                                                                    artifacts from the registry
  -p, --releasedefinition=<value>                                                   Path to YAML file containing map of
                                                                                    packages and package versions to
                                                                                    download
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for
                                                                                    this command invocation
  --npm                                                                             Download artifacts from a
                                                                                    pre-authenticated private npm
                                                                                    registry
  --npmrcpath=<value>                                                               Path to .npmrc file used for
                                                                                    authentication to registry. If left
                                                                                    blank, defaults to home directory
  --scope=<value>                                                                   (required for NPM) User or
                                                                                    Organisation scope of the NPM
                                                                                    package

DESCRIPTION
  Fetch artifacts from an artifact registry that is either NPM compatible or supports universal artifacts

EXAMPLES
  $ sfdx sfpowerscripts:artifacts:fetch -p myreleasedefinition.yaml -f myscript.sh

  $ sfdx sfpowerscripts:artifacts:fetch -p myreleasedefinition.yaml --npm --scope myscope --npmrcpath path/to/.npmrc
```

_See code:_ [_src/commands/sfpowerscripts/artifacts/fetch.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/artifacts/fetch.ts)

## `sfdx sfpowerscripts:artifacts:query [-u <string>] [--apiversion <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Fetch details about artifacts installed in a target org

```
USAGE
  $ sfdx sfpowerscripts:artifacts:query [-u <string>] [--apiversion <string>] [--json] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -u, --targetusername=<value>                                                      username or alias for the target
                                                                                    org; overrides default target org
  --apiversion=<value>                                                              override the api version used for
                                                                                    api requests made by this command
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for
                                                                                    this command invocation

DESCRIPTION
  Fetch details about artifacts installed in a target org

EXAMPLES
  $ sfdx sfpowerscripts:artifacts:query -u <target_org>
```

_See code:_ [_src/commands/sfpowerscripts/artifacts/query.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/artifacts/query.ts)

## `sfdx sfpowerscripts:changelog:generate -d <directory> -n <string> -w <string> -b <string> [--limit <integer>] [--workitemurl <string>] [--showallartifacts] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Generates release changelog, providing a summary of artifact versions, work items and commits introduced in a release. Creates a release definition based on artifacts contained in the artifact directory, and compares it to previous release definition in changelog stored on a source repository

```
USAGE
  $ sfdx sfpowerscripts:changelog:generate -d <directory> -n <string> -w <string> -b <string> [--limit <integer>] [--workitemurl
    <string>] [--showallartifacts] [--json] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -b, --branchname=<value>                                                          (required) Repository branch in
                                                                                    which the changelog files are
                                                                                    located
  -d, --artifactdir=<value>                                                         (required) [default: artifacts]
                                                                                    Directory containing sfpowerscripts
                                                                                    artifacts
  -n, --releasename=<value>                                                         (required) Name of the release for
                                                                                    which to generate changelog
  -w, --workitemfilter=<value>                                                      (required) Regular expression used
                                                                                    to search for work items (user
                                                                                    stories) introduced in release
  --json                                                                            format output as json
  --limit=<value>                                                                   limit the number of releases to
                                                                                    display in changelog markdown
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for
                                                                                    this command invocation
  --showallartifacts                                                                Show all artifacts in changelog
                                                                                    markdown, including those that have
                                                                                    not changed in the release
  --workitemurl=<value>                                                             Generic URL for work items. Each
                                                                                    work item ID will be appended to the
                                                                                    URL, providing quick access to work
                                                                                    items

DESCRIPTION
  Generates release changelog, providing a summary of artifact versions, work items and commits introduced in a release.
  Creates a release definition based on artifacts contained in the artifact directory, and compares it to previous
  release definition in changelog stored on a source repository

EXAMPLES
  $ sfdx sfpowerscripts:changelog:generate -n <releaseName> -d path/to/artifact/directory -w <regexp> -r <repoURL> -b <branchName>
```

_See code:_ [_src/commands/sfpowerscripts/changelog/generate.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/changelog/generate.ts)

## `sfdx sfpowerscripts:orchestrator:build --branch <string> [--diffcheck] [-r <string>] [-f <filepath>] [--artifactdir <directory>] [--waittime <number>] [--buildnumber <number>] [--executorcount <number>] [--tag <string>] [-v <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Build all packages (unlocked/source/data) in a repo in parallel, respecting the dependency of each packages and generate artifacts to a provided directory

```
USAGE
  $ sfdx sfpowerscripts:orchestrator:build --branch <string> [--diffcheck] [-r <string>] [-f <filepath>] [--artifactdir <directory>]
    [--waittime <number>] [--buildnumber <number>] [--executorcount <number>] [--tag <string>] [-v <string>] [--json]
    [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -f, --configfilepath=<value>                                                      [default:
                                                                                    config/project-scratch-def.json]
                                                                                    Path in the current project
                                                                                    directory containing  config file
                                                                                    for the packaging org
  -r, --repourl=<value>                                                             Custom source repository URL to use
                                                                                    in artifact metadata, overrides
                                                                                    origin URL defined in git config
  -v, --devhubalias=<value>                                                         [default: HubOrg] Provide the alias
                                                                                    of the devhub previously
                                                                                    authenticated, default value is
                                                                                    HubOrg if using the Authenticate
                                                                                    Devhub task
  --artifactdir=<value>                                                             [default: artifacts] The directory
                                                                                    where the generated artifact is to
                                                                                    be written
  --branch=<value>                                                                  (required) The git branch that this
                                                                                    build is triggered on, Useful for
                                                                                    metrics and general identification
                                                                                    purposes
  --buildnumber=<value>                                                             [default: 1] The build number to be
                                                                                    used for source packages, Unlocked
                                                                                    Packages will be assigned the
                                                                                    buildnumber from Salesforce directly
                                                                                    if using .NEXT
  --diffcheck                                                                       Only build the packages which have
                                                                                    changed by analyzing previous tags
  --executorcount=<value>                                                           [default: 5] Number of parallel
                                                                                    package task schedulers
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for
                                                                                    this command invocation
  --tag=<value>                                                                     Tag the build with a label, useful
                                                                                    to identify in metrics
  --waittime=<value>                                                                [default: 120] Wait time for command
                                                                                    to finish in minutes

DESCRIPTION
  Build all packages (unlocked/source/data) in a repo in parallel, respecting the dependency of each packages and
  generate artifacts to a provided directory
```

_See code:_ [_src/commands/sfpowerscripts/orchestrator/build.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/orchestrator/build.ts)

## `sfdx sfpowerscripts:orchestrator:deploy -u <string> [--artifactdir <directory>] [--waittime <number>] [-g <array>] [-t <string>] [-b <string> --skipifalreadyinstalled] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Deploy packages from the provided artifact directory, to a given org, using the order and configurable flags provided in sfdx-project.json

```
USAGE
  $ sfdx sfpowerscripts:orchestrator:deploy -u <string> [--artifactdir <directory>] [--waittime <number>] [-g <array>] [-t <string>] [-b
    <string> --skipifalreadyinstalled] [--json] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -b, --baselineorg=<value>                                                         The org against which the package
                                                                                    skip should be baselined
  -g, --logsgroupsymbol=<value>                                                     Symbol used by CICD platform to
                                                                                    group/collapse logs in the console.
                                                                                    Provide an opening group, and an
                                                                                    optional closing group symbol.
  -t, --tag=<value>                                                                 Tag the deploy with a label, useful
                                                                                    for identification in metrics
  -u, --targetorg=<value>                                                           (required) [default: scratchorg]
                                                                                    Alias/User Name of the target
                                                                                    environment
  --artifactdir=<value>                                                             [default: artifacts] The directory
                                                                                    containing artifacts to be deployed
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for
                                                                                    this command invocation
  --skipifalreadyinstalled                                                          Skip the package installation if the
                                                                                    package is already installed in the
                                                                                    org
  --waittime=<value>                                                                [default: 120] Wait time for command
                                                                                    to finish in minutes

DESCRIPTION
  Deploy packages from the provided aritfact directory, to a given org, using the order and configurable flags provided
  in sfdx-project.json

EXAMPLES
  $ sfdx sfpowerscripts:orchestrator:deploy -u <username>
```

_See code:_ [_src/commands/sfpowerscripts/orchestrator/deploy.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/orchestrator/deploy.ts)

## `sfdx sfpowerscripts:orchestrator:prepare [-f <filepath>] [--npmrcpath <filepath>] [--keys <string>] [-v <string>] [--apiversion <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Prepare a pool of scratchorgs with all the packages upfront, so that any incoming change can be validated in an optimized manner

```
USAGE
  $ sfdx sfpowerscripts:orchestrator:prepare [-f <filepath>] [--npmrcpath <filepath>] [--keys <string>] [-v <string>] [--apiversion
    <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -f, --poolconfig=<value>
      [default: config/poolconfig.json] The path to the configuration file for creating a pool of scratch orgs

  -v, --targetdevhubusername=<value>
      username or alias for the dev hub org; overrides default dev hub org

  --apiversion=<value>
      override the api version used for api requests made by this command

  --json
      format output as json

  --keys=<value>
      Keys to be used while installing any managed package dependencies. Required format is a string of key-value pairs
      separated by spaces e.g. packageA:pw123 packageB:pw123 packageC:pw123

  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)
      [default: info] logging level for this command invocation

  --npmrcpath=<value>
      Path to .npmrc file used for authentication to a npm registry when using npm based artifacts. If left blank,
      defaults to home directory

DESCRIPTION
  Prepare a pool of scratchorgs with all the packages upfront, so that any incoming change can be validated in an
  optimized manner

EXAMPLES
  $ sfdx sfpowerscripts:orchestrator:prepare -f config/mypoolconfig.json  -v <devhub>
```

_See code:_ [_src/commands/sfpowerscripts/orchestrator/prepare.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/orchestrator/prepare.ts)

## `sfdx sfpowerscripts:orchestrator:promote -d <directory> [-v <string>] [--apiversion <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Promotes validated unlocked packages with code coverage greater than 75%

```
USAGE
  $ sfdx sfpowerscripts:orchestrator:promote -d <directory> [-v <string>] [--apiversion <string>] [--json] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -d, --artifactdir=<value>                                                         (required) [default: artifacts] The
                                                                                    directory where artifacts are
                                                                                    located
  -v, --targetdevhubusername=<value>                                                username or alias for the dev hub
                                                                                    org; overrides default dev hub org
  --apiversion=<value>                                                              override the api version used for
                                                                                    api requests made by this command
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for
                                                                                    this command invocation

DESCRIPTION
  Promotes validated unlocked packages with code coverage greater than 75%

EXAMPLES
  $ sfdx sfpowerscripts:orchestrator:promote -d path/to/artifacts -v <org>
```

_See code:_ [_src/commands/sfpowerscripts/orchestrator/promote.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/orchestrator/promote.ts)

## `sfdx sfpowerscripts:orchestrator:publish -d <directory> [-p -v <string>] [-t <string>] [--gittag] [--pushgittag] [--scope <string> [--npm | -f <filepath>]] [--npmtag <string> ] [--npmrcpath <filepath> ] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Publish packages to an artifact registry, using a user-provided script that is responsible for authenticating & uploading to the registry.

```
USAGE
  $ sfdx sfpowerscripts:orchestrator:publish -d <directory> [-p -v <string>] [-t <string>] [--gittag] [--pushgittag] [--scope <string>
    [--npm | -f <filepath>]] [--npmtag <string> ] [--npmrcpath <filepath> ] [--json] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -d, --artifactdir=<value>                                                         (required) [default: artifacts] The
                                                                                    directory containing artifacts to be
                                                                                    published
  -f, --scriptpath=<value>                                                          Path to script that authenticates
                                                                                    and uploaded artifacts to the
                                                                                    registry
  -p, --publishpromotedonly                                                         Only publish unlocked packages that
                                                                                    have been promoted
  -t, --tag=<value>                                                                 Tag the publish with a label, useful
                                                                                    for identification in metrics
  -v, --devhubalias=<value>                                                         Provide the alias of the devhub
                                                                                    previously authenticated
  --gittag                                                                          Tag the current commit ID with an
                                                                                    annotated tag containing the package
                                                                                    name and version - does not push tag
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for
                                                                                    this command invocation
  --npm                                                                             Upload artifacts to a
                                                                                    pre-authenticated private npm
                                                                                    registry
  --npmrcpath=<value>                                                               Path to .npmrc file used for
                                                                                    authentication to registry. If left
                                                                                    blank, defaults to home directory
  --npmtag=<value>                                                                  Add an optional distribution tag to
                                                                                    NPM packages. If not provided, the
                                                                                    'latest' tag is set to the published
                                                                                    version.
  --pushgittag                                                                      Pushes the git tags created by this
                                                                                    command to the repo, ensure you have
                                                                                    access to the repo
  --scope=<value>                                                                   (required for NPM) User or
                                                                                    Organisation scope of the NPM
                                                                                    package

DESCRIPTION
  Publish packages to an artifact registry, using a user-provided script that is responsible for authenticating &
  uploading to the registry.

EXAMPLES
  $ sfdx sfpowerscripts:orchestrator:publish -f path/to/script

  $ sfdx sfpowerscripts:orchestrator:publish --npm

  $ sfdx sfpowerscripts:orchestrator:publish -f path/to/script -p -v HubOrg

  $ sfdx sfpowerscripts:orchestrator:publish -f path/to/script --gittag --pushgittag
```

_See code:_ [_src/commands/sfpowerscripts/orchestrator/publish.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/orchestrator/publish.ts)

## `sfdx sfpowerscripts:orchestrator:quickbuild --branch <string> [--diffcheck] [-r <string>] [-f <filepath>] [--artifactdir <directory>] [--waittime <number>] [--buildnumber <number>] [--executorcount <number>] [--tag <string>] [-v <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Build packages (unlocked/source/data) in a repo in parallel, without validating depenencies or coverage in the case of unlocked packages

```
USAGE
  $ sfdx sfpowerscripts:orchestrator:quickbuild --branch <string> [--diffcheck] [-r <string>] [-f <filepath>] [--artifactdir <directory>]
    [--waittime <number>] [--buildnumber <number>] [--executorcount <number>] [--tag <string>] [-v <string>] [--json]
    [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -f, --configfilepath=<value>                                                      [default:
                                                                                    config/project-scratch-def.json]
                                                                                    Path in the current project
                                                                                    directory containing  config file
                                                                                    for the packaging org
  -r, --repourl=<value>                                                             Custom source repository URL to use
                                                                                    in artifact metadata, overrides
                                                                                    origin URL defined in git config
  -v, --devhubalias=<value>                                                         [default: HubOrg] Provide the alias
                                                                                    of the devhub previously
                                                                                    authenticated, default value is
                                                                                    HubOrg if using the Authenticate
                                                                                    Devhub task
  --artifactdir=<value>                                                             [default: artifacts] The directory
                                                                                    where the generated artifact is to
                                                                                    be written
  --branch=<value>                                                                  (required) The git branch that this
                                                                                    build is triggered on, Useful for
                                                                                    metrics and general identification
                                                                                    purposes
  --buildnumber=<value>                                                             [default: 1] The build number to be
                                                                                    used for source packages, Unlocked
                                                                                    Packages will be assigned the
                                                                                    buildnumber from Saleforce directly
                                                                                    if using .NEXT
  --diffcheck                                                                       Only build the packages which have
                                                                                    changed by analyzing previous tags
  --executorcount=<value>                                                           [default: 5] Number of parallel
                                                                                    package task schedulors
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for
                                                                                    this command invocation
  --tag=<value>                                                                     Tag the build with a label, useful
                                                                                    to identify in metrics
  --waittime=<value>                                                                [default: 120] Wait time for command
                                                                                    to finish in minutes

DESCRIPTION
  Build packages (unlocked/source/data) in a repo in parallel, without validating depenencies or coverage in the case of
  unlocked packages
```

_See code:_ [_src/commands/sfpowerscripts/orchestrator/quickbuild.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/orchestrator/quickbuild.ts)

## `sfdx sfpowerscripts:orchestrator:release -u <string> [-p <filepath>] [--scope <string> [--npm | -f <filepath>]] [--npmrcpath <filepath> ] [-g <array>] [-t <string>] [--waittime <number>] [--keys <string>] [-b <string> --generatechangelog] [-v <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Initiate a release to an org, according to the configuration defined in a release-definition YAML file

```
USAGE
  $ sfdx sfpowerscripts:orchestrator:release -u <string> [-p <filepath>] [--scope <string> [--npm | -f <filepath>]] [--npmrcpath
    <filepath> ] [-g <array>] [-t <string>] [--waittime <number>] [--keys <string>] [-b <string> --generatechangelog]
    [-v <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -b, --branchname=<value>
      Repository branch in which the changelog files are located

  -f, --scriptpath=<value>
      (Optional: no-NPM) Path to script that authenticates and downloads artifacts from the registry

  -g, --logsgroupsymbol=<value>
      Symbol used by CICD platform to group/collapse logs in the console. Provide an opening group, and an optional
      closing group symbol.

  -p, --releasedefinition=<value>
      Path to YAML file containing map of packages and package versions to download

  -t, --tag=<value>
      Tag the release with a label, useful for identification in metrics

  -u, --targetorg=<value>
      (required) [default: scratchorg] Alias/User Name of the target environment

  -v, --devhubalias=<value>
      Provide the alias of the devhub previously authenticated, default value is HubOrg

  --generatechangelog
      Create a release changelog

  --json
      format output as json

  --keys=<value>
      Keys to be used while installing any managed package dependencies. Required format is a string of key-value pairs
      separated by spaces e.g. packageA:pw123 packageB:pw123 packageC:pw123

  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)
      [default: info] logging level for this command invocation

  --npm
      Download artifacts from a pre-authenticated private npm registry

  --npmrcpath=<value>
      Path to .npmrc file used for authentication to registry. If left blank, defaults to home directory

  --scope=<value>
      (required for NPM) User or Organisation scope of the NPM package

  --waittime=<value>
      [default: 120] Wait time for package installation

DESCRIPTION
  Initiate a release to an org, according to the configuration defined in a release-definition YAML file

EXAMPLES
  $ sfdx sfpowerscripts:orchestrator:release -p path/to/releasedefinition.yml -u myorg --npm --scope myscope --generatechangelog
```

_See code:_ [_src/commands/sfpowerscripts/orchestrator/release.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/orchestrator/release.ts)

## sfdx sfpowerscripts:orchestrator:validate

Validate the incoming change against an earlier prepared scratchorg

```
USAGE
  $ sfdx sfpowerscripts:orchestrator:validate -p <array> --mode individual|fastfeedback|thorough|ff-release-config|thorough-release-config [--releaseconfig <string>] [--coveragepercent <integer>] [-x]
    [--keys <string>] [--enableimpactanalysis --basebranch <string>] [--enabledependencyvalidation ] [--tag <string>] [--disablediffcheck] [--disableartifactupdate] [-g <array>] [-v
    <string>] [--apiversion <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -g, --logsgroupsymbol=<value>                                                        Symbol used by CICD platform to group/collapse logs in the console. Provide an opening group, and an
                                                                                       optional closing group symbol.
  -p, --pools=<value>                                                                  (required) Fetch scratch-org validation environment from one of listed pools, sequentially
  -v, --targetdevhubusername=<value>                                                   username or alias for the dev hub org; overrides default dev hub org
  -x, --deletescratchorg                                                               Delete scratch-org validation environment, after the command has finished running
  --apiversion=<value>                                                                 override the api version used for api requests made by this command
  --basebranch=<value>                                                                 The pull request base branch
  --coveragepercent=<value>                                                            [default: 75] Minimum required percentage coverage for validating code coverage of packages with Apex
                                                                                       classes
  --disableartifactupdate                                                              Do not update information about deployed artifacts to the org
  --disablediffcheck                                                                   Disables diff check while validating, this will validate all the packages in the repository
  --enabledependencyvalidation                                                         Validate dependencies between packages for changed components
  --enableimpactanalysis                                                               Visualize components impacted by changes in pull request
  --json                                                                               format output as json
  --keys=<value>                                                                       Keys to be used while installing any managed package dependencies. Required format is a string of
                                                                                       key-value pairs separated by spaces e.g. packageA:pw123 packageB:pw123 packageC:pw123
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)     [default: info] logging level for this command invocation
  --mode=(individual|fastfeedback|thorough|ff-release-config|thorough-release-config)  (required) [default: thorough] validation mode
  --releaseconfig=<value>                                                              (Required if the release modes are ff-relese-config or thorough-release-config), Path to the config
                                                                                       file which determines how the release defintion should be generated
  --tag=<value>                                                                        Tag the build with a label, useful to identify in metrics

DESCRIPTION
  Validate the incoming change against an earlier prepared scratchorg

ALIASES
  $ sfdx sfpowerscripts:orchestrator:validateAgainstPool

EXAMPLES
  $ sfdx sfpowerscripts:orchestrator:validate -p "POOL_TAG_1,POOL_TAG_2" --mode=fastfeedback -v <devHubUsername>
```

_See code:_ [_src/commands/sfpowerscripts/orchestrator/validate.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/orchestrator/validate.ts)

## `sfdx sfpowerscripts:orchestrator:validateAgainstOrg -u <string> [--coveragepercent <integer>] [--diffcheck] [--disableartifactupdate] [-g <array>] [--basebranch <string>] [--fastfeedback] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Validate the incoming change against target org

```
USAGE
  $ sfdx sfpowerscripts:orchestrator:validateAgainstOrg -u <string> [--coveragepercent <integer>] [--diffcheck] [--disableartifactupdate] [-g
    <array>] [--basebranch <string>] [--fastfeedback] [--json] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -g, --logsgroupsymbol=<value>                                                     Symbol used by CICD platform to
                                                                                    group/collapse logs in the console.
                                                                                    Provide an opening group, and an
                                                                                    optional closing group symbol.
  -u, --targetorg=<value>                                                           (required) Alias/User Name of the
                                                                                    target environment
  --basebranch=<value>                                                              The pull request base branch
  --coveragepercent=<value>                                                         [default: 75] Minimum required
                                                                                    percentage coverage for validating
                                                                                    code coverage of packages with Apex
                                                                                    classes
  --diffcheck                                                                       Only build the packages which have
                                                                                    changed by analyzing previous tags
  --disableartifactupdate                                                           Do not update information about
                                                                                    deployed artifacts to the org
  --fastfeedback                                                                    Enable validation in fast feedback
                                                                                    mode, In fast feedback mode,
                                                                                    validation will only do selective
                                                                                    deployment of changed components and
                                                                                    selective tests
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for
                                                                                    this command invocation

DESCRIPTION
  Validate the incoming change against target org

EXAMPLES
  $ sfdx sfpowerscripts:orchestrator:validateAgainstOrg -u <targetorg>
```

_See code:_ [_src/commands/sfpowerscripts/orchestrator/validateAgainstOrg.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/orchestrator/validateAgainstOrg.ts)

## `sfdx sfpowerscripts:orchestrator:validateAgainstPool -p <array> [--shapefile <string>] [--coveragepercent <integer>] [-g <array>] [-x] [--keys <string>] [-c <string>] [--enableimpactanalysis --basebranch <string>] [--enabledependencyvalidation ] [--tag <string>] [--disablediffcheck] [--disableartifactupdate] [--fastfeedback] [-v <string>] [--apiversion <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Validate the incoming change against an earlier prepared scratchorg

```
USAGE
  $ sfdx sfpowerscripts:orchestrator:validateAgainstPool -p <array> [--shapefile <string>] [--coveragepercent <integer>] [-g <array>] [-x] [--keys
    <string>] [-c <string>] [--enableimpactanalysis --basebranch <string>] [--enabledependencyvalidation ] [--tag
    <string>] [--disablediffcheck] [--disableartifactupdate] [--fastfeedback] [-v <string>] [--apiversion <string>]
    [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -c, --visualizechangesagainst=<value>
      Branch to conduct change analysis against. Enables visualization of changes and the components affected

  -g, --logsgroupsymbol=<value>
      Symbol used by CICD platform to group/collapse logs in the console. Provide an opening group, and an optional
      closing group symbol.

  -p, --pools=<value>
      (required) Fetch scratch-org validation environment from one of listed pools, sequentially

  -v, --targetdevhubusername=<value>
      username or alias for the dev hub org; overrides default dev hub org

  -x, --deletescratchorg
      Delete scratch-org validation environment, after the command has finished running

  --apiversion=<value>
      override the api version used for api requests made by this command

  --basebranch=<value>
      The pull request base branch

  --coveragepercent=<value>
      [default: 75] Minimum required percentage coverage for validating code coverage of packages with Apex classes

  --disableartifactupdate
      Do not update information about deployed artifacts to the org

  --disablediffcheck
      Disables diff check while validating, this will validate all the packages in the repository

  --enabledependencyvalidation
      Validate dependencies between packages for changed components

  --enableimpactanalysis
      Visualize components impacted by changes in pull request

  --fastfeedback
      Enable validation in fast feedback mode, In fast feedback mode, validation will only do selective deployment of and
      selective tests

  --json
      format output as json

  --keys=<value>
      Keys to be used while installing any managed package dependencies. Required format is a string of key-value pairs
      separated by spaces e.g. packageA:pw123 packageB:pw123 packageC:pw123

  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)
      [default: info] logging level for this command invocation

  --shapefile=<value>
      Path to .zip file of scratch org shape / metadata to deploy

  --tag=<value>
      Tag the build with a label, useful to identify in metrics

DESCRIPTION
  Validate the incoming change against an earlier prepared scratchorg

ALIASES
  $ sfdx sfpowerscripts:orchestrator:validateAgainstPool

EXAMPLES
  $ sfdx sfpowerscripts:orchestrator:validate -p "POOL_TAG_1,POOL_TAG_2" -v <devHubUsername>
```

## `sfdx sfpowerscripts:package:data:create -n <string> -v <string> [--artifactdir <directory>] [--diffcheck] [--branch <string>] [--gittag] [-r <string>] [--refname <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Creates a versioned artifact from a source directory containing SFDMU-based data (in csv format and export json). The artifact can be consumed by release pipelines, to deploy the data to orgs

```
USAGE
  $ sfdx sfpowerscripts:package:data:create -n <string> -v <string> [--artifactdir <directory>] [--diffcheck] [--branch <string>]
    [--gittag] [-r <string>] [--refname <string>] [--json] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -n, --package=<value>
      (required) The name of the package

  -r, --repourl=<value>
      Custom source repository URL to use in artifact metadata, overrides origin URL defined in git config

  -v, --versionnumber=<value>
      (required) The format is major.minor.patch.buildnumber . This will override the build number mentioned in the
      sfdx-project.json, Try considering the use of Increment Version Number task before this task

  --artifactdir=<value>
      [default: artifacts] The directory where the artifact is to be written

  --branch=<value>
      The git branch that this build is triggered on, Useful for metrics and general identification purposes

  --diffcheck
      Only build when the package has changed

  --gittag
      Tag the current commit ID with an annotated tag containing the package name and version - does not push tag

  --json
      format output as json

  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)
      [default: info] logging level for this command invocation

  --refname=<value>
      Reference name to be prefixed to output variables

DESCRIPTION
  Creates a versioned artifact from a source directory containing SFDMU-based data (in csv format and export json). The
  artifact can be consumed by release pipelines, to deploy the data to orgs

EXAMPLES
  $ sfdx sfpowerscripts:package:data:create -n mypackage -v <version>

  $ sfdx sfpowerscripts:package:data:create -n <mypackage> -v <version> --diffcheck --gittag

  Output variable:

  sfpowerscripts_artifact_directory

  <refname>_sfpowerscripts_artifact_directory

  sfpowerscripts_package_version_number

  <refname>_sfpowerscripts_package_version_number
```

_See code:_ [_src/commands/sfpowerscripts/package/data/create.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/package/data/create.ts)

## `sfdx sfpowerscripts:package:data:install -n <string> -u <string> [--artifactdir <directory>] [-s] [--skipifalreadyinstalled] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Installs a SFDMU-based data package consisting of csvfiles and export.json to a target org

```
USAGE
  $ sfdx sfpowerscripts:package:data:install -n <string> -u <string> [--artifactdir <directory>] [-s] [--skipifalreadyinstalled] [--json]
    [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -n, --package=<value>                                                             (required) Name of the package to be
                                                                                    installed
  -s, --skiponmissingartifact                                                       Skip package installation if the
                                                                                    build artifact is missing. Enable
                                                                                    this if artifacts are only being
                                                                                    created for modified packages
  -u, --targetorg=<value>                                                           (required) Alias/User Name of the
                                                                                    target environment
  --artifactdir=<value>                                                             [default: artifacts] The directory
                                                                                    where the artifact is located
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for
                                                                                    this command invocation
  --skipifalreadyinstalled                                                          Skip the package installation if the
                                                                                    package is already installed in the
                                                                                    org

DESCRIPTION
  Installs a SFDMU-based data package consisting of csvfiles and export.json to a target org

EXAMPLES
  $ sfdx sfpowerscripts:package:data:install -n mypackage -u <org>
```

_See code:_ [_src/commands/sfpowerscripts/package/data/install.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/package/data/install.ts)

## `sfdx sfpowerscripts:package:source:create -n <string> -v <string> [--artifactdir <directory>] [--diffcheck] [--branch <string>] [--gittag] [-r <string>] [--refname <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

This task simulates a packaging experience similar to unlocked packaging - creating an artifact that consists of the metadata (e.g. commit Id), source code & an optional destructive manifest. The artifact can then be consumed by release pipelines, to deploy the package

```
USAGE
  $ sfdx sfpowerscripts:package:source:create -n <string> -v <string> [--artifactdir <directory>] [--diffcheck] [--branch <string>]
    [--gittag] [-r <string>] [--refname <string>] [--json] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -n, --package=<value>
      (required) The name of the package

  -r, --repourl=<value>
      Custom source repository URL to use in artifact metadata, overrides origin URL defined in git config

  -v, --versionnumber=<value>
      (required) The format is major.minor.patch.buildnumber . This will override the build number mentioned in the
      sfdx-project.json, Try considering the use of Increment Version Number task before this task

  --artifactdir=<value>
      [default: artifacts] The directory where the artifact is to be written

  --branch=<value>
      The git branch that this build is triggered on, Useful for metrics and general identification purposes

  --diffcheck
      Only build when the package has changed

  --gittag
      Tag the current commit ID with an annotated tag containing the package name and version - does not push tag

  --json
      format output as json

  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)
      [default: info] logging level for this command invocation

  --refname=<value>
      Reference name to be prefixed to output variables

DESCRIPTION
  This task simulates a packaging experience similar to unlocked packaging - creating an artifact that consists of the
  metadata (e.g. commit Id), source code & an optional destructive manifest. The artifact can then be consumed by
  release pipelines, to deploy the package

EXAMPLES
  $ sfdx sfpowerscripts:package:source:create -n mypackage -v <version>

  $ sfdx sfpowerscripts:package:source:create -n <mypackage> -v <version> --diffcheck --gittag

  Output variable:

  sfpowerscripts_artifact_metadata_directory

  <refname>_sfpowerscripts_artifact_metadata_directory

  sfpowerscripts_artifact_directory

  <refname>_sfpowerscripts_artifact_directory

  sfpowerscripts_package_version_number

  <refname>_sfpowerscripts_package_version_number
```

_See code:_ [_src/commands/sfpowerscripts/package/source/create.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/package/source/create.ts)

## `sfdx sfpowerscripts:package:source:install -n <string> -u <string> [--artifactdir <directory>] [--skipifalreadyinstalled] [-s] [-o] [-t] [--waittime <string>] [--refname <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Installs a sfpowerscripts source package to the target org

```
USAGE
  $ sfdx sfpowerscripts:package:source:install -n <string> -u <string> [--artifactdir <directory>] [--skipifalreadyinstalled] [-s] [-o]
    [-t] [--waittime <string>] [--refname <string>] [--json] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -n, --package=<value>                                                             (required) Name of the package to be
                                                                                    installed
  -o, --optimizedeployment                                                          Optimize deployment by triggering
                                                                                    test classes that are in the
                                                                                    package, rather than using the whole
                                                                                    tests in the org
  -s, --skiponmissingartifact                                                       Skip package installation if the
                                                                                    build artifact is missing. Enable
                                                                                    this if artifacts are only being
                                                                                    created for modified packages
  -t, --skiptesting                                                                 Skips running test when deploying to
                                                                                    a sandbox
  -u, --targetorg=<value>                                                           (required) Alias/User Name of the
                                                                                    target environment
  --artifactdir=<value>                                                             [default: artifacts] The directory
                                                                                    where the artifact is located
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for
                                                                                    this command invocation
  --refname=<value>                                                                 Reference name to be prefixed to
                                                                                    output variables
  --skipifalreadyinstalled                                                          Skip the package installation if the
                                                                                    package is already installed in the
                                                                                    org
  --waittime=<value>                                                                [default: 120] wait time for command
                                                                                    to finish in minutes

DESCRIPTION
  Installs a sfpowerscripts source package to the target org

EXAMPLES
  $ sfdx sfpowerscripts:package:source:install -n mypackage -u <org>
```

_See code:_ [_src/commands/sfpowerscripts/package/source/install.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/package/source/install.ts)

## `sfdx sfpowerscripts:package:unlocked:create -n <string> [-b] [-k <string> | -x] [--diffcheck] [--gittag] [-r <string>] [--versionnumber <string>] [-f <filepath>] [--artifactdir <directory>] [--enablecoverage] [-s] [--branch <string>] [--tag <string>] [--waittime <string>] [--refname <string>] [-v <string>] [--apiversion <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Creates a new package version, and generates an artifact that consists of the metadata (e.g. version Id). The artifact can then be consumed by release pipelines, to install the unlocked package. Utilize this task in a package build for DX Unlocked Package

```
USAGE
  $ sfdx sfpowerscripts:package:unlocked:create -n <string> [-b] [-k <string> | -x] [--diffcheck] [--gittag] [-r <string>] [--versionnumber
    <string>] [-f <filepath>] [--artifactdir <directory>] [--enablecoverage] [-s] [--branch <string>] [--tag <string>]
    [--waittime <string>] [--refname <string>] [-v <string>] [--apiversion <string>] [--json] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -b, --buildartifactenabled
      Create a build artifact, so that this pipeline can be consumed by a release pipeline

  -f, --configfilepath=<value>
      [default: config/project-scratch-def.json] Path in the current project directory containing  config file for the
      packaging org

  -k, --installationkey=<value>
      Installation key for this package

  -n, --package=<value>
      (required) ID (starts with 0Ho) or alias of the package to create a version of

  -r, --repourl=<value>
      Custom source repository URL to use in artifact metadata, overrides origin URL defined in git config

  -s, --isvalidationtobeskipped
      Skips validation of dependencies, package ancestors, and metadata during package version creation. Skipping
      validation reduces the time it takes to create a new package version, but package versions created without
      validation can’t be promoted.

  -v, --targetdevhubusername=<value>
      username or alias for the dev hub org; overrides default dev hub org

  -x, --installationkeybypass
      Bypass the requirement for having an installation key for this version of the package

  --apiversion=<value>
      override the api version used for api requests made by this command

  --artifactdir=<value>
      [default: artifacts] The directory where the artifact is to be written

  --branch=<value>
      The git branch that this build is triggered on, Useful for metrics and general identification purposes

  --diffcheck
      Only build when the package has changed

  --enablecoverage
      Please note this command takes a longer time to compute, activating this on every packaging build might not
      necessary

  --gittag
      Tag the current commit ID with an annotated tag containing the package name and version - does not push tag

  --json
      format output as json

  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)
      [default: info] logging level for this command invocation

  --refname=<value>
      Reference name to be prefixed to output variables

  --tag=<value>
      the package version's tag

  --versionnumber=<value>
      The format is major.minor.patch.buildnumber . This will override the build number mentioned in the
      sfdx-project.json, Try considering the use of Increment Version Number task before this task

  --waittime=<value>
      [default: 120] wait time for command to finish in minutes

DESCRIPTION
  Creates a new package version, and generates an artifact that consists of the metadata (e.g. version Id). The artifact
  can then be consumed by release pipelines, to install the unlocked package. Utilize this task in a package build for
  DX Unlocked Package

EXAMPLES
  $ sfdx sfpowerscripts:package:unlocked:create -n <packagealias> -b -x -v <devhubalias> --refname <name>

  $ sfdx sfpowerscripts:package:unlocked:create -n <packagealias> -b -x -v <devhubalias> --diffcheck --gittag

  Output variable:

  sfpowerscripts_package_version_id

  <refname>_sfpowerscripts_package_version_id

  sfpowerscripts_artifact_metadata_directory

  <refname>_sfpowerscripts_artifact_metadata_directory

  sfpowerscripts_artifact_directory

  <refname>_sfpowerscripts_artifact_directory

  sfpowerscripts_package_version_number

  <refname>_sfpowerscripts_package_version_number
```

_See code:_ [_src/commands/sfpowerscripts/package/unlocked/create.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/package/unlocked/create.ts)

## `sfdx sfpowerscripts:package:unlocked:install [-n <string>] [-u <string>] [-k <string>] [-a] [--artifactdir <directory>] [--securitytype <string>] [-f] [-s ] [--upgradetype <string>] [--waittime <string>] [--publishwaittime <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Installs an unlocked package using sfpowerscripts metadata

```
USAGE
  $ sfdx sfpowerscripts:package:unlocked:install [-n <string>] [-u <string>] [-k <string>] [-a] [--artifactdir <directory>] [--securitytype
    <string>] [-f] [-s ] [--upgradetype <string>] [--waittime <string>] [--publishwaittime <string>] [--json]
    [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -a, --apexcompileonlypackage                                                      Each package installation triggers a
                                                                                    compilation of apex, flag to trigger
                                                                                    compilation of package only
  -f, --skipifalreadyinstalled                                                      Skip the package installation if the
                                                                                    package is already installed in the
                                                                                    org
  -k, --installationkey=<value>                                                     installation key for key-protected
                                                                                    package
  -n, --package=<value>                                                             Name of the package to be installed
  -s, --skiponmissingartifact                                                       Skip package installation if the
                                                                                    build artifact is missing. Enable
                                                                                    this if artifacts are only being
                                                                                    created for modified packages
  -u, --targetorg=<value>                                                           Alias/User Name of the target
                                                                                    environment
  --artifactdir=<value>                                                             [default: artifacts] The directory
                                                                                    where the artifact is located
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for
                                                                                    this command invocation
  --publishwaittime=<value>                                                         [default: 10] number of minutes to
                                                                                    wait for subscriber package version
                                                                                    ID to become available in the target
                                                                                    org
  --securitytype=<option>                                                           [default: AllUsers] Select the
                                                                                    security access for the package
                                                                                    installation
                                                                                    <options: AllUsers|AdminsOnly>
  --upgradetype=<option>                                                            [default: Mixed] the upgrade type
                                                                                    for the package installation
                                                                                    <options:
                                                                                    DeprecateOnly|Mixed|Delete>
  --waittime=<value>                                                                [default: 120] wait time for command
                                                                                    to finish in minutes

DESCRIPTION
  Installs an unlocked package using sfpowerscripts metadata

EXAMPLES
  $ sfdx sfpowerscripts:package:unlocked:install -n packagename -u sandboxalias -i
```

_See code:_ [_src/commands/sfpowerscripts/package/unlocked/install.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/package/unlocked/install.ts)

## `sfdx sfpowerscripts:package:version:increment [--segment <string>] [-a -r <string>] [-n <string>] [-d <string>] [-c] [--refname <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Increment the selected version counter by one and optionally commit changes to sfdx-project.json. This command does not push changes to the source repository

```
USAGE
  $ sfdx sfpowerscripts:package:version:increment [--segment <string>] [-a -r <string>] [-n <string>] [-d <string>] [-c] [--refname <string>]
    [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -a, --appendbuildnumber
      Set the build segment of the version number to the build number rather than incremenenting

  -c, --commitchanges
      Mark this if you want to commit the modified sfdx-project json, Please note this will not push to the repo only
      commits in the local checked out repo, You would need to have a push to the repo at the end of the packaging task if
      everything is successfull

  -d, --projectdir=<value>
      The directory should contain a sfdx-project.json for this command to succeed

  -n, --package=<value>
      The name of the package of which the version need to be incremented,If not specified the default package is utilized

  -r, --runnumber=<value>
      The build number of the CI pipeline, usually available through an environment variable

  --json
      format output as json

  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)
      [default: info] logging level for this command invocation

  --refname=<value>
      Reference name to be prefixed to output variables

  --segment=<option>
      [default: BuildNumber] Select the segment of the version
      <options: Major|Minor|Patch|BuildNumber>

DESCRIPTION
  Increment the selected version counter by one and optionally commit changes to sfdx-project.json. This command does
  not push changes to the source repository

EXAMPLES
  $ sfdx sfpowerscripts:package:version:increment --segment BuildNumber -n packagename -c

  Output variable:

  sfpowerscripts_incremented_project_version

  <refname>_sfpowerscripts_incremented_project_version
```

_See code:_ [_src/commands/sfpowerscripts/package/version/increment.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/package/version/increment.ts)

## `sfdx sfpowerscripts:pool:delete -t <string> [-m] [-i | -a] [-v <string>] [--apiversion <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Deletes the pooled scratch orgs from the Scratch Org Pool

```
USAGE
  $ sfdx sfpowerscripts:pool:delete -t <string> [-m] [-i | -a] [-v <string>] [--apiversion <string>] [--json] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -a, --allscratchorgs                                                              Deletes all used and unused Scratch
                                                                                    orgs from pool by the tag
  -i, --inprogressonly                                                              Deletes all In Progress Scratch orgs
                                                                                    from pool by the tag
  -m, --mypool                                                                      Filter only Scratch orgs created by
                                                                                    current user in the pool
  -t, --tag=<value>                                                                 (required) tag used to identify the
                                                                                    scratch org pool
  -v, --targetdevhubusername=<value>                                                username or alias for the dev hub
                                                                                    org; overrides default dev hub org
  --apiversion=<value>                                                              override the api version used for
                                                                                    api requests made by this command
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for
                                                                                    this command invocation

DESCRIPTION
  Deletes the pooled scratch orgs from the Scratch Org Pool

EXAMPLES
  $ sfdx sfpowerscripts:pool:delete -t core

  $ sfdx sfpowerscripts:pool:delete -t core -v devhub
```

_See code:_ [_src/commands/sfpowerscripts/pool/delete.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/pool/delete.ts)

## `sfdx sfpowerscripts:pool:fetch -t <string> [-a <string>] [-s <string>] [-d] [-v <string>] [--apiversion <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Gets an active/unused scratch org from the scratch org pool

```
USAGE
  $ sfdx sfpowerscripts:pool:fetch -t <string> [-a <string>] [-s <string>] [-d] [-v <string>] [--apiversion <string>] [--json]
    [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -a, --alias=<value>                                                               Fetch and set an alias for the org
  -d, --setdefaultusername                                                          set the authenticated org as the
                                                                                    default username that all commands
                                                                                    run against
  -s, --sendtouser=<value>                                                          Send the credentials of the fetched
                                                                                    scratchorg to another DevHub user,
                                                                                    Useful for situations when pool is
                                                                                    only limited to certain users
  -t, --tag=<value>                                                                 (required) (required) tag used to
                                                                                    identify the scratch org pool
  -v, --targetdevhubusername=<value>                                                username or alias for the dev hub
                                                                                    org; overrides default dev hub org
  --apiversion=<value>                                                              override the api version used for
                                                                                    api requests made by this command
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for
                                                                                    this command invocation

DESCRIPTION
  Gets an active/unused scratch org from the scratch org pool

EXAMPLES
  $ sfdx sfpowerkit:pool:fetch -t core

  $ sfdx sfpowerkit:pool:fetch -t core -v devhub

  $ sfdx sfpowerkit:pool:fetch -t core -v devhub -m

  $ sfdx sfpowerkit:pool:fetch -t core -v devhub -s testuser@test.com
```

_See code:_ [_src/commands/sfpowerscripts/pool/fetch.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/pool/fetch.ts)

## `sfdx sfpowerscripts:pool:list [-t <string>] [-m] [-a] [-v <string>] [--apiversion <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Retrieves a list of active scratch org and details from any pool. If this command is run with -m|--mypool, the command will retrieve the passwords for the pool created by the user who is executing the command.

```
USAGE
  $ sfdx sfpowerscripts:pool:list [-t <string>] [-m] [-a] [-v <string>] [--apiversion <string>] [--json] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -a, --allscratchorgs                                                              Gets all used and unused Scratch
                                                                                    orgs from pool
  -m, --mypool                                                                      Filter the tag for any additions
                                                                                    created  by the executor of the
                                                                                    command
  -t, --tag=<value>                                                                 tag used to identify the scratch org
                                                                                    pool
  -v, --targetdevhubusername=<value>                                                username or alias for the dev hub
                                                                                    org; overrides default dev hub org
  --apiversion=<value>                                                              override the api version used for
                                                                                    api requests made by this command
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for
                                                                                    this command invocation

DESCRIPTION
  Retrieves a list of active scratch org and details from any pool. If this command is run with -m|--mypool, the command
  will retrieve the passwords for the pool created by the user who is executing the command.

EXAMPLES
  $ sfdx sfpowerscripts:pool:list -t core

  $ sfdx sfpowerscripts:pool:list -t core -v devhub

  $ sfdx sfpowerscripts:pool:list -t core -v devhub -m

  $ sfdx sfpowerscripts:pool:list -t core -v devhub -m -a
```

_See code:_ [_src/commands/sfpowerscripts/pool/list.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/pool/list.ts)

## `sfdx sfpowerscripts:pool:metrics:publish [-v <string>] [--apiversion <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Publish metrics about scratch org pools to your observability platform, via StatsD or direct APIs for supported platforms

```
USAGE
  $ sfdx sfpowerscripts:pool:metrics:publish [-v <string>] [--apiversion <string>] [--json] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -v, --targetdevhubusername=<value>                                                username or alias for the dev hub
                                                                                    org; overrides default dev hub org
  --apiversion=<value>                                                              override the api version used for
                                                                                    api requests made by this command
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for
                                                                                    this command invocation

DESCRIPTION
  Publish metrics about scratch org pools to your observability platform, via StatsD or direct APIs for supported
  platforms

EXAMPLES
  $ sfdx sfpowerscripts:pool:metrics:publish -v <myDevHub>
```

_See code:_ [_src/commands/sfpowerscripts/pool/metrics/publish.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/pool/metrics/publish.ts)

## `sfdx sfpowerscripts:pool:org:delete -u <string> [-v <string>] [--apiversion <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Deletes a particular scratch org in the pool, This command is to be used in a pipeline with correct permissions to delete any active scratch org record or to be used by an adminsitrator

```
USAGE
  $ sfdx sfpowerscripts:pool:org:delete -u <string> [-v <string>] [--apiversion <string>] [--json] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -u, --username=<value>                                                            (required) Username of the
                                                                                    scratchOrg to be deleted, not
                                                                                    aliases
  -v, --targetdevhubusername=<value>                                                username or alias for the dev hub
                                                                                    org; overrides default dev hub org
  --apiversion=<value>                                                              override the api version used for
                                                                                    api requests made by this command
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for
                                                                                    this command invocation

DESCRIPTION
  Deletes a particular scratch org in the pool, This command is to be used in a pipeline with correct permissions to
  delete any active scratch org record or to be used by an adminsitrator

EXAMPLES
  $ sfdx sfpowerscripts:pool:org:delete -u test-xasdasd@example.com -v devhub
```

_See code:_ [_src/commands/sfpowerscripts/pool/org/delete.ts_](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/pool/org/delete.ts)

## `sfdx sfpowerscripts:releasedefinition:generate (-n <string> | -n <string>) [-b <string> --push] [--forcepush ] [-u <string>] [--apiversion <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Generates release defintion based on the artifacts installed in a org

```
USAGE
  $ sfdx sfpowerscripts:releasedefinition:generate (-n <string> | -n <string>) [-b <string> --push] [--forcepush ] [-u <string>] [--apiversion
    <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -b, --branchname=<value>                                                          Repository branch in which the
                                                                                    release defintion files are to be
                                                                                    written
  -n, --changelogbranchref=<value>                                                  (required) Branch where
                                                                                    releasechangelog.json exists, use
                                                                                    when name should be auto generated
  -n, --releasename=<value>                                                         (required) Name of the release
                                                                                    definition file, ideally the same
                                                                                    name generated by changelog
  -u, --targetusername=<value>                                                      username or alias for the target
                                                                                    org; overrides default target org
  --apiversion=<value>                                                              override the api version used for
                                                                                    api requests made by this command
  --forcepush                                                                       Force push changes to the repository
                                                                                    branch
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for
                                                                                    this command invocation
  --push                                                                            Push the changelog to a repository
                                                                                    to the provided branch

DESCRIPTION
  Generates release defintion based on the artifacts installed in a org

EXAMPLES
  $ sfdx sfpowerscripts:releasedefinition:generate -n <releaseName>  -b <branchName> -u <org>
```

_See code:_ [_src/commands/sfpowerscripts/releasedefinition/generate._](https://github.com/dxatscale/sfpowerscripts/blob/v15.6.0/src/commands/sfpowerscripts/releasedefinition/generate.ts)

## `sfdx sfpowerscripts:dependency:expand -v <string> [-o ] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Expand dependency in sfdx-project.json

```
USAGE
  $ sfdx sfpowerscripts:dependency:expand -v <string> [-o ]  [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -v, --targetdevhubusername=<value>                                                dev hub alias or username
  -o, --overwrite                                                                   Overwritten exsiting SFDX-project.json file
                                                                                    with expanded file
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for
                                                                                    this command invocation

DESCRIPTION
  Expand package dependencies in sfdx-project.json file

EXAMPLES
  $ sfdx sfpowerscripts:dependency:expand -v HubOrg  -o
```

## `sfdx sfpowerscripts:dependency:shrink -v <string> [-o ] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Shrink dependency in sfdx-project.json

```
USAGE
  $ sfdx sfpowerscripts:dependency:shrink -v <string> [-o ]  [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -v, --targetdevhubusername=<value>                                                dev hub alias or username
  -o, --overwrite                                                                   Overwritten exsiting SFDX-project.json file
                                                                                    with shrank file
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for
                                                                                    this command invocation

DESCRIPTION
  Shrink package dependencies in sfdx-project.json file

EXAMPLES
  $ sfdx sfpowerscripts:dependency:shrink -v HubOrg  -o
```
