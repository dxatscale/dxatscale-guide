# Data Package

### Why isn't force:source:push working with Data packages defined in my sfdx-project.json?

The error arises because the Data Package contains csv files, which are not natively supported by Salesforce. In order to bypass the error, add the package path to the `.forceignore` file. This will not inhibit creation of Data packages.

### Why is the version number for data packages have to end with zero? Doesn't it support .NEXT?

At the moment, it is not supported and we have a bug where the .NEXT is not replaced by passed build number. So ensure that all your source packages in your repository has '0' as the build number
