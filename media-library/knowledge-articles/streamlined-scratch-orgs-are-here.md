---
description: 'Published by Caitlyn Mills on July 15, 2021'
---

# Streamlined Scratch Orgs are here!

**Breaking news! \(**and breaking features**\)**

I've already written about scratch org pooling, right? How can we possible make it better? Let's recap on how pools currently work.

Whether its developer pooling or CI pooling, the basic idea is simple \(albeit complex behind the scenes\). You create a number of scratch orgs, tagged to a pool, install all the dependencies and voila! Your scratch orgs are ready to be accessed without the downtime.

So what have we done to improve this? Let's talk about source tracking

**What is source tracking?**

Your Git repo is \(should be\) your 'source of truth' when it comes to package-based development. Source tracking is a feature that is by default enabled in Scratch Orgs and can be enabled in sandboxes too. Once enabled, it allows:

* change tracking on metadata components
* push and pull changes to the source
* identification and resolution of conflicts between your developer org and your source code

More information on source tracking including best practices can be found here: [https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_source\_tracking.htm](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_source_tracking.htm)

**How does this improve pools?**

In earlier pooling a developer would have fetched a scratch org, pushed source code, run scripts, assigned permission sets and the provision users! \(Sound's exhausting\).

What we have done now is streamline all of these activities, ensuring your scratch org has source tracking enabled with all of the additional orchestrator properties you have configured for your packages. This means, wave **GOODBYE** to the frustrating setup you have to do on a new branch. It's like a Sandbox with your test data and configuration fetched in seconds.

Prepare for developer pooling is now a 'one stop shop' for creating developer scratch orgs which are ready to use straight out of the box  
.

![No alt text provided for this image](https://media-exp1.licdn.com/dms/image/C5612AQG28HePrTDVAw/article-inline_image-shrink_1000_1488/0/1626327551967?e=1632960000&v=beta&t=Ohc-4L1VNqQD_l7Y939GjfIy3X2Gtq3LhV4e7qn9118)

**How have we done this?**

One of the main ways we have been able to do this is by deprecating JWT authentication and instead going forward pools using the ‘prepare’ command will authenticate using the platform Auth URL.

The prepare command is also using the orchestrator inputs from your sfdx-project.json to know which scripts to run and which permission sets to assign. https://sfpowerscripts.dxatscale.io/faq/orchestrator

We have also updated the pool config files, you'll notice some slight difference in this config file to what you are currently using and will need to use the config file instead of the current cli flags you are using. Let's take a sneak peak:

```text
{
"tag": "POOL_1",
"maxallocation": 30,
"expiry": 10,
"batchsize": 10,
"configFilePath": "config/project-scratch-def.json",
"relaxAllIPRanges": true,
"installAll": true,
"enableSourceTracking": true,
"retryOnFailure": true,
"succeedOnDeploymentErrors": true,
"fetchArtifacts": {
  "artifactFetchScript":
       "scripts/AzureArtifacts/pullAzureArtifactsDevFeed.sh"
}
}
```

**What's next?**

Going along with the release \(est. 1 August\) we will have some instructions if you are ready to upgrade. Don't stress if you aren’t quite ready, you should switch to the previous version of the docker image in your orchestrator commands, as this is a breaking feature. https://hub.docker.com/r/dxatscale/sfpowerscripts

_You can read my previous articles about scratch org pooling here:_

{% page-ref page="scratch-org-pooling-for-ci.md" %}

{% page-ref page="scratch-org-pooling-for-development.md" %}



