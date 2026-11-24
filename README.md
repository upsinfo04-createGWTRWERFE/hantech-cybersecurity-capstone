# HanTech Cybersecurity Capstone

**TS Academy Cybersecurity Capstone | Group 38**  
**Project:** *From Vulnerability to Compliance: Securing Legacy and Cloud Systems at HanTech*

This repository contains the team's lab assessment, risk analysis, security control recommendations, GRC policy recommendations, and cloud security review.

## Project overview

The practical assessment used Kali Linux to scan a Metasploitable 2 training target in an isolated Oracle VirtualBox lab.

| Item | Details |
|---|---|
| Assessment target | Metasploitable 2 |
| Target IP recorded in report | `10.0.2.4` |
| Tools | Nmap and Nuclei |
| Services assessed | OpenSSH, Apache, Samba, PostgreSQL, ProFTPD |
| Assessment date in supplied report | 8 November 2026 |

All testing described here is intended for the authorized lab environment only.

## Project tasks

| Task | Deliverable | Status |
|---|---|---|
| 1 | Vulnerability identification and scan evidence | Completed |
| 2 | Vulnerability risk assessment | Completed |
| 3 | Security control recommendations | Completed |
| 4 | GRC policy recommendations | Completed |
| 5 | Cloud security basics | Completed |
| Final | Consolidated capstone report | Completed |

## Repository structure

```text
.
├── README.md
├── Task-1-Vulnerability-Assesment/
│   ├── README.md
│   ├── Evidence/
│   └── Task_1_Initial_Vulnerability_Assessment_Updated.pdf
├── Task-2-Risk-Assesment/
│   └── README.md
├── Task_2_Risk_Assessment_HanTech_Revised.pdf
├── Task-3-Security-Controls/
│   └── README.md
├── Task-4-GRC-Policies/
│   └── README.md
├── Task-5-Cloud-Security/
│   └── README.md
└── Final-Report/
    └── README.md
```

The existing Task 1 and Task 2 directory spellings are retained so existing repository links are not broken.

## Key findings at a glance

- **Apache 2.2.8:** High contextual risk in Task 2 due to CVE-2011-3192 and denial-of-service potential.
- **Samba:** High contextual risk if the exact server build and vulnerable configuration conditions are confirmed.
- **PostgreSQL:** High contextual risk if the server is an affected pre-8.3.8 release and the CVE prerequisites apply.
- **OpenSSH and ProFTPD:** Medium contextual risk in the supplied Task 2 assessment, with configuration/prerequisite qualifications.

Scanner results and detected version ranges are not proof of exploitability. The project documents evidence gaps and recommends server-side verification before findings are treated as confirmed.

## How to use this repository

1. Start with Task 1 for service discovery and scan evidence.
2. Read Task 2 for likelihood, impact, risk ratings, CVEs, and evidence limitations.
3. Review Task 3 for remediation actions and validation criteria.
4. Review Task 4 for the proposed governance policies.
5. Review Task 5 for cloud responsibility and security practices.
6. Read the Final Report for the consolidated management-level view.

## Scope and responsible use

The target is a deliberately vulnerable training machine. Only scan or test systems for which you have explicit authorization. Do not use the lab instructions or tools against public, third-party, or production systems without written permission.

## Important note

The recommended controls and policies are proposals, not evidence of implementation or certification. Risk ratings are contextual and should be revisited after exact server versions, configurations, and remediation results are verified.
