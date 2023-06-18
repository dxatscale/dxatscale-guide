---
description: All about collecting metrics from sfpowerscripts
---

# Metrics and Dashboards

Metrics should be a key part of your DevOps process. It is through these metrics, one can drive continuous improvement of your delivery process.

## Metrics available within sfpowerscripts

The following are the list of metrics that are captured.

| METRIC                                            | DESCRIPTION                                                                                                         | TYPE  |
| ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ----- |
| sfpowerscripts.deploy.failed                      | Number of times deploy command failed                                                                               | COUNT |
| sfpowerscripts.deploy.duration                    | Time spent on executing deploy command                                                                              | GAUGE |
| sfpowerscripts.deploy.scheduled                   | Number of times deployment was scheduled to run                                                                     | COUNT |
| sfpowerscripts.deploy.packages.scheduled          | Number of packages that were scheduled to be deployed by the deploy command                                         | GAUGE |
| sfpowerscripts.deploy.succeeded                   | Number of succeeded deploy executions                                                                               | COUNT |
| sfpowerscripts.deploy.succeeded.packages          | Number of packages that were successfully deployed                                                                  | GAUGE |
| sfpowerscripts.deploy.failed                      | Number of times deploy command failed to execute                                                                    | COUNT |
| sfpowerscripts.deploy.failed.packages             | Number and details of packages that failed to deploy                                                                | GAUGE |
| sfpowerscripts.build.scheduled                    | Number of times build was scheduled to run                                                                          | COUNT |
| sfpowerscripts.build.duration                     | Time spent on executing build command                                                                               | GAUGE |
| sfpowerscripts.build.scheduled.packages           | Number of packages being scheduled to build                                                                         | GAUGE |
| sfpowerscripts.build.succeeded.packages           | Number of packages successfully built                                                                               | GAUGE |
| sfpowerscripts.build.failed.packages              | Number of packages failed to build                                                                                  | GAUGE |
| sfpowerscripts.validate.scheduled                 | Number of scheduled validations                                                                                     | COUNT |
| sfpowerscripts.validate.succeeded                 | Number of successful validations                                                                                    | COUNT |
| sfpowerscripts.validate.failed                    | Number of time validate failed to execute                                                                           | COUNT |
| sfpowerscripts.validate.duration                  | Time spent on executing validate command                                                                            | GAUGE |
| sfpowerscripts.validate.packages.scheduled        | Number of packages scheduled for installation in a validation                                                       | GAUGE |
| sfpowerscripts.validate.packages.succeeded        | Number of successful package installations in a validation                                                          | GAUGE |
| sfpowerscripts.validate.packages.failed           | Number of failed package installations in a validation                                                              | GAUGE |
| sfpowerscripts.publish.duration                   | Time spent on executing publish command                                                                             | GAUGE |
| sfpowerscripts.publish.succeeded                  | Number of succeeded publish executions                                                                              | COUNT |
| sfpowerscripts.package.installation               | Number of times a package was installed                                                                             | COUNT |
| sfpowerscripts.package.installation.elapsed\_time | Time taken to install a package                                                                                     | GAUGE |
| sfpowerscripts.package.elapsed                    | Time taken to create a package                                                                                      | GAUGE |
| sfpowerscripts.package.created                    | Number of times a particular package was created                                                                    | COUNT |
| sfpowerscripts.package.metadatacount              | Number of metadata in a package                                                                                     | GAUGE |
| sfpowerscripts.package.testcoverage               | Test Coverage of a package                                                                                          | GAUGE |
| sfpowerscripts.apextests.triggered                | Number of times apex tests were triggered for a package                                                             | COUNT |
| sfpowerscripts.apextest.testtotal                 | Time taken for Apex Test Execution                                                                                  | GAUGE |
| sfpowerscripts.apextest.command.time              | Time taken for Apex Test Execution (Command Time)                                                                   | GAUGE |
| sfpowerscripts.prepare.succeededorgs              | Number of orgs that were succeeded during a run of prepare                                                          | GAUGE |
| sfpowerscripts.prepare.failedorgs                 | Number of orgs that failed during a run of prepare                                                                  | GAUGE |
| sfpowerscripts.prepare.duration                   | Time take to prepare a pool of scratchorgs                                                                          | GAUGE |
| sfpowerscripts.prepare.org.checkpointfailed       | Number of scratch orgs that failed on a checkpoint, during prepare                                                  | COUNT |
| sfpowerscripts.prepare.org.partial                | Number of scratch orgs that partially succeeded, during prepare                                                     | COUNT |
| sfpowerscripts.prepare.packages.scheduled         | Number of packages scheduled for installation when preparing scratch org pools                                      | GAUGE |
| sfpowerscripts.prepare.packages.succeeded         | Number of packages successfully installed when preparing scratch org pools                                          | GAUGE |
| sfpowerscripts.prepare.packages.failed            | Number of packages failed to install when preparing scratch org pools                                               | GAUGE |
| sfpowerscripts.so.packages.requested              | Number of packages requested to be installed to an individual scratch org in the pool                               | GAUGE |
| sfpowerscripts.so.package.installed               | Number of packages successfully installed to an individual scratch org in the pool                                  | GAUGE |
| sfpowerscripts.pool.available                     | Number of scratch orgs that are available in a pool after fetched by validate command                               | GAUGE |
| sfpowerscripts.release.scheduled                  | Number of scheduled releases                                                                                        | COUNT |
| sfpowerscripts.release.succeeded                  | Number of successful releases                                                                                       | COUNT |
| sfpowerscripts.release.failed                     | Number of failed releases                                                                                           | COUNT |
| sfpowerscripts.release.duration                   | Time taken for a release                                                                                            | GAUGE |
| sfpowerscripts.release.packages.scheduled         | Number of packages scheduled for release                                                                            | GAUGE |
| sfpowerscripts.release.packages.succeeded         | Number of packages that were installed successfully in a release                                                    | GAUGE |
| sfpowerscripts.release.packages.failed            | Number of packages that failed to install in a release                                                              | GAUGE |
| sfpowerscripts.release.workitems                  | Aggregated count of workitems in a release (a release is identified by the identifier used in a release definition) | GAUGE |
| sfpowerscripts.release.commits                    | Aggregated count of commits in a release (a release is identified by the identifier used in a release definition)   | GAUGE |

## Sample Dashboards

![](../.gitbook/assets/dashboard\_edited.png)

![](<../.gitbook/assets/image (52) (1) (1) (1).png>)
