# Publish and Release your artifacts

### **Learning Objectives**

* What is an artifact?
* How to publish artifacts to an artifact registry?
* How artifacts are used  by orchestrator?

**Time to complete:** 40 minutes

### Steps

#### Read more about artifacts and how it is being used in the [link](https://dxatscale.gitbook.io/sfpowerscripts/faq/artifacts) 

#### Create a Personal Access token to publish packages to Github Package manager

Follow the [link](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token) to create  a personal access token in Github 

Ensure the following [scopes](https://docs.github.com/en/packages/learn-github-packages/about-permissions-for-github-packages#about-scopes-and-permissions-for-package-registries) are added to your personal token

Authenticate to github package registry using the following command

```text
$ npm login --scope=@OWNER --registry=https://npm.pkg.github.com

> Username: USERNAME
> Password: TOKEN
> Email: PUBLIC-EMAIL-ADDRESS
```

#### Publish your packages to Github Package Registry

```text
sfdx sfpowerscripts:orchestrator:publish -d artifacts --npm --scope <your_github_org_name> --npmrcpath <path_to_your_npmrc> --gittag --pushgittag
```

Notice how the packages are published into you repo.

#### Utilize Release command to orchestrate deployments at ease

Create a release definition file in your root of your repository. Information on creating release definition is available at this [link](https://dxatscale.gitbook.io/sfpowerscripts/commands/release)

Ensure all your external dependencies are marked in your release defintion file

Create a new scratch org and run the release command

Ensure the sfpowerscripts prerequisite package is installed into your org

```text
sfdx sfpowerscripts:orchestrator:release -u <SO_ALIAS> -p .releaseDefinition.yml --npm --scope <GITHUB_ORG_NAME> --generatechangelog
```

Delete the artifacts directory in your folder

Notice how the release command install all the dependencies,  deploy all the packages directly and generate changelog

### Recap 

This module helps you understand how sfpowerscripts can be utilized to orchestrate relases across multiple orgs



