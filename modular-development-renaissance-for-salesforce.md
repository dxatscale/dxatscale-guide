# Modular Development Renaissance for Salesforce

{% embed url="https://www.linkedin.com/pulse/modular-development-renaissance-salesforce-part-1-2-vu-ha/" %}
Part I
{% endembed %}

{% embed url="https://www.linkedin.com/pulse/modular-development-renaissance-salesforce-part-2-vu-ha/" %}
Part 2
{% endembed %}

## Introduction

Modular development adoption across Salesforce implementations has been slow and oftentimes overlooked due to the perception that it is overly complex, has no proven track record of success, and requires a strong talent pool of pro-code developers to drive and maintain the solution.

Arguments can be made for and against each of these factors. Developers and Architects struggle everyday with the unorganized and many times monolithic “happy soup” repository inherited from the traditional org-based delivery model. Many organizations have adopted source control and CI/CD pipelines but continue to struggle with metadata dependencies that stall deployments and put undue stress on their teams to release code quicker.

Contrary to many people's assumptions in Salesforce, the platform has matured to a point where tools and best practices exist today for teams to shift towards a modular, package-based development model if they just make the effort to. Advancements in SFDX ([Salesforce Developer Experience](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_intro.htm)) since its inception in 2015 and success stories from the open-source community leveraging tools, frameworks, and methodology to drive their “[composable](https://architect.salesforce.com/well-architected/adaptable/composable)” renaissance is now widely available for everybody to learn, adopt, and apply.

There are two roles that these impacts most, Developers and Architects. Let’s do a deep dive into each one.

### Developers

The challenges mentioned above are experienced by Developers working on Salesforce engagements every day. Picture this, a Developer is brought on a project, and they want to make an impact right away, where do they start? How can they quickly understand all the various components configured or customized in the org in the shortest amount of time. Having this knowledge enables them to drive a multitude of activities such as troubleshooting a production issue, solutioning a new feature, identifying performance bottlenecks within the underlying architecture design, or isolating potential refactoring tasks to ensure long term stability and maintainability of the application for end users. Trying to untangle the metadata in a traditional non-modularized repository (if one exists) using the legacy metadata API format from Production can be a daunting task for even the most seasoned Salesforce Professional. It may take days if not weeks or months to understand enough before new features or refactoring efforts can begin. Being able to map core business processes to the metadata associated with driving its functionality in an org along with all its dependencies is not possible without modularity. Some tools in the ecosystem may claim to help you do this but they tend to add too much overhead to existing processes rather than starting to organize your codebase from scratch and mature it over time until you have a full representation of your metadata in production.

This also creates a deterrent for developers outside the Salesforce ecosystem potentially considering a career transition to the platform. These developers are usually accustomed to modern technology stacks that have mature tooling and processes to support modular, versioned, and artifact-driven development and adhere to software design best practices and principles. Developer experience is critical in today’s competitive landscape. If you wish to attract the best talent to your platform there must be a shift to a modern package-based development model that creates a welcoming environment.

### Architects

Momentum has been building in the Salesforce Architect space to drive better quality solutions and design decisions on the platform. This is evident on the recently launched [Salesforce Well-Architected Framework](https://architect.salesforce.com/well-architected/overview) guide that focuses on establishing trusted, easy, and adaptable solutions. The complexity of the Salesforce Platform continues to grow with each new release of product to support new and existing industries. Add in the complexities of managed packages from ISVs that build upon these core Salesforce Products to address the remaining business process gaps and you can see how extremely difficult it has become to manage the platform.

Salesforce is no longer simply a Software-As-a-Service (SaaS) Customer Relationship Management (CRM) system. Without the shift in culture to adopt a well-architected, composable framework, the benefits of maintaining the platform begins to erode and maintainability and agility to onboard new developers and deploy new features becomes extremely difficult. At the end of the day, the longer it takes for you to push new features, the lower the return on investment for the platform you have purchased.

## Analogy

In order to simplify the concepts of modularity on the Salesforce Platform, let’s walk through an analogy that most people can relate to at one (or multiple) points in their lives: **Moving**.

When you live in your home for a long period of time, you tend to accumulate (or maybe hoard) belongings that at one point in your life, served a purpose and might still be useful in your new home. Items such as furniture, appliances, electronics, and home decor must be eventually organized and sorted accordingly as you prepare for the big move. How you decide to do this is up to you and your own personal preferences but in general, there tends to be a common overall guideline that most people follow when sorting their personal belongings in boxes. Categories such as kitchen, furniture, clothing, electronics, toiletries, decor, and personal items usually come to mind when thinking how to organize their belongings. Within those categories, you can break them down further into sub-categories that would fit in smaller or medium size boxes. For example, while packing your clothes, you can sort them based on summer/winter attire, formal/informal clothes, kids/adults clothes, and so on. Once you’ve grouped them, then you can sort them further into pants, shirts, underwear, etc. As you can see, although there may be a recommended approach to organizing and packing, no one will really question how you decide to sort your belongings as long as they can be quickly located and you or a family member(s) can locate them again quickly from the label on the box. If for some reason, you decide to re-sort items and shift them to bigger boxes or smaller boxes, there may be some effort required but if it helps keep things organized for the big move, it’s well worth the time invested now rather than later on when you are scrambling to find that favorite winter jacket when the cold weather comes.

The table below summarizes the moving analogy and how it can compare to Salesforce. Don’t take this 1:1 mapping too seriously as there may be different interpretations to this scenario to how I interpret the metadata vs. the next architect. It is meant to be a starting point for you to begin visualizing how “moving” away from the org-based delivery model to a modular, package-based approach can be achieved. Use whatever analogies work for you. Legos, puzzles, recipes, they all work.

| Home                                                  | Salesforce                                                                                          |
| ----------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| House + All Personal Contents (Unorganized)           | Production Org (Metadata Happy Soup)                                                                |
| Living Room, Kitchen, Bedroom, Bathroom, Laundry Room | Core Cloud Products (Sales Cloud, Service Cloud, Marketing Cloud, Industry Cloud, Experience Cloud) |
| Plumbing System, Framing, Electrical System, HVAC     | Frameworks (Trigger Framework, Logging and Error Handling)                                          |
| Furniture, Plants, Artwork, Appliances                | Custom Metadata (Business Domains Customizations)                                                   |
| Paint, Flooring, Blinds/Curtains, Windows, Doors      | Shared User Interface (UI) (Page Layouts, LWC)                                                      |
| Smart Home Components                                 | Managed Packages                                                                                    |
| Security Systems and Locks                            | Access Management (Profiles, Permission Sets, PermSet Groups)                                       |
| Garage, Storage Room, Attic                           | Uncategorized Metadata (Unpackaged, Source Packages)                                                |
| Moving Inventory List / Moving Day Calendar Schedule  | Runbooks (Sandbox Refreshes, Manual Steps for Deployment Releases)                                  |

To finish off the moving analogy, if all your belongings are packaged up, organized, and moved to your new home and the new home is of a similar layout as the old home (things like number of rooms, square footage, etc.) then you should be able to unpack all your belongings, and everything should fit in its intended location.

## Benefits of Modularity

### Managing Complexity

The challenge for most Salesforce Programs as they mature is how complex it is to build new functionality and troubleshoot production issues if there is an absence of modularity. If left unmanaged, metadata within a Salesforce Instance can grow into the double digit thousands of metadata count. This does not even take into account potential record driven data that drives applications built on the platform from Salesforce or ISVs through their managed packages.

When your org is modular designed from the beginning or refactored to be in a modular state, different teams are able to comprehend sections of the org independently faster and understand cross team dependencies as they go while primarily focusing on their new feature. Iterating through their design and build process has a sense of purpose and end goal. The alternative is getting lost in trying to understand the entire org composition and guessing on if their changes will break something unknown. At scale, modularization is inevitable. It is better to drink in small quantities than trying to drink from the fire hose.

### Defining Boundaries and Ownership

Imagine having a team of over 30+ developers all working in the same shared developer org with no boundaries defined around the metadata they are developing. Conflict will arise. Subsequent testing efforts are compromised by the business as changes implemented are not isolated and puts more pressure on the development team to regression test more than they have capacity for. Developers also don’t gain a sense of ownership of their modules to ensure the standard test class coverage and execution runs are done correctly for their package. Boundaries and ownership is fundamental to reducing risks on making changes in an org. If these are not defined early and revisited frequently, chaos will ensue.

### Repeatability

Can you recreate your entire Production Instance to a Scratch Org or migrate to a brand new Production Instance from your current code base on demand, with certainty and repeatability? If the answer is yes, then you are ahead of 90% of the projects out there and I should be reading your articles instead. All jokes aside, there is much to learn and share across the Trailblazer and open-source community to increase the momentum of this modular renaissance for Salesforce. Packages and SFDX are no longer just a one-off side project by a shadow IT team building an application named “force-app” that may or may not be installed in all your environments. They need to treat it as one important lego piece that forms your entire production org. This can be a starter duplo set for kids or an advanced 18+ lego set depending how far your developers and architects decide to take it. Once modular in state, you can be confident to reproduce the same product over and over again with confidence.

## **Tooling Advancements to Support Modularity**

As more teams begin to experiment and implement tools provided by the SFDX Product Team such as the CLI (Command Line Interface), APIs (Application Programming Interfaces), Source Format, Scratch Orgs, Org Shapes, Unlocked Packaging and other add-on CLI plugins and VS Code Extensions, Salesforce will continue to be forced to invest more in maturing the platform and developer tools to support this uptick in demand and consumption for these resources.  You can see this trend with their increased investments in the new [Code Builder (Beta)](https://developer.salesforce.com/tools/vscode/en/codebuilder/about),  [DevOps Center (Beta)](https://help.salesforce.com/s/articleView?id=sf.devops\_center\_overview.htm\&type=5), and the [Salesforce CLI Unification](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_setup.meta/sfdx\_setup/sfdx\_setup\_sf\_intro.htm) over the past few years.   Ideally, this continues to put pressure on their internal product teams to make them Generally Available (GA) sooner than later (that’s the hope, insert proverbial “[Safe Harbor Statement](https://investor.salesforce.com/safe-harbor/default.aspx)” here).

## **Success Stories from the Open-Source Community**

An example from the open-source community that best demonstrates Salesforce Modularity and Architecture Best Practices is the [DX@Scale](https://dxatscale.io/) team that presented at [Dreamforce 2022](https://reg.salesforce.com/flow/plus/dreamforce22/maincontentcatalog/page/Catalog/session/1656082522172001wR1g) for the “[Evolution of a Salesforce Org](https://www.youtube.com/watch?v=0cL0rBXe1lg)”. The team’s end state packaging design evolved as required for the program to succeed and the team did not try to perfect the process from the start. As the saying goes, **analysis paralysis**. This is much too common for organizations that admit to the benefits of modular development but have yet to take the first steps to start through either pilot releases or proof of concept designs. The fear of the unknown and safety net for traditional org-based delivery models with a selective/git diff based deployment approach for metadata limits organizations in achieving long term stability gained through modularity. Investments in upskilling and re-factoring efforts exist but that will always be the case with any software over the course of its lifetime.

## Getting Started

So, how can you start? For the “TL;DR'' people that skipped ahead to this section without reading Part 1 of the blog series, guess what, I forgive you. As a reward, here are some tips and lessons learned to get you up and running.

### Tip #1 - Just Start

* Install the [SFDX CLI](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_setup.meta/sfdx\_setup/sfdx\_setup\_install\_cli.htm).
* Enable your [DevHub](https://help.salesforce.com/s/articleView?id=sf.sfdx\_setup\_enable\_devhub.htm\&type=5) in Production or [Developer Edition Org](https://developer.salesforce.com/signup).&#x20;
* Clone a [sample trailhead app](https://github.com/trailheadapps) from
* Salesforce Create an unlocked package of it, version it, and install on a [Scratch Org](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_scratch\_orgs.htm) or [Sandbox](https://help.salesforce.com/s/articleView?id=sf.create\_test\_instance.htm\&type=5).

If you get stuck, Google is your friend. Your second best friend is the official [Salesforce Developer Documentation](https://developer.salesforce.com/docs). Looking for more friends, check out the [Salesforce Stack Exchange](https://salesforce.stackexchange.com/) or [Trailblazer Community Groups](https://trailhead.salesforce.com/en/trailblazercommunity). With the above items out of the way, you will be equipped with the foundational skills needed to divide and conquer your org.

### Tip #2 - Software Design Principles - Apply if you understand, else learn as you go.

The concept of modular development is not new, given that the same principles apply universally to modern software delivery products for cloud native and app-centric products. Underneath the hood, Salesforce is itself a Platform-As-a-Service that uses these principles to launch their many products and drive their 3 times a year software release cycle that has contributed to their growth and dominance in the industry in the past 20 years.

The following are some, and definitely not a comprehensive list of software design principles and concepts that you may have run across in books, technical articles or blogs that will come up during design or re-factoring discussions with your team.

* Object-Oriented Design&#x20;
* DRY (Don’t Repeat Yourself)&#x20;
* KISS (Keep It Simple, Stupid)&#x20;
* YAGNI (You Aren’t Gonna Need It)&#x20;
* S.O.L.I.D Principles&#x20;
* Horizontal vs. Vertical&#x20;
* Domain-Driven Design (DDD)&#x20;
* Test Driven Design (TDD)&#x20;
* Separations of Concerns&#x20;
* Modularization&#x20;
* Loose Coupling&#x20;
* Abstraction

A quick google of these concepts and you may luck out finding the right principle or design pattern to apply to your Salesforce modular design approach, or like me, get even more confused. Foundational computer science concepts sometimes are taken for granted with modern Software-As-a-Service (SaaS) because they abstract the design from the low code developers and admins and put in false confidence that new customized code can run freely like the wild wild west. Although this has given more people the ability to build a career from non-traditional computer science backgrounds, the technical debt that accumulates is then transferred on to future developers in their organizations to refactor eventually.

Try not to overthink these patterns in the beginning because you will never design the perfect solution right away. Treat these principles as references and guard rails to guide you in your journey to modularity. Your packaging model will evolve and mature as long as you take high level concepts from these principles and learn and re-package as needed. No package is too small, but there are packages that will eventually grow too large and need to be split up further to avoid reverting back to old “happy soup” habits.  Logically separate your metadata as you see fit based on business domains and functions and you will be on your way to success.&#x20;

### Tip #3 - **Package Types Don’t Really Matter for Modularity (At the Beginning)**

The misconception with Salesforce DX and moving to modularity is that teams focus solely on creating unlocked packages first. Although unlocked packages (not org-dependent unlocked packages) should be the end goal, the fact is whether you deploy your code via Metadata API, Change Sets, Source Deploy or Unlocked Packaging, they are all just different transport mechanisms to that allow you to group and segregate metadata and eventually validate and deploy to the next environment. If you have organized your code in a modular fashion, success can be achieved using any one of these approaches by using a combination of manual and scripted solutions and a well documented runbook. The velocity to which it's done and the amount of manual effort versus automation will differ depending on the effort invested by your team.

**Types of Packaging Options for Consideration**

* Source&#x20;
* Unlocked&#x20;
* Org-Dependent Unlocked&#x20;
* Unmanaged / Uncategorized&#x20;
* Data Packages&#x20;
* Managed Packages (ISV)

For more details on the types of packages, refer to the DX@Scale [documentation](https://docs.dxatscale.io/sfpowerscripts/types-of-packaging).

### Tip #4 - **Mono Repo + Source Format = Success**

Begin with one single repository as your main repository for Salesforce Metadata.  Although there may be arguments for multi-repo designs, simplicity is your best friend when starting this new modular journey.  If you already have an existing repository using the old MDAPI format, you can attempt to [convert](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_ws\_convert\_mdapi.htm) it to source format but I would recommend against it.  Start clean and rebuild your repository from the ground up package by package until the entire metadata is represented and deployable.  There are [sample](https://docs.dxatscale.io/scm/repository-structure) source code repository structures out there that you can reference to get started.  Common challenges such as handling access management metadata (Profiles, Permission Sets, PermSet Groups), frameworks, shared UI components, and environment specific metadata are all highlighted and addressed on how to implement them.&#x20;

At the beginning, don’t worry too much about creating second generation [unlocked packages](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_unlocked\_pkg\_intro.htm) in your DevHub. Use the source format, and treat your packages as “[source packages](https://docs.dxatscale.io/sfpowerscripts/types-of-packaging/source-packages)” organized and sorted via folders in your mono repository. Keep the core business logic and cloud modules in Salesforce such as Sales and Service cloud nested in the “src” folder under “src\sales” or “src\service” and go from there like the sample repo above. Experiment deploying them to Scratch Orgs (or Sandboxes) from the CLI in sequence keeping in mind key dependencies as this will be important as you move from source packages to unlocked packages.

**Pro Tips:**

* Set the default package for pulling and retrieving metadata in the sfdx-project.json to a folder named “src-temp”.  This will be used a staging folder to sort and organize your metadata
* Ensure no duplicate metadata is across multiple source package folders. There should be one owner. There may be edge cases where you will need to bend this rule but try to avoid it early on.
* You can always have 100% source packages but you will never have a mono repo that doesn’t contain at least 1 source package or unpackagable/unmanaged metadata.
* Multi-repos are possible once packages are stable and are preferred to be stand alone but complexity can be reduced by sticking to a mono repo design pattern so developers and architects do not get confused looking for multiple sources of truth.
* Keep folders to a maximum of 3 levels deep
* Refer to the Metadata Coverage Report as you go and what will eventually be supported as unlocked packages. Typically, you will only have to deal with around 80-100 unique metadata types mentioned out of the currently supported 578 types from my experience.

### **Tip #5 - Scratch Org Pools Keeps you From Drowning**

[Scratch Orgs](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_scratch\_orgs.htm) are vital to the success of your modular codebase .  As you look to start fresh on a new Salesforce Instance or rebuild your existing org from the ground up, you will need Scratch Orgs.  In the early years of Salesforce DX, Scratch Orgs were treated more like a playground that was no different from the environments that you spin up doing Trailhead Modules.  They were not being leveraged to their full potential to recreate your Production instances from your code base.  This was due to the fact that the significant time and effort required to ensure all features/settings were enabled correctly, install all managed packages, manually configure non-supported metadata, and finally deploy your code took valuable development capacity away from developers building new features.  Sandboxes basically became the default choice for teams and investments on using Scratch Orgs lagged.

The solution from the open-source community to this was creating pools of Scratch Orgs in advance using automation scripts. Whether you script these yourself in your custom pipelines or leverage open-source solutions such as [DX@Scale](https://docs.dxatscale.io/environment/pooling-scratch-orgs) to generate these Scratch Org Pools, the end result is a repeatable process to ensure your code base is working and fully functional to test.  The concept of Scratch Org Pools borrows similar concepts from Infrastructure-As-a-Code techniques used in other Cloud Platforms and software delivery but within the constraints of the Salesforce Platform.  Scratch Org Pool preparation is vital to creating and recreating environments that reflect the latest complete, stable code base.  As you begin to have more modular separation between metadata, it becomes easier to maintain the integrity of the Scratch Org Pool creation process and identify quickly which new pull/merge request broke the creation of new Scratch Orgs.  Instead of developers drowning in time and effort to manually build and maintain their own Scratch Orgs, automation solves this for them so they can focus on building new features.  Continuous Integration jobs also benefit from the Scratch Org Pools as they will be used as the basis for validating new pull requests prior to merging and also reflect the latest stable code base.

With [Org Shape](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_shape\_intro.htm) recently set to [Generally Available](https://help.salesforce.com/s/articleView?id=release-notes.rn\_sfdx\_org\_shape\_ga.htm\&type=5\&release=238) (GA) status since Summer ‘22 Release, the hope is that Scratch Orgs will become easier create as you can eliminate the complexities inherit from trial and error efforts during scratch org definition file creation and jump to validating and deploying your modular code.

### Tip #6 - Mature Salesforce Modularity Uses Artifacts

As your modular journey begins to mature, the concept of “artifacts” should be incorporated into your CI/CD (Continuous Integration / Continuous Delivery) process. Artifacts are traceable, versioned, immutable entities that are critical to ensuring your modular packages are able to be tracked during the release process to upper environments. When deployed to each environment, you are aware of what version of the artifact is installed and the contents of all the packages within that version. If anything goes wrong, you have the confidence in identifying issues with it and can revert to a previous version or move forward with a new version. During unlock package creation, your DevHub also borrows from this artifact concept as it creates a new version of your package and stores and tracks it in its own database tables. Think of artifacts as your new iPhone/Android phone for this year. It itself is a release of a hardware and software artifact that contains the complete set of features that you can use. This should apply to how you deploy new features in Salesforce that may comprise 1:M updated modular packages, grouped in a release artifact with the corresponding release notes for users to reference.

For more information on the concept of artifacts on Salesforce, read the [DX@Scale](https://docs.dxatscale.io/ci-cd/artifacts) documentation regarding artifacts and managing them in artifact registries.

### Tip #7 - Orchestration Brings All the Packages to the Yard

Being able to manage all the packages in your mono-repository can become burdensome and messy as the number of packages grows.  Like juggling, where rhythm and timing is critical to keep the balls in the air, managing the build and release of new and updated packages will require the correct set of tools to do the job as well.  Luckily in the programming world, this can be solved through automation through scripts.

The overhead with building and maintaining custom bash/scripts to plug into your pipeline tool (eg. GitHub Actions, GitLabs, or Azure DevOps, Jenkins, etc.) is a big obstacle for teams with limited developer skill sets necessary to build and maintain these scripts. Although simple YAML pipelines can be developed early on to support an initial set of package creations, installation and source code deployments, more advanced engineering will be required to continually support more complex code bases with dependencies and frequent releases. For most teams, this means they typically take short cuts such as creating monolithic packages, creating only org-dependent packages, or even worst use selective/git diff based deployment deployments for metadata to bypass benefits of modularity in your entire mono-repo. Although this works temporarily, it is not the long term solution that I recommend if you are taking this new journey. Open source tools such as DX@Scale exist today to solve these common problems and eliminate the need to continue to reinvent the wheel for a solution that already exists and is proven. Their suite of orchestrator CLI plugin commands reduces all the complexities of managing multiple packages in a mono-repo.

### Tip #8 - Free Tools Available, Use Them

Packaging and metadata dependencies can be difficult when starting to modularize your org. I’ve listed some of the useful tools native to Salesforce and open-source that will help you make the journey a lot less difficult during dependency impact analysis and package creation. There will always be more tools in the marketplace that are introduced but use these to start. If anyone knows of any visualization tools that work on top of these tools, drop me a message and would love to hear how you use it.

* [Dependency CLI Plugin](https://github.com/forcedotcom/dependencies-cli)&#x20;
* [happysoup.io](https://github.com/pgonzaleznetwork/sfdc-happy-soup#happysoupio)&#x20;
* [Where is this used?](https://help.salesforce.com/s/articleView?id=sf.fields\_references.htm\&type=5)&#x20;
* [Create a Package](https://developer.salesforce.com/docs/atlas.en-us.packagingGuide.meta/packagingGuide/creating\_packages.htm)&#x20;
* [force:source:manifest:create](https://developer.salesforce.com/docs/atlas.en-us.240.0.sfdx\_cli\_reference.meta/sfdx\_cli\_reference/cli\_reference\_force\_source.htm#cli\_reference\_force\_source\_manifest\_create)&#x20;
* [Salesforce Validation Errors re: Deployments](https://salesforce.stackexchange.com/questions/tagged/deployment)

### Tip #9 - Greenfield vs. Brownfield - Different Levels of Effort, Same End Game

The challenge to modular development differs when you are doing it in a brand new Salesforce Instance (Greenfield) or an existing Salesforce Instance that has been in Production for one or more years (Brownfield). A comprehensive playbook on how to execute this is way beyond the scope of this blog as there are different variables in play such as business stakeholder alignment, team size and skill sets, tooling ecosystem, Salesforce licenses/modules, and many other factors. Greenfield implementations are much easier to modularize as they are not impacted by existing production users. Brownfields require more planning, commitment, and investments from both business and IT teams to be successful. Both have the same end goals for modularity but timelines will vary depending on the urgency business stakeholders want it completed. I will highlight some high level tasks and ideas for teams to consider for each type of scenario below.

**Greenfield**

* Invest in training and upskilling on SFDX to all new and existing team members
* Organizing your packages into the following high level grouping and continue to iterate as requiredOrganizing your packages into the following high level grouping and continue to iterate as required
  * Business Domains&#x20;
  * Technical Frameworks&#x20;
  * Source Packages for UI Shared Components and Access Management&#x20;
  * Data Packages for Record Based Configurations and Sample Test Data
* Leverage [templates](https://docs.dxatscale.io/scm/repository-structure) for your mono-repo where possible to get started
* Mono-Repository - See Tip #4
* Implement Scratch Org Pooling (Leverage Org Shape as needed) - See Tip #5
* Enforce Governance Day One
  * Source of Truth is the Repository&#x20;
  * Left to Right Deployment Across Environments&#x20;
  * Well Documented Runbooks for Manual Steps and Environment Refreshes&#x20;
  * Restrict Access to Configure/Deploy to Environments to select few admins and service accounts executing pipelines&#x20;
  * Alignment of Peer Review Process, Pull/Merge Request Approval Process&#x20;
  * Each module must be 100% deployable and pass test class coverage and test runs
* Form Architecture S.W.A.T team and conduct frequent design reviews for packages
* Use Source Packages First and Progress to Unlocked Packages once team is comfortable

**Brownfield**

* Create an inventory list of your entire metadata (both managed package metadata and custom metadata)&#x20;
* Review all currently installed managed packages and unlocked (if any) in your org Identify applications that require Records Based Configurations that drive business logic and account for it in the design for refactoring&#x20;
* Review Technical Frameworks such as Trigger Factories, Error Handling, Logging, and Integration to see potential impacts during modularization&#x20;
* Identify low-hanging fruit applications that are standalone and do not use too much standard objects and fields
* Re-factor access management design such as Profiles, Permission Sets, and Permission Sets. Refer to this [blog](https://www.linkedin.com/pulse/version-controlling-profiles-why-makes-sense-deployments-vu-ha/) for tips.&#x20;
* Create high-level buckets for metadata and experiment with source package deployment and validations to Scratch Orgs and Sandboxes. Resolve dependencies as they are introduced and split packages as needed.&#x20;
* Explore option of re-created new repository from scratch and integrating new features/production fixes into source packages until the entire metadata components are represented in your org but now modularized

### Tip #10 - Campaign, Educate, and Invest in Your People for Modular Development

To be successful, everybody in the organization needs to be onboard with the transition to modular development and the benefits there are to be capitalized on. From Architects to Developers, Business Stakeholders to C-Suite Executives, and Admins to Testers, everybody needs to be educated on why shifting away from the org-based delivery model needs to occur. This reset in mindset is critical to move forward. Sharing this blog is a start to provide people with no-background on the topic.

The next step once commitment is made, is to continue to collaborate and stay informed with updates from Salesforce and the Trailblazer and Open Source community on innovations and updates are released weekly. Invest in your developer experience and everybody will benefit from the outputs.

Keep these benefits in mind as you campaign:

* Smaller packages and modular components are easier to learn, and onboard new developers&#x20;
* Architects will have full visibility in the org through your modular package design like a Table of Contents to quickly focus and pinpoint areas of improvements&#x20;
* Provides cohesion and ownership across teams as they will always evaluate how their feature/contribution will impact the entire org, not just their set of metadata.

## **Roadblocks to Modular Development Serendipity on Salesforce**

There will always be challenges to learn and adopt new approaches to doing software development.  The following table below highlights some of the noticeable technical and non-technical challenges when approaching discussions to using SFDX and modular design.

| Technical Challenges                                                                 | Non-Technical Challenges                                                                     |
| ------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------- |
| Package Dependencies and Deployment Sequencing                                       | Package Ownership Across Business Domains                                                    |
| Metadata Coverage and Unsupported Metadata Types                                     | Governance and Enforcement                                                                   |
| SFDX CLI (Bugs, Depreciation of Commands, SF CLI Unification)                        | Resource Skills Gaps                                                                         |
| Scratch Org Creation (eg. Feature/Settings Support and Instability, License Limits)  | Metadata History (Who and why did we build this metadata?)                                   |
| DevHub Package Creation and Versioning (Performance Issues, Unknown\_Exception)      | Value Proposition                                                                            |
| Salesforce Release Compatibility Issues                                              | Lack of Runbooks and Sandbox Refresh Steps                                                   |
| Records Based Configurations                                                         | Reluctance to change mindset from Traditional Salesforce Low Code and Pro Coder              |
| Data Loads                                                                           | Custom Scripts vs. Open Source DevOps Debates                                                |
| Technical Debt and Refactoring                                                       | Investment into Developer Experience                                                         |
| Test Class Coverage Re-Factoring                                                     | Licenses (Scratch Org Limits, Developer Licenses in Production)                              |
| APEX recompilation times in Production Orgs for each Unlocked Package Installation   | Suck Costs for existing Procured Salesforce DevOps Tools supporting Org-Based Delivery Model |
| Fast Feedback for Pull/Merge Requests Validations                                    |                                                                                              |
| Additional Scripting/Bash Scripts                                                    |                                                                                              |
| Deprecating and Moving Ownership of Metadata Across Packages                         |                                                                                              |
| Future Proof for SF CLI Unifications                                                 |                                                                                              |

Change is not always easily accepted by teams. The fact is, no solution will ever be perfect on Salesforce due to lack of support for 100% metadata coverage on the platform. Applying modular design principles to Salesforce projects is just one step in a series of process improvements teams should explore to re-imagining how they operate on the platform in the short term and long term. Custom deployment scripts, test automations tooling that are repurposed to perform repeatable point and click configurations for deployments are all nice to have and invest in but if you don’t have a sound architecture design for your code base, you will continue to experience issues.

## **Final Thoughts**

To wrap things up, let’s revisit the initial reasons why modular development is still at its infant stages and what can be done to change this going forward.

1. **Complexity**
   * Start small, evolve, experiment, learn and apply concepts from the open-source community. It will get easier the more you practice.
2. **Precedent**
   * Success stories exist from the open-source community and [Dreamforce Presentations](https://www.salesforce.com/plus/experience/Dreamforce\_2022/series/Architects/episode/episode-s1e7/) from 2022. It has been done and programs are reaping the benefits from it.  Don’t fall behind.
3. **People**
   * Invest and upskill to improve Developer Experience and empower both low code and pro coders to work in collaboration for modular developers to make it the default default delivery model going forward. Happy Developers, Happy Ecosystem.

Modularization in Salesforce requires breaking out of your comfort zone and challenging the “norm” of org based development. To continue to grow, we must try new things and with patience, persistence and practice, developing in a modular fashion will become the norm, not the outlier.

Good luck on your journey and welcome to the new renaissance.

## References

* [Salesforce Well Architected - Trusted, Easy, Adaptable ](https://architect.salesforce.com/well-architected/overview)
* [DX@Scale ](https://www.dxatscale.io/)
* [Evolution of a Salesforce Org](https://www.youtube.com/watch?v=0cL0rBXe1lg)&#x20;
* [Salesforce DX Developer Guide](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_intro.htm)&#x20;
* [SFDX DevOps Starter Pack Trailmix](https://trailhead.salesforce.com/users/dxatscale/trailmixes/sfdx-devops-starter-pack)&#x20;
* [Salesforce Developer Tooling Learning Map](https://developertoolinglearningmap.herokuapp.com/)
