# Network Configuration

## Overview

This document defines the network design and connectivity configuration used in the Enterprise SOC Monitoring & Incident Response Home Lab.

The lab consists of an isolated internal VMware network, a NAT network for internet access, and an OpenVPN network used to simulate remote attacker access from AWS.

---

## Network Segments

| Network              | CIDR            | Purpose                             |
| -------------------- | --------------- | ----------------------------------- |
| Internal Lab Network | 192.168.10.0/24 | Communication between lab systems   |
| OpenVPN Network      | 10.8.0.0/24     | Remote VPN access                   |
| NAT Network          | VMware Managed  | Internet access and package updates |

---

## Host-Only Network Configuration

### Network

```text
192.168.10.0/24
```

### Purpose

The Host-Only network provides isolated communication between internal lab systems without exposing them directly to the internet.

### Connected Systems

| Host                          | IP Address    |
| ----------------------------- | ------------- |
| Splunk Server                 | 192.168.10.10 |
| Windows 10 Endpoint           | 192.168.10.20 |
| Active Directory Server       | 192.168.10.30 |
| OpenVPN Server (Internal NIC) | 192.168.10.40 |

### Services

* Active Directory Authentication
* DNS Resolution
* Splunk Log Collection
* Endpoint Telemetry
* Internal Host Communication

---

## NAT Network Configuration

### Purpose

The NAT network provides internet connectivity for selected systems while maintaining isolation from the internal lab network.

### Connected Systems

| Host           | Interface |
| -------------- | --------- |
| Splunk Server  | NIC 1     |
| OpenVPN Server | NIC 1     |

### Usage

* Ubuntu package updates
* Splunk package downloads
* OpenVPN installation and updates
* Administrative internet access

### Addressing

IP addresses are assigned dynamically through VMware NAT DHCP services.

---

## OpenVPN Network Configuration

### Network

```text
10.8.0.0/24
```

### Purpose

Provides secure encrypted connectivity between the AWS-hosted Kali Linux attacker machine and the internal lab environment.

### Connected Systems

| Host             | IP Address |
| ---------------- | ---------- |
| OpenVPN Server   | 10.8.0.1   |
| Kali Linux (AWS) | 10.8.0.2   |

---

## Routing Design

### Traffic Flow

```text
Kali Linux (AWS)
        |
        | OpenVPN Tunnel
        v
OpenVPN Server
        |
        | Route
        v
192.168.10.0/24
        |
        +--> Windows 10 Endpoint
        |
        +--> Active Directory Server
        |
        +--> Splunk Server
```

### Routing Objectives

* Allow VPN clients to access internal lab systems.
* Maintain isolation between the internet and internal network.
* Enable centralized log collection by Splunk.
* Support attack simulation and incident investigation workflows.

---

## VMware Adapter Assignment

| Host                    | NIC 1     | NIC 2     |
| ----------------------- | --------- | --------- |
| Splunk Server           | NAT       | Host-Only |
| Windows 10 Endpoint     | Host-Only | N/A       |
| Active Directory Server | Host-Only | N/A       |
| OpenVPN Server          | NAT       | Host-Only |

---

## Connectivity Validation

After deployment, validate connectivity using the following tests.

### Internal Network Connectivity

#### From Windows 10

```powershell
ping 192.168.10.10
ping 192.168.10.30
ping 192.168.10.40
```

#### From Splunk Server

```powershell
ping 192.168.10.20
ping 192.168.10.30
ping 192.168.10.40
```

#### From Active Directory Server

```powershell
ping 192.168.10.10
ping 192.168.10.20
ping 192.168.10.40
```
#### From OpenVPN Server

```powershell
ping 192.168.10.10
ping 192.168.10.20
ping 192.168.10.30
```

---

## Internet Connectivity Validation

### Splunk Server

```powershell
ping 8.8.8.8
ping google.com
```

### OpenVPN Server

```powershell
ping 8.8.8.8
ping google.com
```

Expected Result:

* Successful internet connectivity through VMware NAT.
* Successful DNS resolution.

---

## VPN Connectivity Validation

After OpenVPN deployment:

### From Kali Linux

```zsh
ping 10.8.0.1
ping 192.168.10.20
ping 192.168.10.30
```

Expected Result:

* VPN tunnel established successfully.
* Internal lab systems reachable through routed VPN access.

---

## Security Design Notes

* Internal enterprise systems remain isolated on the Host-Only network.
* Internet access is restricted to systems requiring updates and external connectivity.
* OpenVPN acts as the controlled entry point into the lab environment.
* Splunk receives telemetry from internal systems through the isolated network.
* Network segmentation supports realistic SOC monitoring and investigation scenarios.
