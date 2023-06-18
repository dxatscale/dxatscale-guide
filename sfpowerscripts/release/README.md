# Release

The `orchestrator:release` command brings uniformity to the CI/CD landscape, allowing you to define 'releases' no matter which platform you are on. A release is defined by a YAML file, where you can specify the artifacts to be installed in the org, in addition to other parameters. The release will then be orchestrated based on the configuration of the YAML definition file.

```
sfdx sfpowerscripts:orchestrator:release -h
Release a  collection of artifacts as defined in the release definition file

USAGE
  $ sfdx sfpowerscripts:orchestrator:release -u <string> [-p <array>] [--scope <string> [--npm | -f <filepath>]] [--npmrcpath <filepath> ] [-g <array>] [-t <string>] [--waittime
    <number>] [--keys <string>] [-d <string>] [-b <string> --generatechangelog] [-v <string>] [--json] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -b, --branchname=<value>                                                          Repository branch in which the changelog files are located
  -d, --directory=<value>                                                           Relative path to directory to which the release defintion file should be
                                                                                    generated, if the directory doesnt exist, it will be created
  -f, --scriptpath=<value>                                                          (Optional: no-NPM) Path to script that authenticates and downloads artifacts
                                                                                    from the registry
  -g, --logsgroupsymbol=<value>                                                     Symbol used by CICD platform to group/collapse logs in the console. Provide an
                                                                                    opening group, and an optional closing group symbol.
  -p, --releasedefinition=<value>                                                   Path to release definiton yaml, Multiple paths can be seperated by commas
  -t, --tag=<value>                                                                 Tag the release with a label, useful for identification in metrics
  -u, --targetorg=<value>                                                           (required) [default: scratchorg] Alias/User Name of the target environment
  -v, --devhubalias=<value>                                                         Provide the alias of the devhub previously authenticated, default value is
                                                                                    HubOrg
  --generatechangelog                                                               Create a release changelog
  --json                                                                            format output as json
  --keys=<value>                                                                    Keys to be used while installing any managed package dependencies. Required
                                                                                    format is a string of key-value pairs separated by spaces e.g. packageA:pw123
                                                                                    packageB:pw123 packageC:pw123
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for this command invocation
  --npm                                                                             Download artifacts from a pre-authenticated private npm registry
  --npmrcpath=<value>                                                               Path to .npmrc file used for authentication to registry. If left blank,
                                                                                    defaults to home directory
  --scope=<value>                                                                   (required for NPM) User or Organisation scope of the NPM package
  --waittime=<value>                                                                [default: 120] Wait time for package installation

DESCRIPTION
  Release a collection of artifacts as defined in the release definition file

EXAMPLES
  $ sfdx sfpowerscripts:orchestrator:release -p path/to/releasedefinition.yml -u myorg --npm --scope myscope --generatechangelog
```

## Release Definition

```
# release-definition.yaml

release: "release-1.0"
skipIfAlreadyInstalled: true
baselineOrg: "myorg"
promotePackagesBeforeDeploymentToOrg:"SIT"
artifacts:
  mypackageA: LATEST_GIT_TAG or LATEST_TAG
  mypackageB: LATEST_TAG # Substituted with version from latest git tag at runtime
  mypackageC: 1.2.3-5 # Provide the exact version to download
packageDependencies:
  Marketing Cloud: 04t0H000000xVrw
changelog:
  workItemFilters: 
   - "BRO-[0-9]{3,4}"
  workItemUrl: "https://www.atlassian.com/software/jira"
  limit: 30
  showAllArtifacts: false
```

{% hint style="info" %}
Please note, when using release definition with exact version numbers. The format of the version number would be \<packageName>: X.Y.Z-BuildNumber, where the version number adopts the following semantics\
X -  Major \
Y -  Minor \
Z -  Patch\
BuildNumber - The build number that produced the package\
\
The version exactly follows the semantics used by the artifact registry (such as Github Packages)\


**Example**:\
A package that has the version core\_crm\_v3.0.0.6936, tagged in git should be referenced \
as core\_crm: 3.0.0-6936
{% endhint %}

| Parameter                            | Required | Type    | Description                                                                                                                                                    |
| ------------------------------------ | -------- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| release                              | Yes      | string  | Name of the release                                                                                                                                            |
| skipIfAlreadyInstalled               | No       | boolean | Skip installation of artifact if it's already installed in target org                                                                                          |
| baselineOrg                          | No       | string  | The org used to decide whether or not to skip installation of an artifact. Defaults to the target org when not provided.                                       |
| artifacts                            | Yes      | Object  | Map of artifacts to deploy and their corresponding version                                                                                                     |
| promotePackagesBeforeDeploymentToOrg | No       | string  | Promote packages before they are installed into an org that matches alias of the org                                                                           |
| packageDependencies                  | No       | Object  | Packages dependencies (e.g. managed packages) to install as part of the release. Provide the 04t subscriber package version Id.                                |
| changelog.repoUrl                    | No       | Prop    | The URL of the version control system to push changelog files                                                                                                  |
| changelog.workItemFilters            | No       | Prop    | An array of  regular expression used to identify work items in your commit messages                                                                            |
| changelog.workitemUrl                | No       | Prop    | The generic URL of work items, to which to append work item codes. Allows easy redirection to user stories by clicking on the work-item link in the changelog. |
| changelog.limit                      | No       | Prop    | Limit the number of releases to display in the changelog markdown                                                                                              |
| changelog.showAllArtifacts           | No       | Prop    | Whether to show artifacts that haven't changed between releases                                                                                                |

## Automated generation of release definition

In a high velocity project operating on a trunk and with substantial number of packages, manually generating release definition can be a chore. This can eased by using generating the release definition file automatically after every publish command. Read on more about release definition generation using the link below.

{% content-ref url="release-definition-generator.md" %}
[release-definition-generator.md](release-definition-generator.md)
{% endcontent-ref %}

## Fetching Artifacts for Release

The `orchestrator:release` command provides a simplified method of fetching artifacts from an artifact repository using the release definition file which contains the name of the artifacts that you want to download, and a mapping to the version to download. If fetching from a **NPM registry**, the command will handle everything else for you. However, for universal artifacts there is no uniform method for downloading artifacts from a repository, so you will need to provide a shell script that calls the relevant API.

{% hint style="info" %}
The`LATEST_TAG` keyword is only supported if the current working directory is pointing to the project directory, and if at least one git tag exists for the package.
{% endhint %}

### Fetching universal artifacts

For universal artifacts, there is no uniform method for downloading artifacts from a registry, so you will need to provide a shell script that calls the relevant API. You need to pass the path to script file using the flag `--scriptpath`

There are multiple parameters available in the shell script. Pass these parameters to the API call, and at runtime they will be substituted with the corresponding values:

1. Artifact name
2. Artifact version
3. Directory to download artifacts

**Eg.** **Fetching from Azure Artifacts using the Az CLI on Linux**

```
#!/bin/bash

# $1 - artifact name
# $2 - artifact version
# $3 - artifact directory 

echo "Downloading Artifact $1 Version $2"

az artifacts universal download --feed myfeed --name $1 --version $2 --path $3 \
    --organization "https://dev.azure.com/myorg/" --project myproject --scope project
```

## Changelog

When the `--generatechangelog` flag is passed to the command, a changelog will automatically be generated if the release is successful. The changelog provides traceability for the artifacts, work items and commits that were introduced by each release, as well as an at-a-glance view of all your orgs and which release they are currently on.

{% hint style="info" %}
To generate a changelog, the`changelog.repoUrl`and`changelog.workItemFilter` parameters must be configured in the release definition file.
{% endhint %}

A changelog is generated in markdown format and pushed to the repo, utilizing the`branchname` flag provided to the release command. If the command finds a previous changelog files, it will utilize to generate an incremental changelog
