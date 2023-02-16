# Install

Install all the external dependencies of a repository into a given org.

```
sfdx sfpowerscripts dependency install [-k <string>] [-v <string>] [-u <string>] [--apiversion <string>] [--json] [--loglevel
    trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -k, --installationkeys=<value>                                                    Installation key for key-protected packages (format is packagename:key --> core:key
                                                                                    nCino:key vlocity:key to allow some packages without installation key)
  -u, --targetusername=<value>                                                      username or alias for the target org; overrides default target org
  -v, --targetdevhubusername=<value>                                                username or alias for the dev hub org; overrides default dev hub org
  --apiversion=<value>                                                              override the api version used for api requests made by this command
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for this command invocation
```

This command is a helper which exposes the inbuilt functionality used by sfpowerscripts orchestrator such as 'prepare', 'validate' etc. One could use this functionality to install all the external dependencies of a repository to given org outside of the orchestrator commands, such as updating packages in a sandbox.

{% hint style="info" %}
An external dependency is a package that is not defined within the current repositories sfdx-project.json. Managed packages and unlocked packages built from other repositories fall into 'external dependency' bucket.  IDs of External packages have to be defined explicitly in the **packageAliases** section.
{% endhint %}

The command supports the usage of installationkeys for unlocked/managed packages. The format is \`packagename:key,packagename2:key2' passed in the installationkeys parameter.

The command will automatically skip the installation if the same version is found to be installed in the target org. It will also continue the installation of remaining packages even if a package installation fails if the target org contains a version that is greater than what is being asked to install

