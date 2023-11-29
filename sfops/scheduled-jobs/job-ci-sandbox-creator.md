# Job - CI Sandbox - Creator

{% hint style="info" %}
Read more about [Sandbox Pooling here](../../environment-management/pooling-sandboxes.md).
{% endhint %}

The CI Sandbox Creator is a specialized GitHub Actions workflow to manage the lifecycle of Salesforce CI sandboxes. The workflow performs two pivotal tasks:

1. **Deleting Old CI Sandboxes**: Clears the stage by removing outdated sandboxes, ensuring a clean environment.
2. **Creating New CI Sandboxes**: Executes the `createSandbox` action to spawn new sandboxes in parallel across multiple domains. It consults a pool configuration file to determine sandbox characteristics and quantities. Importantly, the action initiates sandbox creation but does not wait for completion, thereby optimizing runtime.

The objective behind maintaining this pool of sandboxes is to facilitate parallel and isolated testing environments for different branches or components of your Salesforce development. This is crucial for accelerating CI/CD pipelines, reducing queuing time, and mitigating the risks associated with sharing environments.

**Pool Configuration File**

The pool configuration file is a JSON document dictating the sandbox specifications:

```json
[
  {
    "domain": "CORE",
    "count": 2,
    "sourceSB": "MASTERDEV"
  },
  {
    "domain": "ALL-PRODUCTION",
    "count": 1,
    "sourceSB": "production"
  }
]
```

* `domain`: The sandbox's intended use, like CORE or HOTFIX.
* `count`: Number of sandboxes to instantiate for each domain.
* `sourceSB`: The source sandbox for cloning.

**Parallel Operation**

The workflow operates in parallel for each domain specified in the pool configuration file. It triggers sandbox creation processes but does not await their completion. This parallelism enhances efficiency and minimizes workflow duration.

**Triggers**

* **Manual**: Triggered manually via the GitHub UI.
* **Automatic**: Auto-executes every X hours for periodic upkeep (configurable)



