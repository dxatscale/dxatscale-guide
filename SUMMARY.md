# Table of contents

* [DX@Scale](README.md)
* [Modular Development Renaissance for Salesforce](modular-development-renaissance-for-salesforce.md)
* [Talks on DX@Scale](talks-on-dx-scale.md)
* [Principles](principles.md)

## 💞 Implementing your CI-CD

* [Audience](implementing-your-ci-cd/github.md)
* [Prerequisites](implementing-your-ci-cd/prerequisites.md)
* [Getting Started](implementing-your-ci-cd/getting-started/README.md)
  * [Developer Workstation](implementing-your-ci-cd/getting-started/getting-started.md)
  * [On your Salesforce Org](implementing-your-ci-cd/getting-started/getting-started-1.md)
* [GitHub](implementing-your-ci-cd/github-1/README.md)
  * [GitHub Setup](implementing-your-ci-cd/github-1/getting-started.md)
  * [Solution Overview](implementing-your-ci-cd/github-1/solution-overview.md)
* [GitLab](implementing-your-ci-cd/gitlab/README.md)
  * [GitLab Setup](implementing-your-ci-cd/gitlab/getting-started.md)
  * [Solution Overview](implementing-your-ci-cd/gitlab/solution-overview.md)
* [Azure DevOps](implementing-your-ci-cd/azure-devops/README.md)
  * [Azure DevOps Setup](implementing-your-ci-cd/azure-devops/getting-started.md)
  * [Solution Overview](implementing-your-ci-cd/azure-devops/solution-overview.md)
* [Setting up Dashboards](implementing-your-ci-cd/dashboard-setup/README.md)
  * [New Relic](implementing-your-ci-cd/dashboard-setup/new-relic.md)
  * [Data Dog](implementing-your-ci-cd/dashboard-setup/data-dog.md)
  * [Splunk](implementing-your-ci-cd/dashboard-setup/splunk.md)

## 🧬 Source Code Management

* [Repository Structure](source-code-management/repository-structure.md)
* [Branching Model](source-code-management/branching-model/README.md)
  * [Feature Toggling](source-code-management/branching-model/feature-toggling.md)
  * [Branching Conventions](source-code-management/branching-model/branching-conventions.md)

## ♾ CI/CD

* [A Typical CI/CD Pipeline](ci-cd/a-typical-ci-cd-pipeline.md)
* [Artifacts](ci-cd/artifacts.md)

## 🏗 Development Practices

* [Modular Deployment](development-practices/modular-deployment.md)
* [Organizing your code / config](development-practices/modularizing-your-code-config.md)
* [Defining the boundaries of a package](development-practices/defining-the-boundaries-of-a-package.md)
* [Dealing with Org Specific Metadata](development-practices/dealing-with-sensitive-metadata.md)
* [Managing Profiles](development-practices/managing-profiles.md)
* [Tracking Manual Steps](development-practices/tracking-manual-steps.md)

## 🌲 Environment Management

* [Connecting Environments](environment-management/connecting-environments.md)
* [Developer Environments](environment-management/developer-environments.md)
* [CI Environments](environment-management/ci-environments.md)
* [Pooling Scratch Orgs](environment-management/pooling-scratch-orgs.md)
* [Pooling Sandboxes](environment-management/pooling-sandboxes.md)
* [Refreshing Sandboxes](environment-management/refreshing-sandboxes.md)

## sfpowerscripts

* [Overview](sfpowerscripts/sfpowerscripts.md)
* [Features](sfpowerscripts/features.md)
* [Types of Packaging](sfpowerscripts/types-of-packaging/README.md)
  * [Unlocked Packages](sfpowerscripts/types-of-packaging/unlocked-packages.md)
  * [Source Packages](sfpowerscripts/types-of-packaging/source-packages.md)
  * [Diff Packages](sfpowerscripts/types-of-packaging/diff-packages.md)
  * [Data Packages](sfpowerscripts/types-of-packaging/data-packages.md)
* [Orchestrator](sfpowerscripts/orchestrator.md)
* [Build & Quick Build](sfpowerscripts/build-and-quick-build.md)
* [Publish](sfpowerscripts/publish.md)
* [Release](sfpowerscripts/release/README.md)
  * [Release Config](sfpowerscripts/release/release-config.md)
  * [Release Defnition Generator](sfpowerscripts/release/release-defn-generator.md)
* [Prepare](sfpowerscripts/prepare/README.md)
  * [Scratch Org Pool Configuration](sfpowerscripts/prepare/scratch-org-pool-configuration.md)
  * [Pool Operations](sfpowerscripts/prepare/pool-operations/README.md)
    * [List Scratch Orgs](sfpowerscripts/prepare/pool-operations/list-scratch-orgs.md)
    * [Fetch A Scratch Org](sfpowerscripts/prepare/pool-operations/fetch-a-scratch-org.md)
    * [Delete Pools](sfpowerscripts/prepare/pool-operations/delete-pools.md)
* [Validate](sfpowerscripts/validate.md)
* [Deploy](sfpowerscripts/deploy.md)
* [Dependency Management](sfpowerscripts/dependency-management/README.md)
  * [Transitive Dependency Resolution](sfpowerscripts/dependency-management/transitive-dependency-resolution.md)
  * [Shrink](sfpowerscripts/dependency-management/shrink.md)
  * [Expand](sfpowerscripts/dependency-management/expand-shirnk.md)
  * [Install](sfpowerscripts/dependency-management/install.md)
* [Metadata Specific Support](sfpowerscripts/metadata-specific-support.md)
* [Docker Images](sfpowerscripts/docker-images.md)
* [Metrics and Dashboards](sfpowerscripts/metrics-and-dashboards.md)
* [Environment Variables](sfpowerscripts/environment-variables.md)
* [Command Glossary](sfpowerscripts/command-glossary.md)

## sfops

* [Overview](sfops/overview.md)
* [Environments](sfops/environments/README.md)
  * [Creating an Environment](sfops/environments/creating-an-environment.md)
  * [Authenticating to Environments](sfops/environments/authenticating-to-environments.md)
* [Scheduled Jobs](sfops/scheduled-jobs/README.md)
  * [Job - CI Sandbox - Creator](sfops/scheduled-jobs/job-ci-sandbox-creator.md)
  * [Job - CI Sandbox - Allocate to Pool](sfops/scheduled-jobs/job-ci-sandbox-allocate-to-pool.md)
  * [Jobs - Report results of all tests](sfops/scheduled-jobs/jobs-report-results-of-all-tests.md)
* [Workflows](sfops/workflows/README.md)
  * [Build, Deploy & Publish](sfops/workflows/build-deploy-and-publish.md)
  * [Release a Domain](sfops/workflows/release-a-domain.md)
  * [Hotfix Workflow](sfops/workflows/hotfix-workflow.md)
* [IssueOps](sfops/issueops/README.md)
  * [Request a new developer sandbox](sfops/issueops/request-a-new-developer-sandbox.md)
  * [Request a release branch for hotfix](sfops/issueops/request-a-release-branch-for-hotfix.md)

## Release Management

* [Releasing to an Environment](release-management/release-environment.md)
* [Monitoring Releases](release-management/monrel.md)

## Team Topology

* [Team Structure and Roles](team-topology/team.md)

## ⁉ faq

* [Scratch Orgs](faq/scratch-orgs/README.md)
  * [Handling Org-Wide Email Addresses](faq/scratch-orgs/handling-org-wide-email-addresses.md)
  * [Scratch Org Error Codes](faq/scratch-orgs/scratch-org-error-codes.md)
* [Packaging](faq/packaging/README.md)
  * [Unlocked Package](faq/packaging/unlocked-package.md)
  * [Data Package](faq/packaging/data-package.md)
* [sfpowerscripts](faq/sfpowerscripts.md)

## 🎬 Media Library

* [Knowledge Articles](media-library/knowledge-articles/README.md)
  * [Why you should use scratch orgs?](https://medium.com/@dieffrei/why-you-should-use-scratch-orgs-a-real-journey-c65bf5829496)
  * [Introduction to Scratch Org Pools](https://medium.com/@dieffrei/introduction-to-salesforce-scratch-org-pools-e1616772499c)
  * [Creating Scratch Org Pools at Scale](https://medium.com/@dieffrei/dx-scale-scratch-org-pools-1dbecfcda8f8)
  * [Declarative Field History Tracking](https://medium.com/@gnemiq/declarative-configuration-for-field-history-tracking-d63525a5e7b2)
  * [Handling Entitlements](https://medium.com/@gnemiq/salesforce-entitlement-handling-9e69735e3687)
  * [Salesforce Apex Test Execution Performance Tuning](https://medium.com/@dieffrei/salesforce-apex-test-execution-performance-tuning-d38974a413ee)
  * [Building packages for deployment](media-library/knowledge-articles/building-packages-for-deployment.md)
  * [Version Controlling Profiles and Why It Makes Sense for Deployments?](media-library/knowledge-articles/version-controlling-profiles-and-why-it-makes-sense-for-deployments.md)
  * [Validation in Continuous Integration](media-library/knowledge-articles/validation-in-continuous-integration.md)
  * [Scratch Org Pooling for CI](media-library/knowledge-articles/scratch-org-pooling-for-ci.md)
  * [Scratch Org Pooling for Development](media-library/knowledge-articles/scratch-org-pooling-for-development.md)
  * [Adopting Package Based Development Model in Salesforce](media-library/knowledge-articles/adopting-package-based-development-model-in-salesforce.md)
  * [Elevate your Salesforce deployment experience with just 6 commands](media-library/knowledge-articles/elevate-your-salesforce-deployment-experience-with-just-6-commands.md)
  * [Is it time to roll your own CI/CD for Salesforce?](media-library/knowledge-articles/is-it-time-to-roll-your-own-ci-cd-for-salesforce.md)
  * [The soon to be state of DevOps for Salesforce](media-library/knowledge-articles/the-soon-to-be-state-of-devops-for-salesforce.md)
  * [Change Lead Time for DX Unlocked Packaging](media-library/knowledge-articles/change-lead-time-for-dx-unlocked-packaging.md)
  * [Get the most out of your Salesforce DX Implementation - Part 2](media-library/knowledge-articles/get-the-most-out-of-your-salesforce-dx-implementation-part-2.md)
  * [Get the most out of your Salesforce DX Implementation - Part 1](media-library/knowledge-articles/get-the-most-out-of-your-salesforce-dx-implementation-part-1.md)
  * [Effective Pull Reviews in Salesforce DX Development - Persistent CI](media-library/knowledge-articles/effective-pull-reviews-in-salesforce-dx-development-persistent-ci.md)
* [DX@Scale in the Media](media-library/notable-mentions.md)

***

* [Tools & Assets Registry](assets-registry.md)

## 🌈 About Us

* [Meet Our Team](about-us/meet-our-team.md)
* [Key Contributors](about-us/contributors.md)
* [Code of Conduct](about-us/code-of-conduct.md)
* [Contributing to DX@Scale](about-us/contributing-to-dx-scale.md)
* [Contact Us](about-us/contact-us.md)
