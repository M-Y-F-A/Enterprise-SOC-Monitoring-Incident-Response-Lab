# VMware Lab Setup

## Overview

This document defines the virtual machine specifications used in the Enterprise SOC Monitoring & Incident Response Home Lab.

The environment is designed to simulate a small enterprise network with centralized logging, Active Directory services, endpoint telemetry, and remote attacker access through a VPN tunnel.

---

## VMware Virtual Machines

| VM                      | Operating System    | RAM  | CPU                  | Disk Type | Disk Size |
| ----------------------- | ------------------- | ---- | -------------------- | --------- | --------- |
| Splunk Server           | Ubuntu Server LTS   | 5 GB | 1 Processor, 2 Cores | SSD       | 60 GB     |
| Windows 10 Endpoint     | Windows 10          | 3 GB | 1 Processor, 2 Cores | SSD       | 50 GB     |
| Active Directory Server | Windows Server 2022 | 3 GB | 1 Processor, 2 Cores | HDD       | 50 GB     |
| OpenVPN Server          | Ubuntu Server LTS   | 1 GB | 1 Processor, 1 Core  | SSD       | 15 GB     |

---

## External Infrastructure

| Host       | Platform | Purpose                      |
| ---------- | -------- | ---------------------------- |
| Kali Linux | AWS EC2  | External attacker simulation |

---

## Resource Allocation Summary

| Category      | Value  |
| ------------- | ------ |
| Total RAM     | 12 GB  |
| Total CPU     | 7 vCPU |
| Total Storage | 175 GB |

---

## Network Interfaces (NICs Design)


| Component  | Network                    |
| ---------- | -------------------------- |
| Splunk     | NAT + Host-Only (dual NIC) |
| Windows 10 | Host-Only                  |
| AD Server  | Host-Only                  |
| OpenVPN    | NAT + Host-Only (dual NIC) |
| Kali (AWS) | External (VPN only)        |

---

## Virtual Machine Roles

### Splunk Server

**Operating System:** Ubuntu Server LTS

**Purpose:**

* Centralized log collection and correlation
* SIEM-based detection engineering
* Security dashboards and alerting
* Incident investigation and response support

---

### Windows 10 Endpoint

**Operating System:** Windows 10

**Purpose:**

* User workstation simulation
* Initial access target
* Endpoint telemetry generation
* Authentication activity source

---

### Active Directory Server

**Operating System:** Windows Server 2022

**Purpose:**

* Domain Controller (AD DS)
* Authentication and authorization services
* User and group management
* Domain policy enforcement

---

### OpenVPN Server

**Operating System:** Ubuntu Server LTS

**Purpose:**

* Secure encrypted remote access
* VPN tunnel into internal lab network
* Controlled external entry point for attack simulation

---

### Kali Linux (AWS)

**Platform:** AWS EC2

**Purpose:**

* External attacker simulation
* Offensive security testing
* Adversary emulation through VPN access
* Attack chain initiation into internal environment

---

## Design Considerations

* Lightweight VM sizing for home lab constraints
* Centralized SIEM architecture using Splunk
* Endpoint telemetry via Splunk Universal Forwarder
* Segmented internal network using VMware Host-Only networking
* Dual-NIC Splunk design for internal + management connectivity
* External attack simulation via AWS Kali Linux instance
* Full attack lifecycle visibility for SOC analysis
