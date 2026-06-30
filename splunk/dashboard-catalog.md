# Splunk Dashboard Catalog

## Overview

This document serves as the central catalog for all dashboards developed as part of the Enterprise SOC Monitoring & Incident Response Lab.

The dashboards provide operational visibility into authentication events, endpoint activity, security alerts, threat hunting data, and MITRE ATT&CK coverage using Windows Event Logs, Sysmon telemetry, Active Directory logs, and Splunk Enterprise.

Each dashboard is documented individually under the `dashboards/` directory. This catalog provides a high-level overview of the available dashboards, their objectives, and implementation status.

---

# Dashboard Development Workflow

Each dashboard follows the workflow below:

1. Define the monitoring objective.
2. Identify the required data sources.
3. Design dashboard panels.
4. Develop SPL searches for each panel.
5. Validate dashboard visualizations.
6. Optimize dashboard performance.
7. Document the dashboard.

---

# Dashboard Standard

Every dashboard within this project follows a consistent documentation structure.

Each dashboard includes:

- Overview
- Purpose
- Data Sources
- Dashboard Panels
- Related Detection Rules
- Dashboard Validation

---

# Dashboard Coverage

| Dashboard | Primary Focus | Data Sources |
|-----------|---------------|--------------|
| Authentication | Authentication Monitoring | Windows Security Log, Active Directory |
| Endpoint Activity | Endpoint Monitoring | Sysmon, Windows Security Log, Windows System Log |
| Detection & Alerts | SOC Operations | Splunk Alerts, Windows Logs, Sysmon |
| Threat Hunting | Threat Hunting | Sysmon, Windows Security Log, Windows System Log |
| MITRE ATT&CK Coverage | Detection Engineering | Detection Rules, Splunk Alerts, Windows Logs, Sysmon |

---

# Dashboard Documentation

Detailed documentation for each dashboard is maintained under the `dashboards/` directory.

| Dashboard | Documentation |
|-----------|---------------|
| Authentication | `dashboards/Authentication.md` |
| Endpoint Activity | `dashboards/Endpoint-Activity.md` |
| Detection & Alerts | `dashboards/Detection-Alerts.md` |
| Threat Hunting | `dashboards/Threat-Hunting.md` |
| MITRE ATT&CK Coverage | `dashboards/MITRE-Coverage.md` |