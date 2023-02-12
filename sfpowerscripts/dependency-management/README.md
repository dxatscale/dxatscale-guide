# Dependency Management

sfpowerscripts features commands and functionality that helps in dealing with complexity of defining dependency of unlocked packages. These functionalities are designed considering aspects of a dx@scale project, such as the predominant use of mono repositories in the context of a non-ISV scenarios.

##





&#x20;will automatically resolve the missing package dependencies through the transitive relation from its dependent packages. Users can also define external pacakge dependencies that are not presenting in the sfdx-project.json file.

The feature is controlled by the plugin config:

```
"disableTransitiveDependencyResolver": false
```

