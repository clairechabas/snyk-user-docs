# Risk Score



{% hint style="info" %}
Risk Score is currently in Open Beta for Snyk Open Source and Snyk Container. Use [Snyk Preview](https://docs.snyk.io/snyk-admin/manage-settings/snyk-preview) to replace the Priority Score with the new Risk Score. See [Snyk feature release process](../../more-info/snyk-feature-release-process.md) for more details.
{% endhint %}

The Snyk Risk Score is a single value assigned to an issue, applied by automatic risk analysis for each security issue and based on the potential impact and likelihood of exploitability. Ranging from 0 to 1000, the score represents the risk imposed on your environment and enables a risk-based prioritization approach.&#x20;

Since real risk is scarce, you should expect a significant drift in the distribution of scores, as can be seen in this example Project scores distributions:&#x20;

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1).png" alt="Example Project scores distribution"><figcaption><p>Example Project scores distribution</p></figcaption></figure>

{% hint style="info" %}
As part of the Open Beta, the Risk Score replaces the Priority Score directly. See the [priority score docs](priority-score.md) for how to interact with the Risk Score in the UI, API, and Reports, where it is now introduced when enabled. Risk Score is not available via the CLI.&#x20;
{% endhint %}

{% hint style="info" %}
The Priority Score will be replaced with the Risk Score when Snyk Open Source and Snyk Container Projects are re-tested
{% endhint %}

{% hint style="warning" %}
Note that in the API, the relevant fields are still named with `priority.`When enabled as part of the beta, the scores and factors populated in these fields are based on the Risk Score model.&#x20;
{% endhint %}

## Explore the Risk Score by issue&#x20;

When you are looking at Issue card information, hover on the Risk Score to see the subscore and Risk Factors contributing to the score.

<div data-full-width="false">

<figure><img src="../../.gitbook/assets/image (118) (2).png" alt=".Impact, Likelihood and Risk Factors as part of the Risk Score tooltip" width="563"><figcaption><p>Impact, Likelihood and Risk Factors as part of the Risk Score tooltip</p></figcaption></figure>

</div>

## About the Risk Score Model&#x20;

<figure><img src="../../.gitbook/assets/matrix (2).png" alt="he Snyk Risk Score Model"><figcaption><p>The Snyk Risk Score Model</p></figcaption></figure>

The model that powers the Risk Score applies automatic risk analysis for each security issue based on the potential impact and likelihood of exploitability.

{% hint style="info" %}
The Risk Model results from extensive research conducted by the Snyk Security Data Science team and experienced security researchers. It draws upon years of expertise in developing the [Snyk Vulnerability Database](https://security.snyk.io/).
{% endhint %}

### Impact subscore

* Objective impact factors are the CVSS impact metrics (Availability, Confidentiality, Integrity, and Scope) and are calculated based on the CVSS impact subscore. For Container issues, Provider Urgency is also taken into account.&#x20;
* The business criticality Project attribute ([learn more](../introduction-to-snyk-projects/project-attributes.md)) will be taken into account as a contextual impact factor, increasing or decreasing the impact subscore.

### Likelihood subscore&#x20;

* Objective likelihood factors are taken into account:
  * Exploit Maturity
  * Exploit Prediction Scoring System (EPSS)&#x20;
  * Age of advisory&#x20;
  * CVSS exploitability metrics (Attack vector, Privileges required, User interaction, and Scope)&#x20;
  * Social Trends
  * Malicious Package
  * Provider Urgency (Snyk Container)
  * Package popularity (Snyk Open Source)&#x20;
  * Coming soon -  Disputed vulnerability&#x20;
* Contextual likelihood factors then increase or decrease the likelihood subscore: &#x20;
  * Reachability (Snyk Open Source Java only, JavaScript coming soon)&#x20;
  * Transitive depth
  * Coming soon - Insights such as `Deployed` , `OS condition` and `Public Facing`

{% hint style="info" %}
Fixability is no longer considered part of the Score Calculation, as the effort needed to mitigate a security issue does not affect the risk it imposes. To focus on actionable issues, use Fixability filters and use the Risk Score to start with the riskiest issues.&#x20;
{% endhint %}

## Risk factors drill down

### Objective impact risk factors

#### Confidentiality

Represents the impact on customer’s data confidentiality, based on CVSS definition.

**Possible input values:** _None, Low, High_

#### Integrity

Represents the impact on customer’s data integrity, based on CVSS definition.

**Possible input values:** _None, Low,  High_

#### Availability

Represents the impact of customer’s application availability based on CVSS definition.

**Possible input values:** _None, Low, High_

#### Scope

Indicates whether the vulnerability can affect components outside of the target’s security scope, based on CVSS definition.

**Possible input values:** _Unchanged, Changed_

{% hint style="info" %}
**How would these affect the score?** \
The objective impact subscore is calculated based on the CVSS impact subscore. Learn more about CVSS [impact definitions](https://www.first.org/cvss/v3.1/specification-document#2-3-Impact-Metrics) and [subscore equations](https://www.first.org/cvss/v3.1/specification-document#7-1-Base-Metrics-Equations)
{% endhint %}

#### Provider Urgency (Snyk Container)&#x20;

Urgency rating as provided by the relevant operating system distribution security team ([learn more](https://docs.snyk.io/scan-containers/how-snyk-container-works/understanding-linux-vulnerability-severity#external-information-sources-for-relative-importance)).&#x20;

**Possible input values:** _Critical, High, Medium,_ and _Low._ \
When neither CVSS nor Importance Rating is provided, Provider Urgency is set to 'Low' by default.

{% hint style="info" %}
**How would this affect the score?** \
_Critical_ - Impact subscore will increase significantly\
_High_ - Impact subscore will increase\
_Medium -_ Impact subscore will decrease significantly\
_Low -_ Impact subscore will decrease significantly\
\
Note that Provider Urgency will also affect the Likelihood subscore.&#x20;
{% endhint %}

### Contextual impact risk factors

#### Business Criticality&#x20;

User-defined Project attribute representing the subjective business impact of the respective application ([learn more](https://docs.snyk.io/manage-issues/introduction-to-snyk-projects/project-attributes))

**Possible input values:** _Critical, High, Medium, Low_&#x20;

{% hint style="info" %}
**How would this affect the score?** \
_Critical_ - Impact subscore will increase\
_High_ - Impact subscore will not be affected \
_Medium -_ Impact subscore will decrease\
_Low -_ Impact subscore will decrease significantly\
\
When no Business Criticality is assigned, the Impact subscore will not be affected.&#x20;
{% endhint %}

{% hint style="info" %}
When applying a Bussiness Criticality attribute to a Project, a retest is needed in order for the Risk Scores to incorporate the new data.&#x20;
{% endhint %}

### Objective likelihood risk factors

#### Exploit Maturity&#x20;

Represents the existence and maturity of any public exploit retrieved and validated by Snyk ([learn more](https://docs.snyk.io/manage-issues/issue-management/view-exploits#how-it-works-how-exploits-are-determined))

**Possible input values:** _No Known Exploit, Proof of Concept, Functional, High_

{% hint style="info" %}
**How would this affect the score?** \
_High_ - Impact subscore will increase significantly\
_Functional_ - Impact subscore will increase\
_Proof of Concept -_ Impact subscore will decrease slightly\
_No Known Exploit -_ Impact subscore will decrease significantly\
\
The likelihood subscore will increase significantly according to the level of Exploit Maturity
{% endhint %}

#### EPSS score&#x20;

Exploit Prediction Scoring System (EPSS), predicting whether a CVE would be exploited in the wild, based on an elaborated model created and owned by the FIRST Organization. \
The probability is the direct output of the EPSS model and conveys an overall sense of the threat of exploitation in the wild. This data is updated daily, relying on the latest available EPSS model version. See the EPSS [documentation](https://www.first.org/epss/articles/prob\_percentile\_bins) for more details.

**Possible input values:** _EPSS score \[0.00-1.00]_

{% hint style="info" %}
**How would this affect the score?** \
The likelihood subscore will increase significantly according to the EPSS score
{% endhint %}

#### Attack Vector&#x20;

Represents the context by which vulnerability exploitation is possible, based on the [CVSS definition](https://www.first.org/cvss/v3.1/specification-document#2-1-Exploitability-Metrics).

**Possible input values:** _Network, Adjacent, Local, Physical_

{% hint style="info" %}
**How would this affect the score?**&#x20;

_Network_ - Likelihood subscore will increase

_Adjacent, Local, Physical_ - Likelihood subscore will decrease according to the level of remote access needed to exploit the vulnerability
{% endhint %}

#### Attack Complexity&#x20;

Represents the level of complexity defined by the conditions that must exist to exploit the vulnerability, based on the [CVSS definition](https://www.first.org/cvss/v3.1/specification-document#2-1-Exploitability-Metrics).

**Possible input values:** _Low, High_

{% hint style="info" %}
**How would this affect the score?**&#x20;

_Low_ - Likelihood subscore will increase

_High_ - Likelihood subscore will decrease
{% endhint %}

#### Privileges Required&#x20;

Represents the level of privileges an attacker must possess before successfully exploiting the vulnerability, based on the [CVSS definition](https://www.first.org/cvss/v3.1/specification-document#2-1-Exploitability-Metrics).

**Possible input values:** _None, Low, High_

{% hint style="info" %}
**How would this affect the score?**&#x20;

_None_ - Likelihood subscore will increase&#x20;

_Low, High_ - Likelihood subscore will decrease according to the level of privileges required&#x20;
{% endhint %}

#### User Interaction&#x20;

Represents the need for action from a user as part of the exploitation process, based on the [CVSS definition](https://www.first.org/cvss/v3.1/specification-document#2-1-Exploitability-Metrics).

**Possible input values:** _None, Required_&#x20;

{% hint style="info" %}
**How would this affect the score?**&#x20;

_None_ -  Likelihood subscore will increase&#x20;

_Required_ - Likelihood subscore will decrease&#x20;
{% endhint %}

#### Social Trends&#x20;

Represents the social media traffic regarding this vulnerability. Snyk research has shown that greater social media interaction can predict future exploitation or point to existing exploitation ([learn more](../priorities-for-fixing-issues/vulnerabilities-with-social-trends.md)).&#x20;

**Possible input values:**  _Trending, Not trending_

{% hint style="info" %}
**How would this affect the score?**&#x20;

_Trending_ - Likelihood subscore will increase&#x20;

_Not trending_ - Likelihood subscore will not change&#x20;
{% endhint %}

#### Malicious Package&#x20;

Malicious code deployed as a supply chain dependency is considered highly exploitable

**Possible input values:** _True, False_

{% hint style="info" %}
**How would this affect the score?**&#x20;

The Likelihood subscore will increase significantly for Malicious Packages&#x20;
{% endhint %}

#### Age of vulnerability&#x20;

A new vulnerability (up to one year) is more likely to be exploited than an old vulnerability (more than one year since publication)&#x20;

**Possible input values:**  _Days since the vulnerability was first published._

{% hint style="info" %}
**How would this affect the score?**&#x20;

_Less than one year old_ - Likelihood subscore will increase&#x20;

_Over one year old_ -  Likelihood subscore will decrease&#x20;
{% endhint %}

#### Package Popularity (Snyk Open Source)&#x20;

If a package is relatively more popular for its ecosystem, it is more likely to be exploited as hackers benefit from a wider pool of potential targets.&#x20;

**Possible input values:** _High, Medium, Low_ &#x20;

{% hint style="info" %}
**How would this affect the score?**&#x20;

_High_ - Likelihood subscore will increase&#x20;

_Medium_ - Likelihood subscore will not change &#x20;

_Low_ -  Likelihood subscore will decrease
{% endhint %}

#### CVE disputed (coming soon)&#x20;

These are CVEs that have been acknowledged as being disputed by their Project maintainer or the community at large. Snyk research shows that none of the disputed CVEs in the Snyk Vulnerability DB have been exploited in the wild.

**Possible input values:** _True, False_

{% hint style="info" %}
**How would this affect the score?**&#x20;

_True_ - Likelihood subscore will decrease significantly&#x20;

_False_ - Likelihood subscore will not change
{% endhint %}

#### Provider Urgency (Snyk Container)&#x20;

Importance rating as provided by the relevant operating system distribution security team ([learn more](https://docs.snyk.io/scan-containers/how-snyk-container-works/understanding-linux-vulnerability-severity#external-information-sources-for-relative-importance)).&#x20;

**Possible input values:** _Critical, High, Medium,_ and _Low._ When neither CVSS nor Importance Rating is provided, Provider Urgency is set to 'Low' by default.

{% hint style="info" %}
**How would this affect the score?** \
_Critical_ - Impact subscore will increase significantly\
_High_ - Impact subscore will increase\
_Medium -_ Impact subscore will decrease\
_Low -_ Impact subscore will decrease significantly\
\
Note that Provider Urgency will also affect the Impact subscore.&#x20;
{% endhint %}

### Contextual likelihood risk factors

#### Transitive Depth&#x20;

Building on [past studies](https://arxiv.org/pdf/2301.07972.pdf), Snyk research has shown that if a vulnerability is introduced to a Project transitively rather than directly, it is less likely that an exploitable function path will exist

**Possible input values:** _Direct dependency, Indirect dependency, Great transitive depth (coming soon)_

{% hint style="info" %}
**How would this affect the score?**&#x20;

_Direct Dependency_ - Likelihood subscore will not change &#x20;

_Indirect Dependency_ - Likelihood subscore will decrease

_Great transitive depth -_ Likelihood subscore will decrease significantly (coming soon)
{% endhint %}

#### Reachability&#x20;

Snyk static code analysis determines whether the vulnerable method is being called. This is currently supported only in Java; JavaScript support is coming soon. [Learn more](reachable-vulnerabilities.md).

**Possible input values:** _Reachable, No path found_\
When Reachability is not enabled, the Likelihood subscore will not change, and the factor will not show up.

{% hint style="info" %}
**How would this affect the score?**&#x20;

_Reachable_ - Likelihood subscore will increase, and Transitive Depth will not be considered.&#x20;

_No path found_ - Likelihood subscore will not change
{% endhint %}

#### OS Condition (Coming Soon)&#x20;

Whether or not the operating system and architecture of a given resource are relevant to this specific issue &#x20;

**Possible input values:** _Condition not met, Condition met, No data_

{% hint style="info" %}
**How would this affect the score?**&#x20;

_Condition not met_ - Likelihood subscore will decrease significantly

_Condition met, No data_ - Likelihood subscore will not change.&#x20;
{% endhint %}

#### Deployed (coming soon)&#x20;

Whether or not the container image introducing this issue is deployed.&#x20;

**Possible input values:** _Deployed, Not Deployed, No data_

{% hint style="info" %}
**How would this affect the score?**&#x20;

_Deployed_ - Likelihood subscore will increase

_Not Deployed_ - Likelihood subscore will decrease

_No data_ - Likelihood subscore will not change
{% endhint %}

#### Public Facing (coming soon)&#x20;

Whether or not the asset introducing this issue is exposed to the internet/

**Possible input values:** _Public Facing, Not Public Facing, No data_

{% hint style="info" %}
**How would this affect the score?**&#x20;

_Public Facing_ - Likelihood subscore will increase

_Not Public Facing_ - Likelihood subscore will decrease

_No data_ - Likelihood subscore will not change
{% endhint %}

{% hint style="warning" %}
All factor names and their effect on the score are subject to change during the beta period.&#x20;
{% endhint %}

\
\
