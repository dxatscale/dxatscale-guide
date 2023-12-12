# Connecting Environments

Environments (Sandbox) need to be connected to the CI/CD pipelines for deploying packages to an environment. The preferred authentication mechanism for integrating environments to pipelines is to utilize [SFDX AUTH URL](https://developer.salesforce.com/docs/atlas.en-us.sfdx\_dev.meta/sfdx\_dev/sfdx\_dev\_auth\_view\_info.htm) based authentication. The environment should also be provisioned with a service user (API only user, with a System Admin Profile) and should have the same username.

Each sandbox needs to have the below secret being added to a secrets manager in your CI/CD system or a dedicated secrets manager such as AWS Secrets Manager or Azure Key Vault. Then a new stage is supposed to be created in your CI/CD flow based on your environment strategy.

|                 | Naming Pattern in Secrets Manager | Description                                                                                                                                   |
| --------------- | --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| SFDX\_AUTH\_URL | \<ALIAS>\_SFDX\_AUTH\_URL         | The Auth URL for a particular environment. This consists of the access token which the salesforce CLI uses to authenticate to the environment |

```
//Replace <alias> with alias of your environment
SFDX_AUTH_URL=`aws secretsmanager get-secret-value --secret-id $(<alias>_SFDX_AUTH_URL) --query SecretString --output text | jq -r .<alias>_sfdx_auth_url`
echo $SFDX_AUTH_URL > .authfile
sfdx auth:sfdxurl:store -f .authfile -a <alias>
```

The above script demonstrates how one can fetch the secrets from AWS Secrets Manager
