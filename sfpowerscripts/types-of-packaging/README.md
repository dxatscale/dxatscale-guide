# Types of Packaging

The following pages help you understand the correct packaging technique depending on the metadata/functionality

{% content-ref url="unlocked-packages.md" %}
[unlocked-packages.md](unlocked-packages.md)
{% endcontent-ref %}

{% content-ref url="source-packages.md" %}
[source-packages.md](source-packages.md)
{% endcontent-ref %}

{% content-ref url="data-packages.md" %}
[data-packages.md](data-packages.md)
{% endcontent-ref %}

A short summary of various package types are provided below

| Features                                           | Unlocked Packages                                                                                                | Org Dependent Unlocked Packages                                                                                  | Source Packages                                                                                                                                         | Data Packages                      |
| -------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| Dependency Validation                              | Occurs during package creation                                                                                   | Occurs during package installation                                                                               | Occurs during package installation                                                                                                                      | N/A                                |
| Dependency Declaration                             | Yes                                                                                                              | Yes (supported by sfpowerscripts)                                                                                | Yes                                                                                                                                                     | Yes                                |
| Requires dependency to be resolved during creation | Yes                                                                                                              | No                                                                                                               | No                                                                                                                                                      | N/A                                |
| Supported Metadata Types                           | Unlocked Package Section in [Metadata Coverage Report](https://developer.salesforce.com/docs/metadata-coverage/) | Unlocked Package Section in [Metadata Coverage Report](https://developer.salesforce.com/docs/metadata-coverage/) | <p>Metadata API<br>Section in <a href="https://developer.salesforce.com/docs/metadata-coverage/">Metadata Coverage Report</a></p>                       | N/A                                |
| Code Coverage Requirement                          | Package should have 75% code coverage or more                                                                    | Not enforced by Salesforce, sfpowerscripts by default checks for 75% code coverage                               | Each apex class should have a coverage of 75% or above for optimal deployment, otherwise the entire coverage of the org will be utilized for deployment | N/A                                |
| Component Lifecycle                                | Automated                                                                                                        | Automated                                                                                                        | Explicit, utilize destructiveManifest.                                                                                                                  | N/A                                |
| Component Lock                                     | Yes, only one package can own the component                                                                      | Yes, only one package can own the component                                                                      | No                                                                                                                                                      | N/A                                |
| Version Management                                 | Salesforce enforced versioning; Promotion required to deploy to prod                                             | Salesforce enforced versioning; Promotion required to deploy to prod                                             | sfpowerscripts enforced versioning                                                                                                                      | sfpowerscripts enforced versioning |
