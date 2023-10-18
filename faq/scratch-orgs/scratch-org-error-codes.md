---
description: >-
  If scratch org creation fails, the system generates an error code that can
  help you identify the cause.
---

# Scratch Org Error Codes

<table><thead><tr><th width="187">Error Code</th><th>Description</th></tr></thead><tbody><tr><td>C-9998</td><td>Not a valid scratch org. Contact Salesforce Customer Support for assistance.</td></tr><tr><td>C-9999</td><td>Generic fatal error. Contact Salesforce Customer Support for assistance.</td></tr><tr><td>S-1017</td><td>Namespace isn’t registered. To use a namespace with a scratch org, you must link the Developer Edition org where the namespace is registered to a Dev Hub org. See Salesforce Help: <a href="https://help.salesforce.com/articleView?id=sfdx_dev_reg_namespace.htm&#x26;language=en_US">Link a Namespace to a Dev Hub Org</a>.</td></tr><tr><td>S-2006</td><td>Invalid country.</td></tr><tr><td>SH-0001</td><td>Can't create scratch org from org shape. Contact the source org admin to add your Dev Hub org ID. From Setup, in the Quick Find box, enter Org Shape, and then select <strong>Org Shape</strong>.</td></tr><tr><td>SH-0002</td><td>Can't create scratch org. No org shape exists for the specified sourceOrg. Create an org shape and try again.</td></tr><tr><td>SH-0003</td><td>Can't create scratch org from org shape. The org shape version is outdated. Recreate the org shape and try again.</td></tr><tr><td>SH-9999</td><td>Can’t validate org shape due to fatal error. Contact Salesforce Customer Support for assistance.</td></tr></tbody></table>

{% hint style="info" %}
**Source:** [Salesforce DX Developer Guide - Scratch Org Error Codes](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_scratch\_orgs\_error\_codes.htm)
{% endhint %}
