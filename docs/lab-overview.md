# Lab Overview

## Introduction

This project is an enterprise-style SOC home lab built to simulate realistic attack and defense scenarios in a controlled environment. The lab is designed to provide hands-on experience with security monitoring, log analysis, detection engineering, and incident investigation using industry-standard tools and technologies.

The environment replicates a small corporate network consisting of Windows endpoints, Active Directory services, centralized log collection, and remote access infrastructure.

---

## Lab Objectives

The primary goals of this lab are to:

* Build a centralized logging and monitoring environment using Splunk SIEM.
* Collect endpoint and authentication telemetry from Windows systems.
* Simulate realistic attack scenarios and adversary behavior.
* Develop and validate detection use cases aligned with MITRE ATT&CK.
* Practice incident investigation and security monitoring workflows.

---

## Environment Components

### Splunk Server

**Operating System:** Ubuntu Server LTS

**Role:**

* Centralized log collection
* Search and analysis
* Detection engineering
* Alerting and dashboards
* Incident investigation

---

### Windows 10 Endpoint

**Operating System:** Windows 10

**Role:**

* User workstation simulation
* Endpoint telemetry source
* Authentication activity source
* Initial attack target

---

### Active Directory Server

**Operating System:** Windows Server 2022

**Role:**

* Domain Controller
* DNS services
* User authentication
* Group policy management

**Domain Name:**

```text
lab.local
```

---

### OpenVPN Server

**Operating System:** Ubuntu Server LTS

**Role:**

* Secure remote access
* VPN tunnel termination
* Controlled access into the internal environment

---

### Kali Linux (AWS)

**Platform:** AWS EC2

**Role:**

* External attacker simulation
* Adversary emulation
* Attack execution and testing

---

## Network Architecture

### Internal Network

```text
192.168.10.0/24
```

Hosts:

* Splunk Server (192.168.10.10)
* Windows 10 Endpoint (192.168.10.20)
* Active Directory Server (192.168.10.30)
* OpenVPN Server (192.168.10.40)

---

### VPN Network

```text
10.8.0.0/24
```

Hosts:

* OpenVPN Server (10.8.0.1)
* Kali Linux (10.8.0.2)

---

## Log Collection Architecture

The lab uses Splunk Universal Forwarder to collect and forward logs from Windows systems to Splunk.

### Data Sources

* Windows Security Logs
* Windows System Logs
* Windows Application Logs
* Sysmon Logs

### Log Flow

```text
Windows 10
        |
        | Splunk Universal Forwarder
        v
Splunk Server

Active Directory Server
        |
        | Splunk Universal Forwarder
        v
Splunk Server
```

---

## Attack Simulation Scenario

The lab simulates a realistic remote-access compromise scenario.

An attacker gains unauthorized VPN access using compromised credentials obtained through phishing, malware infection, or other credential theft techniques. Once connected to the VPN, the attacker gains access to the internal network and performs post-compromise activities such as enumeration, authentication attempts, and lateral movement.

The resulting activity generates logs that are collected by Splunk and used for detection, investigation, and incident response exercises.

---

## Security Monitoring Goals

The lab focuses on detecting and investigating:

* Failed and successful authentication events
* Brute force activity
* Suspicious process execution
* Remote access activity
* Lateral movement behavior
* Privilege escalation attempts
* Endpoint telemetry anomalies

---

## Technologies Used

* Splunk SIEM
* Splunk Universal Forwarder
* Active Directory
* Windows Server 2022
* Windows 10
* Sysmon
* OpenVPN
* VMware Workstation
* AWS EC2 (Kali Linux)
