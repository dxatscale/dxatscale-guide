# Delete Pools

### When to drop a scratch org pool?

### Deleting All Scratch orgs in a pool

### Deleting Orphaned Scratch orgs

sfpowerscripts during prepare attempts to create multiple scratch orgs in parallel, while respecting the timeout as provided in Pool configuration.  At times when the Salesforce infrastructure is stretched such as during release windows or during maintenance windows, it could be often seen some of the scratch orgs requested results in being timed out and are discarded by the rest of the pool activities. However, some of these scratch orgs are in fact created by Salesforce without respecting the timeout parameter,  and counted against the active scratch org limits.

These scratch orgs titled **orphaned scratch orgs** in sfpowerscripts lingo can be reclaimed by issuing the pool: delete command with --orphans flag.  This will delete these scratch orgs and hence allow to recover your active scratch org limits

```
// Example command & output demonstrating delete of orphaned scratch orgs
sfdx sfpowerscripts:pool:delete -o -v dxatscale   

-------------------------------------------------------------------------------------------
sfpowerscripts  -- The DX@Scale CI/CD Orchestrator -Version:20.21.1 -Release:February 23
-------------------------------------------------------------------------------------------
The command resulted in the following operation
                                                               
 Operation   OrgId             Username                      
 recovered   00DDJ000000I9W6   test-spqx0dzndh4t@example.com 
 recovered   00D7g0000006HMH   test-4m3ab2ta1ioc@example.com 
 recovered   00D7g0000006QT7   test-6bfnymfrioxg@example.com 
 recovered   00D010000008doh   test-taxvqnsyj8nj@example.com 
 recovered   00D8F0000004n7v   test-nxtpmzrsxxla@example.com 
 recovered   00D7d000008qSJZ   test-nlsfijffwjam@example.com   
```
