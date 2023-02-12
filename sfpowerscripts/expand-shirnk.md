# Expand

Expand the dependency list of all packages given in a sfdx-project.json (Project manifest) by filling the transitive dependencies

```
sfdx sfpowerscripts dependency expand [-o] [-v <string>] [--apiversion <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -o, --overwrite                                                                   Flag to overwrite existing sfdx-project.json file
  -v, --targetdevhubusername=<value>                                                username or alias for the dev hub org; overrides default dev hub org
  --apiversion=<value>                                                              override the api version used for api requests made by this command
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for this command invocation
```

Expand command does the reverse of shrink command. This command can be used to reverse a minified project-manifest to its original state or could be used to understand all the dependencies of a given unlocked package. This command needs a bito of help using the externalDependencyMap defined below to provide dependencies of packages that are external to the repository



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
An external dependency is a package that is not defined within the current repositories sfdx-project.json. Managed packages and unlocked packages built from other repositories fall into 'external dependency' bucket.  IDs of External packages have to be defined explicitly in the **packageAliases** section.
{% endhint %}

##
