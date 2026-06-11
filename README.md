# Enterprise SOC Monitoring & Incident Response Home Lab

A professional SOC home lab designed to simulate enterprise-grade security monitoring, detection engineering, and incident response across a realistic end-to-end attack chain.

---

## SOC Lab Objective

This lab demonstrates a practical blue-team environment focused on:

- End-to-end attack simulation from external access to internal domain compromise
- Centralized telemetry collection and SIEM-based detection engineering
- Incident investigation and response workflows aligned with SOC operations
- Mapping security events to MITRE ATT&CK techniques for structured analysis

---

## Attack Flow

**Kali Linux (AWS) → OpenVPN → Windows 10 → Active Directory → Splunk SIEM**

1. **Kali Linux (AWS):** External attacker simulation host
2. **OpenVPN:** Secure encrypted tunnel into internal lab network
3. **Windows 10 Endpoint:** Initial compromise target and telemetry source
4. **Active Directory (Windows Server):** Identity management and domain control plane
5. **Splunk SIEM:** Centralized logging, correlation, detection, and investigation

---

## Architecture Overview

The lab simulates a segmented enterprise environment with full SOC visibility:

- External access controlled via VPN into isolated internal network
- Windows endpoints joined to Active Directory domain
- Security and endpoint telemetry forwarded to Splunk SIEM
- Detection engineering aligned with ATT&CK framework

### Key References
- `/architecture`
- `/docs`
- `/splunk`

---

## Data Sources (Telemetry)

This lab collects and analyzes the following security data sources:

- Windows Security Event Logs (Authentication, Logon Events)
- Sysmon (Process creation, network connections, file activity)
- VPN logs (remote access and authentication activity)
- Active Directory authentication events
- Splunk ingested normalized event data

---

## Tools Used

- **Splunk SIEM** – detection, correlation, dashboards, and investigations
- **Windows Server Active Directory** – identity and authentication backbone
- **Sysmon** – detailed endpoint telemetry visibility
- **OpenVPN** – secure remote access simulation
- **VMware** – virtualization and network segmentation

---

## Detection Use Cases

The lab focuses on SOC-relevant detection scenarios:

- **Brute Force Activity** (multiple failed authentication attempts)
- **Lateral Movement** (remote service execution, admin share access)
- **Authentication Anomalies** (impossible travel, unusual logon types)
- **Suspicious Process Execution** (parent-child process anomalies)

Details are implemented in:
- `/docs/detection-use-cases.md`
- `/splunk/detection-rules.md`

---

## MITRE ATT&CK Mapping

This lab maps detections and behaviors to ATT&CK techniques:

- **T1110** – Brute Force
- **T1021** – Remote Services (Lateral Movement)
- **T1078** – Valid Accounts
- **T1550** – Use of Alternate Authentication Material

This mapping is used to standardize detection engineering and incident analysis.

---

## Future Improvements

- Expand ATT&CK coverage matrix with detection maturity scoring
- Add automated adversary emulation for repeatable attack testing
- Integrate additional data sources (DNS, proxy, firewall, EDR)
- Build incident response playbooks with severity-based workflows
- Introduce baseline behavior profiling and false-positive tuning

---

## Repository Structure

- `/architecture` – Network topology and architecture diagrams
- `/docs` – Documentation, detection use cases, and logging design
- `/infra` – VMware setup, IP planning, and network configuration
- `/splunk` – Detection rules, dashboards, and configurations
- `/windows` – Sysmon and event logging configuration
- `/openvpn` – VPN configuration and setup guides
- `/attack-simulation` – Attack scenarios and simulation scripts
- `/screenshots` – Evidence of dashboards and alerts
- `/diagrams` – Visual architecture and attack flow diagrams