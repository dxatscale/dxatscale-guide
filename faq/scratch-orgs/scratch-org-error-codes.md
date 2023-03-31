---
description: >-
  If scratch org creation fails, the system generates an error code that can
  help you identify the cause.
---

# Scratch Org Error Codes

| Error Code | Description                                                                                                                                                                                                                                                                                                         |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| C-9998     | Not a valid scratch org. Contact Salesforce Customer Support for assistance.                                                                                                                                                                                                                                        |
| C-9999     | Generic fatal error. Contact Salesforce Customer Support for assistance.                                                                                                                                                                                                                                            |
| S-1017     | Namespace isn’t registered. To use a namespace with a scratch org, you must link the Developer Edition org where the namespace is registered to a Dev Hub org. See Salesforce Help: [Link a Namespace to a Dev Hub Org](https://help.salesforce.com/articleView?id=sfdx\_dev\_reg\_namespace.htm\&language=en\_US). |
| S-2006     | Invalid country.                                                                                                                                                                                                                                                                                                    |
| SH-0001    | Can't create scratch org from org shape. Contact the source org admin to add your Dev Hub org ID. From Setup, in the Quick Find box, enter Org Shape, and then select **Org Shape**.                                                                                                                                |
| SH-0002    | Can't create scratch org. No org shape exists for the specified sourceOrg. Create an org shape and try again.                                                                                                                                                                                                       |
| SH-0003    | Can't create scratch org from org shape. The org shape version is outdated. Recreate the org shape and try again.                                                                                                                                                                                                   |
| SH-9999    | Can’t validate org shape due to fatal error. Contact Salesforce Customer Support for assistance.                                                                                                                                                                                                                    |

{% hint style="info" %}
**Source:** [Salesforce DX Developer Guide - Scratch Org Error Codes](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_scratch\_orgs\_error\_codes.htm)
{% endhint %}
