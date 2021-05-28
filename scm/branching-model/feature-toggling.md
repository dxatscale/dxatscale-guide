# Feature Toggling

Feature Toggles allow new components and changes to be deloyed in an inactive state and enabled at a time when stakeholders or technical dependencies are ready.

This pattern can decouple the risk and logistics of the deployment itself from the business considerations involved in adopting a new feature, and helps to support the practice of small and frequent deployments.

### App Logic - Configuration: Validation Rules, Workflow, Process Builder, Lightning Flow <a id="user-content-app-logic---configuration%3A-validation-rules%2C-workflow%2C-process-builder%2C-lightning-flow"></a>

Use a Custom Metadata Type to define one or more feature activation flags \(i.e. one for the release or one per feature, depending on granularity needed\). This can then be referenced in the following to dynamically activate configuration:  
Formula fields \(e.g. AND\($CustomMetadata.FeatureActivation\_\_mdt.MyFeature.IsActive\_\_c, \[my\_condition\]\)  
Workflow, Process Builders and Visual Workflows \(branching condition that checks the met value as shown above\)

### App Logic - Code <a id="user-content-app-logic---code"></a>

* Use a Trigger Framework which allows for deactivation of any given trigger handler via a Custom Metadata Type or Custom Permission. [Apex Trigger Actions](https://github.com/mitchspano/apex-trigger-actions-framework) and [Nebula Triggers](https://bitbucket.org/nebulaconsulting/nebula-core/src/master/) are examples of open source framerworks which provide this capability
* Apex REST services should return an appropriate error if code is not active \(e.g. “Service Inactive”\)

### UI: Page Layouts, Lightning Pages \(Flexipages\) and Components <a id="user-content-ui%3A-page-layouts%2C-lightning-pages-(flexipages)-and-components"></a>

* Use App assignment to allocate pages to a given App then only allocate that app to a Permission Set that is assigned when your feature is active
* Use a Custom Permission to set visibility on components added to a shared flexipage, add the custom permission to the permission set mentioned above
* For Page Layouts, create a new Layout for your feature, activation/deactivation will be managed by profile assignment
* [The Feature Flag Designs](https://github.com/tsalb/feature-flag-designs) open source framework provides rich capabilities for dynamically switching features using custom permissions and apex dependency inversion

### Sharing Rules / OWD’s <a id="user-content-sharing-rules-%2F-owd%E2%80%99s"></a>

These will be left active unless there are clear impacts from this approach \(this assumes features that are inactive are not fundamentally changing the security or sharing model of core objects such as Account or Case in a way that impacts existing user groups\)

### Apex Managed Sharing <a id="user-content-apex-managed-sharing"></a>

Use a sharing framework that is metadata driven and caters for dormancy. The open source apex sharing framework [FormulaShare](https://github.com/LawrenceLoz/FormulaShare-DX) operates through metadata-driven rules which can be deployed in a disabled state until required

### Other <a id="user-content-other"></a>

* CI/CD pipelines and automated testing will need to setup to adjust to this, as code will be deployed dormant to some environments but active to others, this also means maintaining a separate ‘active’ or ‘dormant’ set of artefacts to enable this. Alternatively features are manually enabled/disabled.
* Cleanup effort is required post activation - for example we will want to remove references to feature toggles in validation rules and workflows once live as if we do not these statements will continue to proliferate throughout the environment

