# Java and Kotlin

## Supported frameworks and package managers

{% hint style="warning" %}
You might encounter false positives or false negatives for partially supported frameworks and package managers.
{% endhint %}

### Code analysis

Snyk Code supports the following frameworks:

* Apache Camel
* Apache Struts
* Dropwizard
* Jakarta XML Services
* Java Servlet
* JSP
* Spring MVC
* Spring JDBC

{% hint style="info" %}
**Snyk Code for Kotlin**

Snyk Code for Kotlin is currently in Open Beta, and you can [enable it through Snyk Preview](../../snyk-admin/manage-settings/snyk-preview.md).

Android is partially supported.
{% endhint %}

### Open source and licensing

Snyk Open Source provides full support for Java and Kotlin, as outlined below.

{% hint style="info" %}
Some features might not be available, depending on your pricing plan. See [pricing plans](https://snyk.io/plans/) for details.
{% endhint %}

{% hint style="info" %}
Gradle Projects imported via Git are tested by parsing `build.gradle` files. You can resolve Gradle dependencies only by executing the tool itself, but even this method can sometimes provide incomplete results.

If possible, enable [lockfiles](java-and-kotlin.md#git-services-for-gradle-projects) in your Gradle Project to improve the accuracy of Git imports.

Snyk recommends using the Snyk CLI to test Gradle Projects for the most accurate results.
{% endhint %}

{% tabs %}
{% tab title="Java" %}
**Java**

| Package managers / Features       | CLI support | Git support | License scanning | Fix PRs         |
| --------------------------------- | ----------- | ----------- | ---------------- | --------------- |
| [Maven](https://maven.apache.org) | ✔︎          | ✔︎          | ✔︎               | ✔︎              |
| [Gradle](https://gradle.org)      | ✔︎          | ✔︎          | ✔︎               | Fix advice only |
{% endtab %}

{% tab title="Kotlin" %}
**Kotlin**

| Package managers / Features       | CLI support | Git support | License scanning | Fix PRs         |
| --------------------------------- | ----------- | ----------- | ---------------- | --------------- |
| [Maven](https://maven.apache.org) | ✔︎          | ✔︎          | ✔︎               | ✔︎              |
| [Gradle](https://gradle.org)      | ✔︎          |             | ✔︎               | Fix advice only |
{% endtab %}
{% endtabs %}

#### Supported versions of Maven and Gradle

| Maven                                                                                                               | Gradle                                                                                                                                                 |
| ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| CLI - Maven `3.*` For details, see the [Snyk Maven plugin readme](https://github.com/snyk/snyk-mvn-plugin#support). | CLI - Gradle `4.*`, `5.*`, `6.*`, `7.*` For more information, see the [Snyk Gradle plugin readme](https://github.com/snyk/snyk-gradle-plugin#support). |
| Git - Maven `3.*`                                                                                                   | Git - Gradle `4.*`, `5.*`, `6.*`, `7.*`                                                                                                                |

{% hint style="info" %}
Gradle 8 is not yet supported in the CLI.&#x20;

If your app does not use Gradle 8 specific features, it is generally possible to install Gradle 7 instead before running Snyk CLI scans.
{% endhint %}

#### Open source policy

To manage licenses from your developer workflows through policy, see the following topics:

* [Defining a secure open source policy](https://snyk.io/series/open-source-security/open-source-policy/)
* [Use Snyk security policies to prioritize fixes more efficiently](https://snyk.io/blog/snyk-security-policies/)

#### Open source license compliance

To check compliance for open source licenses, see [Getting Started with Snyk License Compliance Management](https://docs.snyk.io/scan-application-code/snyk-open-source/licenses/getting-started-snyk-licensing-compliance).

## Getting started with Snyk for Java across environments

### Snyk CLI&#x20;

#### Prerequisites

1. [Create a Snyk account](../../getting-started/quickstart/create-a-snyk-account/)
2. [Install Snyk CLI and authenticate your machine](../../snyk-cli/getting-started-with-the-cli.md#install-the-snyk-cli-and-authenticate-your-machine)
3. [Set the default Organization for all Snyk tests](../../scan-applications/snyk-code/using-snyk-code-from-the-cli/set-the-snyk-organization-for-the-cli-tests/setting-the-default-organization-for-all-cli-tests.md) (code analysis)
4. Install the relevant package manager before you use the Snyk CLI.
5. Include the relevant manifest files supported by Snyk before testing.

#### Code analysis

To start testing your code using Snyk Code open your repository in a terminal and run the following  command:

```javascript
snyk code test
```

To customize test options, run other commands, exclude directories and files, and explore the results in different formats, see the following:

* [Snyk CLI commands](../../snyk-cli/commands/#available-commands)
* [Exclude directories and files from the Snyk tests](../../scan-applications/snyk-code/using-snyk-code-from-the-cli/excluding-directories-and-files-from-the-snyk-code-cli-test.md)
* [Explore test results in a JSON or SARIF format in the terminal ](../../scan-applications/snyk-code/using-snyk-code-from-the-cli/working-with-the-snyk-code-cli-results/outputting-the-test-results-to-json-or-sarif-format-in-the-terminal.md)
* [Exporting the test results to a JSON or SARIF file](../../scan-applications/snyk-code/using-snyk-code-from-the-cli/working-with-the-snyk-code-cli-results/exporting-the-test-results-to-a-json-or-sarif-file.md)

#### Open source and licensing

**Prerequisites for Snyk CLI with Java and Kotlin**

* Install the relevant package manager before you use the Snyk CLI.
* Include the relevant manifest files supported by Snyk before testing.
* Install and authenticate the Snyk CLI to start analyzing Projects from your local environment. See [Getting started with the CLI](../../snyk-cli/getting-started-with-the-cli.md).

The following table lists the steps to start scanning your dependencies. It covers basic commands, such as `snyk test` and `snyk monitor`. To check the full list, see [CLI commands and options summary](../../snyk-cli/cli-commands-and-options-summary.md).&#x20;

{% hint style="info" %}
To scan your dependencies, ensure you install the relevant package manager and that your Project contains the supported manifest files.
{% endhint %}

The way Snyk analyzes and builds the dependencies varies depending on the language and package manager of the Project.

The Snyk CLI tests Maven and Gradle Projects as follows:

* **Snyk CLI with Gradle**: To build the dependency graph, Snyk integrates with Gradle and inspects the dependencies returned by the build. The following manifest files are supported: `build.gradle` (Groovy DSL) and `build.gradle.kts` (Kotlin DSL).
* **Snyk CLI with Maven**: To build the dependency tree, Snyk analyzes the output of the `pom.xml` files.

#### CLI options for Java and Kotlin

This section describes the unique CLI commands available when working with Java-based Projects.

#### Prerequisites for Snyk CLI with Java and Kotlin

* Install the relevant package manager before you use the Snyk CLI.
* Include the relevant manifest files supported by Snyk before testing.
* Install and authenticate the Snyk CLI to start analyzing Projects from your local environment. See [Getting started with the CLI](../../snyk-cli/getting-started-with-the-cli.md).

#### Snyk CLI options for Maven and Gradle

For information about the `snyk test` and `snyk monitor` options available for use with Maven and Gradle, see the following pages:

| Package manager     | Test help                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Monitor help                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Maven               | <p><code>--maven-aggregate-project</code><br><span data-gb-custom-inline data-tag="emoji" data-code="2139">ℹ</span> See the <a href="https://docs.snyk.io/snyk-cli/commands/test#options-for-maven-projects">Options for Maven Projects</a> page for more details.<br></p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | <p><code>--maven-aggregate-project</code><br><span data-gb-custom-inline data-tag="emoji" data-code="2139">ℹ</span> See the <a href="https://docs.snyk.io/snyk-cli/commands/monitor#options-for-maven-projects">Options for Maven Projects</a> page for more details.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Gradle              | <p><code>--sub-project=&#x3C;NAME></code>, <code>--gradle-sub-project=&#x3C;NAME></code> - Test a specific Gradle sub-project.</p><p></p><p><code>--all-sub-projects</code> - Test all Gradle sub-projects.</p><p></p><p><code>--all-projects</code> - Test all Gradle projects.</p><p></p><p><code>--configuration-matching=&#x3C;CONFIGURATION_REGEX></code> - Resolve dependencies using only configuration(s) that match the specified Java regular expression.</p><p></p><p>-<code>-configuration-attributes=&#x3C;ATTRIBUTE>[,&#x3C;ATTRIBUTE>]...</code>- Select certain values of configuration attributes to install and resolve dependencies.</p><p></p><p><code>--init-script=&#x3C;FILE></code> - Used for projects with a Gradle initialization script.</p><p></p><p><span data-gb-custom-inline data-tag="emoji" data-code="2139">ℹ</span> See the <a href="https://docs.snyk.io/snyk-cli/commands/test#options-for-gradle-projects">Options for Gradle Projects </a>page for more details.</p><p></p> | <p><code>--sub-project=&#x3C;NAME></code>, <code>--gradle-sub-project=&#x3C;NAME></code> - Test a specific Gradle sub-project.</p><p></p><p><code>--all-sub-projects</code> - Test all Gradle sub-projects.</p><p></p><p><code>--all-projects</code> - Test all Gradle projects.</p><p></p><p><code>--configuration-matching=&#x3C;CONFIGURATION_REGEX></code> - Resolve dependencies using only configuration(s) that match the specified Java regular expression.</p><p></p><p><code>--configuration-attributes=[,]...</code> - Select certain values of configuration attributes to install dependencies and perform dependency resolution.</p><p></p><p><code>--init-script=&#x3C;FILE></code> - Used for projects with a Gradle initialization script.<br><br><span data-gb-custom-inline data-tag="emoji" data-code="2139">ℹ</span> See the <a href="https://docs.snyk.io/snyk-cli/commands/monitor#options-for-gradle-projects">Options for Gradle Projects</a> page for more details.</p> |
| Build tools         | <p><code>snyk test -- [&#x3C;context-specific_options>]</code><br><br><span data-gb-custom-inline data-tag="emoji" data-code="2139">ℹ</span> See the <a href="https://docs.snyk.io/snyk-cli/commands/test#options-for-build-tools">Options for build tools</a> page for more details.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | <p><code>snyk monitor -- [&#x3C;context-specific_options>]</code><br><br><span data-gb-custom-inline data-tag="emoji" data-code="2139">ℹ</span> See the <a href="https://docs.snyk.io/snyk-cli/commands/monitor#options-for-build-tools">Options for build tools</a> page for more details.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Unmanaged JAR files | <p><code>--scan-unmanaged</code> - Test unmanager files <br></p><p><code>--scan-unmanaged --file=&#x3C;JAR_FILE_NAME></code> - Test individual JAR, WAR, and AAR files<br></p><p><code>--scan-all-unmanaged</code> - Auto-detect Maven, JAR, WAR, and AAR files recursively from the current folder.<br><br><span data-gb-custom-inline data-tag="emoji" data-code="2139">ℹ</span> See the <a href="../../snyk-cli/commands/test.md#scan-all-unmanaged">Options for unmanaged JAR files</a> page for more details. </p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | <p><code>--sub-project=&#x3C;NAME></code>, <code>--gradle-sub-project=&#x3C;NAME></code> - Test a specific Gradle sub-project.</p><p></p><p><code>--all-sub-projects</code> - Test all Gradle sub-projects.</p><p></p><p><code>--all-projects</code> - Test all Gradle projects.</p><p></p><p><code>--configuration-matching=&#x3C;CONFIGURATION_REGEX></code> - Resolve dependencies using only configuration(s) that match the specified Java regular expression.</p><p></p><p><code>--init-script=&#x3C;FILE></code> - Used for projects with a Gradle initialization script.<br><br><span data-gb-custom-inline data-tag="emoji" data-code="2139">ℹ</span> See the <a href="../../snyk-cli/commands/monitor.md#scan-all-unmanaged">Options for unmanaged JAR files</a> page for more details.</p>                                                                                                                                                                                             |

#### **Use Maven arguments with the Snyk CLI**

Test a specific Maven profile called “prod”.

```
snyk test -- -prod
```

Add a system property from your pom.xml file.

Example:

The package version appears in your pom.xml

```
${pkg_version}
```

Define the system property like this:

```
snyk test -- -Dpkg_version=1.4
```

#### **Use Gradle arguments with the Snyk CLI**

*   **Use a specific configuration(s):** if you know of a build configuration that has all the required attributes and the configuration is identical across all sub-projects included in the test, specify that configuration.\
    For example:

    ```
    --configuration-matching=prodReleaseRuntimeClasspath
    ```
*   **Explicitly specify the dependency configuration:** modify intra-project dependencies in your build.gradle file(s) to use a specific configuration

    ```
      dependencies {
          implementation project(path: ':mymodulewithvariants', configuration: 'default')
      }
    ```
*   **Suggest configuration attributes:** if you receive an error when running the command, the error may indicate which attribute values are available, while the error details from Gradle also indicate which dependency variants match which attributes. Using these details, add the attribute filter option.\
    For example:

    ```
    snyk test --configuration-attributes=buildtype:release,usage:java-runtime,mode:demo
    ```

    matches the variants using `com.android.build.api.attributes.BuildTypeAttr=release` and `org.gradle.usage=java-runtime`

#### Daemon

By default, Snyk passes `gradle build --no-daemon` in the background when running `snyk test` and `snyk monitor` on Windows. If, for some reason, you see `snyk test` or `snyk monitor` fail on other operating systems because of daemon-related issues, try adding the `--no-daemon` flag to the Snyk command or set `GRADLE_OPTS: '-Dorg.gradle.daemon=false'`. See the [Gradle documentation](https://docs.gradle.org/current/userguide/gradle\_daemon.html#sec:disabling\_the\_daemon) for tips on disabling the daemon.

#### Lockfiles

If your Gradle Project makes use of a single `gradle.lockfile` or multiple `*.lockfile` per configuration, you may see the following issue:

{% code overflow="wrap" %}
```
Gradle Error (short): > Could not resolve all dependencies for configuration ':compileOnly'. > Locking strict mode: Configuration ':compileOnly' is locked but does not have lock state.
```
{% endcode %}

The **compileOnly configuration** **has been deprecated,** and even if your Project successfully generates a lockfile, the `compileOnly` state is not included because this configuration cannot be resolved.&#x20;

Only resolvable configurations compute a dependency graph. To solve this issue, Snyk suggests you update your `build.gradle` containing `dependencyLocking` logic with the following instruction**:**

```
compileOnly {resolutionStrategy.deactivateDependencyLocking() }
```

This ignores the compileOnly and saves only the necessary information to analyze your Project.

#### Support for Gradle with Snyk

If you are having any trouble testing your Gradle Projects with Snyk, collect the following details and send them to Snyk at [support@snyk.io](mailto:support@snyk.io):

* `build.gradle`
* `settings.gradle` (especially if Snyk did not pick up a version of a package)
* The output from the following commands:
  * `$ snyk test -d`
  * `$ gradle dependencies -q`



### Snyk Web UI (Git repository integration)

You can import Java repositories from any Git services (Source Control Managers) Snyk supports (see [Git repositories](../../integrations/git-repository-scm-integrations/)). After the import, Snyk analyzes your Projects based on their supported manifest files.

:link: [How Snyk works for open source and licensing](../../scan-applications/supported-languages-and-frameworks/introduction-to-snyk-supported-languages-and-frameworks.md#how-snyk-works-for-open-source-and-licensing)

#### Import Project

To import Projects from a Git repository integration:

1. Open Snyk Web UI and go to your Group and Organization.
2. Go to **Projects**.&#x20;
3. Click **Add Projects**, select the import source, and choose the repository.\
   \
   If you have an integrated Git repository (GitHub) it shows up as an option to choose from.

:link: [Import a Project](../../getting-started/quickstart/import-a-project.md)

#### Configure language settings for open source&#x20;

Configure language settings for your open source and licensing at the Organization level. The configuration settings apply to all Projects in that Organization.

1. Open Snyk Web UI and go to **Settings >** **Languages** section.
2. Under **Languages**, go to **Java** and select **Edit settings.**
3. Configure the settings for **Maven**.

* [ ] Setup your [Nexus Repository Manager for Maven](https://docs.snyk.io/integrations/package-repository-integrations/nexus-repo-manager-setup/artifactory-registry-for-maven-1)&#x20;

4. **Update Settings** to save changes.

#### Git settings for Java

From the Snyk UI, you can specify mirrors or repositories from which you’d like to resolve packages in Artifactory for Maven. For more information, see [Artifactory Registry for Maven](../../integrations/package-repository-integrations/artifactory-repository-setup/artifactory-registry-for-maven.md).

The following table includes the Git services available for Maven and Gradle Projects.&#x20;



| Maven Projects                                                                                                                                                                                                                                                                                                                                                                        | Gradle Projects                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Gradle.lockfile                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Snyk creates a Project per <code>pom.xml</code> file when it scans Maven applications. The Project includes all direct and indirect dependencies associated with that file.<br><br><span data-gb-custom-inline data-tag="emoji" data-code="2139">ℹ</span> The Project includes only the production dependencies in the<code>compile</code> and<code>runtime</code> scopes.<br></p> | <p>After you select a Project for import, Snyk builds the dependency tree based on the <code>build.gradle</code> file and (optional) <code>gradle.lockfile</code>.<br><br><span data-gb-custom-inline data-tag="emoji" data-code="2139">ℹ</span> Only production dependencies in the <code>api</code>, <code>compile</code>, <code>classpath</code>, <code>implementation</code>, <code>runtime</code> and <code>runtimeOnly</code> configurations are included.<br><br>If a lockfile is present, Snyk uses the lockfile to more accurately resolve the final version of dependencies used in the Project.</p><p>Gradle lockfiles are an opt-in feature that, among other benefits, enables reproducible builds. For more information, see the <a href="https://docs.gradle.org/current/userguide/dependency_locking.html">Gradle docs on dependency locking</a>.<br><br><span data-gb-custom-inline data-tag="emoji" data-code="26a0">⚠</span> <strong>Kotlin</strong>: <code>build.gradle.kts</code> files are not currently supported in Git.</p> | <p></p><ul><li><p><strong>Using</strong> <strong>Maven, or Gradle with a gradle.lockfile</strong>:</p><p>The Git code repository integration is a great way to use Snyk and get visibility or you may decide to use CLI/IDE or CI/CD integrations to test/gate/monitor, or do both!</p></li></ul><ul><li><p><strong>Using Gradle</strong> <strong>without a Gradle.lockfile</strong>:</p><p>The full dependency tree may not be apparent or artifacts may be pulled in from external resources, so the CLI/IDE workflow (for local scans), and CI/CD is the recommended approach for analysis, otherwise you may not have a complete view of issues and dependencies.</p></li></ul> |

The Snyk team has built plugins to make it easy to integrate Snyk into your workflows:

* [**Gradle Plugin**](https://snyk.io/blog/gradle-plugin-by-snyk-gradle-dependencies-scanning/) **(Community project)**
* [**Maven Plugin**](https://snyk.io/blog/snyk-maven-plugin-integrated-security-vulnerability-scanning-for-developers/)

#### Validating, Monitoring, Alerting, and Gating

The following capabilities are available for all Snyk users:

**With Git integrations**

Snyk allows you to [run PR Checks](../../scan-applications/run-pr-checks/) to validate submitted changes to code and open source packages before merging. Snyk can also retest and alert on the default branch on a scheduled basis, and show results.

These results are viewable on the Snyk projects screen, for:

* Your code with Snyk Code
* Open Source with Snyk Open Source
  * Check for known vulnerabilities (Snyk Open Source)
    * Create Fix Pull Requests to fix known vulnerabilities (Maven)
  * License compliance checks (Snyk Open Source)(Maven)
  * Dependency upgrade - positioning updates to address technical debt (Snyk Open Source) (Maven)

With the Git Integration, you can monitor the following on a daily basis:

* Infrastructure as code (IaC) with Snyk Infrastructure as Code

**With CI/CD integrations**

Snyk can passively monitor and provide a QA gate by failing build checks during testing for policy violations.

Snyk provides flexible capabilities, including:

* [Gradle Plugins](https://snyk.io/blog/gradle-plugin-by-snyk-gradle-dependencies-scanning/) **(Community project)**
* [Maven Plugins](https://snyk.io/blog/snyk-maven-plugin-integrated-security-vulnerability-scanning-for-developers/)
* Dedicated plugins for Jenkins, Circle CI, and others (see relevant marketplaces)
* Using [Github Actions](https://snyk.io/blog/building-a-secure-pipeline-with-github-actions/)
* The Snyk CLI can be used in most CI/CD systems (see [examples](https://github.com/snyk-labs/snyk-cicd-integration-examples))
  * Fail the build based on criteria using options or the [snyk-filter](../../snyk-api-info/other-tools/tool-snyk-filter.md) tool
  * There are [containerized](https://hub.docker.com/r/snyk/snyk) versions available
* With Partner Platforms: Azure, Bitbucket, and AWS have built-in pipes/components for use with Snyk.
  * Note for Java: using the Git integration with Bitbucket Cloud or using the CLI instead of the prepackaged Bitbucket Pipe is suggested.

#### Production monitoring

* (Snyk Enterprise plan only) Snyk can monitor container images and their open source or Linux based packages being used in production using Kubernetes integration, to notify customers of known vulnerabilities for applications in production.
* (All plans) Where a production integration does not exist, use the [snyk monitor](../../snyk-cli/commands/monitor.md) CLI command to take a snapshot and monitor what is being pushed to production.

#### Package Registry Integrations (Artifactory/Nexus) - Maven

Artifactory and Nexus Package Registry integrations are available to Snyk Enterprise plan users.

* Snyk Open Source uses Artifactory or Nexus to resolve transitive dependencies through private packages.
* Snyk can be connected to a publicly available instance using username and password or a private server on your network using the Snyk Broker.
* Snyk Open Source provides integrations with Artifactory and Nexus both as local gatekeeper, and interacting with the registry for security testing. See [Nexus Repository Manager setup](../../integrations/package-repository-integrations/nexus-repo-manager-setup/) and [Artifactory Registry setup](../../integrations/package-repository-integrations/artifactory-repository-setup/)

{% hint style="info" %}
If you are not a Snyk Enterprise user and you use Artifactory or Nexus, analysis is best performed using CLI as the build system will retrieve the dependencies and be present locally.
{% endhint %}

#### What's next?

* [Open a Fix PR](java-and-kotlin.md#open-a-fix-pr)&#x20;
* [Configure PR Checks](../../scan-applications/run-pr-checks/configure-pr-checks.md)

### Snyk integrations&#x20;

:link: For integrated development environments, see [Use Snyk in your IDE](../../integrations/ide-tools/).

:link: If you prefer continuous integration/continuous delivery workflows, you can scan with Snyk based on the integration with your automation software (see [Snyk CI/CD](../../integrations/snyk-ci-cd-integrations/) and [Snyk API](../../snyk-api/)).

## Secure your codebase and dependencies

To apply best practices for Java environments, see [Deployment and rollout recommendations](../../scan-applications/supported-languages-and-frameworks/working-with-snyk-in-your-environment/snyk-for-java-developers.md#deployment-and-rollout-recommendations) and [Language-specific and package manager-specific notes](../../scan-applications/supported-languages-and-frameworks/working-with-snyk-in-your-environment/snyk-for-java-developers.md#language-specific-and-package-manager-specific-notes).

## Troubleshooting

#### Maven Bill of Materials (BOM)

Maven supports [bill of materials (BOM) POM files](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html#bill-of-materials-bom-poms) to centralize dependency versions known to work together.

#### Contents and use of BOM files

A BOM file includes:

* a `pom` packaging type: `<packaging>pom</packaging>`.
* a `dependencyManagement` section.

Third-party Projects can provide BOM files to make dependency management easier. Here are some common examples:

* [spring-data-bom](https://github.com/spring-projects/spring-data-bom) - The Spring team provides a BOM for their Spring Data Project.
* [jackson-bom](https://github.com/FasterXML/jackson-bom) - The Jackson Project provides a BOM for Jackson dependencies.

Here is an example of a BOM file:

{% code title="Example 1 - BOM file" %}
```xml
<project ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>snyk</groupId>
    <artifactId>snyk-bom</artifactId>
    <version>1.0</version>
    <packaging>pom</packaging>
    <name>Snyk Bill Of Materials</name>
    
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>log4j</groupId>
                <artifactId>log4j</artifactId>
                <version>1.2.12</version>
            </dependency>
            <dependency>
                <groupId>commons-logging</groupId>
                <artifactId>commons-logging</artifactId>
                <version>1.1.1</version>
            </dependency>
        </dependencies>
    </dependencyManagement>
</project>
```
{% endcode %}

The `dependencyManagement` section contains dependency elements. Each dependency is a lookup reference for Maven to determine the version to select for transitive (and direct) dependencies.

Defining a dependency in the `dependencyManagement` section does not add it to the dependency tree of the Project. It is used only for lookup reference.

You can run `mvn dependency:tree` on the previous BOM example to show that Maven does not treat the contents as dependencies of the file itself.

This BOM can be imported into a Project POM as a parent. The `log4j` version does not need to be specified; it inherits it from the BOM:

{% code title="Example 2 - Project POM" %}
```xml
<project ...>
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>snyk</groupId>
        <artifactId>snyk-bom</artifactId>
        <version>1.0</version>
    </parent>
    
    <groupId>snyk</groupId>
    <artifactId>snyk-project</artifactId>
    <version>1.0.0-SNAPSHOT</version>
    <packaging>jar</packaging>
    <name>Snyk Project</name>
    
    <dependency>
        <groupId>log4j</groupId>
        <artifactId>log4j</artifactId>
    </dependency>
</project>
```
{% endcode %}

#### How Snyk handles BOMs

Snyk applies the versions in the BOM `dependencyManagement` lookup to any dependencies declared in Project POMs that import it as a `parent`.

When Snyk scans the BOM files, the `dependencyManagement` contents are not considered dependencies of that file. These are only lookups.

The following explains how Snyk analyzes and treats each of the previous example files.

* BOM file - Snyk does not create a Snyk Project for this file because it has no dependencies.
* Project POM - Snyk creates a Project with a single dependency of `log4j,` with `v1.2.12.` Snyk applies the rules from the parent BOM to identify the correct version for `log4j`. The dependency `commons-logging` is not included, as it is not directly declared in the Project POM.

{% hint style="info" %}
If a BOM has direct dependencies outside`dependencyManagement`, then Snyk creates a Project for that BOM.&#x20;
{% endhint %}

If you need help, [contact Snyk Support](https://support.snyk.io/hc/en-us).&#x20;
