# sfpowerscripts orchestrator pool breaking changes

This week we are introducing breaking changes into our sfpowerscripts orchestrator pool features, as teased here:

{% page-ref page="streamlined-scratch-orgs-are-here.md" %}

These breaking changes will enable

* developer pools
* running scripts and assigning permsets with orchestrator support

As we said last time, the way to enable this is by changing the way we authenticate to our DevHub \(prod environment\). Going forward the authentication method used by orchestrator commands will be through the platform Auth URL, this will be critical in order to use the prepare command.

**How do I get my platform Auth URL?**

Salesforce already has instructions for retrieving and storing the sfdxurl, so we won't repeat them here.

You will then store your sfdx url as a secret value in your chosen CI/CD platform and use this to authenticate in your yaml files using

```text
sfdx auth:sfdxurl:store -f authfile -a devhub
```

**Config Files**

We have also introduced pool config files for orchestrator instead of using command line arguments. You will now specify where the config files are stored by using -f in the CLI.

Examples config file:

**Config file**

```text
{
	    "$schema": "https://raw.githubusercontent.com/Accenture/sfpowerscripts/develop/packages/sfpowerscripts-cli/resources/schemas/pooldefinition.schema.json",
	    "tag": "dev",
	    "maxAllocation": 5,
	    "expiry": 10,
	    "batchSize": 5,
	    "configFilePath": "config/project-scratch-def.json",
	    "relaxAllIPRanges": true,
	    "enableSourceTracking": true,
	    "retryOnFailure": true,
	    "succeedOnDeploymentErrors": true,
	    "installAll": true,
	    "fetchArtifacts": {
	        "npm": {
	          "scope": "@org-name",
	          "npmtag": "main"
	        }
	      }
	   
	}

```

As you can see all of the arguments you used to supply through the cli are now included in these config files. This enables easier adjustment and tailoring of settings through the files.

**Not ready to use these features yet?**

No problems! While we highly recommend you update as soon as possible, you can use a previous version of sfpowerscripts in your pipelines. In your current yaml pipelines files, make sure to change the 'container' to the previous version instead of latest.

```text
container: dxatscale/sfpowerscripts:release-july21
```

sfpowerscripts and sfpowerkit full release notes can be found at the links below.

[https://github.com/Accenture/sfpowerscripts/releases](https://github.com/Accenture/sfpowerscripts/releases)

[https://github.com/Accenture/sfpowerkit/releases](https://github.com/Accenture/sfpowerkit/releases)



