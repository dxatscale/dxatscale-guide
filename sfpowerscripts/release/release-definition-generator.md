# Release Definition Generator

Generate a release definition from a provided git reference. The command can also be used to commit and push the generated release definition file into a provided branch. The release definition file supports a YAML based schema (config file) which is required to create the release definition.

```
sfdx sfpowerscripts:releasedefinition:generate -h
Generates release defintion based on the artifacts installed from a commit reference

USAGE
  $ sfdx sfpowerscripts:releasedefinition:generate -c <value> -f <value> -n <value> [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL] [-d
    <value>] [--nopush -b <value>] [--forcepush ]

FLAGS
  -b, --branchname=<value>                                                          Repository branch in which the release defintion files are to be written
  -c, --gitref=<value>                                                              (required) Utilize the tags on the source branch to generate release definiton
  -d, --directory=<value>                                                           Relative path to directory to which the release defintion file should be
                                                                                    generated, if the directory doesnt exist, it will be created
  -f, --configfile=<value>                                                          (required) Path to the config file which determines how the release defintion
                                                                                    should be generated
  -n, --releasename=<value>                                                         (required) Set a releasename on the release definition file created
  --forcepush                                                                       Force push changes to the repository branch
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for this command invocation
  --nopush                                                                          Do not push the changelog to a repository to the provided branch

DESCRIPTION
  Generates release defintion based on the artifacts installed from a commit reference

EXAMPLES
   $ sfdx sfpowerscripts:releasedefinition:generate -n <releaseName>  -b <branchame> -u <org>
```

### Config File

Release definition generator expects a config file defined in YAML as in the below example

```yaml
// Sample to config file

---
​
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

The below table list the options currently that are currently available for configuridefinitionntion

| Parameter                      | Required | Type   | Description                                                                                          |
| ------------------------------ | -------- | ------ | ---------------------------------------------------------------------------------------------------- |
| excludeArtifacts               | No       | Array  | An array of artifacts that need to be excluded while creating the release definition                 |
| includeOnlyArtifacts           | No       | Array  | An array of artifacts that should only be included while creating the release definition             |
| excludePackageDependencies     | No       | Array  | Exclude the mentioned package dependencies from the release definition                               |
| includeOnlyPackageDependencies | No       | Array  | Include only the mentioned package dependencies from the release definition                          |
| releasedefinitionProperties    | No       | Object | Properties of release definition that should be added to the generated release definition. See below |

### Release Definition Properties

| Parameter                                                        | Required | Type    | Description                                                                                                                                                    |
| ---------------------------------------------------------------- | -------- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| releasedefinitionProperties.skipIfAlreadyInstalled               | No       | boolean | Skip installation of artifact if it's already installed in target org                                                                                          |
| releasedefinitionProperties.baselineOrg                          | No       | string  | The org used to decide whether  to to skip installation of an artifact. Defaults to the target org when not provided                                           |
| releasedefinitionProperties.promotePackagesBeforeDeploymentToOrg | No       | string  | Promote packages before they are installed into an org that matches alias of the org                                                                           |
| releasedefinitionProperties.changelog.repoUrl                    | No       | Prop    | The URL of the version control system to push changelog files                                                                                                  |
| releasedefinitionProperties.changelog.workItemFilters            | No       | Prop    | An array of  regular expression used to identify work items in your commit messages                                                                            |
| releasedefinitionProperties.changelog.workitemUrl                | No       | Prop    | The generic URL of work items, to which to append work item codes. Allows easy redirection to user stories by clicking on the work-item link in the changelog. |
| releasedefinitionProperties.changelog.limit                      | No       | Prop    | Limit the number of releases to display in the changelog markdown                                                                                              |
| releasedefinitionProperties.changelog.showAllArtifacts           | No       | Prop    | Whether to show artifacts that haven't changed between releases                                                                                                |

##
