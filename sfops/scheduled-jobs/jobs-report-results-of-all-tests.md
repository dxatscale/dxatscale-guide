# Jobs - Report results of all tests

This workflow is responsible for monitoring code quality and test coverage across multiple Salesforce environments. The workflow performs three key tasks:

**Apex Test Execution**

1. **Environment Identification**: Scans for Salesforce environments marked with `testrun:true`.
2. **Test Runs**: Executes Apex tests in these identified environments.

**Static Code Analysis**

3. **Code Quality Assurance**: Performs static code analysis on Apex classes using PMD.

**Triggers**

* **Manual**: Can be triggered manually via the GitHub UI.
* **Automatic**: Scheduled to run every day at 12:00 UTC. (Can be configured)

**Core Operations**

* **Fetch Salesforce Environments**: Utilizes GitHub Actions to identify Salesforce environments where `testrun:true` is set.
* **Execute Apex Tests**: Uses Salesforce CLI and custom GitHub Actions to run Apex tests in each identified environment.
* **Report Test Results**: Sends the test results to a specified GitHub repository (`sfops-dashboard`).
* **Perform Static Analysis**: Uses PMD and Salesforce CLI for static analysis of Apex classes.

