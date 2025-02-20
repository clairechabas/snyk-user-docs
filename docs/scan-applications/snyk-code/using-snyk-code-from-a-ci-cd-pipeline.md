# Using Snyk Code from a CI/CD pipeline

Use a CI/CD integration to test your code for vulnerabilities and ensure your changes do not introduce new vulnerabilities, keeping your applications secure.

When you set up your CI/CD integration, note the following:

* Snyk Code is not yet supported in the Snyk CI plugins, for example, the Snyk Jenkins plugin, but you can use the [Snyk CLI](using-snyk-code-from-the-cli/) to integrate with your CI server.
* You can [filter the results](using-snyk-code-from-the-cli/working-with-the-snyk-code-cli-results/displaying-only-discovered-issues-above-a-specific-severity-level.md) by severity, for example, fail jobs only when high-severity vulnerabilities are introduced.
* You can [export the CLI output](using-snyk-code-from-the-cli/working-with-the-snyk-code-cli-results/outputting-the-test-results-to-json-or-sarif-format-in-the-terminal.md) to JSON or SARIF standard formats.
* You can generate more visual results using the [Snyk-to-HTML](using-snyk-code-from-the-cli/displaying-the-cli-results-in-an-html-format-using-the-snyk-to-html-feature/) tool.

To integrate Snyk Code into your CI/CD pipeline, see [Snyk CI/CD integrations](../../integrations/snyk-ci-cd-integrations/).
