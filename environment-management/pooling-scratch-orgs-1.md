# Pooling Sandboxes

DX@Scale advocates for Scratch Org based development. However, we understand for existing projects, to refactor and ensuring your project working on a scratch org can be challenging and one that consumes a fair bit of time. In these circumstances, one can utilize Sandboxes or rather a pool of Sandboxes to act as your validation environments during continuous integration. Sandbox pools can also be utilized as just in time test environments.

Considering the rolling limit of sandboxes,  that you can only delete a sandbox once in 24 hours, the time taken to provision a sandbox, naming restrictions, we have designed the pooling of sandboxes bit differently compared to pooling scratch orgs\
\
Sandbox Pools utilize a provided source sandbox or from production.  When created from production, the sandboxes will be using the 'DEVELOPER' licenses, otherwise the sandboxes in the pools will have the exact same license type as your source sandbox. During pooling, all active users in the sandboxes is deactivated except for the users mentioned in the configuration. This allows&#x20;

When sandbox pools are used in the context of DX@Scale  Validation workflow, the current approach is the following

1. A pool is configured with source sandbox and other details, The job proceeds to create a set of sandboxes and assigns it to the pool
2. A job that contains validating a Pull Request or running UI based test will fetch a sandbox from the pool and mark it as "InUse"
3. All subsequent jobs targeting the same pool, will fetch "Available" sandboxes from the pool or wait till an "InUse" sandbox is freed.
4. During a defined interval, the pool is refreshed with new sandboxes, our current recommendation after observing projects is too keep this within 3-4 hours, Existing Sandboxes are marked as "Expired"
5. "Expired" Sandboxes are no longer available and will be deleted by a scheduled job. &#x20;



We recommend only to use half of your total sandbox capacity as the maximum count of available sandboxes when determining the pool allocation and then allocating to each pool accordingly, as sandboxes can be only recycled every 24 hours.

