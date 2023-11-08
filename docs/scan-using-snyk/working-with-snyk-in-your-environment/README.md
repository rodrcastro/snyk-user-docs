# Working with Snyk in your environment

{% hint style="info" %}
**Feature availability**\
Some features mentioned on this may not be available depending on your Snyk plan or product. Each Snyk product provides key capabilities for the ecosystems you are working in.&#x20;

There is a monthly limit to the number of tests performed if a particular product is not purchased. See the [Pricing plans](https://snyk.io/plans) page for more details.
{% endhint %}

Snyk takes a developer-first approach to secure your development work, integrating directly into your IDEs, workflows, and automation pipelines to add security expertise to your toolkit. For details, see [Introducing Snyk](../../getting-started/introducing-snyk.md).

The Snyk developer-first approach allows you to:

* Use Snyk to focus on earlier enablement, not later enforcement.&#x20;
* Run scans while working on a Project to minimize rework by finding issues that require changes before you commit the code.
* Add and test packages before writing the code that interfaces with each package.
* &#x20;After writing a major section of code, scan it to find issues before continuing work.

Using  Snyk begins with importing one or more Projects and scanning for issues.

## Snyk methods of scanning

Snyk supports scanning methods that correspond to Snyk products. Choose the right scanning method for the job you want to do with a view to finding and fixing vulnerabilities early in the Software Development Life Cycle.

[Snyk Open Source](../snyk-open-source/) provides vulnerability testing and monitoring for your Projects. Open-source dependence upgrade and version bumping information, as well as license compliance information, are provided on all Snyk plans. Some capabilities may be limited for some [languages and package managers](../supported-languages-and-frameworks/).

[Snyk Code](../snyk-code/) scans your code for security vulnerabilities using source code analysis.

[Snyk Container](../snyk-container/) scans your Projects for issues with container images.

[Snyk Infrastructure as Code ](../scan-infrastructure/)scans for issues in your cloud infrastructure configurations before and after deployment.

For more information, see [Running scans](running-scans.md) and [What counts as a scan?](what-counts-as-a-test.md)

Snyk Open Source and Snyk Code allow you to [run PR Checks](../run-pr-checks/) to validate changes submitted to code and open-source packages before merging. Snyk can also retest and alert on the default branch on a scheduled basis and show results. You can use PR checks for the following:

* Code analysis with Snyk Code
* Check for Open source and licensing with Snyk Open Source
  * Check for known vulnerabilities and create Fix Pull Requests (npm/Yarn 1,2,3)
  * Check for license compliance (Snyk Open Source)
  * Address dependency upgrades by positioning updates to address technical debt (Snyk Open Source)

As you start planning and designing your applications, and your code progresses through your development process to production, Snyk provides different capabilities at each stage to help you find and fix security issues.&#x20;

## Plan and design your code

The following resources are available for all users:

* [Snyk Advisor](https://snyk.io/advisor): Helps you pick healthy open-source packages or base images to start developing with.
* [Snyk Learn](https://learn.snyk.io/): Assists you in learning to code securely.
* [Snyk Training](https://training.snyk.io/): Provides training on how to use Snyk.

## Write and deploy your code

The following capabilities are available for all Snyk users except as noted in the documentation for each capability.

* Using [Snyk IDE Plugins](../../integrations/ide-tools/) you can test your open-source packages, first-party code, and infrastructure as code (IaC) Kubernetes deployment files in your development environment as you create your Project.
* Using the [Snyk CLI](../../snyk-cli/) you can scan locally on your machine. This is useful in scanning open-source and static code as well as containers and infrastructure as code configurations, including complex files that are templated with variables, such as Terraform plan files.
* Using [Git integrations](../../integrations/git-repository-scm-integrations/) you can improve security in your Git repositories for both your code and deployed applications.
* Using CI/CD plugins and integrations you can fail the build in your integration and deployment pipeline to keep vulnerabilities out of your code.
  * There are options for passive monitoring and establishing a quality assurance gate by failing build checks based on tests for violations of policies.
  * Most CI/CD integrations use the Snyk CLI, allowing you to fail the build based on criteria specified in options or using the [snyk-filter tool](../../snyk-cli/scan-and-maintain-projects-using-the-cli/cli-tools/snyk-filter.md).
  * Snyk CI/CD integrations include Snyk plugins for Jenkins, Circle CI, and other tools as well as Partner Platforms, including Azure, Bitbucket, and AWS, that offer builit-in pipes or components for using Snyk.
  * [Github Actions](../../integrations/ci-cd-integrations/github-actions-integration/) provide additional means for securing your code in your deployment pipeline. For details and an example, see [Building a secure CI/CD pipeline with GitHub Actions for your Java Application](https://snyk.io/blog/building-a-secure-pipeline-with-github-actions/).

## Monitor your code in production

Before integrating your code into production, using the [snyk monitor](../../snyk-cli/commands/monitor.md) or [snyk container monitor](../../snyk-cli/commands/container-monitor.md) CLI command allows you to take a snapshot and monitor for vulnerabilities to avoid pushing them into production.

You can use the `snyk monitor` or [snyk container monitor](../../snyk-cli/commands/container-monitor.md) CLI command and monitor capabilities to identify issues introduced into open-source and container Projects. During implementation, monitoring helps you to gain recognition of vulnerabilities in your Projects. See [Deployment and rollout recommendations](./#deployment-and-rollout-recommendations) for details.

You can use the `snyk monitor` or `snyk container monitor` command to push results from the CLI to the Snyk Web UI, where you can view the information to help in fixing issues. Use the  `--org=` option to indicate the Organization that contains the Project, so you will use the test settings you intend and push the results to the correct Project.

Snyk Enterprise plan customers can monitor container images and their open-source and Linux-based packages being used in production through Kubernetes integration to receive notifications of known vulnerabilities for applications in production.

## How to fix issues using Snyk

If you see hundreds or thousands of issues when first scanning your application, prioritization of issues becomes the most important.

### What to fix - prioritization factors

Some tools only use the single factor of severity to prioritize issues, but this can still result in thousands of results, with no clear starting point to fix these issues.

Snyk provides more factors to help you prioritize issues, such as having a known exploit, it is fixable, or social trending. This can be done both at the Project level when looking at a specific Project, or Enterprise customers can prioritize across all Projects.

To see prioritization in action, see the [Prioritize issues in the Snyk Web UI training course](https://training.snyk.io/learn/video/prioritize-ui).

### How to fix - addressing issues

Snyk offers capabilities in this ecosystem to help address issues, both reactively and proactively:

1. **Being proactive**\
   Use [Snyk Advisor](https://snyk.io/advisor) to identify better packages to begin designing.\
   Use the CLI and IDE plugins to test while developing.\
   Add a package, make sure it’s installed, and scan for security before writing your code.
2. **Remediation advice**\
   Snyk supplies this across integrations on the results screens that calculate the top-level package requiring an update in the package manifest or how to update the line of code to make it secure.
3. **Automation**
   * You can enable automatic fix pull requests created when a new vulnerability is detected with a fix available.
   * When first importing a Project into Snyk, it may already have vulnerabilities. Instead of overwhelming you with fixes, Snyk will present the highest priority known vulnerability for you to fix first. After fixing, the next highest priority known vulnerability is presented. In this way, you can catch up and fix existing issues. You can speed this process up by fixing all vulnerabilities in a single dependency at a time by enabling **Clear backlog faster** [Snyk Preview](../../snyk-admin/manage-settings/snyk-preview.md).
   * You can enable dependency upgrade-related pull requests created when new versions of a package are available. This helps with technical debt by providing PR nudges to update dependencies.

{% hint style="info" %}
Snyk suggests enabling automated PRs on a key project to start before enabling globally to familiarize development on how to interact with Snyk and security issues.
{% endhint %}

## Deployment and rollout recommendations

Startups, small teams, individuals, and open-source maintainers typically onboard their applications using Git, getting results in minutes and starting to address issues almost immediately. Small teams have the benefit of being agile and determining what works best for their workflow.

With large organizations using hundreds of applications, a slower approach is recommended to get developer buy-in and adoption and to ensure a positive rollout experience.

1. Typically, large organizations start with daily monitoring of applications using Git integration, only, initially turning on PR checks for a few key applications.
2. As developers become familiar with Snyk capabilities, your company can widen the scope of applications with PR checks for gating or blocking builds if checks fail.
3. Some customers use CI/CD to passively monitor and then turn on gating by using the Snyk CLI `test` command for each product.
4. If you import a large number of legacy applications, you can use [Priority Score](../../manage-issues/priorities-for-fixing-issues/priority-score.md) (typically 700 as a starting place) or criteria like “Known exploit” or “Fix available” to define a starting point to engage developers to start fixing vulnerabilities for key applications.