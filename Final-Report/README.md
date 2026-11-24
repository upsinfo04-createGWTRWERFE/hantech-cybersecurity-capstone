# HanTech Cybersecurity Capstone – Final Report

**Project:** From Vulnerability to Compliance: Securing Legacy and Cloud Systems at HanTech  
**Group:** 38  
**Assessment date in supplied report:** 8 November 2026  
**Lab target:** Metasploitable 2 – 10.0.2.4

## Executive summary
The capstone used Nmap and Nuclei in an isolated Kali Linux / Metasploitable 2 lab to identify exposed legacy services, assess potential risk, and recommend technical and governance controls. The five assessed services were OpenSSH, Apache HTTP Server, Samba, PostgreSQL, and ProFTPD.

Task 2 rated Apache and the conditional Samba/PostgreSQL findings High contextual risk, while OpenSSH and ProFTPD were rated Medium. These ratings are risk judgments for the lab and depend on validation of the relevant server versions and configurations. No successful exploitation is claimed.

The recommended response is to reduce unnecessary network exposure, upgrade unsupported software, harden authentication and service configuration, apply least privilege, monitor activity, and establish repeatable patch and vulnerability-management processes. The same principles apply to HanTech cloud workloads under the shared responsibility model.

## Project scope and methodology
- **Attacker system:** Kali Linux
- **Target:** Metasploitable 2 training machine
- **Virtualization:** Oracle VirtualBox
- **Tools:** Nmap and Nuclei
- **Services in scope:** OpenSSH, Apache, Samba, PostgreSQL, and ProFTPD
- **Scope limitation:** The work describes scanning and risk assessment. It does not establish that exploitation was performed or that each scanner alert is a confirmed exploitable vulnerability.

The supplied assessment identifies target IP 10.0.2.4 and scan date 8 November 2026. Nmap and Nuclei screenshots are retained in the Task 1 report/evidence supplied by the project.

## Task 1 – Vulnerability identification

| Service | Observed service detail in project | Security concern |
|---|---|---|
| OpenSSH | 4.7p1 Debian build, TCP 22 | Legacy SSH implementation and potentially weak/obsolete cryptographic configuration; applicability of specific CVEs requires cipher/configuration validation. |
| Apache HTTP Server | 2.2.8, DAV/2, TCP 80 | End-of-life web server; CVE-2011-3192 is relevant to affected Apache 2.2 releases and can cause denial of service. |
| Samba | Nmap reported broad 3.x–4.x range; TCP 139/445 | Legacy SMB service; CVE-2007-2447 applies to specific Samba versions/configurations, so exact server build and configuration must be confirmed. |
| PostgreSQL | Nmap indicated legacy 8.3 series, TCP 5432 | Older releases have security issues; server-side version must be confirmed because a local psql client version does not establish the server version. |
| ProFTPD | 1.3.1, TCP 2121 | Legacy FTP daemon and potential security weaknesses; validate exact build and applicable advisory before claiming exploitability. |

Scanner output is a starting point for investigation, not proof of successful exploitation. Findings should be confirmed against server-side versions, configuration, and authoritative vendor advisories.

## Task 2 – Vulnerability risk assessment

| Service | CVE assessed in Task 2 | Likelihood | Impact | Overall risk | Key qualification |
|---|---|---|---|---|---|
| OpenSSH | CVE-2008-5161 | Medium | Low–Medium | Medium | Depends on CBC-mode cipher use; cipher list was not verified. |
| Apache | CVE-2011-3192 | High | High | High | Apache 2.2.8 is in the affected range; crafted Range headers can cause resource exhaustion and denial of service. |
| Samba | CVE-2007-2447 | Medium–High | High | High | Exact Samba version and vulnerable configuration must be confirmed. |
| PostgreSQL | CVE-2009-3230 | Medium | High | High | Affected server releases are earlier than 8.3.8; verify server version and applicable conditions. |
| ProFTPD | CVE-2008-4242 | Low–Medium | Medium | Medium | Browser-based FTP CSRF scenario requires an existing browser FTP session and user interaction. |

### Risk interpretation
Likelihood and impact are qualitative judgments for this lab, not a production risk calculation. CVSS scores from different versions (v2, v3.0, v3.1) should not be compared as if they used an identical scale. The overall contextual rating also considers network reachability and prerequisites.

**Evidence gaps to close:** Obtain the exact Samba server version and configuration; verify the PostgreSQL server version (not just the client); inspect the effective SSH cipher configuration; and confirm the ProFTPD build and configuration. Reassess ratings after validation.

## Task 3 – Security control recommendations

| Service | Primary control | Practical action |
|---|---|---|
| OpenSSH | Patch management | Upgrade to a supported release, disable obsolete algorithms, restrict administration access, and prohibit direct root login. |
| Apache | Software update | Replace Apache 2.2.8 with a supported release, remove unused modules, and restrict inbound web access to required paths and sources. |
| Samba | Version upgrade | Upgrade to a supported Samba release, disable SMB1 where possible, restrict SMB network access, and enforce authenticated least-privilege shares. |
| PostgreSQL | Access restriction | Upgrade, limit listening interfaces and client networks, harden pg_hba.conf, require strong authentication, and grant minimum database privileges. |
| ProFTPD | Vulnerability patching | Upgrade or replace legacy FTP; prefer SFTP/FTPS and restrict accounts, directories, and network access. |

Cross-cutting measures include an asset inventory, formal patch/change management, network segmentation, MFA, centralized logging, protected backups, and post-remediation scanning. Closure requires evidence of the changed version/configuration and a successful verification test.

## Task 4 – GRC policy recommendations
1. **Access Control Policy:** Unique accounts, role-based access, least privilege, MFA for privileged access, prompt deprovisioning, and quarterly access reviews.
2. **Password and Authentication Policy:** Long unique credentials, blocking compromised passwords, MFA, removal of defaults, secure credential storage, and secrets management.
3. **Patch and Change Management Policy:** Asset inventory, risk-based patch deadlines, testing, approved change records, post-install verification, and time-limited exceptions.
4. **Vulnerability Management Policy:** Authorized scanning, validation, risk-based prioritization, assigned owners and due dates, re-testing, and documented risk acceptance.
5. **Acceptable Use Policy:** Authorized use only, no unapproved scanning or software, protection of company data and credentials, and prompt incident reporting.

Policies should have named owners, management approval, staff awareness, measurable compliance indicators, an exception process, and at least annual review.

## Task 5 – Cloud security basics
- **Shared responsibility:** Providers secure underlying cloud infrastructure; HanTech remains responsible for its data, identities, tenant configuration, and (depending on IaaS/PaaS/SaaS) operating systems and applications.
- **IAM:** Authenticate users, authorize access through roles, and audit actions through protected logs.
- **MFA:** Require additional authentication for privileged accounts, cloud consoles, remote access, and email; prefer phishing-resistant methods where supported.
- **Least privilege:** Use scoped roles, separate admin accounts, short-lived credentials, and regular access reviews.
- **Threats:** Misconfiguration, weak credentials, excessive permissions, unpatched workloads, unencrypted data, denial of service, insecure APIs, and insider misuse.
- **Best practices:** Default-deny networking, encryption in transit and at rest, secure images, secrets management, centralized monitoring, tested backups, asset inventory, and incident response.
- **Compliance:** Determine obligations from actual data types, jurisdictions, and contracts. Potentially relevant regimes include Nigeria's Data Protection Act 2023, GDPR where applicable, PCI DSS for in-scope payment-card environments, and HIPAA only for applicable protected-health-information relationships. ISO/IEC 27001 can provide an ISMS framework. This report is not a legal determination or certification claim.

## Prioritized action plan
| Sequence | Action | Expected outcome |
|---|---|---|
| Immediate | Confirm authorization/scope and restrict unnecessary exposed ports | Reduced attack surface |
| High | Validate Apache, Samba, and PostgreSQL versions/configurations; upgrade affected unsupported components | Removal or confirmation of high-risk exposure |
| High | Enforce strong authentication, MFA, and least privilege | Reduced account compromise and privilege abuse |
| Medium | Upgrade/harden SSH and replace or secure legacy FTP | Safer administrative and file-transfer access |
| Ongoing | Formalize patch, vulnerability, access-review, logging, and backup processes | Repeatable security governance |
| Ongoing | Re-scan and document remediation evidence | Verifiable risk reduction |

## Conclusion
The lab demonstrates how exposed services and unsupported software can increase risk. HanTech should first validate the conditional findings, reduce unnecessary exposure, and remediate unsupported services. Technical controls must be supported by accountable GRC policies and cloud governance. Follow-up testing and documented evidence are necessary before any finding can be marked resolved.

## References
- Nmap: https://nmap.org/
- ProjectDiscovery Nuclei: https://github.com/projectdiscovery/nuclei
- OpenSSH: https://www.openssh.com/
- NVD – CVE-2008-5161: https://nvd.nist.gov/vuln/detail/CVE-2008-5161
- Apache HTTP Server 2.2 security advisories: https://httpd.apache.org/security/vulnerabilities_22.html
- Samba – CVE-2007-2447: https://www.samba.org/samba/security/CVE-2007-2447.html
- PostgreSQL 8.3 security information: https://www.postgresql.org/support/security/8.3/
- NVD – CVE-2009-3230: https://nvd.nist.gov/vuln/detail/CVE-2009-3230
- Debian Security Tracker – CVE-2008-4242: https://security-tracker.debian.org/tracker/CVE-2008-4242

## Source note
This report consolidates the supplied TS Academy Cybersecurity Capstone Project | HanTech document (Group 38, assessment date 8 November 2026) and the repository's Task 1/Task 2 materials. It preserves the risk qualifications and evidence limitations stated in Task 2. It does not claim that recommended controls have been deployed.
