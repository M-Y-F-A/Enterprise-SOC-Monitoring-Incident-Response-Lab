# Attack Scenarios

## Overview

This document defines the attack scenarios executed throughout the Enterprise SOC Monitoring & Incident Response Lab.

Each scenario represents a realistic enterprise attack sequence designed to generate security telemetry, validate Splunk detection content, and support incident investigation workflows.

The execution details, tools, and commands for each attack are documented separately in `attack-simulation/playbooks.md`.

All activities are performed exclusively within the isolated lab environment.

---

# Objectives

The attack scenarios are designed to:

- Simulate realistic attacker behavior.
- Generate Windows, Sysmon, Active Directory, and network telemetry.
- Validate Splunk detection rules.
- Verify dashboard visibility.
- Support threat hunting activities.
- Produce evidence for incident investigations.
- Measure detection coverage using the MITRE ATT&CK framework.

---

# Enterprise Attack Lifecycle

```text
External Attacker
        │
        ▼
    VPN Access
        │
        ▼
  Authentication
        │
        ▼
    Execution
        │
        ▼
   Persistence
        │
        ▼
Privilege Manipulation
        │
        ▼
 Credential Access
        │
        ▼
 Lateral Movement
        │
        ▼
    Discovery
        │
        ▼
  SOC Detection
        │
        ▼
Incident Investigation
```

---

# Attack Scenario Mapping

| Scenario | Description | Playbook | Detection Rule | Dashboard |
|----------|-------------|----------|----------------|-----------|
| Initial Access | Password Brute Force against domain accounts | AS-001 | DR-001 | Authentication |
| Authentication | Abnormal authentication behavior | AS-002 | DR-002 | Authentication |
| Execution | Malicious PowerShell execution | AS-003 | DR-003 | Endpoint Activity |
| Privilege Manipulation | Local account creation and privilege assignment | AS-004 | DR-004 | Endpoint Activity |
| Persistence | Scheduled task and service creation | AS-005 | DR-005 | Endpoint Activity |
| Credential Access | LSASS credential dumping | AS-006 | DR-006 | Detection Alerts |
| Lateral Movement | Remote administration between hosts | AS-007 | DR-007 | Threat Hunting |
| Discovery | Internal network reconnaissance | AS-008 | DR-008 | MITRE Coverage |

---

# End-to-End Attack Flow

## Phase 1 — Initial Access

An external attacker attempts repeated authentication against Active Directory accounts until valid credentials are obtained.

**Playbook**

- AS-001

**Detection**

- DR-001

---

## Phase 2 — Authentication

The attacker authenticates successfully and performs additional authentication attempts using different hosts or logon methods.

**Playbook**

- AS-002

**Detection**

- DR-002

---

## Phase 3 — Execution

PowerShell is executed to establish an interactive foothold and launch post-exploitation activities.

**Playbook**

- AS-003

**Detection**

- DR-003

---

## Phase 4 — Privilege Manipulation

Administrative accounts are created or modified to increase privileges.

**Playbook**

- AS-004

**Detection**

- DR-004

---

## Phase 5 — Persistence

Persistence mechanisms are established to maintain long-term access.

**Playbook**

- AS-005

**Detection**

- DR-005

---

## Phase 6 — Credential Access

The attacker attempts to obtain credentials from LSASS memory.

**Playbook**

- AS-006

**Detection**

- DR-006

---

## Phase 7 — Lateral Movement

Compromised credentials are used to access additional systems.

**Playbook**

- AS-007

**Detection**

- DR-007

---

## Phase 8 — Discovery

Internal reconnaissance is performed to identify hosts and services.

**Playbook**

- AS-008

**Detection**

- DR-008

---

# Expected Evidence

Each completed scenario should produce evidence including:

- Windows Event Logs
- Sysmon Events
- PowerShell Operational Logs
- Active Directory Events
- Network Activity
- Splunk Search Results
- Detection Alerts
- Dashboard Visualizations
- Investigation Timeline
- MITRE ATT&CK Mapping

---

# Validation Criteria

A scenario is considered successfully validated when:

- All expected telemetry is ingested into Splunk.
- Related detection rules trigger successfully.
- Dashboards visualize the attack activity.
- Investigation evidence is collected.
- The attack can be reconstructed using available telemetry.

---

# Notes

This document provides the high-level attack narratives executed within the lab. Detailed execution procedures, commands, and tools are maintained separately in `attack-simulation/playbooks.md`, while detection logic and monitoring content are documented within the Splunk detection and dashboard catalogs.