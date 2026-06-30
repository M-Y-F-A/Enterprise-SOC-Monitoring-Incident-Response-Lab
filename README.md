# Enterprise SOC Monitoring & Incident Response Lab

A professional blue-team home lab designed to simulate enterprise security monitoring, detection engineering, threat hunting, and incident response across a realistic end-to-end attack lifecycle using Splunk Enterprise, Active Directory, Sysmon, and OpenVPN.

![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux-blue)
![SIEM](https://img.shields.io/badge/SIEM-Splunk%20Enterprise-green)
![Status](https://img.shields.io/badge/Status-In%20Progress-orange)
![MITRE](https://img.shields.io/badge/MITRE-ATT%26CK-red)
![License](https://img.shields.io/badge/License-Educational-lightgrey)

---

## Table of Contents

- [Enterprise SOC Monitoring \& Incident Response Lab](#enterprise-soc-monitoring--incident-response-lab)
  - [Table of Contents](#table-of-contents)
  - [Repository Guide](#repository-guide)
  - [SOC Lab Objectives](#soc-lab-objectives)
  - [Attack Chain](#attack-chain)
  - [Network Architecture](#network-architecture)
  - [Architecture Overview](#architecture-overview)
  - [Technology Stack](#technology-stack)
  - [Detection Engineering](#detection-engineering)
  - [MITRE ATT\&CK Coverage](#mitre-attck-coverage)
  - [Repository Structure](#repository-structure)
  - [Skills Demonstrated](#skills-demonstrated)
  - [Evidence](#evidence)
  - [Future Improvements](#future-improvements)
  - [License](#license)

---

## Repository Guide

If you're reviewing this repository for the first time, the recommended reading order is:

1. `docs/lab-overview.md`
2. `architecture/README.md`
3. `docs/logging-architecture.md`
4. `splunk/README.md`
5. `docs/detection-use-cases.md`
6. `splunk/detection-catalog.md`
7. `splunk/rules/`
8. `attack-simulation/playbooks.md`
9. `docs/attack-scenario.md`
10. `splunk/dashboard-catalog.md`
11. `splunk/dashboards/`
12. `logs-evidence/`
13. `screenshots/`
14. `MITRE-ATTACK-MAPPING.md`

---

## SOC Lab Objectives

This project demonstrates the implementation of an enterprise-style Security Operations Center (SOC) environment focused on:

- Building centralized log collection and monitoring with Splunk Enterprise
- Simulating realistic attacker behavior inside an isolated lab environment
- Developing and validating detection rules for common attack techniques
- Creating SOC dashboards for monitoring and incident response
- Performing threat hunting using Windows and Sysmon telemetry
- Mapping detections to the MITRE ATT&CK framework
- Documenting end-to-end detection engineering workflows

---

## Attack Chain

```text
External Attacker (Kali Linux)
            │
            ▼
        OpenVPN Access
            │
            ▼
     Windows Workstation
            │
            ▼
      Active Directory
            │
            ▼
   Windows & Sysmon Logs
            │
            ▼
     Splunk Enterprise
            │
            ▼
     Detection Rules
            │
            ▼
      Splunk Alerts
            │
            ▼
      SOC Dashboards
            │
            ▼
 Incident Investigation
```

---

## Network Architecture

![Enterprise SOC Lab Architecture](screenshots\phase-1-infrastructure\01-vm-creation\network-diagram.png)

---

## Architecture Overview

The lab simulates a small enterprise environment with centralized security monitoring.

Core components include:

- Active Directory domain infrastructure
- Windows workstation endpoint
- Splunk Enterprise SIEM
- Sysmon endpoint telemetry
- OpenVPN remote access
- External attacker simulation from Kali Linux (AWS)

For detailed architecture diagrams and network design, see:

- `/architecture`
- `/docs/lab-overview.md`
- `/docs/logging-architecture.md`

---

## Technology Stack

| Technology | Purpose |
|------------|---------|
| Splunk Enterprise | SIEM, detection engineering, dashboards, investigations |
| Windows Server 2022 | Active Directory Domain Controller |
| Windows 10 | Domain-joined endpoint |
| Sysmon | Advanced endpoint telemetry |
| Splunk Universal Forwarder | Log forwarding |
| OpenVPN | Secure remote access simulation |
| VMware Workstation | Virtualization platform |
| AWS EC2 (Kali Linux) | External attacker simulation |
| Git & GitHub | Version control and project documentation |

---

## Detection Engineering

The Detection Engineering workflow includes:

- Detection Use Cases
- Splunk Detection Rules
- Attack Simulation Playbooks
- Attack Scenarios
- SOC Dashboards
- MITRE ATT&CK Mapping

Implemented detection categories include:

- Brute Force Authentication
- Authentication Anomalies
- Malicious PowerShell
- Account Manipulation
- Windows Persistence
- Credential Access
- Lateral Movement
- Network Reconnaissance

Each detection is documented with:

- Detection objective
- SPL search
- Required telemetry
- Windows Event IDs
- MITRE ATT&CK mapping
- Alert severity
- Investigation guidance
- False positive considerations

---

## MITRE ATT&CK Coverage

Current detection coverage includes:

| Technique | Description |
|-----------|-------------|
| T1110 | Brute Force |
| T1078 | Valid Accounts |
| T1059.001 | PowerShell |
| T1136 | Create Account |
| T1098 | Account Manipulation |
| T1053.005 | Scheduled Task |
| T1543.003 | Create or Modify System Process: Windows Service |
| T1003.001 | LSASS Memory |
| T1021 | Remote Services |
| T1046 | Network Service Discovery |

Additional ATT&CK coverage will be added as new detections are implemented.

---

## Repository Structure

```text
Enterprise-SOC-Monitoring-Incident-Response-Lab
│
├── architecture/         Architecture diagrams and design
├── attack-simulation/    Attack playbooks
├── docs/                 Project documentation
├── infra/                Infrastructure configuration
├── logs-evidence/        Alerts, telemetry, and investigation evidence
├── openvpn/              VPN configuration
├── screenshots/          Validation screenshots
├── splunk/               Detection engineering and SIEM configuration
└── windows/              Windows logging configuration
```

---

## Skills Demonstrated

This project demonstrates practical experience in:

- Splunk Enterprise Administration
- Detection Engineering
- SIEM Administration
- Windows Event Analysis
- Sysmon Monitoring
- Active Directory Security
- Threat Hunting
- Incident Investigation
- Log Analysis
- MITRE ATT&CK Mapping
- VPN Security Monitoring
- SOC Monitoring & Operations
- Blue Team Methodology

---

## Evidence

The repository includes supporting evidence for each implementation phase, including:

- Infrastructure deployment screenshots
- Splunk configuration validation
- Detection rule validation
- Dashboard screenshots
- Attack simulation evidence
- Windows and Sysmon logs
- Splunk alerts
- Incident investigation artifacts

---

## Future Improvements

Planned enhancements include:

- Expand MITRE ATT&CK coverage
- Add additional Windows attack techniques
- Integrate DNS, Firewall, and Syslog telemetry
- Build additional SOC dashboards
- Improve detection tuning and false positive reduction
- Develop complete incident response case studies
- Expand attack simulation playbooks
- Introduce detection coverage metrics

---

## License

This project is intended for educational purposes, detection engineering practice, and blue-team skill development within an isolated lab environment.

All attack simulations are performed in a controlled environment and are intended solely for defensive security research and learning.