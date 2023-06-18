# On your Salesforce Org

To enable modular package development, there are a few configurations in Salesforce as a System Administrator that needs to be turned on to be able to create Scratch Orgs and Unlock Packages.

## A. Enable Dev Hub

[Enable Dev Hub](https://help.salesforce.com/s/articleView?id=sf.sfdx\_setup\_enable\_devhub.htm\&type=5) in your Salesforce org so you can create and manage scratch orgs and second-generation packages. Scratch orgs are disposable Salesforce orgs to support development and testing.

1. Navigate to the **Setup** menu
2. Go to **Development > Dev Hub**
3. Toggle the button to on for **Enable Dev Hub**

![](<../../.gitbook/assets/image (18).png>)

## B. Enable Unlocked Packages and Second-Generation Managed Packages

[Unlocked packages](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_unlocked\_pkg\_intro.htm) help organize your existing metadata, package an app, extend an app that you’ve purchased from AppExchange, or package new metadata.

1. Navigate to the **Setup** menu
2. Go to **Development > Dev Hub**
3. Toggle the button to on for **Enable Unlocked Packages and Second-Generation Managed Packages**

![](<../../.gitbook/assets/image (1) (1).png>)

## C. Create Service Account for Deployment

For auditing purposes, it is best practice to create a separate [service account](https://help.salesforce.com/s/articleView?id=000331470\&type=1) to manage deployments to your Salesforce instance. The separation of user owned accounts and service accounts ensures traceability to your metadata and configuration changes.

1. Navigate to the **Setup** menu
2. Go to **Users > Users**
3. Click on **New User** button
4. Enter **CICD** for **First Name** and **User** for **Last Name**
5. Enter in a Email address and Username
6. Set **User License** to **Salesforce**
7. Set **Profile** to **System Administrator**
8. Scroll down and click on **Save**

![](<../../.gitbook/assets/image (68).png>)

{% hint style="info" %}
Only certain [editions](https://help.salesforce.com/s/articleView?id=000326486\&type=1) of Salesforce has API Access. It's best to create a new **Profile** or **Permission Set** and configure the **System Permissions** and enable the **API Enabled** and **Api Only User** permission.
{% endhint %}

{% hint style="warning" %}
Future [requirements](https://help.salesforce.com/s/articleView?id=sf.security\_mfa\_exclude\_exempt\_users.htm\&type=5) to enable MFA across all users will require a special user permissions to be assigned to the Service Account.  Details will be provided in the future and updated in the above steps to implement.&#x20;
{% endhint %}

## D. Authenticate to DevHub via CLI

Authorize your production instance and/or Developer Edition Org using the [web login flow](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_cli\_reference.meta/sfdx\_cli\_reference/cli\_reference\_auth\_web.htm). The example below uses "**DevHub**" as the alias for the instance where you will use it to create Unlock Packages and manage Scratch Orgs.

```bash
sfdx auth:web:login -a DevHub -r https://login.salesforce.com
```

## E. Install sfpowerscripts Scratch Org Pooling Unlocked Package in DevHub

The [Scratch Org Pooling Unlocked Package](https://github.com/dxatscale/sfpower-scratchorg-pool) adds additional custom fields, validation rules, and workflow to the standard object "**ScratchOrgInfo**" in the DevHub to enable associated scratch org pool commands to work for the pipeline.

```bash
sfdx force:package:install -p 04t1P000000katQQAQ -u DevHub -r -a package -s AdminsOnly -w 30
```

## F. Install sfpowerscripts-artifact Unlocked Package in DevHub and Lower Existing Sandboxes

The [sfpowerscripts-artifact package](https://github.com/dxatscale/sfpowerscripts-artifact) is a lightweight unlocked package consisting of a custom setting **SfpowerscriptsArtifact2\_\_c** that is used to keep a record of the artifacts that have been installed in the org. This enables package installation, using sfpowerscripts, to be skipped if the same artifact version already exists in the org.

```bash
sfdx force:package:install --package 04t1P000000ka9mQAA -u <OrgAlias> --securitytype=AdminsOnly --wait=120
```

## G. Authenticate to Lower Sandbox Environments via CLI

The template assumes you are following the environment strategy defined in our DX@Scale Guide. The following sandboxes are recommended to be created and [authenticated](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_cli\_reference.meta/sfdx\_cli\_reference/cli\_reference\_auth\_web.htm) first prior to running the pipeline.

* SHAREDDEV (Shared Development)
* ST (System Test)
* SIT (System Integration Test)
* UAT (User Acceptance Test)
* PROD (Production)

{% hint style="info" %}
Assuming that Production is also your Dev Hub, we still recommend creating multiple CLI entries to segregate the connections.
{% endhint %}

Additional environments and customization can be made once you are familiar with the scripts.

{% tabs %}
{% tab title="Sandbox" %}
```bash
sfdx auth:web:login -a <orgAlias> -r https://test.salesforce.com
```
{% endtab %}

{% tab title="Production" %}
```
sfdx auth:web:login -a <orgAlias> -r https://login.salesforce.com
```
{% endtab %}
{% endtabs %}

## H. Generate SFDX auth URL for Pipeline Authentication

In order for the GitHub pipeline to authenticate to the DevHub and other environments, [SFDX auth URL](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_cli\_reference.meta/sfdx\_cli\_reference/cli\_reference\_auth\_sfdxurl.htm) is the preferred method over [JWT Bearer Flow](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_auth\_jwt\_flow.htm). For each environment, execute the following command on a previously authenticated environment and save the sfdxAuthUrl for use in future pipeline configuration steps.

```bash
sfdx force:org:display -u <orgAlias> --verbose --json > authFile.json
cat authFile.json
> {
  "status": 0,
  "result": {
    "id": "XXXXYYY",
    "accessToken": "00D8G0000009g7h!uhuRfGKbvPeubTZKztmFWgrykDuuVdxbffzjjVTqjMyRcV{wb+2JtxsevgKfGiGXRz02jY83uNBsD4CuWHwv.b21KZdFxbTi",
    "instanceUrl": "https://your.salesforce.com",
    "username": "vu.ha@accenture.com.dxatscale.shareddev",
    "clientId": "PlatformCLI",
    "connectedStatus": "Connected",
    "sfdxAuthUrl": "force://PlatformCLI::Cq$QLeQvDxpvUoNKgiDkoTqyVHdeoMupiZvkgHYcdVHsfMaDpqKJNbg#8ZtUpfBuIdVaUD0B21cFav5X2Pzv5X2@yoursalesforce.com",
    "alias": "SharedDev"
  }
}
```

{% hint style="info" %}
Save only the following part of the **sfdxAuthUrl** for each environment

`force://PlatformCLI::Cq$QLeQvDxpvUoNKgiDkoTqyVHdeoMupiZvkgHYcdVHsfMaDpqKJNbg#8ZtUpfBuIdVaUD0B21cFav5X2Pzv5X2@yoursalesforce.com`
{% endhint %}

## I.  Public Group and Sharing Rules Creation for Developer Access to Scratch Org Pools

For developers (who are on limited access license) to access scratch orgs created by the CI service user, for their local development, a sharing setting needs to be created on the **ScratchOrgInfo** object. The sharing setting should grant read/write access to the ScratchOrgInfo records owned by a public group consisting of the CI service user and a public group consisting of the developer users.

1.  Create Public Groups **(Setup > Users > Public Groups)**

    * CI Users (Admin users/ CI users who creates scratch orgs in pool)



    <figure><img src="../../.gitbook/assets/image (55).png" alt=""><figcaption><p>Public Group: CI Users<br></p></figcaption></figure>

    * Developers (developers who are allowed to fetch scratch orgs from pool)\


    <figure><img src="../../.gitbook/assets/image (81).png" alt=""><figcaption><p>Public Group: Developers</p></figcaption></figure>
2.  Create Sharing Rule **"ScratchOrgInfo RW to Developers"** **(Setup > Security > Sharing Settings)**

    * Grant Read/Write access to the ScratchOrgInfos records owned by the CI Users to Developers&#x20;

    <figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption><p>Sharing Rule</p></figcaption></figure>
3.  Assign Users to Public Groups **(Setup > Security > Sharing Settings)**

    * CI Users
    * Developers



    <figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption><p>Public Group: User Assignment</p></figcaption></figure>

## J. Permission Set Creation for Developer Access to ScratchOrgInfo Object

The developers must also have object-level and FLS permissions on the ScratchOrgInfo object. One way to achieve this is to assign a permission set that has Read, Create, Edit and Delete access on ScratchOrgInfos, as well as Read and Edit access to the custom fields used for scratch org pooling: `Allocation_status__c`, `Password__c`, `Pooltag__c` and `SfdxAuthUrl__c`

**Permission Set Name:** "Scratch Org Developer"

**Object:** Scratch Org Info

1. Object Permissions
   * Read, Create, Edit and Delete
2. Field Permissions
   *   Read, Edit for Custom Fields

       * `Allocation_status__c`
       * `Password__c`
       * `Pooltag__c`
       * `SfdxAuthUrl__c`



       <figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption><p>Permission Set: Object/Field Permissions</p></figcaption></figure>

**System Permissions:**

* API Enabled = True
* API Only User = False
* Create and Update Second-Generation Packages = True

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption><p>Permission Set: System Permissions</p></figcaption></figure>

## **K. Profile and Permission Set Assignment for Developers in Production**

To onboard new developers, the following Profiles and Permission Set will need to be assigned to the new Developer User Account in Salesforce.

**Profile** (Choose 1 Only)

1. Minimum Access - Salesforce
   * Licence Type - Salesforce
2. Limited Access User
   * Licence Type - Salesforce Limited Access - Free

**Permission Set**&#x20;

* Scratch Org Developer

**Public Groups**

* Developers - Add Users to "Developers" Group

## Frequently Asked Questions (FAQs)

1. Unable to fetch scratch org from Dev Pool even though there are available scratch orgs in DevHub.\
   \
   ERROR running sfpowerscripts:pool:fetch: <mark style="color:red;">No scratch org available at the moment for dev, try again in sometime.</mark>\
   \
   Possible Solutions:\
   \- Check that you have added the Developer User to the **Public Group** prior to fetching the scratch org from the pool\
   \- Confirm the **tag** is correct for the scratch org pool that you are fetching from
