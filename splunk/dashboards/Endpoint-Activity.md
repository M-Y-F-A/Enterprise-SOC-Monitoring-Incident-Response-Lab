# Endpoint Activity Dashboard

## Overview

The Endpoint Activity Dashboard provides visibility into endpoint behavior using Sysmon and Windows Event Logs. It enables SOC analysts to monitor process execution, PowerShell activity, persistence mechanisms, and other endpoint events that may indicate malicious activity.

This dashboard supports endpoint monitoring, detection validation, threat hunting, and incident investigations.

---

# Purpose

- Monitor endpoint activity across Windows systems.
- Visualize process creation and execution trends.
- Detect suspicious PowerShell usage.
- Identify persistence techniques.
- Support incident response and threat hunting.

---

# Data Sources

- Sysmon
- Windows Security Log
- Windows System Log

---

# Dashboard Panels

## Process Creation Activity

**Purpose**

Display process creation events across monitored endpoints.

**Event IDs**

- Sysmon Event ID 1

---

## PowerShell Execution

**Purpose**

Monitor PowerShell usage and identify suspicious command execution.

**Event IDs**

- Sysmon Event ID 1
- 4103
- 4104

---

## Parent-Child Process Relationships

**Purpose**

Visualize parent-child process relationships to identify abnormal process execution chains.

**Event IDs**

- Sysmon Event ID 1

---

## Network Connections

**Purpose**

Display outbound and inbound network connections initiated by endpoint processes.

**Event IDs**

- Sysmon Event ID 3

---

## Scheduled Task Activity

**Purpose**

Monitor the creation and modification of scheduled tasks used for persistence.

**Event IDs**

- 4698
- 4699
- 4700
- 4701

---

## Windows Service Activity

**Purpose**

Identify newly installed or modified Windows services.

**Event IDs**

- 7045

---

## User Account Activity

**Purpose**

Monitor account creation, enablement, and privilege assignment events.

**Event IDs**

- 4720
- 4722
- 4728
- 4732
- 4756

---

## Endpoint Activity Timeline

**Purpose**

Provide a chronological view of endpoint events to support investigations and identify abnormal activity.

---

# Related Detection Rules

- DR-003 — Malicious PowerShell
- DR-004 — Account Manipulation
- DR-005 — Windows Persistence
- DR-006 — Credential Access

---

# Dashboard Validation

The dashboard is considered successfully implemented when:

- Endpoint telemetry is successfully indexed in Splunk.
- All dashboard panels display accurate event data.
- Detection rules can be validated using dashboard visualizations.
- Dashboard supports endpoint investigations and threat hunting activities.