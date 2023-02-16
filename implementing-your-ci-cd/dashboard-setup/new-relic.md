# New Relic

## Account Setup

1.  Create a [new account](https://newrelic.com/signup) on New Relic and verify your email.\


    <figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>New Relic: Account Creation</p></figcaption></figure>

    \


    <figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>New Relic Home Page </p></figcaption></figure>
2.  Click on your **Profile** and navigate to "**API keys**".\


    <figure><img src="../../.gitbook/assets/image (54).png" alt=""><figcaption><p>API Keys</p></figcaption></figure>
3.  Click on "**Create a key**"\


    <figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption><p>Create a key</p></figcaption></figure>
4.  Select "**Ingest - Licence**" for the **Key Type** and enter in details for the "**Name**" and "**Notes**"\


    <figure><img src="../../.gitbook/assets/image (64).png" alt=""><figcaption><p>Ingest - License - Key Creation</p></figcaption></figure>
5.  Confirm Licence has been created\


    <figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption><p>Licence Created</p></figcaption></figure>
6.  Copy the **key** from the new "**Ingest - Licence"** and create a variable in your pipeline labeled "`SFPOWERSCRIPTS_NEWRELIC_API_KEY`" and assign the value of the key.  Ensure to mask this value.\


    <figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption><p>Sample GitLab Variable for New Relic API Key</p></figcaption></figure>
7.  Add another additional variable named "SFPOWERSCRIPTS\_NEWRELIC" and set the value to "**true**". \


    <figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption><p><strong>SFPOWERSCRIPTS_NEWRELIC Variable</strong></p></figcaption></figure>
8.  Retrieve your "**Account ID**" under **Profile > Administration > Access Management > Accounts**\
    ****

    <figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>
9.  Update the `cicd-dashboard.json` file in `dashboards/NewRelic` folder with the value of the "**Account id**" for all instances of `<your-account-id>`in the file.  Ensure to include the quotation marks for the "Account id". (eg. "1234567")\


    <figure><img src="../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>
10. Trigger the scheduled job for "**schedule-report-so-pool**" job and confirm success.

{% hint style="warning" %}
Avoid checking in the updated **"Account id"** file directly in your repository if you want to keep this as a secret.  This is only needed to import into the Dashboard in the next section.
{% endhint %}

## Dashboard View

1.  Navigate to the Dashboard and click on "**Import Dashboard**".\


    <figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption><p>Import Dashboard</p></figcaption></figure>
2.  Copy and paste the edited contents of the "`cicd-dashboard.json"` file in the previous section with the updated "Account id".\


    <figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption><p>JSON Import Dashboard</p></figcaption></figure>
3. Click on "**Import dashboard**"
4.  Confirm the "**Salesforce CI/CD Dashboard**" is created.\


    <figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>
5.  Click to view details for the "**Salesforce CI/CD Dashboard**"\
    \


    <figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Metrics are meant to be reviewed and monitored to ensure the success of your CI/CD setup.  Ensure that the team is reviewing the dashboard frequently and identify issues across Scratch Org Creations, Deployments,
{% endhint %}
