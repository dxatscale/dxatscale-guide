# Delete Pools

pool: delete allows you to delete scratch orgs associated with a pool.

```
sfp pool:delete -h
Deletes the pooled scratch orgs from the Scratch Org Pool

USAGE
  $ sfdx sfpowerscripts pool delete [-t <string>] [-i | -a] [-o] [-v <string>] [--apiversion <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

FLAGS
  -a, --allscratchorgs                                                              Deletes all used and unused Scratch orgs from pool by the tag
  -i, --inprogressonly                                                              Deletes all In Progress Scratch orgs from pool by the tag
  -o, --orphans                                                                     Recovers scratch orgs that were created by salesforce but were not tagged to sfpowerscripts due to timeouts etc.
  -t, --tag=<value>                                                                 tag used to identify the scratch org pool
  -v, --targetdevhubusername=<value>                                                username or alias for the dev hub org; overrides default dev hub org
  --apiversion=<value>                                                              override the api version used for api requests made by this command
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: info] logging level for this command invocation

```

To keep the pools up to date, a nightly scheduled job can be utilised which can delete all the scratch orgs in each pool. In the case of developer pools (pools with source tracking and used by developers as opposed to CI pools), care must be taken to delete only the `unassigned` pools by omitting the `--allscratchorgs` flag.

{% hint style="warning" %}
Be careful when running delete command against developer pools with `-allscratchorg` flag. It will delete the scratch orgs that are used by developer and can result in potential loss of work
{% endhint %}

### Deleting Orphaned Scratch orgs

sfpowerscripts during prepare attempts to create multiple scratch orgs in parallel, while respecting the timeout as provided in Pool configuration. At times when the Salesforce infrastructure is stretched such as during release windows or during maintenance windows, it could be often seen some of the scratch orgs requested results in being timed out and are discarded by the rest of the pool activities. However, some of these scratch orgs are in fact created by Salesforce without respecting the timeout parameter, and counted against the active scratch org limits.

These scratch orgs titled **orphaned scratch orgs** in sfpowerscripts lingo can be reclaimed by issuing the pool: delete command with --orphans flag. This will delete these scratch orgs and hence allow to recover your active scratch org limits

```
// Example command & output demonstrating delete of orphaned scratch orgs
sfp pool:delete -o -v dxatscale   

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
