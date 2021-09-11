# Solution Overview

In order to configure DX@Scale with GitLab, there are a number of key features that need to be setup on the platform before executing the pipeline. Whether you are new to GitLab or have prior experience developing CI/CD for other software stacks on GitLab, this guide is meant to summarize the key configuration steps on the platform and use the templates provided in our sample repository.

For a deeper dive on the platform, documentation is available on [GitLab Docs](https://docs.gitlab.com/).

## GitLab Overview

![GitLab Architecture](../../../.gitbook/assets/image%20%2823%29.png)

<table>
  <thead>
    <tr>
      <th style="text-align:left">Feature</th>
      <th style="text-align:left">Summary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>Organization</b>
      </td>
      <td style="text-align:left">Top level hierarchy in GitLab used to configure your users and access
        to projects.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Project</b>
      </td>
      <td style="text-align:left">Used to host your codebase, track issues, plan work, collaborate on code,
        and continuously build, test, and use built-in CI/CD to deploy your app.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Repository</b>
      </td>
      <td style="text-align:left">Store your code in metadata <a href="https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_source_file_format.htm">source format</a> and
        make changes to it. Your changes are tracked with version control.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Issues</b>
      </td>
      <td style="text-align:left">Collaborate on ideas, solve problems, and plan work.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>CI/CD</b>
      </td>
      <td style="text-align:left">
        <p>Tooling built into GitLab for software development through the continuous
          methodologies:</p>
        <ul>
          <li>Continuous Integration (CI)</li>
          <li>Continuous Delivery (CD)</li>
          <li>Continuous Deployment (CD)</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Package &amp; Repository</b>
      </td>
      <td style="text-align:left">Acts as a private or public registry for a variety of common package managers
        (eg. npm) and allows you to publish and share packages.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Settings</b>
      </td>
      <td style="text-align:left">Update general project settings, merge request approvals, default and
        protected branches, access tokens, CI/CD variables.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Others</b>
      </td>
      <td style="text-align:left">
        <p>Additional menu options in GitLab such as Project Information, Security
          &amp; Compliance, Deployments, Monitor, Infrastructure, Analytics, Wiki,
          and</p>
        <p>Snippets.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Member</b>
      </td>
      <td style="text-align:left">Users and groups who have access to your project. Each member gets a role,
        which determines what they can do in the project.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Group</b>
      </td>
      <td style="text-align:left">Use to manage one or more related projects at the same time.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Subgroup</b>
      </td>
      <td style="text-align:left">Nested groups or hierarchical groups.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>User</b>
      </td>
      <td style="text-align:left">Each GitLab account has a user profile, which contains information about
        you and your GitLab activity. Set up of Personal Access Tokens and SSH
        Keys will enable users to to securely access the GitLab API from their
        computers.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Roles</b>
      </td>
      <td style="text-align:left">Users have different abilities depending on the role they have in a particular
        group or project. The roles available in GitLab are <b>Owner, Maintainer, Developer, Reporter and Guest.</b>
      </td>
    </tr>
  </tbody>
</table>

## GitLab Terminology

| Area | Description |
| :--- | :--- |
| Access Tokens |  |
| Anchors |  |
| Artifacts |  |
| before\_script |  |
| Environments |  |
| Needs |  |
| Resource Groups | concurrency control |
| Roles |  |
| Rules |  |
| Runners and Agents |  |
| Script |  |
| Variables |  |

## Configuration File

The [.gitlab-ci.yml](https://docs.gitlab.com/ee/ci/yaml/gitlab_ci_yaml.html) template file is the primary configuration file used to executing continuous integration, delivery and deployment on the platform. This CI/CD configuration file exists by default in the root directory of your repository and controls pipeline execution of stages and jobs triggered from updates to the repository via merge requests/merges, scheduled executions, and manual triggering of the pipeline.

![](../../../.gitbook/assets/image%20%2824%29.png)

In the template file provided, the structure of the [YAML](https://yaml.org/) file follows the following structure:

![Template Code Structure](../../../.gitbook/assets/image%20%2835%29.png)

<table>
  <thead>
    <tr>
      <th style="text-align:left">Section</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>Comments</b>
      </td>
      <td style="text-align:left">General header for DX@Scale Template for GitLab and reference links to
        review.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Project CI/CD Variables</b>
      </td>
      <td style="text-align:left">
        <p>Initial project Project CI/CD Variables required to be created in the
          project to authenticate and setup DevHub and Sandbox Environment alias,
          NPM Variables Scope for artifacts, and optional dashboard connection details
          for</p>
        <p>DataDog or New Relic.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Image</b>
      </td>
      <td style="text-align:left">Docker image to use for the job, defaulted to the <a href="https://hub.docker.com/r/dxatscale/sfpowerscripts">docker-sfpowerscripts</a> image
        running on Ubuntu.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Variables</b>
      </td>
      <td style="text-align:left">
        <p>Custom variable used in the .gitlab-ci.yml during pipeline execution.</p>
        <p>
          <br />Custom</p>
        <ul>
          <li></li>
        </ul>
        <p></p>
        <p>Predefined Variables</p>
        <ul>
          <li></li>
        </ul>
        <p></p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>DevHub Authentication</b>
      </td>
      <td style="text-align:left">&lt;b&gt;&lt;/b&gt;</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>NPM Configuration</b>
      </td>
      <td style="text-align:left">&lt;b&gt;&lt;/b&gt;</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Git Repo Configuration</b>
      </td>
      <td style="text-align:left">&lt;b&gt;&lt;/b&gt;</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Stages</b>
      </td>
      <td style="text-align:left">&lt;b&gt;&lt;/b&gt;</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Anchors</b>
      </td>
      <td style="text-align:left">&lt;b&gt;&lt;/b&gt;</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Trigger Job(s)</b>
      </td>
      <td style="text-align:left">&lt;b&gt;&lt;/b&gt;</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Schedule Jobs(s)</b>
      </td>
      <td style="text-align:left">&lt;b&gt;&lt;/b&gt;</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Manual Jobs(s)</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

## Additional Configurations





