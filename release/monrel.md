# Monitoring Releases

Monitoring releases is a critical activity for DX@Scale practitioners. DX@Scale practitioners utilize multiple dashboards to understand the various attributes of a release and how the pipelines can be further optimized for realizing further value.

DX@Scale practitioners utilize metrics emitted from sfpowerscripts to track the following attributes of a release

| Metric | Description | Service Level Objective \(SLO\) | SLI |
| :--- | :--- | :--- | :--- |
| Average Number of Packages in a Release | The average number of packages carried in a release | Smaller the better, strive to keep releases under 10 packages  |  |
| Average Time taken for a Release to Prod | The average time taken for a release to production | Should strive for all the release activity including manual step to be completed in less than an hour |  |
| Average Time taken for a Release to Non-Production Environments | The average time taken for a release to non-production environments | Should strive for all the release activity including manual step to be completed in less than an hour |  |
| Time taken for Last Release to prod | The last time taken for a release to prod | Should strive for all the release activity including manual step to be completed in less than an hour |  |
| Time taken for a Release to Each Environment | The average time taken for a release to each non-production environments | Should strive for all the release activity including manual step to be completed in less than an hour |  |
| Number of Releases to Prod | Number of releases in a defined a time period     | More the better |  |
| Number of Releases to Non-prod Environments | Number of releases in a defined a time period     | More the better |  |
| Number of Failed Releases per Environments | Number of failed releases per environment | Less the better |  |
| Average Number of Work Items/Commits per Release | Number of work items/commits per release | Less the better |  |
| Success Ratio | 100 - \( Failed Releases / \( Success Releases + Failed Releases \) \) \* 100 | Success Ration of Releases |  |

![](../.gitbook/assets/dashboard_edited.png)

{% hint style="info" %}
DX@Scale practitioners follow a concept of deployment budget, where a maximum time is set for a release to production. This is an inherent SLO for the team to focus on and the time of deployment should be below this mark. If any deployment exceeds the allocated budget, the team should discuss various approaches and plans to mitigate it.
{% endhint %}

{% hint style="danger" %}
If a release is retried more than 3 times to an environment due to a failure, the release should be marked as a failed release \(even if the release succeeds in the 4th attempt\) and the team should do a root cause analysis of the issue and methods to mitigate should be addressed as a priority before attempting the next release.
{% endhint %}

