# C/C++

## Supported frameworks and package managers

{% hint style="warning" %}
You might encounter false positives or false negatives for partially supported frameworks and package managers.
{% endhint %}

### Code analysis

* **.NET 6.0 (LTS)**
* **ASP.NET (version 6.x)**
* **.NET Core**

### Open source and licensing

#### Open source policy

To manage licenses from your developer workflows through policy, see the following topics:

* [Defining a secure open source policy](https://snyk.io/series/open-source-security/open-source-policy/)
* [Use Snyk security policies to prioritize fixes more efficiently](https://snyk.io/blog/snyk-security-policies/)

<table><thead><tr><th width="267">Package managers / Features</th><th>CLI support</th><th>Git support</th><th>License scanning</th><th>Fix PRs</th></tr></thead><tbody><tr><td>C/C++</td><td>✔︎</td><td></td><td>✔︎</td><td></td></tr></tbody></table>

#### Open source license compliance

To check compliance for open source licenses, see [Getting Started with Snyk License Compliance Management](https://docs.snyk.io/scan-application-code/snyk-open-source/licenses/getting-started-snyk-licensing-compliance).

## Getting started with Snyk for C/C++ across environments

Scans are powered by an open source database, periodically updated with the latest source code from online sources.

{% hint style="info" %}
To navigate through the vulnerabilities for C/C++, use the [Snyk Vuln DB](https://security.snyk.io).
{% endhint %}

When you run the [`snyk test --unmanaged`](../../snyk-cli/commands/test.md#unmanaged) command, Snyk does the following:

1. Converts all files from your current folder into a list of hashes.
2. Sends hashes to the Snyk scan server to compute the dependencies list.
3. Queries the database to find a list of potentially matching dependencies.
4. Links the dependencies to the known vulnerabilities.
5. Displays the results.

{% hint style="info" %}
For Snyk to scan the Project, the dependencies must be available as source code in the scanned directory. If the dependencies are in a different location, that location must be scanned.
{% endhint %}

### Scanning archives

By default, archives are not scanned. However, Snyk CLI can recursively extract archives to analyze the source code inside.

To enable archive extraction, specify the depth of the extraction using the `--max-depth` option.

The supported archive formats are:

* zip-like archives
* tar archives
* tar with gzip compression algorithm

### Constraints and limitations

{% hint style="info" %}
The following constraints and limitations are by design. While Snyk may work on improvements in the future, they are not considered an issue.&#x20;
{% endhint %}

### **Source code dependencies need to be available in the scanned folder**

For Snyk CLI to be able to find dependencies in your source code, enough of the full dependencies source code needs to be present in the scanned folder.

Having a large percentage of files in their original (unchanged) form is critical to accurately identifying dependencies and reporting the correct set of vulnerabilities back. Modifying that source code reduces the confidence of the scanning engine, resulting in less accurate results. Other potential issues could include dependencies not being identified or being identified incorrectly, as a different version or even a different package.

The example that follows shows a typical package with dependencies listed:

```
c-example
├── deps
│   ├── curl-7.58.0
│   │   ├── include
│   │   │   ├── Makefile.am
│   │   │   ├── Makefile.in
│   │   │   ├── README
│   │   │   └── curl
│   │   ├── install-sh
│   │   ├── lib
│   │   │   ├── asyn.h
│   │   │   ├── base64.c
│   │   │   ├── checksrc.pl
│   │   │   ├── config-amigaos.h
│   │   │   ├── conncache.c
│   │   │   ├── conncache.h
│   │   ├── src
│   │   │   ├── tool_binmode.c
│   │   │   ├── tool_binmode.h
│   │   │   ├── tool_bname.c
│   │   │   ├── tool_xattr.c
...
```

### Data collection note

When you scan C++ Projects, the following data is collected and may be stored for troubleshooting purposes:

**Hashes of the scanned files:** All files are converted to a list of irreversible hashes.

**Relative paths to scanned files:** The paths to files relative to the directory being scanned are included for better identification and matching.\
\
Example:\
`./project-name/vendor/bzip2-1.0.6/blocksort.c`

### Snyk CLI&#x20;

#### Prerequisites

1. [Create a Snyk account](../../getting-started/quickstart/create-a-snyk-account/)
2. [Install Snyk CLI and authenticate your machine](../../snyk-cli/getting-started-with-the-cli.md#install-the-snyk-cli-and-authenticate-your-machine)
3. [Set the default Organization for all Snyk tests](../snyk-code/using-snyk-code-from-the-cli/set-the-snyk-organization-for-the-cli-tests/setting-the-default-organization-for-all-cli-tests.md) (code analysis)

#### Code analysis

To start testing your code using Snyk Code open your repository in a terminal and run the following  command:

```javascript
snyk code test
```

To customize test options, run other commands, exclude directories and files, and explore the results in different formats, see the following:

* [Snyk CLI commands](../../snyk-cli/commands/#available-commands)
* [Exclude directories and files from the Snyk tests](../snyk-code/using-snyk-code-from-the-cli/excluding-directories-and-files-from-the-snyk-code-cli-test.md)
* [Explore test results in a JSON or SARIF format in the terminal ](../snyk-code/using-snyk-code-from-the-cli/working-with-the-snyk-code-cli-results/outputting-the-test-results-to-json-or-sarif-format-in-the-terminal.md)
* [Exporting the test results to a JSON or SARIF file](../snyk-code/using-snyk-code-from-the-cli/working-with-the-snyk-code-cli-results/exporting-the-test-results-to-a-json-or-sarif-file.md)

#### Open source and licensing

**Run the test**

To test your Project for vulnerabilities, run the following:

```
$ snyk test --unmanaged
```

**Displaying dependencies**

To display dependencies, use the `--print-deps` option:

```bash
$ snyk test --unmanaged --print-deps

Dependencies:

  cpython|https://github.com/python/cpython/archive/v3.7.2.zip@3.7.2
  confidence: 1.000
  
  zip|http://ftp.debian.org/debian/pool/main/z/zip/zip_3.0.orig.tar.gz@3.0
  confidence: 0.993
```

To learn what files contributed to each dependency being identified, use the `--print-dep-paths` option:

```bash
$ snyk test --unmanaged --print-dep-paths

Dependencies:

  curl|https://github.com/curl/curl/releases/download/curl-7_58_0/curl-7.58.0.tar.xz@7.58.0
  confidence: 1.000
  matching files:
    - c-example/deps/curl-7.58.0/CHANGES
    - c-example/deps/curl-7.58.0/CMake/CMakeConfigurableFile.in
    - c-example/deps/curl-7.58.0/CMake/CurlSymbolHiding.cmake
    ... and 2857 more files
```

**Understanding the confidence level**

You may need to change the source code of the dependencies that you use in your software. As Snyk uses file signatures to find the closest possible match to an open-source library, your changes may decrease the accuracy of the identification of the actual library.

To learn how confident Snyk is about the identified dependency and its version, use the `--print-deps` or `--print-dep-paths` command line option:

```
curl|https://github.com/curl/curl/releases/download/curl-7_58_0/curl-7.58.0.tar.xz@7.58.0
confidence: 0.993
```

This confidence level shows how confident Snyk is about the actual identification of the dependency. The number can be between **0** and **1** and the higher it is, the more accurate the identification is. Thus a confidence of **1** means that all the files in the source tree fully matched all the expected files in the Snyk database.

**JSON output**

To get a machine-readable output in JSON, use the `--json` option:

```
$ snyk test --unmanaged --json
[
  {
    "issues": [
      {
        "pkgName": "curl|https://github.com/curl/curl/releases/download/curl-7_58_0/curl-7.58.0.tar.xz",
        "pkgVersion": "7.58.0",
        "issueId": "CVE-2019-5481",
        "fixInfo": {
          "isPatchable": false,
          "isPinnable": false
        }
      }
    ],
    "issuesData": {
      "CVE-2019-5481": {
        "severity": "high",
        "CVSSv3": "",
        "originalSeverity": "high",
        "severityWithCritical": "high",
        "type": "vuln",
        "alternativeIds": [
          ""
        ],
        "creationTime": "2019-09-16T19:15:00.000Z",
        "disclosureTime": "2019-09-16T19:15:00.000Z",
        "modificationTime": "2020-10-20T22:15:00.000Z",
        "publicationTime": "2019-09-16T19:15:00.000Z",
        "credit": [
          ""
        ],
        "id": "CVE-2019-5481",
        "packageManager": "cpp",
        "packageName": "curl|https://github.com/curl/curl/releases/download/curl-7_58_0/curl-7.58.0.tar.xz",
        "language": "cpp",
        "fixedIn": [
          ""
        ],
        "patches": [],
        "exploit": "No Data",
        "functions": [
          ""
        ],
        "semver": {
          "vulnerable": [
            "7.58.0"
          ],
          "vulnerableHashes": [
            ""
          ],
          "vulnerableByDistro": {}
        },
        "references": [
          {
            "title": "https://curl.haxx.se/docs/CVE-2019-5481.html",
            "url": "https://curl.haxx.se/docs/CVE-2019-5481.html"
          },
        ],
        "internal": {},
        "identifiers": {
          "CVE": [
            "CVE-2019-5481"
          ],
          "CWE": [],
          "ALTERNATIVE": [
            ""
          ]
        },
        "title": "CVE-2019-5481",
        "description": "",
        "license": "",
        "proprietary": true,
        "nearestFixedInVersion": ""
      }
    },
    "fileSignaturesDetails": {
      "curl|https://github.com/curl/curl/releases/download/curl-7_58_0/curl-7.58.0.tar.xz@7.58.0": {
        "filePaths": [
          "deps/curl-7.58.0/CHANGES",
          "c-example/deps/curl-7.58.0/CMake/CMakeConfigurableFile.in",
          "c-example/deps/curl-7.58.0/CMake/CurlSymbolHiding.cmake"
        ],
        "confidence": 1
      }
    }
  }
]
```

**Command line options**

The following `snyk` command line options are supported with the `snyk test --unmanaged` and `snyk monitor --unmanaged` commands:

`--org=<ORG_ID>`\
`--json`\
`--json-file-output=<OUTPUT_FILE_PATH>` (`snyk test` only)\
`--remote-repo-url=<URL>`\
`--severity-threshold=<low|medium|high|critical>` (`snyk test` only)\
`--max-depth`\
`--print-dep-paths`\
`--target-reference=<TARGET_REFERENCE>` (`snyk monitor` only)\
`--project-name=<c-project>` (`snyk monitor` only)

For more information about command line options, see the Snyk help docs: [Options for scanning with `snyk test --unmanaged`](https://docs.snyk.io/snyk-cli/commands/test#options-for-scanning-using-unmanaged) or [`snyk monitor --unmanaged`](https://docs.snyk.io/snyk-cli/commands/monitor#options-for-scanning-using-unmanaged).

To import the test results (issues and dependencies) in the Snyk CLI, run the `snyk monitor --unmanaged` command:

```
$ snyk monitor --unmanaged
Monitoring /c-example (c-example)...

Explore this snapshot at https://app.snyk.io/org/example-org/project/8ac0e233-d0f9-403e-b422-5970e7a37443/history/5de4616d-3967-485f-bf21-bbbe91068029

Notifications about newly disclosed issues related to these dependencies will be emailed to you.
```

This creates a snapshot of dependencies and vulnerabilities and imports them into the Snyk Web UI, where you can review the issues and see them included in your reports.

Importing a Project with unmanaged dependencies creates a new Project:

<figure><img src="../../.gitbook/assets/Screenshot 2023-08-04 at 11.18.10.png" alt=""><figcaption><p>Project with unmanaged dependencies</p></figcaption></figure>

{% hint style="info" %}
Snyk Web UI supports only code analysis, using Snyk Code.
{% endhint %}

### Snyk integrations

#### Snyk Code

No additional options are required. The Snyk plugin has views within the IDE for displaying results.

**Snyk Open Source**&#x20;

Under **Additional Parameters** in the IDE settings, enter the **--unmanaged** option to scan for C/C++ open source dependencies.

<figure><img src="../../.gitbook/assets/Screenshot 2023-08-04 at 12.18.01.png" alt=""><figcaption><p>Scan for dependencies</p></figcaption></figure>

## Secure your codebase and dependencies

To apply best practices for C/C++ environments, see [Deployment and rollout recommendations](broken-reference) and [Language/Open Source specific facts for using Snyk](broken-reference).

## Troubleshooting

### **Is my Snyk Open Source code sent to Snyk servers?**

No. The files are converted to a list of hashes before they are sent for scanning.

### **Why did Snyk not find any dependencies?**

Snyk stores the official releases of many open-source components in the Snyk database but it is possible that the source code you scanned is not there or is not found. If your scan does not find any dependencies [submit a request to support](https://support.snyk.io/hc/en-us/requests/new).

Here are a few things that you can check on your own:

* The source code of the dependencies you scanned is available as source code (unpacked) in the folder that you scanned. If you use a package manager, such as Conan, the source code is likely to be in the Conan cache, along with the source code of other dependencies of your other Projects. To scan dependencies managed by a package manager, Snyk recommends that you do that in a clean environment (for example, during a build).
* The source code of the dependencies is not from an official release of the open source software (OSS) component, and Snyk does not have it in the database.
* The source code of the OSS has been modified too much, so Snyk cannot detect it. If there are too few files and you modify most of them, Snyk cannot match them to a component from the Snyk database. Examples of common modifications are whitespace formatting and adding license or copyright headers.
* Symlinks are not followed when collecting files for hashing. However, a Linux source package unzipped in Windows will usually have in-package symlinks replaced by _copies_ of linked files, thus creating a situation where the Windows representation is different from the original source. If the difference is too large, this can lead to Snyk not detecting it.
* The source code of the OSS components is too new. The Snyk database is refreshed monthly but it takes time for the latest releases to get processed.
