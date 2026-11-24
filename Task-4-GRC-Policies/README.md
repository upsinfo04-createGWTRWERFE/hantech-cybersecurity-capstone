# Task 4: GRC Policy Recommendations

**Organization:** HanTech  
**Purpose:** Establish repeatable rules that address weaknesses observed in the legacy-system assessment and support secure cloud operations.

These are proposed policy baselines for management approval and tailoring. They are not a claim that HanTech has formally adopted them.

## 1. Access Control Policy
**Purpose:** Ensure that only approved people and services can access HanTech systems, networks, and information.

**Minimum requirements**
- Assign each workforce member a unique account; prohibit shared administrator accounts.
- Use role-based access control and least privilege for systems, databases, cloud consoles, and file shares.
- Require MFA for privileged accounts and remote access.
- Approve access before provisioning; promptly disable access when a person leaves or changes role.
- Review privileged and sensitive access at least quarterly.
- Restrict SSH, SMB, PostgreSQL, FTP/SFTP, and management interfaces to approved networks and users.
- Log authentication, privilege changes, and access to sensitive resources.

**Ownership:** System owners approve business access; IT/security administers access and reviews; managers certify their team's access.

## 2. Password and Authentication Policy
**Purpose:** Reduce account compromise caused by weak, reused, exposed, or default credentials.

**Minimum requirements**
- Use long, unique passwords or passphrases and block known-compromised/common passwords.
- Require MFA for administrators, cloud consoles, VPN, email, and other high-impact accounts.
- Change all default credentials before a system is connected to a network.
- Never store passwords, API keys, or private keys in source code or public repositories.
- Store credentials using an approved secrets manager or secure password manager.
- Use secure password hashing for application-stored passwords; protect reset and recovery workflows.
- Rotate credentials when compromise is suspected, access is no longer needed, or policy/contract requires it.
- Use managed, narrowly scoped service credentials and monitor their use.

**Ownership:** Security defines requirements; IT enforces identity settings; users protect credentials and report suspected compromise.

## 3. Patch and Change Management Policy
**Purpose:** Keep operating systems, applications, appliances, and cloud workloads supported and updated.

**Minimum requirements**
- Maintain an inventory of assets, software versions, owners, and end-of-life dates.
- Subscribe to vendor security advisories and assess updates based on severity, exploitability, exposure, and business impact.
- Prioritize internet-facing and critical systems; define remediation deadlines in an approved standard.
- Test updates, back up relevant data/configuration, and use an approved change process.
- Record deployment evidence and verify versions after installation.
- Replace unsupported software when no secure patch is available.
- Document exceptions with business justification, compensating controls, an accountable approver, and expiry date.

**HanTech application:** Check legacy Apache, Samba, OpenSSH, PostgreSQL, and ProFTPD components against supported vendor releases and upgrade or retire them.

## 4. Vulnerability Management Policy
**Purpose:** Identify, validate, prioritize, remediate, and track weaknesses throughout the asset lifecycle.

**Minimum requirements**
1. Maintain an authorized asset and scope list before scanning.
2. Perform authenticated and unauthenticated scans at risk-based intervals and after material changes.
3. Validate scanner findings against actual product versions, configuration, and vendor advisories.
4. Prioritize using severity, exploitability, asset exposure, business impact, and compensating controls.
5. Assign each confirmed finding an owner, due date, remediation plan, and tracking record.
6. Re-test after remediation and close findings only when evidence supports closure.
7. Escalate overdue findings and formally approve time-limited risk exceptions.
8. Protect scan output and evidence because they may contain sensitive system details.

**Ownership:** Security coordinates scanning and validation; asset owners remediate; management accepts residual risk.

## 5. Acceptable Use Policy
**Purpose:** Define appropriate use of HanTech information systems and reduce misuse, accidental exposure, and unsafe behavior.

**Minimum requirements**
- Use company systems and data only for authorized business or approved learning activities.
- Do not scan, access, or test systems without documented authorization and a defined scope.
- Do not install unapproved software, disable security controls, or bypass access restrictions.
- Protect confidential information and use approved storage, transfer, and collaboration services.
- Report suspected phishing, malware, lost devices, credential exposure, or policy violations promptly.
- Do not disclose credentials or share accounts.
- Use the isolated capstone lab only for authorized exercises; never direct testing at public or third-party systems.

**Ownership:** All users comply; managers communicate requirements; IT/security investigates reported issues.

## Governance, exceptions, and review
- **Approval:** Executive management or the designated risk owner approves each policy and material revision.
- **Implementation:** IT and system owners translate policy into technical standards and procedures.
- **Awareness:** Staff and contractors receive training at onboarding and periodically thereafter.
- **Exceptions:** Identify the requirement, reason, risk, compensating controls, owner, approver, and expiry date.
- **Monitoring:** Track access reviews, MFA coverage, patch compliance, vulnerability aging, exceptions, and incidents.
- **Review cycle:** Review at least annually and after major incidents, material technology changes, or regulatory changes.

## Policy-to-finding mapping

| Assessment observation | Policy response |
|---|---|
| Legacy and potentially vulnerable services | Patch Management and Vulnerability Management |
| Exposed SSH, web, SMB, database, and FTP ports | Access Control and secure network configuration |
| Potential weak/default credentials | Password and Authentication |
| Broad or unnecessary privileges | Access Control and least privilege |
| Unauthorized testing or unsafe system use | Acceptable Use |

## Compliance note
Applicable legal and contractual obligations depend on the type of data HanTech processes, where individuals are located, and the services it provides. HanTech should complete a data inventory and obtain qualified legal/compliance advice before determining which privacy, payment-card, or sector-specific requirements apply. ISO/IEC 27001 may be used as an information-security management framework; certification is not implied by this project.
