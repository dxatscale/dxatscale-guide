---
description: Current Principles followed by DX@Scale practitioners
---

# Principles

## 1. Version Control is the source of truth

Any aspect of code or config that gets deployed into a Salesforce org should be traceable to an artifact built from a point in time from a source code repository. The artifact should have a name, version number and an associated lifecycle. 

## 2.  Developer productivity is paramount

DX@Scale projects will strive to improve developer productivity  by ensuring ease of usability for these practices and frameworks

## 3. Limit Batch Size

Every DX@Scale practitioner will follow a concept of build/deployment budget and also minimizes the duration which a feature branch lives, they will strive to do whatever they can to keep these attributes in check 

## 4. Loosely Coupled Architecture

DX@Scale practitioners will design their modules in such a way that it reduce the inter-dependencies, facilitate integration, deployment and test

## 4. Automate Manual Deployment

Recurring manual steps hampers the path to production by making it unaffordable to deploy at will.  This is one of the major reasons why Salesforce deployments are always batched. DX@Scale practitioners will remove any such recurring manual steps, by designing the code or config around it or introduce automation using variety of techniques

## 5. Continuous Emphasis on reducing technical debt

Technical debt can arise in various forms, be it a functional element that can be realized differently or it could be short cuts that have taken to release a feature. DX@Scale emphasise technical debts will always be prioritized along with other development and due care will taken to mitigate it

