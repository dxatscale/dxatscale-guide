# Fetch A Scratch Org

The developers can fetch a scratch org with all the dependencies installed and the latest code base has been pushed from a pool for their feature development. the developer can start developing new features without spending a few hours preparing the development environment.

```
sfp pool:fetch -t dev-pool -v devhub

Fetching a scratch org from pool dev-pool in Org 00D6F000002Xfaixxx
Enabling source tracking, this will take a bit of time, please hang on
Copying the repository to /var/folders/0n/qs0txqqj6p7gkjlztgmf224h0000gn/T/tmp-11226-pTuia24bl8Gs
Successfully created temporary repository at /var/folders/0n/qs0txqqj6p7gkjlztgmf224h0000gn/T/tmp-11226-pTuia24bl8Gs with commit HEAD
Total Artifacts to Analyze: 1

Installed managed packages:
Packages installed in org:
                                                              
 Package             Version       Type      isOrgDependent 
 FSL                 238.0.35.1    Managed   false          
 Conga Composer      8.174.0.15    Managed   false          
 Conga Batch         8.22.0.3      Managed   false          
 Vlocity Insurance   890.333.0.1   Managed   false          
                                                              
Artifacts installed in org:
                                                                                          
 Artifact                      Version         Commit Id                                
 utils                         1.2.2.1        f79efddfd7f57e52d63222f6d9c23fb1e6a47152 

                                                                                          
======== Scratch org details ========
 KEY         VALUE                                                                                                                                               
 ─────────── ─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── 
 Id          2SR5m0000001d0vxxx                                                                                                                                  
 orgId       00D2O000000Hxxx                                                                                                                                     
 loginURL    https://efficiency-data-0000.my.salesforce.com/                                                                                                     
 username    test-zey1higmxxxx@example.com                                                                                                                       
 password    **********                                                                                                                                       
 expiryDate  2023-03-03                                                                                                                                          
 sfdxAuthUrl force://PlatformCLI::*******@efficiency-data-0000.my.salesforce.com 
 status      Assigned                                                                                                                                            
----------------------------------------------------------------------------------------------------
Succesfully fetched a scratch org and enabled source tracking  in 00:00:11.291
----------------------------------------------------------------------------------------------------

```

The status of the scratch org will be changed to "Assigned", so no one will be able to fetch the same one.
