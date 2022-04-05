---
description: The DX@Scale Developer Toolkit
---

# sfpowerkit

A Salesforce DX Plugin with multiple functionalities aimed at improving development and operational workflows



### Installation

To install the stable version from the release branch, use the following command

```
$ sfdx plugins:install sfpowerkit
```

If you need to install automatically the plugin, via a CI process or Dockerfile, use the following line:

```
$ echo 'y' | sfdx plugins:install sfpowerkit
```

Beta versions are the latest versions that are in being reviewed/ undergoing testing etc and built from the master branch and can be downloaded using the following command

```
$ sfdx plugins:install sfpowerkit@beta
```

To review a pull request (for contributors/reviewers), the best option is to clone the repository, checkout to the particular branch and utilize the following command from the project directory

```
$ sfdx plugins:link
```
