# Dealing with Org Specific Metadata

The following metadata types usually contain Org specific information, which means it has to be customized for each org when it's getting deployed, or the configuration in your develop org would end up being deployed to production. 

The type of org specific metadata include

* [AuthProviders](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_authproviders.htm)
* [AutoResponseRules](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_autoresponserules.htm)
* [ConnectedApps](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_connectedapp.htm)
* [CSP Trusted Sites](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_csptrustedsite.htm)
* [CustomMetadata](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_custommetadata.htm) \(in most cases\)
* [DataSource](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_datasource.htm)
* [NamedCredential](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_namedcredential.htm)
* [RemoteSiteSetting](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_remotesitesetting.htm)
* [SamlSSOConfigs](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_samlssoconfig.htm)
* [Settings](https://developer.salesforce.com/docs/metadata-coverage/) \(that contains any sensitive information\)
* [WebLinks](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_weblink.htm)

{% hint style="info" %}
**sfpowerscripts** provide a concept of an [aliasified](https://dxatscale.gitbook.io/sfpowerscripts/faq/source-packages#what-are-my-options-with-source-packages) package, where a source package will have folders that match the alias of the target org where the metadata is getting deployed. The components ****have to be duplicated across each of the environments with settings 
{% endhint %}





