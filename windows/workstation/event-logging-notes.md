# Windows Endpoint Event Logging

## Overview

This document describes the Windows event logs collected from the Windows 10 endpoint using Splunk Universal Forwarder.

The selected log sources provide visibility into authentication activity, system events, endpoint behavior, PowerShell execution, and Sysmon telemetry to support security monitoring and incident response.

---

## Log Sources

### Security Log

**Log Name**

```text
Security
```

**Index**

```text
windows
```

**Purpose**

Collects Windows security auditing events including:

* Successful logons
* Failed logons
* Account lockouts
* Privilege assignments
* User management events
* Security policy changes

---

### System Log

**Log Name**

```text
System
```

**Index**

```text
windows
```

**Purpose**

Collects operating system events such as:

* Service creation and failures
* Driver events
* System startup and shutdown
* Hardware-related events

---

### Application Log

**Log Name**

```text
Application
```

**Index**

```text
windows
```

**Purpose**

Collects application-generated events, including application errors, warnings, and informational messages.

---

### Sysmon Operational Log

**Log Name**

```text
Microsoft-Windows-Sysmon/Operational
```

**Index**

```text
sysmon
```

**Purpose**

Provides enhanced endpoint telemetry for threat detection, including:

* Process creation
* Network connections
* Driver loading
* File creation
* Registry modifications
* Process injection
* Image loads
* DNS queries

---

### PowerShell Operational Log

**Log Name**

```text
Microsoft-Windows-PowerShell/Operational
```

**Index**

```text
windows
```

**Purpose**

Captures PowerShell operational events to support detection of malicious script execution and administrative activity.

---

### Windows PowerShell Log

**Log Name**

```text
Windows PowerShell
```

**Index**

```text
windows
```

**Purpose**

Collects classic PowerShell events related to interactive sessions and command execution.

---

## Event Collection Summary

| Log Source             | Index   | Security Value                       |
| ---------------------- | ------- | ------------------------------------ |
| Security               | windows | Authentication and security auditing |
| System                 | windows | Operating system events              |
| Application            | windows | Application activity                 |
| Sysmon Operational     | sysmon  | Advanced endpoint telemetry          |
| PowerShell Operational | windows | PowerShell monitoring                |
| Windows PowerShell     | windows | PowerShell execution history         |

---

## Detection Coverage

The collected logs support detection of:

* Brute force attacks
* Account compromise
* Privilege escalation
* Suspicious PowerShell activity
* Process execution anomalies
* Lateral movement
* Persistence mechanisms
* Defense evasion techniques

---

## Data Collection Method

Logs are collected locally by Splunk Universal Forwarder and forwarded to the central Splunk Enterprise server for indexing, correlation, detection, and investigation.

---

## Notes

* Security, System, Application, and PowerShell logs are stored in the **windows** index.
* Sysmon events are stored in the dedicated **sysmon** index to separate endpoint telemetry from standard Windows event logs.
* XML rendering is enabled for Security and Sysmon logs to preserve complete event data for detailed analysis.
