# Environment Strategy

One of the key tenants of DX@Scale is a simplified environment strategy which is based on these principles

* Any org should be able to be recreated using artifacts as well as the runbooks.
* Any development should be carried out in an individual scratch org provisioned just for the feature/task in hand
* There will be no long-lived continuous integration environments  

![](../.gitbook/assets/image%20%2850%29.png)

The above diagram is high level view of the environment map used by DX@Scale practitioners. The following sequence of activites  happen across environments

*  A work item is always developed in a scratch org. Then once it is unit tested and approved by  product owner or stakeholders \( in case of hotfix\), a PR is raised to the respective branch \(predominantly master/main, occasionally  to a release branch due a bug fix, read more on branching strategy\). 
* The code is validated in an Just in time CI environment \(typically fetched from a pool\) and validated for dependencies, accuracy of metadata and test coverage
* Once the work item is peer reviewd,  and upon a succesfull merge, a set of quick build packages are generated which is then deployed to DEV sandbox for upgrade validation. This environment is also used to test the runbook created for this feature \(if any manual one-off steps are are required\). 
* Succesful packages after above process, are published into an NPM or suitable artifacts repository for further deployment
* The first round of testing happens   

