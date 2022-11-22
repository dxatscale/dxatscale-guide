# Unlocked Package

### How to change type of a package from Unlocked to Org Dependent Unlocked Package?

Apply the following steps

* Create a new version of unlocked package with just one entity
* Install the new version of unlocked package with ‘deprecation’ mode to all the orgs

```
// sfdx force:package:install --package 04t... -t DeprecateOnly
```

* Create a new package (new name) with type as Org Dependent Unlocked Package

```
//  sfdx force:package:create -n YourPackageName -d "Your Package Descripton" -t Unlocked -r directory --orgdepependentnt
```

* Create a new version of the Org Dependent unlocked package
* Propagate the new version of Org Dependent unlocked package across the whole org(s)
* Remove the lock on the one entity on the unlocked package using the UI
* Delete the version of unlocked package installed in all orgs
* Move the single entity back to Org Dependent unlocked
* Reinstall the version of packages across whole orgs
* Delete all the version of unlocked package from DevHub
* Delete the package from DevHub

### Can I add an unlocked or managed package as a dependency to source package?

Yes, an unlocked package or managed package can be added as a dependency to source package. If these packages are not part of your repository, sfpowerscripts will automatically install it during prepare/validate. Other than that, source packages are not validated during build stage and assumed to meet all its dependencies during installation to an org.

### Can I add a source package as a dependency to unlocked package?

No, source package is a sfpowerscripts only construct. From a salesforce perspective, it's nothing more than metadata deployment, hence salesforce is unaware of such a package. Unlocked packages only allow any other unlocked (excluding org dependent unlocked) and managed package to be added as a dependency. All the dependency is validated during the build stage any incorrect dependency will result in error
