# Tracking Manual Steps

#### 

Salesforce API surface has been steadily increasing over the years, however, there are still gaps around various components, which need to be manually enabled for deployment to succeed.  Typically these manual steps are tracked in excel sheets or as a document in confluence or any other system outside the version control.

### Runbooks Managed in Source Code Repository

In the DX@Scale model, manual steps are managed in version control in the same repository along with any other packages. It also has the same importance of code/configuration that is being version controlled.

The following structure is advised for every DX@Scale implementation

![](../.gitbook/assets/image%20%2825%29.png)

The repository need to contain a folder called runbooks, with the following subfolders

**\(1\) env-refresh :**  This folder contains a single file in markdown format that is all about the manual  steps taken after a sandbox is refreshed. Read more about it here.

**\(2\) release-X** : Each release need to have a dedicated folder with the name of the release. It needs to have two files in markdown format titled runbook_post.md_ and _runbook\_pre.md._ These files will track any steps that need to be done before a release and after a release into an environment.

{% hint style="danger" %}
Any addition to the runbook should be carefully reviewed and ascertained that it is indeed a manual step during the pull request validation process.  If its a recurring step, all effort should be taken to avoid it, including changing the design.
{% endhint %}

### Template for runbooks

{% tabs %}
{% tab title="Runbook Template" %}
### Release 0.3 - Pre Run Once

This document outlines the steps that are required to be run once in each environment we are deploying to.

1. Start the Async Batch Processor \(As the System User\)." - Developer Console -&gt; Debug -&gt; Open Execute Anonymous Window  - Execute the following code

```text
AsyncProcessorBatch.start();
```

| Environment | Completed | By | Date |
| :--- | :--- | :--- | :--- |
| ST01 | X |  |  |
| DEV | X |  |  |
| DM | X |  |  |
| DEV TRAINING | X |  |  |
| STAGING | X |  |  |
| PROD |  |  |  |

* |  |
  | :--- |
{% endtab %}
{% endtabs %}

