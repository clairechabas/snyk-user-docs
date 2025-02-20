# Using Snyk Code from the CLI

The [Snyk Command Line Interface](../../../snyk-cli/) (CLI) enables you to bring the functionality of Snyk Code into your development workflow. Using the Snyk CLI, you can run Snyk Code tests locally or incorporate them into your CI/CD pipeline to scan your source code for security vulnerabilities.

## Prerequisites for using the Snyk CLI with Snyk Code

Before using the Snyk CLI for testing your source code with Snyk Code, verify you have the following prerequisites:

* A Snyk account.\
  For more information, see [Create a Snyk account](../../../getting-started/quickstart/create-a-snyk-account/).
* Repositories with code in a supported language and framework.\
  For more information, see [Snyk Code - Supported languages and frameworks](../snyk-code-language-and-framework-support.md).
* The **Snyk Code** option [enabled in your Snyk Org settings](../getting-started-with-snyk-code/enabling-the-snyk-code-option-in-an-organization.md).
* The Snyk CLI installed and authenticated.
  * For instructions, see [Install or update the Snyk CLI](../../../snyk-cli/install-or-update-the-snyk-cli/) and [Authenticate the Snyk CLI](../../../snyk-cli/authenticate-the-cli-with-your-account.md).
  * The minimum Snyk CLI version for Snyk Code, version 1.716.0. Snyk recommends using the latest version of the CLI.

## Using the Snyk CLI for Snyk Code tests

To test your repository code using the Snyk CLI, use the [`snyk code test`](../../../snyk-cli/commands/code-test.md) command.\
For more information, see [Testing your source code via the CLI](testing-your-source-code-using-the-cli.md).

Before running Snyk Code tests with the CLI, you may want to do the following:

* [Update your Snyk CLI version](../../../snyk-cli/install-or-update-the-snyk-cli/).
* [Set the Organization for the CLI tests](set-the-snyk-organization-for-the-cli-tests/).
* [Exclude directories and files from the Snyk Code test](excluding-directories-and-files-from-the-snyk-code-cli-test.md).

After running a Snyk Code test, you can do the following:

* [Explore the Snyk Code CLI results](snyk-code-cli-results.md).
* [Filter the CLI results, and display only issues with a specific severity level and higher](working-with-the-snyk-code-cli-results/displaying-only-discovered-issues-above-a-specific-severity-level.md).
* [Output the CLI results to a JSON or SARIF format in the terminal](working-with-the-snyk-code-cli-results/outputting-the-test-results-to-json-or-sarif-format-in-the-terminal.md).
* [Export the CLI results to a JSON or SARIF format file](working-with-the-snyk-code-cli-results/exporting-the-test-results-to-a-json-or-sarif-file.md).
* [Display the CLI results in an HTML format using the Snyk-to-HTML feature](displaying-the-cli-results-in-an-html-format-using-the-snyk-to-html-feature/).
