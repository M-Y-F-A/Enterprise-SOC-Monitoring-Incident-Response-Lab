# Enterprise SOC Monitoring & Incident Response Home Lab

A professional SOC home lab repository designed to simulate enterprise-grade security monitoring and incident response operations across a realistic attack path.

## SOC Lab Objective

Build and operate a practical blue-team environment that demonstrates:
- End-to-end attack simulation from external access to internal domain activity
- Centralized telemetry collection and SIEM-based detections
- Investigation and response workflows aligned to enterprise SOC expectations

## Attack Flow

**Kali Linux (AWS) → OpenVPN → Windows 10 → Active Directory → Splunk SIEM**

1. **Kali Linux (AWS):** external adversary simulation host
2. **OpenVPN:** controlled secure tunnel into the lab environment
3. **Windows 10 Endpoint:** initial target and user workstation telemetry source
4. **Active Directory (Windows Server):** identity and domain control plane
5. **Splunk SIEM:** centralized logging, correlation, alerting, and triage

## Architecture Overview

The lab models segmented infrastructure with enterprise SOC visibility:
- Perimeter entry via VPN into a private lab network
- Domain-joined Windows endpoint(s) connected to AD services
- Endpoint and security telemetry forwarded to Splunk
- Detection content mapped to ATT&CK-aligned tactics and techniques

See:
- `/architecture`
- `/diagrams`
- `/docs/logging-architecture.md`

## Tools Used

- **Splunk SIEM** – ingestion, detection rules, dashboards, and investigations
- **Windows Server Active Directory** – domain, authentication, and policy backbone
- **Sysmon** – deep endpoint telemetry for process/network/file behaviors
- **OpenVPN** – secure remote entry and attack simulation path
- **VMware** – lab virtualization and segmented network simulation

## Detection Use Cases

The repository includes use-case documentation for:
- **Brute Force Activity** (e.g., repeated failed logons and lockout patterns)
- **Lateral Movement Indicators** (e.g., remote service execution, admin share use)
- **Authentication Anomalies** (e.g., unusual logon types, source hosts, timing)

Details are tracked in `/docs/detection-use-cases.md` and `/splunk/detection-rules.md`.

## MITRE ATT&CK Relevance

This lab maps observed behavior and detections to ATT&CK techniques, including examples such as:
- **T1110** – Brute Force
- **T1021** – Remote Services (lateral movement)
- **T1078** – Valid Accounts
- **T1550** – Use of Alternate Authentication Material (scenario-dependent)

The goal is to improve detection engineering and analyst triage using ATT&CK as a shared language for threat behavior.

## Future Improvements

- Add full ATT&CK coverage matrix with detection maturity scoring
- Introduce adversary emulation automation for repeatable test runs
- Expand data sources (DNS, firewall, proxy, EDR) for richer correlation
- Add incident response playbooks with severity-based workflows
- Add validation datasets and baseline metrics for false-positive tuning

## Repository Structure

- `/architecture` – architecture and network diagram placeholders
- `/docs` – lab overview, attack scenario, detections, and logging docs
- `/infra` – VMware setup notes, IP planning, and network config
- `/splunk` – Splunk configs, detection placeholders, and dashboards
- `/windows` – Sysmon/Winlogbeat placeholders and event logging notes
- `/openvpn` – server/client placeholder configs and setup guide
- `/attack-simulation` – attack scenario documentation and script placeholders
- `/screenshots` – dashboard and alert screenshot placeholders
- `/diagrams` – architecture diagram artifacts and references
