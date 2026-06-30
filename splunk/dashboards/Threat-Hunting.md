# Threat Hunting Dashboard

## Overview

The Threat Hunting Dashboard provides SOC analysts with visibility into suspicious endpoint and network activity that may not generate security alerts. It supports proactive threat hunting by highlighting anomalous behaviors, rare events, and attacker techniques observed across the environment.

This dashboard complements detection-based monitoring by enabling analysts to identify potential threats before they are detected by existing rules.

---

# Purpose

- Support proactive threat hunting.
- Identify abnormal endpoint behavior.
- Discover suspicious process execution.
- Monitor unusual network activity.
- Assist security investigations.

---

# Data Sources

- Sysmon
- Windows Security Log
- Windows System Log

---

# Dashboard Panels

## Top Executed Processes

**Purpose**

Display the most frequently executed processes across monitored endpoints.

**Event IDs**

- Sysmon Event ID 1

---

## Rare Processes

**Purpose**

Identify uncommon or infrequently executed processes that may require investigation.

**Event IDs**

- Sysmon Event ID 1

---

## PowerShell Activity

**Purpose**

Monitor PowerShell execution and highlight potentially suspicious command-line activity.

**Event IDs**

- Sysmon Event ID 1
- 4103
- 4104

---

## Command Prompt Activity

**Purpose**

Track Command Prompt execution to identify potentially malicious administrative activity.

**Event IDs**

- Sysmon Event ID 1

---

## Parent-Child Process Relationships

**Purpose**

Visualize process relationships to detect suspicious execution chains.

**Event IDs**

- Sysmon Event ID 1

---

## Network Connections

**Purpose**

Monitor outbound network connections initiated by endpoint processes.

**Event IDs**

- Sysmon Event ID 3

---

## New Windows Services

**Purpose**

Identify newly installed Windows services that may indicate persistence.

**Event IDs**

- 7045

---

## Scheduled Task Activity

**Purpose**

Monitor scheduled task creation and modification for persistence detection.

**Event IDs**

- 4698
- 4699
- 4700
- 4701

---

## Top Destination IP Addresses

**Purpose**

Identify external or internal IP addresses receiving the highest number of connections.

**Event IDs**

- Sysmon Event ID 3

---

# Related Detection Rules

- DR-003 — Malicious PowerShell
- DR-005 — Windows Persistence
- DR-006 — Credential Access
- DR-007 — Lateral Movement
- DR-008 — Network Reconnaissance

---

# Dashboard Validation

The dashboard is considered successfully implemented when:

- Endpoint telemetry is successfully indexed in Splunk.
- Dashboard panels accurately display hunting-related data.
- Suspicious behaviors can be identified without relying solely on alerts.
- Dashboard supports proactive threat hunting and investigation workflows.