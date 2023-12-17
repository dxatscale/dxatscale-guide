# On Push

sfops features prebuilt workflows that is deployed to your projects. These workflows follow roughly the prescribed environment strategy mentioned in DX@Scale docs, at the same time it is slightly different. The below sections details the workflow on how a **Release Candidate** gets created upon every merge and how built packages are deployed to **TEST** environments\


<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

This workflow gets triggered on a merge to the `main` branch (or any other configured branches).

Upon merge, sfops computes the impacted domains (or release configs) and triggers the build-deploy-publish of each domain in the sequence of impacted packages\
\
Within an individual build-deploy-publish cycle, the following happens in sequence

1. Impacted packages are detected and queued for build
2. Upon successful completion of the build, the packages that are created are deployed in parallel to a dynamic list of deployment targets. These deployment targets form your test environments
3. If all the deployment targets succeeded, the packages are published and a release candidate is created for the corresponding domain

{% hint style="info" %}
There could be 0..N deployment targets, and these deployment targets are marked by the filter "type:test, branch:\<current\_branch>", If no deployment targets , the process is skipped and moved to publish. The deployment targets could be dynamic or static
{% endhint %}

One then could determine, after further testing whether the created release candidate can be promoted to production or rejected. As you must have noticed, these tests are more quality gates. Tests such as User Acceptance Testing should be carried out before the work item is merged to the branch. If any bugs are discovered at this stage, these should be fixed in priority or the feature should be toggled off or excluded from release candidate for further promotion
