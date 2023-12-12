---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Github App

This section deals with setting up a GitHub App which is required for sfops to function. sfops require additional permissions which allow to write into other repository such as 'sfops-dashboard' and also permission to trigger workflows etc. These permissions are beyond what is being provided by the built in GITHUB\_TOKEN.   A Github App is recommended over using a Service Account and its Personal Access Token, as the service account takes an additional license and has limitations on the api requests.\


This guide is crafted to facilitate the user to create a `sfops-bot` GitHub App to automate the worflows provided out of the box with sfops.  It provides a step-by-step approach for creating the app, elaborating on the necessary permissions, installation, and secure storage of sensitive information.\
\
You can refer to this link to understand how this work behind the scenes

[https://docs.github.com/en/apps/creating-github-apps/authenticating-with-a-github-app/making-authenticated-api-requests-with-a-github-app-in-a-github-actions-workflow#authenticating-with-a-github-app](https://docs.github.com/en/apps/creating-github-apps/authenticating-with-a-github-app/making-authenticated-api-requests-with-a-github-app-in-a-github-actions-workflow#authenticating-with-a-github-app)\


## Step-by-Step Creation and Configuration

### **Step 1: Registration of sfops-bot GitHub App**

* Navigate to your GitHub organization's settings.
* Click on "Developer settings" and select "GitHub Apps".
* Hit "New GitHub App" and input `sfops-bot` as the name.
* Add an icon and background color in the 'Display Information' to make the app identifiable in your workflows

### **Step 2: Permissions Configuration**

* Assign the app permissions based on the requirements for sfops:

#### Repository Permissions

* **Contents**: Set to read and write for the app to manage code, branches, commits, and merges. This access allows the app to automate code integration processes.
* **Issues**: Read and write permissions enable the app to automate issue tracking, commenting, and labeling.
* **Deployments**: Read and write access empowers the app to manage deployments, essential for continuous delivery workflows.
* **Environments**: Read and write access to create  environments, which will be consumed by workflows
* **Pull Requests**: Read and write permissions are necessary for the app to automate the handling of pull requests, including merging and labeling.
* **Actions**: Read and write access is crucial for the app to manage GitHub Actions, which are integral to automation workflows.
* **Projects**: Read and write permissions allow the app to connect issues to projects for better project management.
* **Secrets**: Read-only access lets the app manage secrets without compromising their security, essential for secure workflows.
* **Variables:**  Read and write permissions that permit the app to read the variables in the repo, This is vital for dynamic configuration of the environment and branch related configurations
* **Workflows**: Read and write permissions permit the app to update workflow files, which is vital for maintaining automated processes.

#### Organisation Permissions

* **Projects**: Read and write permissions allow the app to connect issues to projects for better project management.  \


{% hint style="info" %}
The new GitHub projects are created at organisation level, and requires organisation permissions
{% endhint %}

### **Step 3: Generate and Secure a Private Key**

* In the 'General' section of your app's settings, locate the 'Private keys' subsection.
* Click on "Generate a private key" and download the `.pem` file immediately to your secure location.

### **Step 4: Installation of the App**

* Navigate to the 'Install App' tab within your app settings.
* Click "Install" to initiate the installation process.
* Select your organization and choose to install the app on all repositories or specific ones such as Salesforce repositories and `sfops-dashboard`.

### **Step 5: Storing the Private Key and App ID as Secrets**

* Access your organization or repository settings and go to the 'Secrets' area.
* Choose "New repository secret" or "New organization secret" for both the private key and App ID.
* Label the private key secret as `SFOPSBOT_APP_PRIVATE_KEY` and the App ID secret as `SFOPSBOT_APP_ID`.
* Paste the contents of the private key file and the numerical App ID into their respective secrets.

####

The workflows provided by sfops utilizes the above variables to authenticated to do repository operations as provided in the below example\


```
// Sample code demonstrating how the token is used
      - name: Generate a token
        id: generate_token
        uses: actions/create-github-app-token@v1
        with:
          app-id: ${{ var.SFOPSBOT_APP_ID }}
          private-key: ${{ secrets.SFOPSBOT_APP_PRIVATE_KEY }}

      - name: Use the token
        env:
          GITHUB_TOKEN: ${{ steps.generate_token.outputs.token }}
        run: |
          gh workflow <>
```

