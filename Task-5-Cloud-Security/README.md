# Task 5: Cloud Security Basics

## Introduction
HanTech's assessment focused on a legacy on-premises training server, but the same security principles apply to cloud workloads. Moving a system to a cloud provider does not automatically remove responsibility for patching, access control, data protection, or secure configuration.

## 1. Shared responsibility model
Security responsibilities are divided between the cloud provider and the customer. The exact division depends on the service model and contract.

| Service model | Provider generally manages | HanTech generally manages |
|---|---|---|
| Infrastructure as a Service (IaaS) | Data-centre facilities, physical hardware, networking infrastructure, and virtualization layer | Guest OS, patching, applications, workload configuration, identities, network rules, and data |
| Platform as a Service (PaaS) | Infrastructure, operating system, and managed runtime/platform components | Application code, identities, data, access settings, and secure use of platform services |
| Software as a Service (SaaS) | Application platform and underlying infrastructure | Users, roles, tenant configuration, data governance, endpoint security, and appropriate sharing |

The contract and provider responsibility matrix must be checked for each service. If HanTech deploys an outdated Apache server on an IaaS virtual machine, HanTech remains responsible for patching and securing that guest workload.

## 2. Identity and Access Management (IAM)
IAM governs who can access cloud resources and what they can do.
- **Authentication:** Verify identity using unique accounts and strong authentication.
- **Authorization:** Grant only required permissions through roles and groups.
- **Auditing:** Record sign-ins, administrative actions, policy changes, and access to sensitive resources.

Recommended practices:
- Use centralized identity and single sign-on where appropriate.
- Require MFA, especially for privileged and remote access.
- Avoid shared administrator accounts and long-lived access keys.
- Use role-based access and separate production from development privileges.
- Review access regularly and remove stale accounts and permissions.
- Alert on unusual sign-ins, privilege escalation, and disabled logging.

## 3. Multi-factor authentication (MFA)
MFA requires more than one independent proof of identity. It reduces the chance that a stolen password alone can be used to access an account.

Require MFA for cloud root/owner and administrator accounts, management consoles and privileged command-line access, VPN and remote access, email and identity-provider accounts, and access to sensitive business/customer data. Prefer phishing-resistant methods such as FIDO2 security keys or passkeys where supported. Provide secure recovery methods and protect emergency accounts.

## 4. Least privilege
Grant users, applications, and services only the permissions necessary for their tasks, for only as long as needed.
- Use roles and groups rather than broad one-off grants.
- Separate everyday accounts from privileged administration accounts.
- Use short-lived credentials or workload identities instead of embedded static keys.
- Scope service permissions to specific resources and actions.
- Review access quarterly and when roles change.
- Log and investigate privileged activity.

An exposed root shell or unrestricted administrative interface is inconsistent with least privilege and should be disabled or tightly restricted.

## 5. Cloud threats relevant to HanTech

| Threat | Potential consequence | Mitigation |
|---|---|---|
| Misconfigured storage, firewall, or security group | Public exposure of systems or sensitive data | Secure baselines, default-deny rules, configuration scanning, and peer review |
| Weak or compromised credentials | Unauthorized console or workload access | MFA, phishing-resistant authentication, secrets management, and monitoring |
| Excessive permissions | Wider impact after account or workload compromise | Least privilege, role separation, access reviews, and just-in-time elevation |
| Unpatched images and workloads | Exploitation of known software flaws | Patch SLAs, hardened images, vulnerability scanning, and retirement of unsupported software |
| Unencrypted traffic or storage | Disclosure or alteration of information | TLS in transit, encryption at rest, and managed key controls |
| Denial of service | Loss of service availability | Rate limiting, capacity planning, provider protections, monitoring, and response plans |
| Insecure APIs | Data exposure or unauthorized actions | Strong authentication, authorization checks, input validation, API inventory, and logging |
| Insider misuse or compromised endpoints | Data theft or destructive changes | Segregation of duties, endpoint protection, audit trails, and alerting |

## 6. Cloud security best practices
1. Maintain an inventory of cloud accounts, assets, data stores, and owners.
2. Apply secure configuration baselines and infrastructure-as-code review.
3. Use private networking and default-deny ingress wherever practical.
4. Encrypt sensitive data in transit and at rest; manage keys securely.
5. Store secrets in a secrets manager, never in code or repository history.
6. Centralize logs in a protected account and alert on high-risk events.
7. Back up critical data and test recovery procedures.
8. Scan container images, virtual-machine images, dependencies, and cloud configurations before deployment.
9. Separate development, test, and production environments.
10. Plan incident response, including credential revocation and provider escalation.

## 7. Compliance and governance
Applicable obligations depend on the data HanTech processes, the location of affected individuals, payment activity, industry, and contractual commitments.

Potential frameworks or requirements to assess include:
- Nigeria Data Protection Act 2023 and applicable Nigerian data-protection requirements where relevant.
- GDPR where its territorial scope and processing conditions apply.
- PCI DSS where payment-card data is stored, processed, or transmitted or the environment is otherwise in scope.
- HIPAA only where HanTech is a covered entity/business associate handling protected health information under applicable conditions.
- ISO/IEC 27001 as a voluntary information-security management system framework.

This project does not determine legal applicability or establish compliance. HanTech should inventory data flows, identify jurisdictions and contractual obligations, and seek qualified legal/compliance advice.

## Conclusion
Cloud security requires clear ownership, strong identity controls, least privilege, secure configuration, encryption, monitoring, and tested recovery. The Task 1 and Task 2 findings reinforce that legacy software and exposed services remain HanTech's responsibility when deployed in cloud workloads.
