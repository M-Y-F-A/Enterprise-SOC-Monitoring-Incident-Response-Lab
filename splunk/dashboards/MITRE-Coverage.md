# MITRE ATT&CK Coverage Dashboard

## Overview

The MITRE ATT&CK Coverage Dashboard provides visibility into the organization's detection coverage by mapping implemented detection rules to the MITRE ATT&CK framework. It helps SOC analysts evaluate defensive capabilities, identify coverage gaps, and measure detection effectiveness across different attack tactics and techniques.

This dashboard supports Detection Engineering, threat hunting, and continuous security improvement.

---

# Purpose

- Visualize detection coverage across the MITRE ATT&CK framework.
- Monitor alerts by ATT&CK tactics and techniques.
- Identify detection gaps.
- Measure detection effectiveness.
- Support Detection Engineering and SOC reporting.

---

# Data Sources

- Splunk Alerts
- Detection Rules
- Windows Security Log
- Sysmon

---

# Dashboard Panels

## Alerts by ATT&CK Tactic

**Purpose**

Display alerts grouped by MITRE ATT&CK tactic.

---

## Alerts by ATT&CK Technique

**Purpose**

Visualize alerts generated for each ATT&CK technique.

---

## Detection Coverage

**Purpose**

Show implemented detection rules mapped to ATT&CK tactics and techniques.

---

## Most Triggered Techniques

**Purpose**

Identify the ATT&CK techniques generating the highest number of alerts.

---

## ATT&CK Tactic Distribution

**Purpose**

Visualize the distribution of detections across ATT&CK tactics.

---

## ATT&CK Timeline

**Purpose**

Display ATT&CK-related detections over time to identify attack trends.

---

## Detection Coverage Summary

**Purpose**

Provide an overview of implemented detection rules and their ATT&CK mappings.

---

# Related Detection Rules

- DR-001 — Brute Force Authentication
- DR-002 — Authentication Anomaly
- DR-003 — Malicious PowerShell
- DR-004 — Account Manipulation
- DR-005 — Windows Persistence
- DR-006 — Credential Access
- DR-007 — Lateral Movement
- DR-008 — Network Reconnaissance

---

# Dashboard Validation

The dashboard is considered successfully implemented when:

- Detection rules are correctly mapped to the MITRE ATT&CK framework.
- ATT&CK tactics and techniques are accurately visualized.
- Dashboard panels reflect current detection coverage.
- Dashboard supports gap analysis and detection reporting.