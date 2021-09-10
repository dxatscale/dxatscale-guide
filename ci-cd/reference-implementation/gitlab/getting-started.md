# Getting Started

The following getting started guide will enable you to configure and setup CI/CD using GitLab and DX@Scale for Salesforce.  Assuming you have reviewed and completed the prerequisite account setup and software tool installations, this guide will walk you through the initial setup process for the GitLab template and provide some general tips as you customize it for your implementation.

We welcome any feedback from the community to continuously improve upon this user guide so please [contact us](https://docs.dxatscale.io/about-us/contact-us) for any questions or concerns.

## Developer Workstation

In order to successfully troubleshoot and interact with GitLab and Salesforce using the CLI, the following commands should be executed on your computer to validate you have the tools configured correctly.  Depending on your workstation operating system \(eg. **Mac OS, Windows, Linux**\), there may be some variation in the commands and outputs below.

###  A. Git

```bash
git version
> git version 2.32.0
```

### B. SFDX CLI

```bash
sfdx version
> sfdx-cli/7.110.0 darwin-x64 node-v16.6.0
```

### C. SFDX Plugins

```bash
sfdx plugins
> @dxatscale/sfpowerscripts 8.2.1
  sfdmu 4.4.5
  sfpowerkit 3.2.2
```

### D. Visual Studio Code

```bash
code --version
> 1.60.0
e7d7e9a9348e6a8cc8c03f877d39cb72e5dfb1ff
x64
```

### E. NPM

```bash
npm --version
> 7.19.1
```

## Salesforce

To enable modular package development, there are a few configurations in Salesforce that needs to be enabled.  

### A. Enable Dev Hub

1. Navigate to the **Setup** menu
2. Go to **Development &gt; Dev Hub**
3. Toggle the button to on for **Enable Dev Hub**

![](../../../.gitbook/assets/image%20%281%29.png)

### B. Enable Unlocked Packages and Second-Generation Managed Packages

1. Navigate to the **Setup** menu
2. Go to **Development &gt; Dev Hub**
3. Toggle the button to on for **Enable Unlocked Packages and Second-Generation Managed Packages**

![](../../../.gitbook/assets/image.png)

## GitLab: Part I

## Repository

## GitLab: Part II



```
$ give me super-powers
```

{% hint style="info" %}
 Super-powers are granted randomly so please submit an issue if you're not happy with yours.
{% endhint %}

Once you're strong enough, save the world:

{% code title="hello.sh" %}
```bash
# Ain't no code for that yet, sorry
echo 'You got to trust me on this, I saved the world'
```
{% endcode %}



## Closing Thoughts

Good luck on your journey.

