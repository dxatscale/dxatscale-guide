---
description: Current Principles followed by DX@Scale practitioners
---

# Principles

## 1. Version Control is the Source of Truth

Any aspect of code or config that gets deployed into a Salesforce org should be traceable to an artifact built from a point in time from a source code repository. The artifact should have a name, version number and an associated lifecycle. 

## 2.  Developer Productivity is Paramount

DX@Scale projects will strive to improve developer productivity by ensuring ease of usability for these practices and frameworks.

## 3. Limit Batch Size

Every DX@Scale Practitioner will follow a concept of build/deployment budget.  They will look to minimize the duration of which a feature branch lives and strive to do whatever they can to keep these attributes in check across their packages.   

## 4. Loosely Coupled Architecture

DX@Scale Practitioners will design their modules in such a way that it reduce the inter-dependencies, facilitate integration, deployment and test.

## 5. Automate Manual Deployment Steps

Recurring manual steps hampers the path to production by making it unaffordable to deploy at will.  This is one of the major reasons why Salesforce deployments are infrequent and batched together. DX@Scale practitioners will remove any such recurring manual steps, by designing the code or config around it or introduce automation using a variety of techniques.

## 6. Continuous Emphasis on Reducing Technical Debt

Technical debt can arise in various forms.  It can be a functional element that can be realized differently or short cuts that have taken to release a feature. DX@Scale emphasizes technical debts will always be prioritized along with other development and due care will taken to mitigate it.

## 7. Traceability, Repeatability and Accountability

Artifacts, run books, and release notes are fundamental tools to enable complete visibility to changes in the environments.  Ensure the team adheres to the DevOps governance process and configuration changes outside the deployment pipeline are documented consistently to refer to historically as needed. 

