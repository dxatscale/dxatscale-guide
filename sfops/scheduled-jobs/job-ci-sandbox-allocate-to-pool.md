# Job - CI Sandbox - Allocate to Pool

The "Job - CI Sandbox - Allocate to Pool" workflow serves a specialized role in sfops sandbox automation. It conducts continuous monitoring to evaluate the availability status of existing sandboxes. The workflow performs two critical tasks:

1. **Sandbox Status Validation**: The workflow scans for sandboxes that are in 'InProgress' state and checks if they have transitioned to 'Completed.'
2. **Provisioning and Cleanup**: If a sandbox is 'Completed,' it is provisioned to be 'Available,' and all other users except the specified ones are deactivated. The sandbox then becomes part of an available pool for CI/CD tasks.

This workflow is crucial for dynamic resource allocation, ensuring that CI/CD pipelines have immediate access to ready sandboxes, thereby reducing latency and improving efficiency.

**Triggers**

* **Manual**: Initiated manually via the GitHub UI.
* **Automatic**: Scheduled to run every 30 minutes..

The core of this workflow performs the following:

* **Fetches existing sandboxes**: Utilizes the GitHub API to fetch sandboxes that are in 'InProgress' state
* **Checks Sandbox Status**: Uses Salesforce CLI to examine if these sandboxes have transitioned to 'Completed.'
* **User Deactivation and Provisioning**: If 'Completed,' deactivates all users except those specified. Marks the sandbox as 'Available' for CI/CD tasks.

