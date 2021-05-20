# Monitoring Releases

Monitoring releases is a critical activity for DX@Scale practitioners. DX@Scale practitioners utilize multiple dashboards to understand the various attributes of a release and how the pipelines can be further optimized for realizing further value.

DX@Scale practitioners utilize metrics emitted from sfpowerscripts to track the following attributes of a release

| METRIC | Description | Goal | SLI |
| :--- | :--- | :--- | :--- |
| Average Number of packages in a release | The average number of packages carried in a release | Smaller  the better, strive to keep releases under 10 packages  |  |
| Average time taken for a release to Prod | The average time taken for a release to production | Should strive for all the release activity including manual step to be completed in less than an hour |  |
| Average time taken for a release to Non Prod | The average time taken for a release to  non production environments | Should strive for all the release activity including manual step to be completed in less than an hour |  |
| Time taken for Last release to prod | The last time taken for a release to prod | Should strive for all the release activity including manual step to be completed in less than an hour |  |
| Ttime taken for a release to each environment | The average time taken for a release to each  non production environments | Should strive for all the release activity including manual step to be completed in less than an hour |  |
| Number of releases to prod | Number of releases in a defined time period     | More the better |  |
| Number of releases to non -prod | Number of releases in a defined time period     | More the better |  |
| Number of failed releases / environment | Number of failed releases per environment |  |  |
| Average number of Work Item/Commit per release |  |  |  |
| Success Ratio | 100 - \(  Failed Releases / \( Succes Releases + Failed Releases \) \) \* 100 | Success Ration of releases |  |

![](../.gitbook/assets/image%20%2852%29%20%281%29%20%281%29.png)

{% hint style="info" %}
DX@Scale practitioners follow a concept of deployment budget, where a maximum time is set for a release to production. This is an inherent SLA for the team to focus on and the time of deployment should be below this mark. If any particular deployment exceeds the allocated budget, the team should discuss various approaches and plans to mitigate it.
{% endhint %}

{% hint style="danger" %}
If a release is retried more than 3 times to an environment due to a failure, the release should be marked as a failed release \(even if the release succeeds in the 4th attempt\) and the team should do a root cause analysis of the issue and methods to mitigate should be addressed as a priority before attempting the next release.
{% endhint %}

