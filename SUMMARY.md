# Table of contents

* [DX@Scale](README.md)
* [Talks on DX@Scale](talks-on-dx-scale.md)
* [Principles](principles.md)

## 🤸 Learn with hands-on exercises <a href="#challenges" id="challenges"></a>

* [Intro](challenges/intro.md)
* [Prerequisites](challenges/prerequisites.md)
* [Challenges](challenges/challenges/README.md)
  * [Deploy to a Sandbox](challenges/challenges/1.-deploy-to-a-sandbox.md)
  * [Using Source Format](challenges/challenges/2.-using-source-format.md)
  * [Introduction to Scratch Orgs](challenges/challenges/4.-scratch-org-introduction.md)
  * [Scratch Org Shape](challenges/challenges/5.-scratch-org-shape.md)
  * [Using a Package](challenges/challenges/3.-using-a-package.md)
  * [Create your own package](challenges/challenges/7.-create-your-own-package.md)
  * [Intro to sfpowerscripts orchestrator](challenges/challenges/intro-to-orchestrator.md)
  * [Building your packages](challenges/challenges/build-your-package.md)
  * [Publish and Release your artifacts](challenges/challenges/publish-and-fetch-your-artifacts.md)
  * [Scratch Org Pooling Part 1](challenges/challenges/scratch-org-pooling.md)
  * [Scratch Org Pooling Part 2](challenges/challenges/scratch-org-pooling-part-2-prepare.md)
  * [Validating your changes](challenges/challenges/validating-your-changes.md)

## 🧬 Source Code Management <a href="#scm" id="scm"></a>

* [Repository Structure](scm/repository-structure.md)
* [Branching Model](scm/branching-model/README.md)
  * [Feature Toggling](scm/branching-model/feature-toggling.md)
  * [Branching Conventions](scm/branching-model/branching-conventions.md)

## ♾ CI/CD

* [A Typical CI/CD Pipeline](ci-cd/a-typical-ci-cd-pipeline.md)
* [Artifacts](ci-cd/artifacts.md)

## 💞 Implementing your CI-CD

* [GitHub](implementing-your-ci-cd/github/README.md)
  * [Prerequisites](implementing-your-ci-cd/github/prerequisites.md)
  * [Getting Started](implementing-your-ci-cd/github/getting-started.md)
  * [Solution Overview](implementing-your-ci-cd/github/solution-overview.md)
* [GitLab](implementing-your-ci-cd/gitlab/README.md)
  * [Prerequisites](implementing-your-ci-cd/gitlab/prerequisites.md)
  * [Getting Started](implementing-your-ci-cd/gitlab/getting-started.md)
  * [Solution Overview](implementing-your-ci-cd/gitlab/solution-overview.md)
* [Azure DevOps](implementing-your-ci-cd/azure-devops/README.md)
  * [Prerequisites](implementing-your-ci-cd/azure-devops/prerequisites.md)
  * [Getting Started](implementing-your-ci-cd/azure-devops/getting-started.md)

## sfpowerscripts

* [Overview](sfpowerscripts/sfpowerscripts.md)
* [Features](sfpowerscripts/features.md)
* [Types of Packaging](sfpowerscripts/types-of-packaging/README.md)
  * [Unlocked Packages](sfpowerscripts/types-of-packaging/unlocked-packages.md)
  * [Source Packages](sfpowerscripts/types-of-packaging/source-packages.md)
  * [Data Packages](sfpowerscripts/types-of-packaging/data-packages.md)
* [Orchestrator](sfpowerscripts/orchestrator/README.md)
  * [Build & Quick Build](sfpowerscripts/orchestrator/build-and-quick-build.md)
  * [Publish](sfpowerscripts/orchestrator/publish.md)
  * [Deploy](sfpowerscripts/orchestrator/deploy.md)
  * [Release](sfpowerscripts/orchestrator/release.md)
  * [Prepare](sfpowerscripts/orchestrator/prepare/README.md)
    * [Scratch Org Pool Configuration](sfpowerscripts/orchestrator/prepare/scratch-org-pool-configuration.md)
  * [Validate](sfpowerscripts/orchestrator/validate.md)
* [Docker Images](sfpowerscripts/docker-images.md)
* [Metrics and Dashboards](sfpowerscripts/metrics-and-dashboards.md)
* [Environment Variables](sfpowerscripts/environment-variables.md)
* [Command Glossary](sfpowerscripts/command-glossary.md)

## 🏗 Development Practices

* [Modular Deployment](development-practices/modular-deployment.md)
* [Organizing your code / config](development-practices/modularizing-your-code-config.md)
* [Defining the boundaries of a package](development-practices/defining-the-boundaries-of-a-package.md)
* [Dealing with Org Specific Metadata](development-practices/dealing-with-sensitive-metadata.md)
* [Managing Profiles](development-practices/managing-profiles.md)
* [Tracking Manual Steps](development-practices/tracking-manual-steps.md)

## 🌲 Environment Management <a href="#environment" id="environment"></a>

* [Environment Strategy](environment/env-strategy.md)
* [Connecting Environments](environment/connecting-environments.md)
* [Developer Environments](environment/developer-environments.md)
* [CI Environments](environment/ci-environments.md)
* [Pooling Scratch Orgs](environment/pooling-scratch-orgs.md)
* [Refreshing Sandboxes](environment/refreshing-sandboxes.md)

## Release Management <a href="#release" id="release"></a>

* [Monitoring Releases](release/monrel.md)
* [Releasing to an Environment](release/release-environment.md)

## Team Topology <a href="#roles-and-responsibilites" id="roles-and-responsibilites"></a>

* [Team Structure and Roles](roles-and-responsibilites/team.md)

## ⁉ faq

* [Packaging](faq/packaging/README.md)
  * [Unlocked Package](faq/packaging/unlocked-package.md)
  * [Data Package](faq/packaging/data-package.md)
* [sfpowerscripts](faq/sfpowerscripts.md)

## 🍕 projects

* [sfp-cli](projects/sfp-cli/README.md)
  * [Command Glossary](projects/sfp-cli/command-glossary.md)
* [sfpowerkit](projects/sfpowerkit/README.md)
  * [Command Glossary](projects/sfpowerkit/command-glossary.md)
* [sfmc-devtools](https://github.com/Accenture/sfmc-devtools)

## 🎬 Media Library

* [Knowledge Articles](media-library/knowledge-articles/README.md)
  * [Handling Entitlements](https://medium.com/@gnemiq/salesforce-entitlement-handling-9e69735e3687)
  * [sfpowerscripts orchestrator pool breaking changes](media-library/knowledge-articles/sfpowerscripts-orchestrator-pool-breaking-changes.md)
  * [Streamlined Scratch Orgs are here!](media-library/knowledge-articles/streamlined-scratch-orgs-are-here.md)
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
* [DX@Scale in the media](media-library/notable-mentions.md)

***

* [Tools & Assets Registry](assets-registry.md)

## 🌈 About Us

* [Meet Our Team](about-us/meet-our-team.md)
* [Key Contributors](about-us/contributors.md)
* [Contributing to DX@Scale](about-us/contributing-to-dx-scale.md)
* [Contact Us](about-us/contact-us.md)
