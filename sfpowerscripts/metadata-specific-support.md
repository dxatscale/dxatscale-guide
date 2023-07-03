# Metadata Specific Support

sfpowerscripts support handling the following metadata without using any additional plugins. Read on more how to configure these metadata specific behaviours

### &#x20;Profile Support

sfpowerscripts support built in support for handling profiles using the dual pass reconcile functionality. You can read more on this section

{% content-ref url="../development-practices/managing-profiles.md" %}
[managing-profiles.md](../development-practices/managing-profiles.md)
{% endcontent-ref %}

Profile reconciliation against a target org is enabled by 'default' on all source packages.  To disable this functionality, add the keyword as described in the sample below

<pre class="language-json"><code class="lang-json">```json
<strong>{
</strong>    "packageDirectories": [
        {
            "path": "./src-access-mgmt",
            "package": "access-mgmt",
            "versionName": "Version 1.0.6",
            "versionNumber": "1.0.6.NEXT",
            "reconcileProfiles": false // Control Profile Reconcile
        }
    ]
  }
``` 
</code></pre>

### &#x20;Entitlement Version Support

sfpowerscripts supports entitlement version handling, where you could have a package with multiple entitlements. Read more on how sfpowerscripts handle entitlement below

{% embed url="https://medium.com/@gnemiq/salesforce-entitlement-handling-9e69735e3687" %}

Disable entitlement handling by using the plugins section of sfdx-project.json

````json
```json
"plugins": {
        "sfpowerscripts": {
          "disableEntitlementFilter": true //disable entitlement filtering
          }
        }
```
````

### Field History Tracking Support

sfpowerscripts supports a dual mechanism for field history tracking. One can use a  declarative approach to configure field history tracking / feed tracking using a YML file or let sfpowerscripts automatically determine the course of action if an unlocked package contains fields which have field history tracking enabled in its associated metadata.\
\
&#x20;If you are using the YAML mode, a package should have a folder with the title 'postDeploy' and can have the following files

| File Name            | Description                                                                                                                                                                          |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| history-tracking.yml | A YAML file which has a list of object and fields, where field history tracking should be applied (Applies only to fields, Objects should be enabled with history tracking manually) |
| feed-tracking.yml    | A YAML file which has a list of object and fields, where feed tracking should be applied                                                                                             |

Read more on the link below

{% embed url="https://medium.com/@gnemiq/declarative-configuration-for-field-history-tracking-d63525a5e7b2" %}

This feature can be controlled by specifying the value on the package descriptor as shown below&#x20;

````json
```json
{
    "packageDirectories": [
        {
            "path": "./src-env-specific-alias-pre",
            "package": "src-env-specific-alias-pre",
            "versionNumber": "1.0.0.0",
            "aliasfy": true,
            "ignoreOnStage": [
                "prepare",
                "validate",
                "quickbuild",
                "build"
            ]
        },
        {
            "path": "./src/frameworks/feature-mgmt",
            "package": "feature-mgmt3",
            "versionName": "Version 1.0.6",
            "versionNumber": "1.0.6.NEXT",
            "enableFHT": false // Control FHT deployment on a package
            "preDeploymentScript": "scripts/suspendDeferSharingCalc.sh",
            "postDeploymentScript": "scripts/unSuspendDeferSharingCalc.sh"
        }
    ]
  }
```
```n
````

### Picklist Support

sfpowerscripts supports picklist deployments during unlocked package upgrades, which has been a known issue of Salesforce

{% embed url="https://issues.salesforce.com/issue/a028c00000qPzYUAA0/picklist-values-not-getting-deployed-during-unlocked-package-upgrades" %}

During the build stage, sfpowerscripts checks if picklist exists in an unlocked package. As a pre-deployment step, it retrieves the picklist from the target org, compares it with the local changes and updates the org if any value changes are detected.&#x20;

For more details, please check the below article

{% embed url="https://medium.com/@gnemiq/deploy-picklists-from-unlocked-packages-102c1366664f" %}
