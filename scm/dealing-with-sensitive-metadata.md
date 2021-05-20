# Dealing with Org Specific Metadata

The following metadata types usually contain Org specific information, which means it has to be customized for each org when it's getting deployed, or the configuration in your develop org would end up being deployed to production. 

The type of org specific metadata include

* AuthProviders
* AutoResponseRules
* ConnectedApps
* CSP Trusted Sites
* CustomMetadata \(in most cases\)
* DataSources
* NamedCredential
* RemoteSiteSettings
* SamlSSOConfigs
* Settings \(that contains any sensitive information\)

{% hint style="info" %}
**sfpowerscripts'** provide a concept of an [aliasified](https://dxatscale.gitbook.io/sfpowerscripts/faq/source-packages#what-are-my-options-with-source-packages) package, where a source package will have folders that match the alias of the target org where the metadata is getting deployed. The components ****have to be duplicated across each of the environments with settings 
{% endhint %}





