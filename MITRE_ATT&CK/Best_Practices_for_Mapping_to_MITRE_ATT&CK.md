# Best Practices for MITRE ATT&CK Mapping

## INTRODUCTION

For the Cybersecurity and Infrastructure Security Agency (CISA), understanding adversary behavior is often the first step in protecting networks and data. The success network defenders have in detecting and mitigating cyberattacks depends on this understanding. The MITRE ATT&CK framework is a globally accessible knowledge base of adversary tactics and techniques based on real-world observations. ATT&CK provides details on 100+ threat actor groups, including the techniques and software they are known to use.[^1] ATT&CK can be used to identify defensive gaps, assess security tool capabilities, organize detections, hunt for threats, engage in red team activities, or validate mitigation controls. CISA uses ATT&CK as a lens through which to identify and analyze adversary behavior. CISA created this guide with the Homeland Security Systems Engineering and Development Institute (HSSEDI), a DHS-owned, federally funded research and development center (FFRDC) that works with the MITRE ATT&CK team.

[^1]: Not every adversary behavior is documented in ATT&CK

### What’s New

Since the initial release of Best Practices for MITRE ATT&CK Mapping in June 2021, malicious cyber operators and operations have continued to evolve at a rapid pace. To maintain relevancy and maximize impact for defenders, MITRE ATT&CK has also evolved the ATT&CK framework, adding major new structures, features, and techniques. Beginning with ATT&CK version nine (v9) these changes include:

* The introduction of new platforms,

* Expansion of macOS and Linux coverage,

* Increased equity between the Industrial Control Systems (ICS), Mobile, and Enterprise matrices,

* The redefinition of data sources and detections, and

* The addition of ATT&CK Campaigns.

As of version 12 (v12), ATT&CK for Enterprise contains 14 tactics, 193 techniques, and 401 subtechniques.

The January 2023 update of Best Practices for MITRE ATT&CK Mapping covers the above list of ATT&CK updates. This version of the best practices also covers common analytical biases, mapping mistakes, and specific ATT&CK mapping guidance for ICS.

### ATT&CK Levels

ATT&CK describes behaviors across the adversary lifecycle, commonly known as tactics, techniques, and procedures (TTPs). In ATT&CK, these behaviors correspond to four increasingly granular levels:

1. Tactics represent the "why" of an ATT&CK technique or sub-technique. They are the adversary's technical goals, the reason for performing an action, and what they are trying to achieve. For example, an adversary may want to achieve credential access to gain access to a target network. Each tactic contains an array of techniques that network defenders have observed being used in the wild by threat actors. Note: The ATT&CK framework is not intended to be interpreted as linear-with the adversary moving through the tactics in a straight line (i.e., left to right) to accomplish their goal.[^2] Additionally, an adversary does not need to use all the ATT&CK tactics to achieve their operational goals.

2. Techniques represent "how" an adversary achieves a tactical goal by performing an action. For example, an adversary may dump credentials to achieve credential access. Techniques may also represent what an adversary gains by performing an action. A technique is a specific behavior to achieve a goal and is often a single step in a string of activities intended to complete the adversary's overall mission. Note: Some of the techniques within ATT&CK enable an adversary to achieve multiple tactical goals and thus apply to multiple ATT&CK tactics. Many techniques also include legitimate system functions that can be used for malicious purposes (referred to as "living off the land").
   
3. Sub-techniques provide more granular descriptions of techniques. For example, there are behaviors under the OS credential dumping [T1003] technique that describe specific methods to perform the technique, such as accessing Local Security Authority Subsystem Service (LSASS) memory [T1003.001], Security Account Manager [T1003.002], or /etc/passwd and /etc/shadow [T1003.008]. Sub-techniques are often, but not always, operating system- or platform-specific. Not all techniques have sub-techniques.

4. Procedures represent "what" an adversary did and are instances of how an adversary has used a technique or sub-technique. For example, there are many different procedures of OS credential dumping: LSASS memory [T1003.001] based on using different tools, utilities, and commands. Knowing procedures may be useful for replication of an incident with adversary emulation and for detecting malicious activity.

[^2]:  For example, after initial access [TA0001] and during an operation, the adversary may exfiltrate data (exfiltration [TA0010]) and then implement additional persistence mechanisms (persistence [TA0003]), switching tactics from right to left.

### ATT&CK Technology Domains

ATT&CK is organized in three "technology domains"-the ecosystem within which an adversary operates. The ATT&CK domains have matrices that reflect associated platforms (or systems) within each technology domain:

* MITRE ATT&CK - Enterprise:[^3]
  * Operating systems: Windows, Linux, and MacOS
  * Cloud: Azure AD, Office 365, Google Workspace, Software-as-a-Service (SaaS), Infrastructure-as-a-Service (IaaS)
  * Network: Network infrastructure devices
  * Containers: Container technologies
  * PRE: Covering preparatory techniques, deprecating the previous PRE-ATT&CK domain
* MITRE ATT&CK - Mobile: Provides a model of adversarial tactics and techniques to operate within the Android and iOS platforms. ATT&CK for Mobile also contains a separate matrix of network-based effects, which are techniques that an adversary can employ without access to the mobile device itself.
* MITRE ATT&CK - Industrial Control Systems (ICS): Focuses on tactics and techniques of adversaries whose primary goal is disrupting an industrial control process, including supervisory control and data acquisition (SCADA) systems, and other control system configurations.

[^3]: ATT&CK Version 8 integrated PRE-ATT&CK techniques into ATT&CK for Enterprise, creating the new Reconnaissance and Resource Development tactics. The PRE-ATT&CK matrix was deprecated and although it remains in the knowledge base, it will no longer be updated. See MITRE's ATT&CK blog: Bringing PRE into Enterprise, October 27, 2020.

### ATT&CK Mapping Guidance

CISA is providing this guidance to help analysts accurately and consistently map adversary behaviors to the relevant ATT&CK techniques as part of cyber threat intelligence (CTI)-whether the analyst wishes to incorporate ATT&CK into a cybersecurity publication or an analysis of raw data.

Successful applications of ATT&CK should produce an accurate and consistent set of mappings, which will not directly solve security challenges but can be used to enable other operations such as:

* Developing adversary profiles.

* Conducting activity trend analysis.

* Augmenting reports for detection, response, and mitigation purposes.

Although there are different ways to approach this task, this guidance provides a starting point. Note: CISA and MITRE ATT&CK recommend that analysts first become comfortable with mapping finished reports to ATT&CK, as there are often more clues within finished reports that can aid an analyst in determining the appropriate mapping.

For additional resources on learning about and using the ATT&CK framework, see Appendix A. For guidance on mapping ATT&CK to ICS, see Appendix B.

To Map or Not to Map

Why sufficient context matters

Without adequate contextual technical details to sufficiently describe and add insight into an adversary behavior, there is little value to ATT&CK mapping. For example, a simple list of ATT&CK tactics or techniques-without associated technical context that explains how the adversary executed the techniques-may not be actionable enough to enable network defenders to detect, mitigate, or respond to the threat.

## References

https://www.cisa.gov/sites/default/files/2023-01/Best%20Practices%20for%20MITRE%20ATTCK%20Mapping.pdf
