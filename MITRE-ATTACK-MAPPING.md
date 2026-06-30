# MITRE ATT&CK Mapping

## Overview

This document maps the implemented detection rules within the Enterprise SOC Monitoring & Incident Response Lab to the MITRE ATT&CK framework.

The mapping provides a standardized view of adversary behaviors, detection coverage, and SOC monitoring capabilities. Each detection rule is aligned with one or more ATT&CK tactics and techniques to demonstrate how security events are identified throughout the attack lifecycle.

---

# ATT&CK Coverage Matrix

| Detection ID | Detection Rule | ATT&CK Tactic | ATT&CK Technique | Technique ID |
|--------------|----------------|---------------|------------------|--------------|
| DR-001 | Brute Force Authentication | Credential Access | Password Guessing | T1110.001 |
| DR-002 | Authentication Anomaly | Defense Evasion, Persistence, Initial Access | Valid Accounts | T1078 |
| DR-003 | Malicious PowerShell | Execution | PowerShell | T1059.001 |
| DR-004 | Account Manipulation | Persistence, Privilege Escalation | Create Account | T1136 |
| DR-004 | Account Manipulation | Persistence | Account Manipulation | T1098 |
| DR-005 | Windows Persistence | Persistence | Scheduled Task | T1053.005 |
| DR-005 | Windows Persistence | Persistence | Create or Modify System Process: Windows Service | T1543.003 |
| DR-006 | Credential Access | Credential Access | OS Credential Dumping: LSASS Memory | T1003.001 |
| DR-007 | Lateral Movement | Lateral Movement | Remote Services | T1021 |
| DR-008 | Network Reconnaissance | Discovery | Network Service Discovery | T1046 |

---

# Coverage by ATT&CK Tactic

| ATT&CK Tactic | Detection Rules |
|---------------|-----------------|
| Initial Access | DR-002 |
| Execution | DR-003 |
| Persistence | DR-002, DR-004, DR-005 |
| Privilege Escalation | DR-004 |
| Defense Evasion | DR-002 |
| Credential Access | DR-001, DR-006 |
| Discovery | DR-008 |
| Lateral Movement | DR-007 |

---

# Detection Coverage Summary

| Category | Coverage |
|----------|----------|
| Authentication Security | DR-001, DR-002 |
| Endpoint Execution | DR-003 |
| Identity & Account Security | DR-004 |
| Persistence Mechanisms | DR-005 |
| Credential Protection | DR-006 |
| Lateral Movement | DR-007 |
| Network Discovery | DR-008 |

---

# Detection Workflow

Each implemented detection follows the same engineering workflow:

1. Define the attack technique.
2. Identify the required telemetry.
3. Develop the Splunk SPL search.
4. Validate using a controlled attack simulation.
5. Tune the detection to reduce false positives.
6. Deploy the search as a Splunk alert.
7. Map the detection to the MITRE ATT&CK framework.
8. Document investigation guidance.

---

# Detection Coverage Status

| Detection Rule | ATT&CK Mapping | Status |
|----------------|----------------|--------|
| DR-001 | Complete | Implemented |
| DR-002 | Complete | Implemented |
| DR-003 | Complete | Implemented |
| DR-004 | Complete | Implemented |
| DR-005 | Complete | Implemented |
| DR-006 | Complete | Implemented |
| DR-007 | Complete | Implemented |
| DR-008 | Complete | Implemented |

---

# Future Coverage

Planned enhancements include expanding detection coverage to additional ATT&CK techniques, including:

- Kerberoasting
- Pass-the-Hash
- Pass-the-Ticket
- Golden Ticket
- DCSync
- Remote WMI Execution
- Remote PowerShell
- SMB Relay
- DNS Enumeration
- Command and Control
- Data Exfiltration

---

# References

- MITRE ATT&CK Enterprise Matrix
- Splunk Enterprise Security Best Practices
- Microsoft Windows Security Auditing Documentation
- Sysmon Event Documentation