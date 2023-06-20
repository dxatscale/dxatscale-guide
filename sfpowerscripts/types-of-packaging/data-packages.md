# Data Packages

Data packages are a sfpowerscripts construct that utilise the [SFDMU plugin](https://github.com/forcedotcom/SFDX-Data-Move-Utility) to create a versioned artifact of Salesforce object records in csv format, which can be deployed to the a Salesforce org using the sfpowerscripts package installation command.

The Data Package offers a seamless method of integrating Salesforce data into your CICD pipelines , and is primarily intended for record-based configuration of managed package such as CPQ, Vlocity (Salesforce Industries), and nCino.

## Benefits of Data Packages over using SFDMU Scripts directly

Data packages are a wrapper around SFDMU that provide a few key benefits:

* **Ability to skip the package if already installed:** By keeping a record of the version of the package installed in the target org with the support of an unlocked package, sfpowerscripts can skip installation of data packages if it is already installed in the org
* **Versioned Artifact:** Aligned with sfpowerscripts principle of traceability, every deployment is traceable to a versioned artifact, which is difficult to achieve when you are using a folder to deploy
* **Orchestration:** Data package creation and installation can be orchestrated by sfpowerscripts, which means less scripting

## Defining a Data package

Simply add an entry in the package directories, providing the package's name, path, version number and type (data). Your editor may complain that the 'type' property is not allowed, but this can be safely ignored.

```
  {
    "path": "path--to--data--package",
    "package": "name--of-the-data package", //mandatory, when used with sfpowerscripts
    "versionNumber": "X.Y.Z.0 // 0 will be replaced by the build number passed",
    "type": "data", // required
    "postDeploymentScript":"path--to--script" // script such as populating the record ID to custom setting after data package is loaded
  }
```

## Generating the contents of the data package

Export your Salesforce records to csv files using the [SFDMU plugin](https://github.com/forcedotcom/SFDX-Data-Move-Utility). For more information on plugin installation, creating an export.json file, and exporting to csv files, refer to _Plugin Basic > Basic Usage_ in SFDMU's [documentation](https://help.sfdmu.com/quick-start).

![](<../../.gitbook/assets/image (9).png>)

## **Options with Data Packages**

Data packages support the following options, through the sfdx-project.json.

```
  {
    "path": "path--to--package",
    "package": "name--of-the-package", //mandatory, when used with sfpowerscripts
    "versionNumber": "X.Y.Z.[NEXT/BUILDNUMBER]",
    "type": "data", // required
    "aliasfy": <boolean>, // Only for source packages, allows to deploy a subfolder whose name matches the alias of the org when using deploy command
    "assignPermSetsPreDeployment: ["","",],
    "assignPermSetsPostDeployment: ["","",],
    "preDeploymentScript":<path>, //All Packages
    "postDeploymentScript":<path> // All packages
  }
```

## Adding Pre/Post Deployment Scripts to Data Packages

Refer to this [link](../orchestrator.md#executing-pre-post-deployment-scripts) for more details on how to add a pre/post script to data package

```
# $1 package name
# $2 org
# $3 alias
# $4 working directory
# $5 package directory

sfdx force:apex:execute -f scripts/datascript.apex -u $2
```

## Defining a vlocity Data Package

sfpowerscripts support vlocity RBC migration using the vlocity build tool (vbt). sfpowerscripts will be automatically able to detect whether a data package need to be deployed using vlocity or using sfdmu. (Please not to enable vlocity in preparing scratchOrgs, the enableVlocity flag need to be turned on in the pool configuration file)

![Defining a vlocity data package](<../../.gitbook/assets/image (72).png>)

A vlocity data package need to have vlocityComponents.yaml file in the root of the package directory and it should have the following definition

```
projectPath: src/vlocity-config // Path to the package directory
expansionPath: datapacks // Path to the folder containing vlocity attributes
autoRetryErrors: true //Additional items
manifest:
```

The same package would be defined in the sfdx-project.json as follows

```
        {
            "path": "./src/vlocity-config",
            "package": "vlocity-attributes",
            "versionNumber": "1.0.0.0",
            "type": "data"
        },
```
