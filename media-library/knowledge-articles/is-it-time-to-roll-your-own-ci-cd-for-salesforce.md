---
description: Published on November 6, 2019 by Azlam Abdulsalam
---

# Is it time to roll your own CI/CD for Salesforce?

![](<../../.gitbook/assets/image (4).png>)

CI/CD for Salesforce is in a very exciting phase. On one end you have awesome 'only for Salesforce' DevOps platforms such as Autorabit, Gearset, Copado etc which gets you going as quickly as possible. On the other end, often in the case of large enterprises, a custom-built pipeline is often the preferred choice.

Let's first look at what are the possible reasons for enterprises preferring this route.

1. Platform/System/DevOps teams have already been established and have a preferred list of tooling such as version control, ci/cd platform, monitoring system etc and are maintained centrally across the enterprise.
2. Reluctance to adopt an exclusive DevOps platform for Salesforce either due to duplication of the feature across the enterprise tech stack or difficulty in integration with other tools
3. Salesforce DX and its modern toolset have made adopting techniques used across other tech stacks easier than ever before.
4. Level of Automation that is often above what the vendor offers, often resulting in running scripts before/after utilizing the tool and maintaining long deployment checklist

In my experience, the last point is really significant as most of the tools currently in the market are driven by manual interaction and often based on a compare, select, deploy and observe pattern. With the advent of Salesforce DX, It is now possible to use a generic CI/CD solution along with custom scripts (CLI, API and a bit of UI) to orchestrate the deployments with minimal manual intervention. Often the deployment scripts have to be modelled around what's being contained in the package, as the package in its entirety is being deployed multiple times daily (contrast to the delta deployments of the past). Having a highly automated pipeline configured per project becomes a necessity rather than a 'nice to have'.

As it is evident there is an increased need for a configurable pipeline and automation, enterprise programs have to invest significant resource to create and maintain these scripts. This is where I believe a case exists for a hybrid approach, where an externally maintained reusable set of commands running on a generic CI/CD platform can be utilized to build a highly extensible pipeline. The community has produced some awesome reusable commands. Check this link [here](https://github.com/mshanemc/awesome-sfdx-plugins).

This is what I along with my colleagues have been working on for a while, utilizing these community-driven plugins along with our own open-source projects to build custom pipelines for our projects.

Check out the details of our open source projects here.

[sfpowerkit](https://github.com/Accenture/sfpowerkit): An open-source collection of commands packaged as an SFDX Plugin to help with operational and development workflows.

[sfpowerscripts](https://sfpowerscripts.com): A plugin for Azure DevOps which brings you granular tasks that eliminates the need for scripting the deployment tasks in CI/CD yourself. We are planning to port sfpowerscripts to Jenkins (Plugin), GitHub (as an Action) and Circle CI (Orbs), thus helping you build your custom Salesforce DevOps pipeline's in no time.

What do you think?
