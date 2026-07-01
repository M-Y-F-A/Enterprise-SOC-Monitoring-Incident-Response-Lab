# Splunk Configuration Overview

## Overview

This directory contains the Splunk configuration and detection engineering assets used in the Enterprise SOC Monitoring & Incident Response Home Lab.

The Splunk instance is deployed as a single-node **Splunk Enterprise 10.4.0** installation on Ubuntu Server and serves as the central SIEM platform for log collection, indexing, search, detection engineering, and incident investigation.

---

## Splunk Role in the Lab

Splunk serves as the central security monitoring platform and is responsible for:

* Collecting logs from Windows endpoints, Active Directory, and VPN infrastructure
* Parsing and indexing security telemetry
* Supporting threat hunting and incident investigation
* Running correlation searches and detection rules
* Providing centralized visibility through dashboards and reports

---

## Log Sources

### Windows Endpoint

The Windows 10 workstation forwards the following telemetry through Splunk Universal Forwarder:

* Windows Security Logs
* Windows System Logs
* Windows Application Logs
* PowerShell Operational Logs
* Sysmon Events

### Active Directory

The Domain Controller forwards:

* Security Event Logs
* Directory Service Logs
* DNS Server Logs

These logs provide visibility into:

* User authentication activity
* Kerberos and NTLM authentication
* User and group management events
* Directory changes
* Domain security events

### VPN Infrastructure

The OpenVPN server forwards:

* VPN authentication logs
* Connection and disconnection events
* Remote access activity

---

## Data Flow Architecture

```text
Windows 10 Endpoint (UF) ───────┐
                                │
Domain Controller (UF) ─────────┼──► Splunk Enterprise
                                │       192.168.10.10
OpenVPN Server ─────────────────┘
                                         │
                                         ▼
                             Search • Dashboards
                             Detections • Investigations
```

All data sources send logs directly to the Splunk receiving port:

```text
192.168.10.10:9997
```

The Splunk Web Interface is available on:

```text
http://192.168.10.10:8000
```

---

## Index Strategy

The Splunk environment uses a source-based index model to separate telemetry by function and improve visibility during investigations.

| Index   | Data Source                                                | Purpose                                                                                                                            |
| ------- | ---------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| windows | Windows Security, System, Application, and PowerShell Logs | Endpoint monitoring, authentication tracking, and user activity visibility                                                         |
| sysmon  | Sysmon Operational Logs                                    | High-fidelity endpoint telemetry including process execution, network connections, registry modifications, and threat hunting data |
| ad      | Active Directory Domain Controller Logs                    | Domain authentication, directory services, DNS activity, and identity monitoring                                                   |
| vpn     | OpenVPN Logs                                               | Remote access monitoring, VPN authentication events, and session tracking                                                          |

---

## Configuration Architecture

```text
                       Splunk Server
                      (192.168.10.10)
                   ┌────────────────────┐
                   │    indexes.conf    │
                   │     props.conf     │
                   └─────────┬──────────┘
                             │
          ┌──────────────────┼──────────────────┐
          │                  │                  │
          ▼                  ▼                  ▼

      Windows 10          DC01            OpenVPN Server

     inputs.conf      inputs.conf         inputs.conf
     outputs.conf     outputs.conf        outputs.conf
```

---

## Configuration Files

### indexes.conf

Defines all custom indexes used in the environment:

* windows
* sysmon
* ad
* vpn

Each index is configured with dedicated storage paths and a 30-day retention period.

---

### inputs.conf

Defines the data sources collected from each system.

#### Windows Endpoint

* Security Logs
* System Logs
* Application Logs
* PowerShell Logs
* Sysmon Operational Logs

#### Domain Controller

* Security Logs
* Directory Service Logs
* DNS Server Logs

#### OpenVPN Server

* OpenVPN log monitoring

---

### outputs.conf

Defines forwarding destinations for Splunk Universal Forwarders.

All forwarders send telemetry to:

```text
192.168.10.10:9997
```

---

### props.conf

Handles event parsing and normalization.

Current configuration includes parsing support for:

* Windows Event Logs
* Sysmon Operational Logs
* OpenVPN Logs

---

## Detection Engineering

Detection content is organized using a catalog-based structure.

The `detection-catalog.md` document provides a high-level overview of all implemented detection rules, while detailed documentation for each rule is maintained individually under the `rules/` directory.

Each detection rule includes:

- Detection objective
- Threat description
- SPL search
- Required data sources
- Windows Event IDs
- MITRE ATT&CK mapping
- Detection threshold
- Investigation guidance

Detection content is validated through attack simulations and mapped to the MITRE ATT&CK framework.

---

## Dashboards

Dashboard documentation follows the same catalog-based structure as the detection content.

The `dashboard-catalog.md` document provides an overview of all dashboards, while detailed documentation for each dashboard is maintained under the `dashboards/` directory.

Implemented dashboards include:

- Authentication Dashboard
- Endpoint Activity Dashboard
- Detection & Alerts Dashboard
- Threat Hunting Dashboard
- MITRE ATT&CK Coverage Dashboard

---

## Deployment Notes

* Splunk Enterprise 10.4.0
* Single-node deployment
* Ubuntu Server LTS
* Web Interface Port: 8000
* Management Port: 8089
* Receiving Port: 9997
* Universal Forwarder deployed on Windows systems
* Centralized log ingestion architecture

---

## Purpose of This Lab

This Splunk deployment is designed to simulate a real-world Security Operations Center (SOC) environment and provide hands-on experience with:

* SIEM Administration
* Security Monitoring
* Log Analysis
* Detection Engineering
* Incident Investigation
* Threat Hunting
* Active Directory Monitoring
* Endpoint Visibility