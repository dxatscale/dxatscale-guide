# Packaging

### How to change type of a package from Unlocked to Org Dependent Unlocked package?

Apply the following steps

* Create a new version of unlocked package with just one entity&#x20;
* Install the new version of unlocked package with ‘deprecation’ mode to all the orgs&#x20;

```
// sfdx force:package:install --package 04t... -t DeprecateOnly
```

* Create a new package (new name) with type as Org Dependent Unlocked Package

```
//  sfdx force:package:create -n YourPackageName -d "Your Package Descripton" -t Unlocked -r directory --orgdepependentnt
```

* &#x20;Create a new version of the Org Dependent unlocked package
* &#x20;Propagate the new version of Org Dependent unlocked package across the whole org(s)
* Remove the lock on the one entity on the unlocked package using the UI&#x20;
* Delete the version of unlocked package installed in all orgs
* &#x20;Move the single entity back to Org Dependent unlocked
* &#x20;Reinstall the version of packages across whole orgs
* &#x20;Delete all the version of unlocked package from DevHub
* &#x20;Delete the package from DevHub
