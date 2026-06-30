# Splunk Detection Rules Catalog 

## Overview

This document serves as the central catalog for all Splunk detection rules developed as part of the Enterprise SOC Monitoring & Incident Response Lab.

The detection rules are designed to identify malicious or suspicious activity across Windows endpoints, Active Directory, and enterprise network infrastructure using Windows Event Logs, Sysmon telemetry, and Splunk Enterprise.

Each detection rule is documented individually under the `rules/` directory following a standardized Detection Engineering methodology. This catalog provides a high-level overview of the current detection coverage and implementation status.

---

# Detection Engineering Workflow

Each detection rule is developed using the following workflow:

1. Define the attack scenario.
2. Identify the required telemetry.
3. Develop the SPL detection logic.
4. Validate the detection through attack simulation.
5. Tune the detection to minimize false positives.
6. Convert the search into a scheduled Splunk alert.
7. Document investigation procedures.
8. Maintain and improve the detection as new attack techniques emerge.

---

# Detection Rule Standard

Every detection rule within this project follows a consistent documentation standard.

Each rule contains:

- Rule Information
- Objective
- Threat Description
- SPL Search
- Required Data Sources
- Windows Event IDs
- MITRE ATT&CK Mapping
- Alert Severity
- Detection Threshold
- False Positive Considerations
- Investigation Guidance

---

# Detection Coverage

| Detection ID | Detection Rule | MITRE ATT&CK Tactic | Severity |
|--------------|----------------|---------------------|----------|
| DR-001 | Brute Force Authentication | Credential Access | High |
| DR-002 | Authentication Anomaly | Defense Evasion | Medium |
| DR-003 | Malicious PowerShell | Execution | High |
| DR-004 | Account Manipulation | Persistence / Privilege Escalation | High |
| DR-005 | Windows Persistence | Persistence | High |
| DR-006 | Credential Access | Credential Access | Critical |
| DR-007 | Lateral Movement | Lateral Movement | High |
| DR-008 | Network Reconnaissance | Discovery | Medium |

---

# Detection Documentation

Detailed documentation for each detection rule is available under the `rules/` directory.

| Detection ID | Documentation |
|--------------|---------------|
| DR-001 | `rules/DR-001-Brute-Force.md` |
| DR-002 | `rules/DR-002-Authentication-Anomaly.md` |
| DR-003 | `rules/DR-003-Malicious-PowerShell.md` |
| DR-004 | `rules/DR-004-Account-Manipulation.md` |
| DR-005 | `rules/DR-005-Windows-Persistence.md` |
| DR-006 | `rules/DR-006-Credential-Access.md` |
| DR-007 | `rules/DR-007-Lateral-Movement.md` |
| DR-008 | `rules/DR-008-Network-Reconnaissance.md` |
