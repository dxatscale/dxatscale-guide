# Environment Strategy

One of the key tenants of DX@Scale is a simplified environment strategy that is based on these principles

* Any org should be able to be recreated using artifacts and associated run books \(if required\)
* Any development should be carried out in an individual scratch org provisioned just for the feature/task in hand
* There will be no long-lived continuous integration environments

![](../.gitbook/assets/environment-strategy-revised.png)



The below table details each environment and the role of each environment in a typical DX@Scale project. Projects could have variation in the number of environments in the dev channel or release channel, such as multiple integrated environments, but the below environments are absolute essential.

| Environment | Type | License Type | Integrated | Role |
| :--- | :--- | :--- | :--- | :--- |
| DEV | Scratch Org | N/A | No | Development, any work item in a DX@Scale project will be developed in a scratch org. These scratch org's could be provisioned individually or fetched from a [pool](pooling-scratch-orgs.md).  Any bug fixes or hot fixes done against an existing release should be demonstrable in a scratch org.  This is intended to minimize pushing features as bug fixes to production using hot fix pathway. |
| CI | Scratch Org | N/A | No | Validate integration of a work item from a developer against main line using just in time CI Orgs. To speed up the process, the CI orgs could be pre-provisioned using pools. |
| Shared Dev | Sandbox | Developer | No | This sandbox is used in a CI pipeline, where after merge, the created packages are deployed to this long lived sandbox for checking upgradeability.  Can apply pre/post steps to validate deployment process. |
| System Testing | Sandbox | Developer | No | This environment is the first environment where all new packages will be tested. This environment will also have test data. |
| Staging | Sandbox | Developer Pro / Partial | Yes | Staging is the integrated environment where work items are tested against other connected environments. Test data will be deployed to this environment to make it meaningful. During the normal course of development, this environment mainly takes the role of SIT \(System Integration Testing\) environment.  As the development nears a release, or the release branch is cut, the environment is attached to the release feed and release packages are installed. The behaviour of the system changes to User Acceptance Testing.  If there are not enough integration endpoints to connect to, this environment may be only possible in one consolidated UAT environment. |
| Data Migration Dev\*\* | Sandbox | Developer | No | Environment utilized by the Data Migration developers in a large program to test their data migration scripts for mock deployments. Only packages that are successfully tested in System Testing Environment should be pushed into this environment.    |
| Data Migration Test\*\* | Sandbox | Partial Copy | No | Used by data migration teams to test the data migration scripts on a bigger data set. |
| Data Migration Mock\*\* | Sandbox | Full Sandbox | No | Used by data migration teams to test the full data migration scripts to a full sandbox to benchmark performance and data quality issues.  Depending on the release model, this could be refreshed multiple times before the major release to ensure migration success. |
| Training\*\* | Sandbox | Developer Pro, Partial, or Full Sandbox | No | Environment utilized for developing training assets.  Depending on requirements for data sets, a partial or full sandbox may be required. |
| Hotfix | Sandbox | Developer Pro | No | Environment utilized to test hotfix. This environment follows the artifacts deployed to production and not necessarily one in staging during release hardening phase . |
| PreProd or DR \(Dress Rehearsal\)  | Sandbox | Developer, Full Sandbox | No | Final staging environment before a release. This environment is deployed all the packages for the release and the data migration scripts are triggered \*\* to test the accuracy of scripts before deploying to production.  Use of a Developer sandbox can be leverage for artifact deployments as they can be refreshed or created more frequently than Full Sandboxes. |
| Prod | Production | Production | Yes | Production Org and Dev Hub |

\*\* Denotes optional environments, only utilized during a large transformation program where salesforce is to be introduced and data must be migrated from existing solutions



If you have sufficient licenses and availability of other systems, you can remove the dual role of staging environment in the above strategy to one mentioned below, where you have a dedicated integration environment both in the develop and release channels. 

![](../.gitbook/assets/environment-strategy-optional-1-.png)



| Environment | Type | License Type | Integrated | Role |
| :--- | :--- | :--- | :--- | :--- |
| System Integrated Testing \(SIT\) | Sandbox | Developer Pro/Partial | Yes | SIT is the integrated environment where work items are tested against other connected environments. Test data will be deployed to this environment to make it meaningful. During the normal course of development, this environment mainly takes the role of SIT \(System Integration Testing\) environment.  |
| User Acceptance Testing \(UAT\) | Sandbox | Full Sandbox | Yes | UAT is a fully integrated environment where business users test the application prior to sign-off for release to production. The environment will have at a minimum test data and most of the time contained scrubbed Production Data. This is a controlled environment with restricted System Administrator access and will the latest stable release candidate will be deployed. |

