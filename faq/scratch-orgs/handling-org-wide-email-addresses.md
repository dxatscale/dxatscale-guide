---
description: >-
  Handles the issue that OWEAs cannot be created in scratch orgs prior to
  deployment
---

# Handling Org-Wide Email Addresses

### Issue Description&#x20;

OWEA's cannot be created in Scratch Orgs prior to deployment. The following error occurs when Email Alerts are pushed to a Scratch Org without a verified OrgWideEmailAddress.

```
Email Alerts need a verified OrgWideEmailAddress
```

### Workaround&#x20;

Handle all emails that would use an OWEA at the Apex level.&#x20;

* Create an apex class that queries for the OWEA desired.&#x20;
* If found ->  use it as the from address. &#x20;
* If not found (e.g. scratch org) -> use the current user’s email address as the from address
* Add the InvocableMethod decorator to enable calling from flows

Example

```sql
Messaging.SingleEmailMessage mail = new Messaging.SingleEmailMessage();

OrgWideEmailAddress[] owea = [select Id from OrgWideEmailAddress where Address = 'owea@test.com'];

if ( owea.size() > 0 ) {
    mail.setOrgWideEmailAddressId(owea.get(0).Id);
} 

mail.toAddresses = new String[] { <contact ID> };
mail.subject = 'OWEA Test Message';
mail.plainTextBody = 'This is the message body.';

Messaging.SingleEmailMessage[] messages = new List<Messaging.SingleEmailMessage> {mail};
Messaging.SendEmailResult[] results = Messaging.sendEmail(messages);
```
