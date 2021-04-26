# Syncing Changes from Production \[DRAFT\]

Salesforce is a SaaS based lowcode platform, where changes in production is directly allowed. Large scale programs especially like the one's used with DX@Scale, typically discourages changing any attribute in production directly. However there are certain components which is allowed to change directly in production and there might be some specific instances where components are directly changed in production

### Components Allowed to be changed in Production Org

* **Reports/Dashboards** :  We allow admins or users with sufficient permissions to create reports/dashboards directly in prod, as long as they do not modify any reports that are delivered by the development teams. The Reports/Dashboards that are delivered by development teams are either built to a spec or should be treated as a template
* Changes to most  [Org specific Metadata](../scm/dealing-with-sensitive-metadata/):  As mentioned in the earlier section, most of these settings are not captured in version control and would directly need to be changed in production

### Hotfixes in Production

DX@Scale disallows any changes in production directly. However, in the extreme cases, where it is required, admins are allowed to change the particular entity and immediately raise an equivalent pull request detailing the approach

#### Identifying changes in Production and retrofitting to Repository



