# Repository Structure

![Repository Structure](../.gitbook/assets/repostructure.png)

DX@Scale projects predominantly follow a multiple mono-repo structure similar to the picture shown above.  Each reposotitory has as src folder that holds one or more packages.

Different folders in each of the structure are explained as below

1. core-crm:  A folder to house all the core model of your org which is shared with all other domains
2. frameworks: This folder houses multiple packages which are basically utilities/ technical frameworks  such as Trigger, Dependency Injection etc.
3. sales:  An example of a domain in your org. Under this particular domain, multiple packages that belong to the domain are included
4. src-access-management:  This package is typically one of the packages that is deployed second to last in the deployment order and used to store profiles that are applied across the org
5. src-env-specific: An aliasified packaged  which carries metadata for each particular stage of your path to production 

This will form your initial structure of packaging. Once some development cycles are being completed,  frameworks can be moved into its own repository.  If you also figure a particular domain is being not iterated upon frequently anymore and the there are no upward dependency, they could also be removed into  another reposiotrye

