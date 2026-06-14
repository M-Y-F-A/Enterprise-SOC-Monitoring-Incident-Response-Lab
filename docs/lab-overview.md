# Lab Overview

## Introduction

This project is an enterprise-style SOC home lab designed to simulate realistic attack and defense scenarios in a controlled environment. The lab provides hands-on experience in security monitoring, log analysis, detection engineering, and incident investigation using industry-standard tools and frameworks.

The environment replicates a small corporate network with Active Directory infrastructure, Windows endpoints, centralized logging, VPN-based remote access, and attacker simulation capabilities.

---

# Lab Objectives

The primary objectives of this lab are:

* Build a centralized logging and monitoring environment using Splunk SIEM.
* Deploy and configure Active Directory for identity and access management.
* Collect endpoint and authentication telemetry from Windows systems.
* Simulate real-world attack scenarios and adversary behavior.
* Develop detection use cases aligned with MITRE ATT&CK framework.
* Practice incident investigation and SOC workflows.
* Understand enterprise-level security architecture and hardening practices.

---

# Environment Overview

## Domain Information

| Item              | Value                                    |
| ----------------- | ---------------------------------------- |
| Domain Name       | lab.local                                |
| Forest            | lab.local                                |
| Domain Controller | DC1                                      |
| Directory Service | Active Directory Domain Services (AD DS) |

---

## Virtual Machines

| Hostname         | Role                      | Operating System    |
| ---------------- | ------------------------- | ------------------- |
| DC1              | Domain Controller         | Windows Server 2022 |
| WIN10-CLIENT1    | Domain-Joined Workstation | Windows 10          |
| SPLUNK-SERVER    | SIEM Platform             | Ubuntu Server LTS   |
| VPN-SERVER       | Remote Access Server      | Ubuntu Server LTS   |
| KALI-LINUX (AWS) | External Attacker         | Kali Linux (Cloud)  |

---

# Network Architecture

## Internal Network

```text
192.168.10.0/24
```

### Hosts:

* SPLUNK-SERVER → 192.168.10.10
* WIN10-CLIENT1 → 192.168.10.20
* DC1 → 192.168.10.30
* VPN-SERVER → 192.168.10.40

---

## VPN Network

```text
10.8.0.0/24
```

### Hosts:

* VPN-SERVER → 10.8.0.1
* KALI-LINUX → 10.8.0.2

---

# Active Directory Infrastructure

## Domain Configuration

* Domain Name: `lab.local`
* Primary Domain Controller: `DC1`

---

## Full Active Directory Structure

```text
lab.local
└── Corp (OU)
    ├── Computers (OU)
    │   │
    │   ├── Domain Controllers (OU)
    │   │   └── DC1                     → Computer
    │   │
    │   ├── Servers (OU)
    │   │   ├── SPLUNK-SERVER           → Computer
    │   │   └── VPN-SERVER              → Computer
    │   │
    │   └── Workstations (OU)
    │       ├── WIN10-CLIENT1           → Computer
    │       └── WIN10-CLIENT2           → Computer
    │
    ├── Groups (OU)
    │   │
    │   ├── IT Admins                   → Security Group
    │   │   └── it.admin
    │   │
    │   ├── HR Staff                    → Security Group
    │   │   └── hr.user1
    │   │
    │   ├── SOC Analysts                → Security Group
    │   │   ├── soc.analyst1
    │   │   └── soc.analyst2
    │   │
    │   └── VPN Users                   → Security Group
    │       ├── hr.user1
    │       ├── it.admin
    │       └── soc.analyst1
    │
    ├── Security (OU)
    │   │
    │   ├── Audit Policies              → OU (logging & auditing GPOs)
    │   ├── GPO Targets                 → OU (GPO linking scope)
    │   └── Restricted Groups           → OU (local admin control policies)
    │
    └── Users (OU)
        │
        ├── HR Users (OU)
        │   └── hr.user1                → User        
        |
        ├── IT Users (OU)
        │   ├── it.admin                → User
        │   └── it.user1                → User
        │
        ├── Sales (OU)
        │   └── sales.user1             → User
        │
        ├── Service Accounts (OU)
        |    ├── splunk.service         → User (service account)
        |    ├── vpn.service            → User (service account)
        |    └── sysmon.service         → User (service account)   
        |     
        └── SOC Users (OU)
             ├── soc.analyst1           → User
             └── soc.analyst2           → User
```

---

## User Accounts

### IT Users

* it.admin
* it.user1

### HR Users

* hr.user1

### Sales Users

* sales.user1

### SOC Users

* soc.analyst1
* soc.analyst2

### Service Accounts

* splunk.service
* vpn.service
* sysmon.service

---

## Security Groups

### IT Admins

* it.admin

### HR Staff

* hr.user1

### SOC Analysts

* soc.analyst1
* soc.analyst2

### VPN Users

* it.admin
* hr.user1
* soc.analyst1

---

## Group Policy Objects (GPOs)

The following GPOs were implemented for security hardening and monitoring:

* SEC-Audit-Policies
* SEC-Workstation-Baseline
* SEC-Server-Hardening
* SEC-Restricted-LocalAdmins

### Configured Controls:

* Logon and authentication auditing
* Process creation monitoring
* Credential validation tracking
* Windows Firewall enforcement
* Local administrator restriction policies

---

# Log Collection Architecture

Splunk Universal Forwarder is used to collect logs from Windows endpoints and forward them to the Splunk SIEM server.

## Data Sources

* Windows Security Logs
* Windows System Logs
* Windows Application Logs
* Sysmon Logs (planned or deployed)

## Log Flow

```text
WIN10-CLIENT1 → Splunk Universal Forwarder → SPLUNK-SERVER
DC1           → Splunk Universal Forwarder → SPLUNK-SERVER
```

---

# VPN & Attack Simulation

The lab includes a VPN-based remote access layer to simulate real-world external access scenarios.

## Scenario Overview

An attacker gains access via VPN using compromised credentials and performs post-compromise activities such as:

* Network enumeration
* Authentication attempts
* Privilege escalation
* Lateral movement

All activities generate telemetry that is collected and analyzed in Splunk for detection engineering and incident response exercises.

---

# Security Monitoring Goals

The lab focuses on detecting:

* Authentication anomalies (success/failure patterns)
* Brute force attempts
* Suspicious process execution
* Remote login behavior
* Privilege escalation attempts
* Lateral movement activity
* Endpoint telemetry anomalies

---

# Technologies Used

* Splunk SIEM
* Splunk Universal Forwarder
* Active Directory Domain Services
* Windows Server 2022
* Windows 10
* Sysmon
* OpenVPN
* VMware Workstation
* AWS EC2 (Kali Linux)