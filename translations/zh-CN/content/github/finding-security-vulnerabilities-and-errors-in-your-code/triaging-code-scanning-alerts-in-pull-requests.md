---
title: Triaging code scanning alerts in pull requests
shortTitle: Triaging alerts in pull requests
intro: 'When {% data variables.product.prodname_code_scanning %} identifies a problem in a pull request, you can review the highlighted code and resolve the alert.'
product: '{% data reusables.gated-features.code-scanning %}'
permissions: 'People with write permission to a repository can resolve {% data variables.product.prodname_code_scanning %} alerts.'
versions:
  free-pro-team: '*'
  enterprise-server: '>=2.22'
---

{% data reusables.code-scanning.beta %}

### About {% data variables.product.prodname_code_scanning %} results on pull requests

In repositories where {% data variables.product.prodname_code_scanning %} is configured as a pull request check, {% data variables.product.prodname_code_scanning %} checks the code in the pull request. By default, this is limited to pull requests that target the default branch or protected branches, but you can change this configuration within {% data variables.product.prodname_actions %} or in a third-party CI/CD system. If merging the changes would introduce new {% data variables.product.prodname_code_scanning %} alerts to the target branch, these are reported as check results in the pull request. The alerts are also shown as annotations in the **Files changed** tab of the pull request. If you have write permission for the repository, you can see any existing {% data variables.product.prodname_code_scanning %} alerts on the **Security** tab. For information about repository alerts, see "[Managing {% data variables.product.prodname_code_scanning %} alerts for your repository](/github/finding-security-vulnerabilities-and-errors-in-your-code/managing-code-scanning-alerts-for-your-repository)."

If {% data variables.product.prodname_code_scanning %} has any results with a severity of `error`, the check fails and the error is reported in the check results. If all the results found by {% data variables.product.prodname_code_scanning %} have lower severities, the alerts are treated as warnings or notices and the check succeeds. If your pull request targets a protected branch, and the repository owner has configured required status checks, then you must either fix or close any error alerts before the pull request can be merged. ????????????????????????[???????????????????????????](/github/administering-a-repository/about-required-status-checks)??????

![Example pull request check status with {% data variables.product.prodname_code_scanning %} alert](/assets/images/help/repository/code-scanning-check-failure.png)

### About {% data variables.product.prodname_code_scanning %} as a pull request check

There are many options for configuring {% data variables.product.prodname_code_scanning %} as a pull request check, so the exact setup of each repository will vary and some will have more than one check. The check that contains the results of {% data variables.product.prodname_code_scanning %} is: **Code scanning results**.

If the repository uses the {% data variables.product.prodname_codeql_workflow %} a **{% data variables.product.prodname_codeql %} / Analyze (LANGUAGE)** check is run for each language before the results check runs. The analysis check may fail if there are configuration problems, or if the pull request breaks the build for a language that the analysis needs to compile (for example, C/C++, C#, or Java). As with other pull request checks, you can see full details of the check failure on the **Checks** tab. For more information about configuring and troubleshooting, see "[Configuring {% data variables.product.prodname_code_scanning %}](/github/finding-security-vulnerabilities-and-errors-in-your-code/configuring-code-scanning)" or "[Troubleshooting {% data variables.product.prodname_code_scanning %}](/github/finding-security-vulnerabilities-and-errors-in-your-code/troubleshooting-code-scanning)."

### Triaging an alert on your pull request

When you look at the **Files changed** tab for a pull request, you see annotations for any lines of code that triggered the alert.

![Example {% data variables.product.prodname_code_scanning %} alert shown as an annotation in the "Files changed" view of a pull request](/assets/images/help/repository/code-scanning-pr-annotation.png)

Some annotations contain links with extra context for the alert. In the example above, from {% data variables.product.prodname_codeql %} analysis, you can click **user-provided value** to see where the untrusted data enters the data flow (this is referred to as the source). In this case you can view the full path from the source to the code that uses the data (the sink) by clicking **Show paths**. This makes it easy to check whether the data is untrusted or if the analysis failed to recognize a data sanitization step between the source and the sink. For information about analyzing data flow using {% data variables.product.prodname_codeql %}, see "[About data flow analysis](https://help.semmle.com/QL/learn-ql/intro-to-data-flow.html)."

For more information about an alert, click **Show more details** on the annotation. This allows you to see all of the context and metadata provided by the tool in an alert view. In the example below, you can see tags showing the severity, type, and relevant common weakness enumerations (CWEs) for the problem. The view also shows which commit introduced the problem.

Alerts from some tools, like {% data variables.product.prodname_codeql %}, also include a description and a **Show more** link for guidance on how to fix the problem in the code.

![Example of "Show more details" for a {% data variables.product.prodname_code_scanning %} alert in a pull request](/assets/images/help/repository/code-scanning-pr-alert.png)

### Resolving an alert on your pull request

Anyone with write permission for a repository can resolve alerts on a pull request. If you commit changes to the pull request this triggers a new run of the pull request checks. If your changes fix the problem, the alert is resolved and the annotation removed.

If you don't think that an alert needs to be fixed, you can close the alert manually. {% data reusables.code-scanning.close-alert-examples %} The **Close** button is available in annotations and in the alerts view if you have write permission for the repository.

{% data reusables.code-scanning.false-positive-fix-codeql %}
