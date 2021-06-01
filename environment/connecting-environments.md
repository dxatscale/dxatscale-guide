# Connecting Environments

Environments \(Sandbox\) need to be connected to the CI/CD pipelines for deploying packages to an environment. The preferred authentication mechanism for integrating environments to pipelines is to utilize JWT based authentication which is detailed at this [link](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_auth_jwt_flow.htm). The environment should also be provisioned with a service user \(API only user, with a System Admin Profile\) and should have the same username.

Each sandbox needs to have these below two secrets being added to a secrets manager such as AWS Secrets Manager or Azure Key Vault.  
  


|  | Naming Pattern in Secrets Manager | Description |
| :--- | :--- | :--- |
| SERVER\_KEY | &lt;ALIAS&gt;SERVER\_KEY | The Private Key used while creating the connected app, The alias is the alias used for the particular environment  |
| CLIENTID/CONSUMER\_KEY | &lt;ALIAS&gt;_CONSUMER\_KEY_ | The client identifier also know as the consumer key from the connected app |

```text
SERVER_KEY=`aws secretsmanager get-secret-value --secret-id $(server_key) --query SecretString --output text | jq -r .server_key`
CONSUMER_KEY=`aws secretsmanager get-secret-value --secret-id $(consumer_key) --query SecretString --output text | jq -r .consumer_key`
echo $SERVER_KEY > JWT_KEYFILE && \
sed -i 's/- /-\n/' JWT_KEYFILE && sed -i 's/ -/\n-/' JWT_KEYFILE && \
sfdx force:auth:jwt:grant -u buildbot@yourorg.com.$(org_suffix) -i $CONSUMER_KEY -f JWT_KEYFILE -a $(alias) -r https://test.salesforce.com 

```

The above script demonstrates how one can fetch the secrets from AWS Secrets Manager

