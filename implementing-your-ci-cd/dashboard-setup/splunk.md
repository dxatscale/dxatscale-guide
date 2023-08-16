# Splunk

## Git Pipeline Setup

1. Create a "**index**" and "**HEC-Token**" in Splunk.
2.  Copy the **HEC-Token** and create a variable in your pipeline labeled "`SFPOWERSCRIPTS_SPLUNK_API_KEY`" and assign the value of the key. Ensure to mask this value.\\

    <figure><img src="../../.gitbook/assets/splunk_api_key.png" alt=""><figcaption><p>Sample GitLab Variable for Splunk API Key</p></figcaption></figure>
3.  Add another additional variable named "`SFPOWERSCRIPTS_SPLUNK`" and set the value to "**true**".\\

    <figure><img src="../../.gitbook/assets/splunk_git_key.png" alt=""><figcaption><p><strong>SFPOWERSCRIPTS_SPLUNK Variable</strong></p></figcaption></figure>
4.  Copy the full **Splunk Event Collector Url** and create a variable in your pipeline labeled "`SFPOWERSCRIPTS_SPLUNK_HOST`" and assign the value of the url. "**Splunk Url**". Ensure to mask this value.\\

    <figure><img src="../../.gitbook/assets/splunk_host_key.png" alt=""><figcaption><p><strong>SFPOWERSCRIPTS_SPLUNK_HOST Variable</strong></p></figcaption></figure>

## Dashboard View

1. Navigate in Splunk to **Dashboards** and click **Create New Dashboards**.
2. Create a title and select **Classic Dashboards**.\\

<figure><img src="../../.gitbook/assets/splunk_dashboard_modal.png" alt=""><figcaption><p><strong>Splunk Dashboard Title</strong></p></figcaption></figure>

3. Click on **Source**.\\

<figure><img src="../../.gitbook/assets/splunk_dashboard_source.png" alt=""><figcaption><p><strong>Splunk Dashboard Source Button</strong></p></figcaption></figure>

4. Choose a splunk xml template from github [dxscale/dxscale-template](https://github.com/dxatscale/dxatscale-template/tree/main/dashboards/Splunk)
5. In this example the **CICD\_PackageOverview**. Copy the contents.\\

<figure><img src="../../.gitbook/assets/splunk_package_xml.png" alt=""><figcaption><p><strong>CICD_PackageOverview.xml</strong></p></figcaption></figure>

6. Paste the xml content in the **Splunk Source Editor**.\\

<figure><img src="../../.gitbook/assets/splunk_source_editor.png" alt=""><figcaption><p><strong>Splunk Source Editor</strong></p></figcaption></figure>

7. Update the source content file value of the **index** for all instances of in the file.\\

<figure><img src="../../.gitbook/assets/splunk_source_index.png" alt=""><figcaption><p><strong>Change Index Values</strong></p></figcaption></figure>

8.  Update the time range to see all incoming metrics.\\

    <figure><img src="../../.gitbook/assets/splunk_time_range.png" alt=""><figcaption><p><strong>Change Index Values</strong></p></figcaption></figure>
9. Click Save. 👏
