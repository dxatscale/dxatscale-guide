---
description: 'Published on May 19, 2019 by Azlam Abdulsalam'
---

# Change Lead Time for DX Unlocked Packaging

One of the common challenges which are discussed by DX team’s is around the cycle time to get a change packaged up. Lets look at activities involved and the average time found in my experience

Change Lead Time is a commonly used metrics to track a DevOps team. You can read more on the common DevOps metrics here \( [https://devops.com/metrics-devops/](https://devops.com/metrics-devops/)\)

But for today’s discussion, to simplify lets define the change lead time as the time taken for a feature to be reflected in your testing sandbox, once you have started working on a story which has met the Definition of Ready and being assigned to you.

**Change Lead Time for a DX Unlocked Package** _**=**_

**Initializing scratch org for feature development** \( Installing Dependent Packages + Source Push + Test Data\)

+**Time for Feature Development**

**+Time Consumed for Pull Request/Merge Request Validation** \( Creating Scratch org on CI server, Installing Dependent Packages, Source Push, Automated Tests\)

**+** **Time consumed for a Pull/Merge Request Review**

**+Time consumed for Package Creation**

**+Time consumed for Package Installation in the target sandbox**

Let’s look into each of these steps into detail and later onto some tips on reducing this

#### **Initializing scratch org for feature development**

**Average Time Noticed so far in our projects with multiple dependencies and keeping managed package dependency to a minimum: 30 Minutes**

This activity includes, creation of a feature/topic branch and creating a scratch org for local development. This is often one of the most time consuming activities, where multiple dependent packages has to be installed \(including managed packages\), source codes have to be pushed and test data need to be created in the org.

As ‘snapshot’ feature for Scratch Org’s is not yet ready \(soon to be in pilot\), getting a scratch org created if you have a dependency on large managed packages often takes you an average time anywhere between 20 to 35 minutes to nearly 2 hours plus depending on the dependent packages being installed. Each package installation also triggers an entire org wide apex compilation \( more options are available in Summer 19\) adding to the delays. On top of this you need to push you current package in source format, along with test data if needed.

#### **Time for feature development**

**Average Time Noticed so far in our projects : X**

This is often dependent on the topic that is being developed and can go from an hour to few days including unit tests. Let’s keep this as the variable element in our discussion

#### **Time Consumed for Pull Request/Merge Request Validation** \( Creating Scratch org on CI server, Installing Dependent Packages, Source Push, Automated Tests\)

**Average Time Noticed so far in our projects : 30 Mins per each PR Validation Run and on an average 2 runs per topic branch ~~ 60 Mins**

One of the practices commonly followed in modern tech stack’s is the practice of pull/merge request validation where a virtual merge of topic/feature branch with mainline is validated before being submitted for review. This include running unit tests, static code analysers etc. Typically a developer wants to get a PR validated as fast as possible, to catch any errors in the submitted code or during integration and also to redo certain parts of the code on step 4, after a peer review. As most projects uses a lock down merge on the mainline, that a merge is allowed only after a valid PR and review, this is usually where a considerable amount of time is spent, so it gives plenty of opportunity for optimization.

During each of these run’s the CI system has to exactly do the steps as described in Step 1 \(Initializing Scratch Org\) and have additional validation steps to be run. This process is also run on a server, which means depending on your CI setup, there could be a queue before your PR gets triggered for a run.

#### **Time consumed for a Pull/Merge Request Review**

**Average Time Noticed so far in our projects : Y**

Again another variable activity as it depends on the team size, the person who is doing the review, and the practices that’s being followed\( is it just your tech lead, then queue on the lead, or a peer review process with multiple votes\)

#### **Time consumed for a Package Creation**

**Average Time Noticed so far in our projects : Average of 30 Minutes \( Highly dependent on the size of the package, and its dependents\)**

Assuming you have made your way after the merge to the mainline, then you are left with packaging of the project , where now Salesforce does exactly what what is being mentioned in Step 1 or Step 3 and provide us with the package id. This time will be roughly same as of your PR validation run’s

#### **Time consumed for Package Installation**

**Average Time Noticed so far in our projects : Average of 8 Minutes**

The last step of the journey is installing the package into the target org, This is often the quickest and mostly depends on the size of the apex in the target org, as package installation triggers a full compilation \(can be turned off in Summer 20\) and deploying the metadata. Provided the dependencies are already there in the target org, this is the easiest step.

So that leaves us with an average of **X+Y+100 Minutes \(** Loads of assumption here, 2 PR Run’s , average sized package with 1 managed package dependency and installation to one target org\). Eliminating the variables it leaves us with a 100 Minute for a new version to be in your test org..

In the next post, let’s look whether it’s worth it, what about traditional metadata deployment etc.

