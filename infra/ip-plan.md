# IP Addressing Plan

## Overview

This document defines the IP addressing scheme used throughout the Enterprise SOC Monitoring & Incident Response Home Lab.

The environment consists of an internal VMware network, an OpenVPN network for remote access, and an external AWS-hosted Kali Linux attacker machine.

---

## Internal VMware Network

**Network:** 192.168.10.0/24

**Purpose:** Internal enterprise network hosting Active Directory, endpoints, and SIEM infrastructure.

| Host                          | Role                       | IP Address    |
| ----------------------------- | -------------------------- | ------------- |
| Splunk Server                 | SIEM Platform              | 192.168.10.10 |
| Windows 10 Endpoint           | User Workstation           | 192.168.10.20 |
| Active Directory Server       | Domain Controller          | 192.168.10.30 |
| OpenVPN Server (Internal NIC) | Internal Routing Interface | 192.168.10.40 |

---

## Management Interfaces

| Host | Interface | Network Type | Addressing |
|--------|--------|--------|--------|
| Splunk Server | NIC 2 | NAT | DHCP |
| OpenVPN Server | NIC 1 | NAT | DHCP |

---

## OpenVPN Network

**Network:** 10.8.0.0/24

**Purpose:** Secure remote access network connecting the external attacker environment to the internal lab.

| Host             | Role        | IP Address |
| ---------------- | ----------- | ---------- |
| OpenVPN Server   | VPN Gateway | 10.8.0.1   |
| Kali Linux (AWS) | VPN Client  | 10.8.0.2   |

---

## Domain Information

| Setting           | Value         |
| ----------------- | ------------- |
| Domain Name       | lab.local     |
| Domain Controller | 192.168.10.30 |
| DNS Server        | 192.168.10.30 |

---

## Network Segmentation

### Internal Enterprise Network

```text
192.168.10.0/24
```

Contains:

* Splunk Server
* Windows 10 Endpoint
* Active Directory Server
* OpenVPN Internal Interface

---

### VPN Network

```text
10.8.0.0/24
```

Contains:

* OpenVPN Gateway
* Remote VPN Clients
* Kali Linux Attacker System

---

## Connectivity Flow

```text
Kali Linux (AWS)
        |
        | VPN Tunnel
        v
OpenVPN Server (10.8.0.1)
        |
        | Route
        v
Internal Network (192.168.10.0/24)
        |
        +--> Windows 10 Endpoint
        |
        +--> Active Directory Server
        |
        +--> Splunk Server
```

---

## Reserved Addresses

| IP Address         | Purpose                           |
| ------------------ | --------------------------------- |
| 192.168.10.1       | Reserved for future gateway usage |
| 192.168.10.50-99   | Future servers and services       |
| 192.168.10.100-199 | Additional endpoints              |
| 192.168.10.200-254 | Lab expansion and testing         |

---

## Design Considerations

* Static IP addressing is used for all infrastructure systems.
* Active Directory provides DNS services for the internal environment.
* OpenVPN routes traffic between the VPN network and the internal VMware network.
* Splunk is reachable from the internal network for centralized log collection.
* Network ranges are intentionally separated to simplify routing and investigation activities.
