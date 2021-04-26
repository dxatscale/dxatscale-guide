# Refreshing Sandboxes

When refreshing sandboxes from production, care must be taken to address the following concerns, a [runbook](../scm/tracking-manual-steps.md) should be maintained which addresses the below areas. Also care must be taken when refreshing sandboxes with license type partial copy and full copy as they have refresh dates associated. They should be scheduled along with the testing team to make the most out of it.

![Sandbox Refresh Interval](../.gitbook/assets/image%20%2850%29.png)

* **Users** 
  * When sandbox is created, typically all users email address get suffixed with instance name to prevent emails from being sent to actual users. This is automatically taken care by the Salesforce refresh process. Some users such as developers or admins would need to have their email reset. This can only be done by the user who initiated the refresh of the sandbox.
* **Single Sign On**
  * Check whether there is a need to turn off  SSO \(Single Sign On\) in all profiles, if the refreshed org is not to be set up with SSO. 
  * Update the SSO Delegated URL in case the refresh org need to be set up with SSO.
  * Check the end-point URLs In case of any SSO applications \(outbound messages etc.\)
* **Custom Settings**
  * Custom Settings will point to the data available in production. It has to be reset to non-prod values
* **Workflows**
  * From Adress of Workflows will be reset to production
* **Emails**
  * DX@Scale practice is to use different From Email address using "Organization-Wide Email Addresses" setting for each sandboxes. This can be done using **aliasifed**  source packages. This package could be redeployed after a refresh
  * Remove/Change the additional email addresses e.g "cc" fields \(which are mostly real users\), for workflows \(Email alerts\)
  * Update Email Links in Email templates from [https://login.salesforce.com](https://login.salesforce.com/)  to [https://test](https://test/)  [salesforce.com](http://salesforce.com/) 
  * Mask Email type fields from Lead, Case, Contact, Opportunity objects \(This list will depend upon the most used Objects in respective project\).
  * Check If Queue's has an email address from non-production
  * Email deliverability usually after refresh it reflects “System Only Email” instead of “All Email”
* Check for the site URLs which might be pointing to production rather than non prod environments
* **Emails**
  * Reconfiguration of Connected-Apps with non-prod cert which will be required for the JWT …etc. based on project requirements
  * Update the pipelines with new keys if the environment is connected to the CI/CD pipelines. 
* Community publish \(if applicable\) 
* Execute Post Steps as per the project requirements, since the Dev/Dev-Prod sandboxes will have only metadata, to bring the env to shape and make available for Devs/Testers, this step will be required

Read more about refreshing Partial or Fully Copy Sandboxes here [https://help.salesforce.com/articleView?id=000313358&type=1&mode=1](https://help.salesforce.com/articleView?id=000313358&type=1&mode=1)

