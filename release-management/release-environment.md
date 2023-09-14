# Releasing to an Environment

A release is a set of packages (or artifacts) and their dependencies being deployed to an environment. Releases are defined using a YAML file definition and orchestrated by sfpowerscripts. Read more about the release definition and release command using the below link.

{% content-ref url="../sfpowerscripts/release/" %}
[release](../sfpowerscripts/release/)
{% endcontent-ref %}

Assuming you are following the release model described the environment strategy below, there will be artifacts that are generated from the trunk (dev channel) which will be tested in the day-to-day cycle, and once it is satisfactorily tested, the release candidate (defined by the [release definition ](../sfpowerscripts/release/release-defn-generator.md)) can be promoted to the release channel

![](../.gitbook/assets/environment-strategy-revised.png)

A release candidate  is generated automatically by the release definition generator at the end of the publish job. The release definition will typically have the artifacts pointing to the versions of packages at that point in time. These candidates compose of artifacts from the trunk (main) and is quite frequent, often multiple times throughout a day. The release pipelines could be designed to be either on a scheduled interval or could be triggered on demand as required.

To release to the environments in the release channel, the release command is triggered by selecting the release candidate and providing it to the release commands.

## Activities during a Release to non-prod environment

1. Execute Pre Runbook for the particular release
2. Trigger Release from your CI/CD Platform
3. Execute Post Runbook for the particular release
4. Conduct Post verification test of your release in the particular environment

## Activities during a Release to Prod environment

1. Trigger a dry run of the release using release command with `--dryrun` feature, so that it displays the artifacts, work items and commits that form the particular release. Ensure all of the work items are tested and signed off previously in your ALM application,
2. Execute Pre Runbook for the particular release
3. Trigger Release from your CI/CD Platform
4. Execute Post Runbook for the particular release
5. Conduct Post verification test of your release

{% hint style="warning" %}
DX@Scale practitioners follow a concept of deployment budget, that is a deployment as part of the release should not take more than an hour (for minor releases) and more than three retries to an org. If it takes more than three retries the release should be abandoned
{% endhint %}
