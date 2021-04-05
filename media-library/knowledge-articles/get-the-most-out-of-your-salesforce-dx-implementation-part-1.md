---
description: 'Published on February 13, 2019 by Azlam Abdulsalam'
---

# Get the most out of your Salesforce DX Implementation - Part 1

### 1. Invest in upskilling and juggle the team structure until you find the right balance

Salesforce programs are staffed with a mix of functional configurators and developers. Most of them while experts in Salesforce related functionality, are quite new to the world of version control, pull requests etc. Salesforce DX is based on version control as its core principle and it is important the team understands the usage of version control and not gets panicked when a conflict arises or when they see an issue while using the CLI.  The same process has to be followed thoroughly when a new developer is onboard'ed, so they are aware of the tools/process followed in the project.

It is very significant to have a seasoned developer leading the team so that he/she can help with code reviews and also explaining/fixing nuances when things don't work as expected \(More on that later\)

**Tip:** Gamify onboarding by providing access to Dev Hub only on the successful completion of DX trailhead  ****

### 2. Understand DX is much more than 'DevOps' tooling and is Salesforce bringing modern engineering practices that are tried and dusted in other platforms/tech stack

The above messaging needs to be quite well articulated and understood to fully reap the benefits. Salesforce DX comprises of Source Driven Development, Command Line Interface, Scratch Orgs \(Similar to Docker, each developer gets their own environments\), modularized development through packaging and Artifact management through DevHub. Due emphasis should be given to the idea of modularization and the benefits needed to be articulated to the team and program management, especially around the total cycle time in an enterprise setting. Salesforce's Lightning platform is a hpaPaaS \(High Productivity application Platform as a Service\) and modularization as a technique is a quite new to the world of Salesforce Development

**Tip:** Have your Salesforce developers interact with developers from a different tech stack and introduce to the tooling and development workflow that they follow. 

**Tip:** Unlocked packages are the real stuff in the whole DX story, though Scratch org's share the limelight. Adopting scratch org's to mimic an org based development is a very challenging endeavour. Suggest looking into CLI to work against sandboxes.

### 3. Have a System/Platform/DevOps team to support the tooling and creation of pipelines.. also invest in tools that support release management

As you progress along the utilization of DX, it is imperative that you have the support of System/Platform/DevOps team \(whatever you call it\) to support the tooling and building the pipelines. Also rather than approaching pipelines for Salesforce as a whole, look at pipelines for each of the individual package and model the package all the way to production including manual steps and necessary approval gates. This will result in having a localised approach to automation for each of the individual packages and also provides with a healthy backlog for the system team to automate further during the course of the program

**Tip:** Understand not everything is automatable, and there is no need for that either. Classify steps into what have 'org-wide' implications and what should be owned by a package/team.For eg: metadata like 'named credentials' \(which define the integration endpoints\) need not be deployed through packaging unless you are building a package for your end customers to utilise as an ISV. 

**Tip:** SFDX CLI allows you to trigger anonymous apex classes. This can be interleaved before/after deployment of the package to automate steps like user creation, permission set assignments etc. Encourage teams to add these scripts along with their package repo and orchestrate these as part of the CD process.

### 4. Be Pragmatic around the limitations of Scratch Org and in dealing with metadata that cannot be packaged

Salesforce DX is still in infancy and has its rough edges, and there are some bugs that can snowball and consumes a lot of time in investigating/fixing it. Be pragmatic about it and utilise the SFDX CLI and the sandbox environment to retrieve the offending metadata. This is one of the practices we follow especially regarding metadata like 'Profile', and 'Community' which has issues with source tracking in the scratch org.

**Tip:** Installing packages consume the biggest time in setting up the scratch org, So be judicious on when scratch orgs are created. If you prefer the idea of spinning scratch orgs for every feature branch, then ensure that feature branch is building at-least a couple of days of work including configuration+development. If its too granular, the knock-on impact of set up time mounts up quickly.

**Tip:** If you have a lot of managed packages as a dependency, ignore scratch org's for now and wait till Summer 19, when features like 'snapshot' will be available.  

**Tip:** Salesforce DX has a very active chatter group with the product team actively answering queries. There are many approaches being discussed on how to handle metadata and packaging... Recommend subscribing to Salesforce DX / Unlocked Packages group

Stay tuned, as we have a lot more to speak on this exciting new era for Salesforce.

