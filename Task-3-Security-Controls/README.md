# Task 3: Security Control Recommendations

**Project:** From Vulnerability to Compliance: Securing Legacy and Cloud Systems at HanTech  
**Target:** Metasploitable 2 (10.0.2.4), isolated Kali Linux / VirtualBox lab

## Objective
Recommend practical controls for the five services identified in Task 1 and prioritized in Task 2. These are remediation recommendations, not evidence that changes have already been deployed.

## Control recommendations

| Finding / service | Recommended control | Implementation guidance | Validation |
|---|---|---|---|
| OpenSSH 4.7p1, TCP 22 | Patch management and secure SSH configuration | Upgrade to a supported release; disable obsolete algorithms; prohibit direct root login; prefer key-based authentication; restrict SSH to approved administration networks. | Confirm server version and effective configuration; test permitted and denied logins; review authentication logs. |
| Apache HTTP Server 2.2.8, TCP 80 | Software update and web-server hardening | Replace the end-of-life release with a supported version; remove unused modules including WebDAV if not required; apply vendor updates; restrict network access. | Check version and enabled modules; run a safe vulnerability scan; verify only required routes are reachable. |
| Samba smbd, TCP 139/445 | Version upgrade and SMB access restriction | Upgrade to a supported release; disable SMB1 where possible; restrict SMB to trusted hosts; require authentication; remove guest access unless justified; apply least-privilege share permissions. | Confirm server-side version/configuration; test authorized and unauthorized share access; review permissions and logs. |
| PostgreSQL, TCP 5432 | Access restriction and database hardening | Upgrade to a supported release; bind only to required interfaces; restrict clients with firewall rules and pg_hba.conf; require strong authentication and TLS where appropriate; minimize database-role privileges. | Verify the server version, not merely the psql client version; review listening interfaces and pg_hba.conf; test allowed and rejected connections. |
| ProFTPD 1.3.1, TCP 2121 | Vulnerability patching and secure file transfer | Upgrade or replace the legacy FTP service; prefer SFTP or FTPS; disable anonymous access unless explicitly required; isolate transfer directories; restrict network access. | Verify daemon version and TLS configuration; test authentication, directory boundaries, and network restrictions. |

## Cross-cutting controls
1. Maintain an asset inventory with owner, business purpose, exposure, software version, and lifecycle status.
2. Establish risk-based patch deadlines; test updates, deploy through change control, and record exceptions.
3. Apply default-deny network rules and expose only documented services to required source networks.
4. Use unique accounts, MFA for administrators, strong authentication, and least privilege.
5. Centralize authentication, system, database, and network logs; alert on suspicious activity.
6. Keep protected backups and test restoration on a defined schedule.
7. Re-scan after remediation and track every finding through closure.

## Suggested remediation order
1. Restrict unnecessary network exposure and disable unused services to reduce the reachable attack surface.
2. Upgrade Apache and verify the Range-header denial-of-service exposure; Task 2 rated this network-reachable finding High.
3. Confirm Samba server build/configuration and upgrade if affected; potential command execution has high system impact.
4. Confirm PostgreSQL server version and restrict database access to protect sensitive records.
5. Upgrade and harden OpenSSH and ProFTPD.

## Evidence and completion criteria
For each remediation, retain the change/ticket identifier, owner, date, approved maintenance window, before-and-after version/configuration evidence, firewall or access-control evidence, safe re-scan and functional test results, and any accepted residual risk with approver and review date.

A recommendation is not proof of remediation. Completion requires verification that the affected version/configuration has changed and a follow-up test confirms the intended control.

## Scope note
Some details remain unverified, notably the exact Samba build, PostgreSQL server version, and SSH cipher configuration. Confirm these before associating a CVE conclusively or claiming a vulnerability is present. All testing must remain within the authorized isolated lab.
