# Release Config

A release configuration defines how packages should be organized across your project in terms of various activites be it validating, building or release.  All sfpowerscripts orchestrator command supports a release config input, which can be used to filter the commands to operate only on the packages as mentioned in the release configuration.  A release configuration can be used to create workflows such as supporting parallel development and release  of independent domains.=

A release config follows a very similar structure to that of a release definition but with additonal filters available.  By combining release config and [release definition generator](release-defn-generator.md) , one can create a release definition at any given point of a repository.&#x20;

```yaml
// Sample release config file

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

The below table list the options that are currently available for release definition

<table><thead><tr><th>Parameter</th><th>Required</th><th width="134">Type</th><th>Description</th></tr></thead><tbody><tr><td>excludeArtifacts</td><td>No</td><td>Array</td><td>An array of artifacts that need to be excluded while creating the release definition</td></tr><tr><td>includeOnlyArtifacts</td><td>No</td><td>Array</td><td>An array of artifacts that should only be included while creating the release definition</td></tr><tr><td>excludePackageDependencies</td><td>No</td><td>Array</td><td>Exclude the mentioned package dependencies from the release definition</td></tr><tr><td>includeOnlyPackageDependencies</td><td>No</td><td>Array</td><td>Include only the mentioned package dependencies from the release definition</td></tr><tr><td>releasedefinitionProperties</td><td>No</td><td>Object</td><td>Properties of release definition that should be added to the generated release definition. See below</td></tr></tbody></table>

### Release Definition Properties

| Parameter                                                        | Required | Type    | Description                                                                                                                                                    |
| ---------------------------------------------------------------- | -------- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| releasedefinitionProperties.skipIfAlreadyInstalled               | No       | boolean | Skip installation of artifact if it's already installed in target org                                                                                          |
| releasedefinitionProperties.baselineOrg                          | No       | string  | The org used to decide whether to to skip installation of an artifact. Defaults to the target org when not provided                                            |
| releasedefinitionProperties.promotePackagesBeforeDeploymentToOrg | No       | string  | Promote packages before they are installed into an org that matches alias of the org                                                                           |
| releasedefinitionProperties.changelog.repoUrl                    | No       | Prop    | The URL of the version control system to push changelog files                                                                                                  |
| releasedefinitionProperties.changelog.workItemFilters            | No       | Prop    | An array of regular expression used to identify work items in your commit messages                                                                             |
| releasedefinitionProperties.changelog.workitemUrl                | No       | Prop    | The generic URL of work items, to which to append work item codes. Allows easy redirection to user stories by clicking on the work-item link in the changelog. |
| releasedefinitionProperties.changelog.limit                      | No       | Prop    | Limit the number of releases to display in the changelog markdown                                                                                              |
| releasedefinitionProperties.changelog.showAllArtifacts           | No       | Prop    | Whether to show artifacts that haven't changed between releases                                                                                                |

##
