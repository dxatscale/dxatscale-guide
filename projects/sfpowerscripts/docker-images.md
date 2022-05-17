---
description: Using docker images in your CI/CD
---

# Docker Images

Put simply, the sfpowerscripts Docker image will allow you to run your builds / releases within a container, which is like a virtualized environment running on a physical system and has its own OS, apps etc. For more information on Docker and containerization, visit [Docker's documentation](https://docs.docker.com).

The sfpowerscripts Docker image is available at:

* [**Docker Hub**](https://hub.docker.com/r/dxatscale/sfpowerscripts)
* [**GitHub Container Registry** ](https://github.com/orgs/dxatscale/packages/container/package/sfpowerscripts)**(Recommended)**

We recommend using the sfpowerscripts Docker image because it will grant your CICD pipelines **greater reliability** - avoiding breakages due to updates in sfpowerscripts or its dependencies (e.g. SFDX CLI, SFDMU). Each sfpowerscripts image has static versions of sfpowerscripts and its dependencies, which means that it will not be affected by any updates.

Utilizing the sfpowerscripts Docker image will give you the surety that your **builds are consistently running in the same environment** - meaning that you can safely assume that discrepancies between builds are not a result of environment setup.

Most of all, the sfpowerscripts Docker image makes things easy. We have already done all the hard work of creating an image that has all the required dependencies installed (Node, JDK, sfpowerkit, sfdmu, etc.). All that is required from you is to pull the image from the registry and run it.

To use this docker in your CI/CD Pipelines, please check the documentation of your CI/CD provider.

Docker Images released through Github are signed. You can utilize the below public key to check the accuracy of the image. You can use cosign to verify the signature

`cosign verify --key cosign.pub ghcr.io/dxatscale/sfpowerscripts:latest`

For more information on signed docker images, click on the link below

[https://github.blog/2021-12-06-safeguard-container-signing-capability-actions/](https://github.blog/2021-12-06-safeguard-container-signing-capability-actions/)

{% file src="../../.gitbook/assets/cosign.pub" %}
`Public Key for verifying signature`
{% endfile %}

Checkout below samples

{% tabs %}
{% tab title="GitHub Actions" %}
```
name: sfpowerscripts prepare

# Definition when the workflow should run
on:
    workflow_dispatch:
    schedule:
        - cron: '0 0 * * *'

# Read more about using contaniers
# https://docs.github.com/en/actions/guides/about-service-containers

# Jobs to be executed
jobs:
    prepare:
        runs-on: ubuntu-latest
        container: ghcr.io/dxatscale/sfpowerscripts
```
{% endtab %}

{% tab title="Azure Pipelines" %}
```
pool:
    vmImage: 'ubuntu-latest'

# Specify a container job to use the docker image. Read more about using 
# container jobs at https://docs.microsoft.com/en-us/azure/devops/pipelines/process/container-phases?view=azure-devops

container: ghcr.io/dxatscale/sfpowerscripts:latest
```
{% endtab %}
{% endtabs %}
