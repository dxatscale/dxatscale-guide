# Shrink

Shrink the dependency list of a given sfdx-project.json (Project manifest) by eliminating transitive dependencies

```
sfdx sfpowerscripts dependency shrink [-o] [-v <string>] [--apiversion <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -o, --overwrite                                                                   Flag to overwrite existing sfdx-project.json file
  -v, --targetdevhubusername=<value>                                                username or alias for the dev hub org; overrides default dev hub org
  --apiversion=<value>                                                              override the api version used for api requests made by this command
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for this command invocation
```



It is very often that the sfdx-project.json file can be exceptionally large as the number of the packages in the project increases throughout its lifecycle.&#x20;

Shrink command helps to build a minimal sfdx-project.json file for easy maintenance, as it will also scan the project manifest to remove transitive dependencies and  also creates empty entry in the external dependency map for those packages that are not listed in the `packageDirectories`

A minimized project config file will be automatically expanded while the package building process.

External dependency can be defined in plugin section:

```
"plugins": {
      "sfpowerscripts": {
          "disableTransitiveDependencyResolver": false,
              "externalDependencyMap": {
                  "tech-framework@2.0.0.38": [
                      {
                          "package": "sfdc-framework",
                          "versionNumber": "2.3.2.3" 
                      }
                  ]
              }
      }
  }
```

{% hint style="info" %}
An external dependency is a package that is not defined within the current repositories sfdx-project.json. Managed packages and unlocked packages built from other repositories fall into 'external dependency' bucket. IDs of External packages have to be defined explicitly in the **packageAliases** section.
{% endhint %}

