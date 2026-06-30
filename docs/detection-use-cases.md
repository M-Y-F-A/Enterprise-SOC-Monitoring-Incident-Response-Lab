# Detection Use Cases

## Overview

This document defines the security monitoring use cases implemented as part of the Enterprise SOC Monitoring & Incident Response Lab.

Each use case represents a real-world attack technique or suspicious behavior that is monitored through Splunk detection rules. The use cases are aligned with the MITRE ATT&CK framework and validated through controlled attack simulations.

---

# Detection Engineering Workflow

Each use case follows the process below:

1. Identify the attack technique.
2. Define the monitoring objective.
3. Identify required telemetry.
4. Develop the corresponding detection rule.
5. Validate through attack simulation.
6. Tune the detection to reduce false positives.

---

# Detection Use Cases

| Use Case ID | Use Case | Objective | ATT&CK Technique | Detection Rule |
|-------------|----------|-----------|------------------|----------------|
| UC-001 | Brute Force Authentication | Detect repeated failed authentication attempts targeting user accounts. | T1110 — Brute Force | DR-001 |
| UC-002 | Authentication Anomaly | Detect abnormal or suspicious authentication behavior. | T1078 — Valid Accounts | DR-002 |
| UC-003 | Malicious PowerShell | Detect suspicious PowerShell execution commonly used during post-exploitation. | T1059.001 — PowerShell | DR-003 |
| UC-004 | Account Manipulation | Detect unauthorized account creation and privilege assignment. | T1136 — Create Account<br>T1098 — Account Manipulation | DR-004 |
| UC-005 | Windows Persistence | Detect common Windows persistence techniques such as scheduled tasks and services. | T1053.005 — Scheduled Task<br>T1543.003 — Windows Service | DR-005 |
| UC-006 | Credential Access | Detect attempts to access or dump credentials from LSASS memory. | T1003.001 — LSASS Memory | DR-006 |
| UC-007 | Lateral Movement | Detect remote administration and movement between enterprise hosts. | T1021 — Remote Services | DR-007 |
| UC-008 | Network Reconnaissance | Detect internal host discovery and network service enumeration. | T1018 — Remote System Discovery<br>T1046 — Network Service Discovery | DR-008 |

---

# Data Sources

The implemented use cases rely on the following telemetry sources:

- Windows Security Log
- Windows System Log
- Sysmon
- Active Directory Logs
- PowerShell Operational Logs
- Splunk Alerts

---

# MITRE ATT&CK Coverage

| ATT&CK Tactic | Detection Use Cases |
|---------------|---------------------|
| Execution | UC-003 |
| Persistence | UC-004, UC-005 |
| Privilege Escalation | UC-004 |
| Credential Access | UC-001, UC-006 |
| Discovery | UC-008 |
| Lateral Movement | UC-007 |
| Defense Evasion | UC-002 |