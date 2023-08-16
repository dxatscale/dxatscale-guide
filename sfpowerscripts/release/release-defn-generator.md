# Release Defnition Generator

Generate a release definition from a provided git reference. The command can also be used to commit and push the generated release definition file into a provided branch. The release definition file supports a YAML based schema (config file) which is required to create the release definition.

```
sfp releasedefinition:generate -h
Generates release definition based on the artifacts installed from a commit reference

USAGE
  $ sfp releasedefinition:generate -c <value> -f <value> -n <value> [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL] [-d
    <value>] [--nopush -b <value>] [--forcepush ]

FLAGS
  -b, --branchname=<value>                                                          Repository branch in which the release definition files are to be written
  -c, --gitref=<value>                                                              (required) Utilize the tags on the source branch to generate release definition
  -d, --directory=<value>                                                           Relative path to directory to which the release definition file should be
                                                                                    generated, if the directory doesnt exist, it will be created
  -f, --configfile=<value>                                                          (required) Path to the config file which determines how the release definition
                                                                                    should be generated
  -n, --releasename=<value>                                                         (required) Set a releasename on the release definition file created
  --forcepush                                                                       Force push changes to the repository branch
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for this command invocation
  --nopush                                                                          Do not push the changelog to a repository to the provided branch

DESCRIPTION
  Generates release definition based on the artifacts installed from a commit reference

EXAMPLES
  $ sfp releasedefinition:generate -n <releaseName> -b <branchname> -u <org>
```

Release definition generator expects a config file defined in YAML as in the below example. For more information on Release Config, check the link [here](release-config.md)

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



##
