---
description: 'Published on February 23, 2019 by Azlam Abdulsalam'
---

# Get the most out of your Salesforce DX Implementation - Part 2

This is a continuation of a series on learnings from my experience in implementing Salesforce DX on a large scale enterprise project. 

### 5. Fully realize the power of the open ecosystem of SFDX Plugins 

Salesforce DX brings an extensible command line interface, which is built on Heroku's Open CLI Framework \(oclif\). It also features a plugin generation command which generates the scaffolding if you want to write your own plugins. It has a lot of potential benefits such as not having your custom scripts parsing the output of CLI, jumbling around with authentication and ability to run this locally on a developer machine without worrying about update mechanism etc And most of the plugins are open source, so you can always checkout the code and understand, modify and fix.  

**Tip**: Use some awesome plugins such as [shane](https://github.com/mshanemc/shane-sfdx-plugins), [texei](https://github.com/texei/texei-sfdx-plugin), [etcopydata ](https://github.com/eltoroit/ETCopyData)to automate some mundane tasks 

**Tip**: Periodically scan the npm.js repo for discovering new sfdx plugins. 

**Tip**: As with any open source projects, have a look at the source code, activity etc. before making it as a core part of your deployment workflow. As always do remember of 'System of Development' is as important as the 'System of Engagement' and 'System of Record' that you are trying to build using Salesforce :\)

### 6. Managing dependencies between packages can be a bit challenging, Do not fret it, it's not that big a deal 

 As I have discussed earlier, adopting unlocked packages has a lot of potential benefits in managing the Org in the long run, especially as your Org grows. 'Unlocked' package provides ownership of the metadata that it contains and one doesn't need to be worried on subsequent releases of other packages impacting this one, thus reducing the testing overhead compared to an Org based development.

Ideally, you want your packages to be independent as possible, often modelling around domains. Use techniques such as Bounded Context from Domain Driven Design to figure out how to organize your packaging. Alternatively, if you are starting fresh, organize your packages around the core business functionalities that you are delivering supported by shared schema and tech enablement packages, the key here is not to go too modular and not broad.  

If you are an existing program and converting it to unlocked packages, start doing a bottom-up approach, figuring out the tech enablement layer and work upwards into the business layer.  

**Tip**: For programs that are starting new, follow a top-down approach for dependencies and organise your team around bounded contexts.  

**Tip**: Follow an app-centric packaging \(also it would help to have one app holding the majority of customization around an SObject than floating it around multiple apps\) rather than layering. Layering does not scale in the larger context. 

**Tip**: Rely on dependency injection for a downstream package to trigger code on a nondependent package. 

**Tip**: Use Platform Events to communicate between packages. There are some excellent videos on how to utilize such as this one, [Microservice Based Architecture Using Platform Events](https://youtu.be/FgCa1yPzVMw)

**Tip**: Use your PI planning/cross stream sprint planning or sprint shaping \(assuming you are doing agile\) to figure out the dependencies between streams and detail the contracts which each team is to produce/consume. Again lean back on the rest of the enterprise on best practices followed in programs such as Java/API/Web app development 

### 7. Build a RACI Matrix for each of the packages and communicate it early, so teams know who owns what and what is the process to update on a shared package 

Packages need ownership, there will be fixes and feature additions during the course of the program. As the team who would have initially contributed a lot to a particular package would have been moved onto attacking another business area, a clear strategy should be planned on transitioning the ownership of these built ones. Is it a shared ownership model? Is it transitioned to the ops team? Remember its no longer an org based development, where all the metadata and code lies in one giant repo, so draw up a RACI matrix, communicate and update it.

**Tip**: Treat the 'unpackageable' metadata as a core entity. Some of these are org-wide settings and also need to be treated diligently as of packages. 'Unpackaged' metadata that belongs to a particular package, can leave along with the package itself as a folder, which makes the ownership clear at least in the repo

### 8. Old habits die hard.. Ask the system team to take a step back once the pipelines are stable 

Salesforce DX brings a new set of practices and tools to Salesforce Development. As the system team builds the pipelines and the necessary tooling, it would be expected of them to provide support to the development team initially to assist with Git, CI/CD based deployment etc. However please ensure system team doesn't become a Salesforce Release/Deployment team \(as it was usually the process followed in most teams, a dedicated team takes care of pre/post steps, migration etc\) , rather equip the individual teams themselves to deploy and promote packages all through different environments and to production

### 9. Next time you buy a managed package, please check how easy is to deploy customizations across multiple environments

As with any addition to enterprise, do a due diligence on the managed packages that are introduced into the salesforce ecosystem, many vendor's have started adopting DX and has started providing CLI based tooling to migrate configuration data across environments. The big enterprise managed package players rely on complex data schemas and is often hard to migrated configuration data across environments. Don't forget to add deployment, release management etc to your evaluation criteria.

I am excited to hear more about your DX Journey. Please feel free to post on the comments / Salesforce DX Group on your queries regarding DX. I can also chime in along with other DX Trailblazers.

