# List Scratch Orgs

List all the active scratch orgs with the given pool tag, only 'available' and 'in progress' scratch orgs are displayed

```
sfp pool:list -t dev-pool -v devhub

======== Scratch org Details ========
Unused Scratch Orgs in the Pool : 1 

Scratch Orgs being provisioned in the Pool : 1 

 TAG                   ORG ID          USERNAME                      EXPIRY DATE STATUS                   LOGIN U R L                                      
 ──────── ─────────────── ───────────────────────────── ─────────── ──────────────────────── ──────────────────────────────────────────────── 
 dev-pool 00D2O000000xxxx test-zey1higmxxxx@example.com 2023-03-03  Provisioning in progress https://efficiency-data-0000.my.salesforce.com/  
 dev-pool 00D2N000000xxxx test-ofakal3gxxxx@example.com 2023-03-03  Available                https://inspiration-saas-0000.my.salesforce.com/ 
```
