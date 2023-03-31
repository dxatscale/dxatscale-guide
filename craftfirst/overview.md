# Overview

Craft-first is a collection of open source production ready libraries and frameworks built on our experience in delivering large DX@Scale Programs



## sfdc-feature-management

**A consistent way to check if features are enabled in apex**

Salesforce has multiple ways of determining if a user should have access to be able to perform a function, including but not limited to Custom Permissions, Custom Settings, Custom Metadata and Permission Sets/Profiles. This can result in codebases having multiple ways of dealing with granting access to features.

The goal of this project is to provide an abstraction on top of these different methodologies and provide a consistent API for apex to use. This library will also contain some common implementations as well as an extension point to add in your own implementations.

{% embed url="https://github.com/Craft-First/sfdc-feature-management" %}

## sfdc-trigger-framework

**Lightweight trigger framework**

There are many trigger frameworks out there that look to overcomplicate how we handle dml changes on our records. This library allows us to avoid writing boilerplate code in the triggers, providing the beginning of a clear separation of concern.

This library defines several interfaces that can be implemented in isolation.

{% embed url="https://github.com/Craft-First/sfdc-trigger-framework" %}

## **sfdc-trigger-bypass-strategy**

#### Simple Custom Setting Bypass for the sfdc-trigger-framework

This package implements a simple bypass strategy for the [sfdc-trigger-framework](https://github.com/Craft-First/sfdc-trigger-framework) based on a custom setting to define whether a specific trigger handler should be bypassed.

{% embed url="https://github.com/Craft-First/sfdc-trigger-bypass-strategy" %}

\
