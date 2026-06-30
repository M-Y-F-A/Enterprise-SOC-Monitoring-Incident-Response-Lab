# Screenshots

## Overview

This directory contains screenshots captured throughout the implementation of the Enterprise SOC Monitoring & Incident Response Lab.

The screenshots provide visual evidence of each project phase, documenting the deployment, configuration, validation, and operation of the lab environment. They also demonstrate the implementation of security monitoring, detection engineering, attack simulations, dashboards, and incident investigation workflows.

All screenshots were captured from the live lab environment during development and validation.

---

# Purpose

The screenshots serve as supporting evidence for:

- Infrastructure deployment
- Active Directory configuration
- Splunk Enterprise installation and configuration
- Endpoint onboarding and log collection
- VPN deployment and connectivity
- Detection rule validation
- Dashboard implementation
- Attack simulation execution
- Incident investigation and evidence collection

---

# Directory Structure

```text
screenshots/
│
├── phase-1-infrastructure/
├── phase-2-active-directory/
├── phase-3-splunk/
├── phase-4-endpoint-monitoring/
├── phase-5-vpn/
├── phase-6-detections/
├── phase-7-dashboards/
├── phase-8-investigations/
└── phase-9-attack-scenarios/
```

---

# Phase Description

| Phase | Description |
|--------|-------------|
| Phase 1 – Infrastructure | Virtual machine deployment, network configuration, and connectivity validation |
| Phase 2 – Active Directory | Domain deployment, Organizational Units, users, groups, and Group Policy configuration |
| Phase 3 – Splunk | Splunk Enterprise installation, index creation, and SIEM configuration |
| Phase 4 – Endpoint Monitoring | Sysmon deployment, Splunk Universal Forwarder configuration, and log ingestion validation |
| Phase 5 – VPN | OpenVPN deployment, client connectivity, and remote access validation |
| Phase 6 – Detections | Detection rule implementation, SPL validation, alert generation, and detection testing |
| Phase 7 – Dashboards | Dashboard creation, panel validation, and operational monitoring views |
| Phase 8 – Investigations | Incident investigation workflow, timeline analysis, search results, and collected evidence |
| Phase 9 – Attack Scenarios | Controlled attack execution, generated telemetry, detection validation, and attack evidence |

---

# Screenshot Standards

Each screenshot should demonstrate one or more of the following:

- Successful installation or deployment
- Correct configuration
- Operational service status
- Log collection validation
- Detection rule execution
- Alert generation
- Dashboard visualization
- Investigation evidence
- Attack simulation results

Where applicable, screenshots should include timestamps, hostnames, and relevant system information while avoiding the disclosure of sensitive information.

---

# Related Documentation

The screenshots support the documentation available throughout the repository, including:

- `README.md`
- `docs/lab-overview.md`
- `architecture/README.md`
- `docs/logging-architecture.md`
- `docs/detection-use-cases.md`
- `docs/attack-scenario.md`
- `attack-simulation/playbooks.md`
- `splunk/README.md`
- `splunk/detection-catalog.md`
- `splunk/dashboard-catalog.md`
- `MITRE-ATTACK-MAPPING.md`

---

# Notes

As the project evolves, additional screenshots will be added to document new detections, dashboards, attack scenarios, investigations, and infrastructure enhancements. Together, these screenshots provide visual validation of the complete Security Operations Center (SOC) workflow implemented within this lab.