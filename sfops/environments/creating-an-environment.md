---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Creating an Environment

Environments in sfops is tied to GitHub Environments ([https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment](https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment)) with additional metadata such as described below\
\


<figure><img src="../../.gitbook/assets/EnvVariables.png" alt=""><figcaption></figcaption></figure>

<table><thead><tr><th width="139">Name</th><th width="143.33333333333331">Type</th><th>Purpose</th></tr></thead><tbody><tr><td>SBXNAME</td><td>variable : string</td><td>(Optional) Stores the name of the sandbox associated with the environment. If SB_SFDX_AUTH_URL  is not provided use, the name to handle authentication. Read more <a href="authenticating-to-environments.md">here</a></td></tr><tr><td>TESTRUN</td><td>variable : boolean</td><td>Use this environment for daily full test tuns by a scheduled sfops workflow</td></tr><tr><td>TYPE</td><td>variable : string</td><td>Denotes the type of the environment, an environment could be  one of 'development', 'test'  or 'release'</td></tr><tr><td>SB_SFDX_AUTH_URL</td><td>secret : string</td><td>Auth URL to the environment, Read <a href="authenticating-to-environments.md">here </a>on how to generate one </td></tr></tbody></table>

In order to create an environment, 'sfops' provides an issue template '**Request a new environment**', where you could fill in the details, and the environment gets created.  Please note the sandbox has to be created previously before triggering the request.

<figure><img src="../../.gitbook/assets/RequestEnvTemplate.png" alt=""><figcaption><p>Issue  form to create an environment</p></figcaption></figure>
