# Attack Simulation Playbooks

## Overview

This document contains the attack simulation playbooks used throughout the Enterprise SOC Monitoring & Incident Response Lab.

Each playbook documents the tools, commands, execution procedures, and expected telemetry required to simulate real-world attacker techniques in a controlled lab environment.

These playbooks are used to validate Splunk detection rules, dashboards, threat hunting workflows, and incident response procedures.

All activities are performed exclusively within the isolated lab environment.

---

# Playbook Workflow

Each playbook follows the workflow below:

1. Verify prerequisites.
2. Execute the attack technique.
3. Generate security telemetry.
4. Validate Splunk detections.
5. Verify dashboard visibility.
6. Perform investigation.
7. Restore the environment.

---

# Playbook Standard

Each playbook includes:

- Objective
- Target Systems
- Required Tools
- Prerequisites
- Execution Steps
- Expected Telemetry
- Related Detection Use Cases
- Related Detection Rules
- Expected Splunk Alerts
- Cleanup

---

# Attack Simulation Playbooks

---

## AS-001 — Password Brute Force

### Objective

Simulate repeated password guessing against Windows or Active Directory accounts.

### Target Systems

- Domain Controller
- Windows Endpoint

### Required Tools

- Hydra

### Prerequisites

- Test domain account
- Network connectivity
- Splunk log ingestion verified

### Execution Steps

1. Configure target IP.
2. Select target username(s).
3. Execute Hydra brute-force attack.
4. Continue until failed logon events are generated.
5. (Optional) Trigger account lockout.

### Expected Telemetry

- Windows Event ID 4625
- Windows Event ID 4624
- Windows Event ID 4740

### Related Detection

- UC-001
- DR-001

### Expected Splunk Alerts

- Brute Force Authentication

### Cleanup

- Unlock test accounts if required.

---

## AS-002 — Authentication Anomaly

### Objective

Generate abnormal authentication behavior.

### Target Systems

- Active Directory
- Windows Endpoint

### Required Tools

- Windows
- PowerShell
- RunAs

### Prerequisites

- Multiple test accounts
- Domain connectivity

### Execution Steps

1. Authenticate from multiple hosts.
2. Use different logon types.
3. Authenticate outside the normal baseline.
4. Execute RunAs with explicit credentials.

### Expected Telemetry

- Event IDs 4624
- 4625
- 4648
- 4768
- 4769

### Related Detection

- UC-002
- DR-002

### Expected Splunk Alerts

- Authentication Anomaly

### Cleanup

- Log off test sessions.

---

## AS-003 — Malicious PowerShell

### Objective

Simulate attacker PowerShell activity.

### Target Systems

- Windows Endpoint

### Required Tools

- PowerShell

### Prerequisites

- PowerShell Operational Logging
- Sysmon

### Execution Steps

1. Execute encoded commands.
2. Execute IEX.
3. Execute Download Cradle.
4. Execute ExecutionPolicy Bypass.

### Expected Telemetry

- Sysmon Event ID 1
- PowerShell Event IDs 4103
- PowerShell Event IDs 4104

### Related Detection

- UC-003
- DR-003

### Expected Splunk Alerts

- Malicious PowerShell

### Cleanup

- Remove downloaded files.

---

## AS-004 — Account Manipulation

### Objective

Simulate unauthorized account management.

### Target Systems

- Windows Endpoint
- Domain Controller

### Required Tools

- PowerShell
- net.exe

### Prerequisites

- Administrative privileges

### Execution Steps

1. Create test account.
2. Add account to Administrators.
3. Modify group membership.
4. Remove privileges.

### Expected Telemetry

- Event IDs 4720
- 4728
- 4732
- 4756

### Related Detection

- UC-004
- DR-004

### Expected Splunk Alerts

- Account Manipulation

### Cleanup

- Remove test account.

---

## AS-005 — Windows Persistence

### Objective

Simulate common Windows persistence techniques.

### Target Systems

- Windows Endpoint

### Required Tools

- schtasks.exe
- sc.exe
- PowerShell

### Prerequisites

- Administrative privileges

### Execution Steps

1. Create scheduled task.
2. Install Windows service.
3. Modify existing service.

### Expected Telemetry

- Event IDs 4698
- 7045
- Sysmon Event ID 1

### Related Detection

- UC-005
- DR-005

### Expected Splunk Alerts

- Windows Persistence

### Cleanup

- Delete scheduled tasks.
- Remove created services.

---

## AS-006 — Credential Access

### Objective

Simulate credential dumping activity.

### Target Systems

- Windows Endpoint

### Required Tools

- Mimikatz

### Prerequisites

- Administrative privileges
- Sysmon

### Execution Steps

1. Execute Mimikatz.
2. Access LSASS.
3. Dump credentials.

### Expected Telemetry

- Sysmon Event ID 10
- Sysmon Event ID 1

### Related Detection

- UC-006
- DR-006

### Expected Splunk Alerts

- Credential Access

### Cleanup

- Remove artifacts.

---

## AS-007 — Lateral Movement

### Objective

Simulate movement between enterprise hosts.

### Target Systems

- Windows Endpoint
- Domain Controller

### Required Tools

- PsExec
- Evil-WinRM
- RDP
- SMB

### Prerequisites

- Administrative credentials
- Multiple hosts

### Execution Steps

1. Authenticate remotely.
2. Execute remote commands.
3. Access administrative shares.
4. Open remote sessions.

### Expected Telemetry

- Event IDs 4624
- 4648
- 5140
- Sysmon Event ID 1

### Related Detection

- UC-007
- DR-007

### Expected Splunk Alerts

- Lateral Movement

### Cleanup

- Close remote sessions.

---

## AS-008 — Network Reconnaissance

### Objective

Simulate internal reconnaissance.

### Target Systems

- Internal Network

### Required Tools

- Nmap
- NetExec (CrackMapExec)

### Prerequisites

- Network connectivity

### Execution Steps

1. Perform host discovery.
2. Scan open ports.
3. Enumerate SMB.
4. Enumerate network services.

### Expected Telemetry

- Sysmon Event ID 3

### Related Detection

- UC-008
- DR-008

### Expected Splunk Alerts

- Network Reconnaissance

### Cleanup

- No cleanup required.

---

# Validation Criteria

Each playbook is considered successfully validated when:

- The attack technique executes successfully.
- Expected Windows and Sysmon telemetry is generated.
- Splunk ingests all relevant events.
- Related detection rules trigger successfully.
- Dashboard visualizations reflect the simulated activity.
- The environment is restored to its original state.

---

# Notes

These playbooks provide a standardized approach for executing controlled attack simulations throughout the lab. As additional attack techniques and detection rules are introduced, new playbooks will be added to expand detection coverage, improve SOC monitoring, and strengthen incident response capabilities.