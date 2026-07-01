# Architecture Overview

## Overview

This document describes the architecture of the Enterprise SOC Monitoring & Incident Response Lab.

The environment is designed to simulate a small enterprise network with centralized security monitoring, Active Directory infrastructure, secure remote access, and an end-to-end detection engineering workflow using Splunk Enterprise.

---

# Architecture Objectives

The architecture is designed to:

- Simulate a realistic enterprise environment
- Centralize security log collection
- Support detection engineering and threat hunting
- Validate attack simulations
- Demonstrate SOC monitoring and incident response workflows
- Provide complete visibility across endpoints, identity, and remote access

---

# Network Architecture

The lab consists of four primary systems:

| Host | Role |
|------|------|
| SPLUNK-SERVER | Central SIEM Platform |
| DC1 | Active Directory Domain Controller |
| WIN10-CLIENT1 | Domain-Joined Endpoint |
| VPN-SERVER | Secure Remote Access |

External attacker simulation is performed from a Kali Linux host running on AWS EC2.

---

# Network Diagram

![Enterprise SOC Lab Architecture](..\screenshots\phase-1-infrastructure\01-vm-creation\network-diagram.png)

---

# Active Directory Architecture

```text
lab.local
│
├── Active Directory Domain Services
├── Organizational Units
├── Security Groups
├── User Accounts
└── Group Policy Objects
```

For the complete Active Directory structure, including Organizational Units, users, groups, service accounts, and GPOs, see:

`docs/lab-overview.md`


---

# Log Collection / Data Flow

```text
Windows Endpoint
Domain Controller
OpenVPN Server
        │
        ▼
Splunk Universal Forwarder
        │
        ▼
Splunk Enterprise
        │
        ▼
Indexes
        │
        ▼
Splunk Add-on for Microsoft Windows
        │
        ▼
Field Extraction & Normalization
        │
        ▼
Detection Rules
        │
        ▼
Alerts
        │
        ▼
Dashboards
        │
        ▼
Threat Hunting
        │
        ▼
Incident Investigation
```

---

# Attack Flow

The simulated attack lifecycle follows a realistic enterprise intrusion path.

```text
External Attacker
        │
        ▼
VPN Authentication
        │
        ▼
Windows Endpoint
        │
        ▼
Active Directory
        │
        ▼
PowerShell Execution
        │
        ▼
Account Manipulation
        │
        ▼
Persistence
        │
        ▼
Credential Access
        │
        ▼
Lateral Movement
        │
        ▼
Detection
        │
        ▼
Incident Investigation
```

---

# Security Visibility

The architecture provides visibility into:

- Windows authentication activity
- Active Directory events
- Process creation
- PowerShell execution
- Network connections
- User and group management
- Persistence mechanisms
- Credential access attempts
- Remote administration
- Network reconnaissance

---

# Supporting Documentation

Related documentation:

- `docs/lab-overview.md`
- `docs/logging-architecture.md`
- `docs/detection-use-cases.md`
- `docs/attack-scenario.md`
- `attack-simulation/playbooks.md`
- `splunk/README.md`
- `splunk/detection-catalog.md`
- `splunk/dashboard-catalog.md`
- `MITRE-ATTACK-MAPPING.md`