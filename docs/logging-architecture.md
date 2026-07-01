# Logging Architecture

## Overview

This document describes how security telemetry is collected, forwarded, processed, and utilized throughout the Enterprise SOC Monitoring & Incident Response Lab.

The logging architecture provides centralized visibility into endpoint, authentication, Active Directory, and VPN activity by forwarding logs to Splunk Enterprise for indexing, detection engineering, threat hunting, and incident investigation.

---

# Telemetry Sources

| Source | Collected Logs |
|----------|----------------|
| Windows 10 Endpoint | Security, System, Application, PowerShell, Sysmon |
| Active Directory (DC1) | Security, Directory Service, DNS |
| OpenVPN Server | Authentication, Connection, Session Logs |

---

# Log Collection Flow

Security telemetry follows the pipeline below:

```text
(Windows Endpoint, Domain Controller, OpenVPN Server)
        │
        ▼
Splunk Universal Forwarders
        │
        ▼
Splunk Enterprise
        │
        ▼
Indexes
        │
        ▼
Detection Rules
        │
        ▼
Alerts
        │
        ▼
Dashboards
        │
        ▼
Threat Hunting & Incident Investigation
```

---

# Log Forwarding

Windows systems use Splunk Universal Forwarder to collect and forward event logs to the Splunk Enterprise server.

The OpenVPN server forwards VPN logs for remote access monitoring.

All telemetry is sent to the Splunk receiving port:

```text
192.168.10.10:9997
```

---

# Index Strategy

Collected events are organized into dedicated indexes based on their source.

| Index | Purpose |
|--------|---------|
| windows | Windows Event Logs |
| sysmon | Sysmon Endpoint Telemetry |
| ad | Active Directory Logs |
| vpn | OpenVPN Logs |

Detailed index configuration is documented in `splunk/README.md`.

---

# Detection Pipeline

After ingestion, security events move through the following workflow:

```text
Telemetry
     │
     ▼
Parsing & Indexing
     │
     ▼
Searches
     │
     ▼
Detection Rules
     │
     ▼
Alerts
     │
     ▼
SOC Dashboards
     │
     ▼
Threat Hunting
     │
     ▼
Incident Investigation
```

---

# Supported Security Monitoring

The logging architecture provides visibility into:

- Authentication activity
- PowerShell execution
- Process creation
- Account management
- Windows persistence
- Credential access
- Lateral movement
- Network reconnaissance
- VPN activity

---

# Related Documentation

- `architecture/README.md`
- `splunk/README.md`
- `docs/detection-use-cases.md`
- `splunk/detection-catalog.md`
- `MITRE-ATTACK-MAPPING.md`