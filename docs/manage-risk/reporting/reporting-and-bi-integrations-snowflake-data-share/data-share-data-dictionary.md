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

# Data Share Data Dictionary

Snyk Data Share is a comprehensive dataset encompassing various data pillars that support a wide range of use cases. You can use this dataset to present key security metrics such as issue backlog, aging, MTTR, SLA compliance, and test coverage, as well as to prioritize issues based on different factors, such as risk score, severity, CVSS, EPSS, and many more.

This dictionary is designed to help you navigate the dataset efficiently, with clear explanations of each table's purpose and the specific data contained in each column, enabling you to leverage the X dataset to meet your data reporting needs.

## Data Share Tables

<figure><img src="../../../.gitbook/assets/Screenshot 2024-08-12 at 1.43.10 PM.png" alt="A database diagram defining the objects listed in the data dictionary"><figcaption><p>A database diagram defining the objects listed in the data dictionary</p></figcaption></figure>

The diagram above represents the objects listed in the data dictionary as a database diagram. It covers the following tables:

* [Groups](data-share-data-dictionary.md#groups)
* [Orgs](data-share-data-dictionary.md#orgs)
* [Projects](data-share-data-dictionary.md#projects)
* [Issues](data-share-data-dictionary.md#issues)
* [Usage events](data-share-data-dictionary.md#usage-events)
* [Jira issues](data-share-data-dictionary.md#issue-jira-issues)

### Groups

> current version: v1.0

The `GROUPS` table contains the main attributes of Snyk Groups. This data can be utilized for performing aggregations on the Group level or for zooming into the scope of specific Groups.

| Column name    | Data type      | Description                                                                          |
| -------------- | -------------- | ------------------------------------------------------------------------------------ |
| `public_id`    | varchar        | A universally unique identifier for a Group, assigned i the records source database. |
| `display_name` | varchar        | The name of this group.                                                              |
| `slug`         | varchar        | The name of the Group within Snyk.                                                   |
| `created`      | timestamp\_ntz | When this record was created in Snyk.                                                |
| `deleted`      | timestamp\_ntz | When this record was deleted from Snyk.                                              |
| `modified`     | timestamp\_ntz | When this record was last modified within Snyk.                                      |
| `__updated_at` | timestamp\_ntz | When the data share data transformation last updated this record.                    |

### Orgs

> current version: v1.0

The `ORGS` table contains the main attributes of Snyk Organizations. This data can be utilized for performing aggregations on the organization level or for zooming into the scope of specific organizations.

{% hint style="info" %}
The `group_public_id` column allows you to query organizations in specific groups.
{% endhint %}

| Column name       | Data type      | Description                                                                                   |
| ----------------- | -------------- | --------------------------------------------------------------------------------------------- |
| `public_id`       | varchar        | A universally unique identifier for an organization, assigned in the records source database. |
| `group_public_id` | varchar        | A universally unique identifier for a group, assigned in the records source database.         |
| `display_name`    | varchar        | The display name set for this organization.                                                   |
| `slug`            | varchar        | The name for the Organization within Snyk.                                                    |
| `created`         | timestamp\_ntz | When this record was created in Snyk.                                                         |
| `deleted`         | timestamp\_ntz | When this record was deleted from Snyk.                                                       |
| `modified`        | timestamp\_ntz | When this record was last modified within Snyk.                                               |
| `__updated_at`    | timestamp\_ntz | When the data share data transformation last updated this record.                             |

### Projects

> current version: v1.0

The `PROJECTS` table contains main attributes of Snyk Projects, as well as the related target. Its data can be utilized for performing aggregations of filters on the project or target levels, including based on project collections, project tags or specific repo branches (using `target_ref`).

{% hint style="info" %}
Snyk Reports only presents monitored projects that were not deleted. To match your results with Snyk Reports, filter your query with `IS_MONITORED = TRUE` and `DELETE IS NULL.`
{% endhint %}

| Column name                        | Data type      | Description                                                                                                                                                                                                                                |
| ---------------------------------- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `public_id`                        | varchar        | A universally unique identifier for a project, assigned in the record's source database.                                                                                                                                                   |
| `org_public_id`                    | varchar        | A universally unique identifier for an organisation, assigned in the record's source database.                                                                                                                                             |
| `group_public_id`                  | varchar        | A universally unique identifier for a group, assigned in the record's source database.                                                                                                                                                     |
| `name`                             | varchar        | The name given to this project, when added to Snyk.                                                                                                                                                                                        |
| `is_monitored`                     | boolean        | Whether this project is currently set to be actively monitored.                                                                                                                                                                            |
| `project_type`                     | varchar        | The scanning method to use for a particular Project, such as Static Application Security Testing (SAST) for scanning using Snyk Code, or Maven for a Maven project using Snyk Open Source. This is part of the configuration for scanning. |
| `project_type_display_name`        | varchar        | A display name Snyk assigned to internal project type values.                                                                                                                                                                              |
| `test_frequency`                   | varchar        | The frequency of testing for a given Project. For example, Daily, Weekly, and so on.                                                                                                                                                       |
| `origin`                           | varchar        | The Origin defines the Target ecosystem, such as CLI, GitHub, or Kubernetes. Origins are a property of Targets.                                                                                                                            |
| `target_ref`                       | varchar        | A reference that differentiates this project, for example, a branch name or version. Projects having the same reference can be grouped based on that reference.                                                                            |
| `target_runtime`                   | varchar        | The environment in which the Target is executed and run.                                                                                                                                                                                   |
| `target_display_name`              | varchar        | A display name for a project's target.                                                                                                                                                                                                     |
| `is_private_target`                | boolean        | Whether the target's source is private or publicly reachable.                                                                                                                                                                              |
| `target_source_type`               | varchar        | The hosting provider of a given target, for example, docker-hub, github, and so on.                                                                                                                                                        |
| `target_source_type_display_value` | varchar        | A display value that represents the grouping for target sources, for example, Source Control, Container Registry, and so on.                                                                                                               |
| `target_upstream_url`              | varchar        | The URL pointing to a target's upstream source, such as a URL for a GitHub repository.                                                                                                                                                     |
| `criticalities`                    | array          | A project attribute that indicates business criticality. For example, low, medium, high, critical.                                                                                                                                         |
| `lifecycles`                       | array          | A project attribute, for example, production, development, sandbox.                                                                                                                                                                        |
| `environments`                     | array          | A project attribute, for example, frontend, backend, internal, external, mobile, saas, onprem, hosted, distributed.                                                                                                                        |
| `project_collections`              | array          | All Project collections to which this project has been added.                                                                                                                                                                              |
| `project_tags`                     | array          | All tags which have been assigned to this project.                                                                                                                                                                                         |
| `project_owner_email`              | varchar        | The email of the user assigned as the owner of this project.                                                                                                                                                                               |
| `project_owner_username`           | varchar        | The username of the user assigned as the owner of this project.                                                                                                                                                                            |
| `created`                          | timestamp\_ntz | When this record was created in Snyk.                                                                                                                                                                                                      |
| `deleted`                          | timestamp\_ntz | When this record was deleted from Snyk.                                                                                                                                                                                                    |
| `modified`                         | timestamp\_ntz | When this record was last modified within Snyk.                                                                                                                                                                                            |
| `__updated_at`                     | timestamp\_ntz | When the data share data transformation last updated this record.                                                                                                                                                                          |

### Issues

> current version: v1.0

The `ISSUES` table contains various attributes of Snyk Issues. Issues can be easily correlated with their originating project, target, org or group, utilizing the corresponding ID columns. On top of the issue's basic attributes, such as its introduction date, type, severity, score, etc., there are columns that elaborate on the vulnerability attributes, such as the CVSS score, EPSS Score, NVD Score, etc.

Querying the issues table allows:

* Concluding various metrics and KPIs, among issue backlog, aging, MTTR and SLA compliance.
* Visualizing trends of identified, ignored, resolved issues over time
* Prioritize issues based on multiple factors and considerations

{% hint style="warning" %}
If you would like to match your results with Snyk Reports, filter your query with `DELETE IS NULL`, as Snyk Reports don't present deleted issues.
{% endhint %}

{% hint style="info" %}
`computed_fixability` indicates whether the issue can be fixed based on the vulnerability remediation paths, for example:

* **Fixable**: There is a fix for all the identified issues, meaning that all detailed paths have remediation.
* **Partially fixable:** The issue has upgradable paths, but not all detailed paths have remediation.
* **No supported fix**: The issue has no upgradable paths.
{% endhint %}

| Column name                      | Data type      | Description                                                                                                                                                                                   |
| -------------------------------- | -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                             | varchar        | A unique identifier, representing a unique instance of a given vulnerability in a project.                                                                                                    |
| `problem_id`                     | varchar        | Snyk Vulnerability database ID that uniquely identifies the vulnerability.                                                                                                                    |
| `project_public_id`              | varchar        | A universally unique identifier for a project, assigned in the record's source database.                                                                                                      |
| `org_public_id`                  | varchar        | A universally unique identifier for an organization, assigned in the record's source database.                                                                                                |
| `group_public_id`                | varchar        | A universally unique identifier for a group, assigned in the record's source database.                                                                                                        |
| `product_name`                   | varchar        | The Snyk Product which initially identified this issue.                                                                                                                                       |
| `problem_title`                  | varchar        | Name of the Snyk discovered vulnerability.                                                                                                                                                    |
| `vuln_db_url`                    | varchar        | URL which directs to the Snyk's Public Vulnerability Database website.                                                                                                                        |
| `issue_type`                     | varchar        | Indicates whether the issue is related to a vulnerability, license, or configuration.                                                                                                         |
| `issue_sub_type`                 | varchar        | A more granular variation of issue type.                                                                                                                                                      |
| `issue_url`                      | varchar        | URL which directs to the given's project's instance of this vulnerability on the Snyk Website.                                                                                                |
| `issue_status`                   | varchar        | Indicates whether the issue is open, resolved, or ignored.                                                                                                                                    |
| `issue_severity`                 | varchar        | Indicates the assessed level of risk, as Critical, High, Medium, or Low.                                                                                                                      |
| `score`                          | float          | A score based on an analysis model. Priority score is released in General Availability, while Risk Score is in Early Access.                                                                  |
| `cve`                            | array          | Mitre CVE ID(s)                                                                                                                                                                               |
| `cwe`                            | array          | Mitre CWE ID(s)                                                                                                                                                                               |
| `exploit_maturity`               | varchar        | Represents the existence and maturity of public exploits validated by Snyk, for example, Mature, Proof of concept.                                                                            |
| `introduction_category`          | varchar        | A Snyk generated classification describing the nature of an issue's introduction in the context of Snyk product usage, for example, Baseline Issue, Non Preventable Issue, Preventable Issue. |
| `snyk_cvss_score`                | number         | Snyk's recommended Common Vulnerability Scoring System (CVSS) score.                                                                                                                          |
| `snyk_cvss_vector`               | varchar        | The vector string of the metric values used to determine the CVSS score.                                                                                                                      |
| `nvd_severity`                   | varchar        | The vulnerability's severity as rated by NVD.                                                                                                                                                 |
| `nvd_score`                      | number         | The vulnerability's score as calculated by NVD.                                                                                                                                               |
| `epss_score`                     | number         | The probability of exploitation in the wild in the next 30 days.                                                                                                                              |
| `epss_percentile`                | number         | The proportion of all vulnerabilities with the same or lower EPSS score.                                                                                                                      |
| `computed_fixability`            | varchar        | Indicates whether the issue can be fixed based on the vulnerability remediation paths.                                                                                                        |
| `fixed_in_available`             | boolean        | Is the given vulnerability fixed in a different version of responsible source.                                                                                                                |
| `fixed_in_version`               | variant        | The first version in which a given vulnerability was fixed.                                                                                                                                   |
| `semver_vulnerable_range`        | variant        | The vulnerable range of package versions (based on semantic versioning).                                                                                                                      |
| `vulnerability_publication_date` | date           | The date a given vulnerability was first published by Snyk.                                                                                                                                   |
| `first_introduced`               | timestamp\_ntz | The timestamp of the first scan that identified the issue.                                                                                                                                    |
| `last_introduced`                | timestamp\_ntz | The most recent instance of an issue having been introduced (or reintroduced).                                                                                                                |
| `last_ignored`                   | timestamp\_ntz | The most recent instance of an issue having been ignored within Snyk's product.                                                                                                               |
| `last_resolved`                  | timestamp\_ntz | The most recent instance of an issue having been resolved.                                                                                                                                    |
| `reachability`                   | varchar        | Indicates whether the issue is related to functions that are being called by the application and thus has a greater risk of exploitability.                                                   |
| `package_name_and_version`       | varchar        | The vulnerability's associated package name and version.                                                                                                                                      |
| `deleted`                        | timestamp\_ntz | When this record was deleted from Snyk.                                                                                                                                                       |
| `__updated_at`                   | timestamp\_ntz | When the data share data transformation last updated this record.                                                                                                                             |

### Usage Events

> current version: v1.0

The `USAGE_EVENTS` table contains CLI interactions data that is collected from Snyk's CLI interfaces (CLI, IDE plugins, CI/CD pipeline tools). The CLI interaction events can be correlated with the execution context, such as their target, org or group, utilizing the corresponding ID columns.

Querying the `USAGE_EVENTS` table allows to measure:

* Developers' usage and adoption of Snyk IDE plugins
* Snyk tests in CI/CD pipelines
* Snyk CLI utilization per the different commands: test, monitor, SBOM, etc.

| Column name                               | Data type      | Description                                                                                                                                                                                                                                                                                                                          |
| ----------------------------------------- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `id`                                      | varchar        | The client-generated ID of the interaction event in the form of `urn:snyk:interaction:00000000-0000-0000-0000-000000000000`                                                                                                                                                                                                          |
| `org_public_id`                           | varchar        | A universally unique identifier for an organization, assigned in the record's source database.                                                                                                                                                                                                                                       |
| `group_public_id`                         | varchar        | A universally unique identifier for a group, assigned in the record's source database.                                                                                                                                                                                                                                               |
| `product_display_name`                    | varchar        | The Snyk product used during this interaction, for example, Snyk Open Source, Snyk IaC, Snyk Code, Snyk Container.                                                                                                                                                                                                                   |
| `runtime_application_name`                | varchar        | The application used to execute a snyk interaction, for example, PyCharm, Visual Studio, snyk-ls, snyk-cli.                                                                                                                                                                                                                          |
| `runtime_application_version`             | varchar        | The version of the integration.                                                                                                                                                                                                                                                                                                      |
| `runtime_application_data_schema_version` | varchar        | The data schema version of Snyk's runtime interactions. The current version (v2) was released in Q2 2024. Prior versions' data may behave differently.                                                                                                                                                                               |
| `interaction_type`                        | varchar        | The type of interaction, could be "Scan done". Scan Done indicates that a test was run no matter if the CLI or IDE ran it, other types can be freely chosen types.                                                                                                                                                                   |
| `interaction_categories`                  | array          | The category vector used to describe the interaction in detail, "oss","test".                                                                                                                                                                                                                                                        |
| `interaction_timestamp`                   | array          | When the interaction was started in UTC.                                                                                                                                                                                                                                                                                             |
| `interaction_status`                      | timestamp\_ntz | Status would be "success" or "failure", where success means the action was executed, while failure means it didn't run.                                                                                                                                                                                                              |
| `interaction_stage`                       | varchar        | The stage of the SDLC where the Interaction occurred, such as "dev"\|"cicd"\|"prchecks"\|"unknown".                                                                                                                                                                                                                                  |
| `interaction_exit_code`                   | integer        | The interaction's exit code as returned by the running process. More info about the exit codes and their meaning is available in Snyk Docs per a given interaction (test, monitor, etc.)                                                                                                                                             |
| `interaction_target_id`                   | varchar        | A purl is a URL composed of seven components. scheme:type/namespace/name@version?qualifiers#subpath The purl specification is available here: `https://github.com/package-url/purl-spec` Some purl examples `pkg:github/package-url/purl-spec@244fd47e07d1004f0aed9c` `pkg:npm/%40angular/animation@12.3.1` `pkg:pypi/django@1.11.1` |
| `environment_display_name`                | varchar        | The Environment used during this interaction, for example: CLI, Eclipse, Jetbrains IDE, Visual Studio, Visual Studio Code, or Other                                                                                                                                                                                                  |
| `runtime_platform_os`                     | varchar        | The operating system for the integration (darwin, windows, linux, etc).                                                                                                                                                                                                                                                              |
| `runtime_platform_arch`                   | varchar        | The architecture for the integration (AMD64, ARM64, 386, ALPINE).                                                                                                                                                                                                                                                                    |
| `runtime_environment_name`                | varchar        | The environment for the integration (e.g., IntelliJ Ultimate, Pycharm).                                                                                                                                                                                                                                                              |
| `runtime_environment_version`             | varchar        | The version of the integration environment (e.g. 2023.3)                                                                                                                                                                                                                                                                             |
| `runtime_integration_name`                | varchar        | The name of the integration, could be a plugin or extension.                                                                                                                                                                                                                                                                         |
| `runtime_integration_version`             | varchar        | The version of the integration, for example: 2.3.4.                                                                                                                                                                                                                                                                                  |
| `runtime_performance_duration_ms`         | number         | The duration in milliseconds of the interaction                                                                                                                                                                                                                                                                                      |
| `user_email`                              | varchar        | The email of the user who was authenticated during the interaction.                                                                                                                                                                                                                                                                  |
| `user_name`                               | varchar        | The name of the user who was authenticated during the interaction.                                                                                                                                                                                                                                                                   |
| `deleted`                                 | timestamp\_ntz | When this record was deleted from Snyk.                                                                                                                                                                                                                                                                                              |
| `__updated_at`                            | timestamp\_ntz | When the data share data transformation last updated this record.                                                                                                                                                                                                                                                                    |

### Issue Jira Issues

> current version: v1.0

The `ISSUE_JIRA_ISSUES` table allows to correlate between Snyk issues and assigned Jira issues. As Snyk enables more than one type of Jira integration, it's important to emphasize that the Jira issues that are available in the dataset are originated from the Jira integration that is explained in [this](https://docs.snyk.io/integrate-with-snyk/jira-and-slack-integrations/jira-integration) article.

| Object name            | Data type     | Description                                                                                    |
| ---------------------- | ------------- | ---------------------------------------------------------------------------------------------- |
| id                     | varchar       | A unique identifier, representing a unique instance of a given vulnerability in a project.     |
| `problem_id`           | varchar       | Snyk Vulnerability Database ID that uniquely identifies the vulnerability.                     |
| `project_public_id`    | varchar       | A universally unique identifier for a project, assigned in the record's source database.       |
| `org_public_id`        | varchar       | A universally unique identifier for an organization, assigned in the record's source database. |
| `group_public_id`      | varchar       | A universally unique identifier for a group, assigned in the record's source database.         |
| `jira_integration_uri` | varchar       | The URL of the Jira account provided to the Snyk Jira integration.                             |
| `jira_issues`          | array         | An array of all Jira Issues ever created for this issue.                                       |
| `latest_jira_issue`    | varchar       | The most recently created Jira Issue for this issue.                                           |
| `__updated_at`         | tiestamp\_ntz | When the data share data transformation last updated this record.                              |