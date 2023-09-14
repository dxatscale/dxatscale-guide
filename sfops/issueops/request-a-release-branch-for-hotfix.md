# Request a release branch for hotfix

This issue allows a developer to request a patch to the release branch with code of each packages reset to the artifacts mentioned in the release definition.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

The above issue is used in the scenario for a hotfix workflow, where the artifacts in the main trunk is unable to be promoted to higher environments, if it contains work items  that didn't pass extensive testing or found a critical issue,  at the same time, there is a patch that needs to be applied to the an existing release that is currently in production.  Triggering this issue will create a release branch, from the main branch with each artifact reset to the code base as mentioned in the release definition. A subsequent change can be merged into the release branch and can be used to  create artifacts which can be pushed to 'Release' environments\


{% hint style="info" %}
This operation is used seldomly, and in most context not required. Please note that a hotfix workflow is an antipattern. You should utilize your regular  deployment workflow to deploy the fix on a priority to your 'Release' Environments
{% endhint %}
