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
├── Domain Controller (DC1)
│
├── Organizational Units
│   ├── Users
│   ├── Groups
│   ├── Computers
│   └── Security
│
└── Group Policy Objects
    ├── Audit Policies
    ├── Workstation Baseline
    ├── Server Hardening
    └── Restricted Groups
```

---

# Log Collection Architecture

Security telemetry is forwarded to Splunk Enterprise using Splunk Universal Forwarder.

```text
Windows Endpoint
        │
        ▼
Universal Forwarder
        │
        ▼
Splunk Enterprise
        │
        ▼
Indexes
        │
        ▼
Detection Rules
        │
        ▼
Dashboards
        │
        ▼
Incident Investigation
```

---

# Data Flow

```text
Windows Security Logs
PowerShell Logs
Sysmon Logs
Active Directory Logs
VPN Logs
        │
        ▼
Splunk Universal Forwarders
        │
        ▼
Splunk Enterprise
        │
        ▼
Indexes
        │
        ▼
Searches
        │
        ▼
Detection Rules
        │
        ▼
Alerts
        │
        ▼
SOC Dashboards
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

# Trust Boundaries

The environment is logically divided into multiple security zones.

| Security Zone | Components |
|--------------|------------|
| External Network | Kali Linux (AWS) |
| Remote Access Zone | OpenVPN Server |
| Internal Network | Windows Endpoint, Active Directory |
| Monitoring Zone | Splunk Enterprise |

---

# Detection Architecture

Security events progress through the following workflow:

```text
Telemetry Collection
        │
        ▼
Log Parsing
        │
        ▼
Indexing
        │
        ▼
Detection Rules
        │
        ▼
Alert Generation
        │
        ▼
SOC Dashboards
        │
        ▼
Threat Hunting
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