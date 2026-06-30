# DR-008 — Network Reconnaissance

## Rule Information

| Field | Value |
|-------|-------|
| Rule Name | Network Reconnaissance Detection |
| Detection ID | DR-008 |
| Category | Discovery |
| Severity | Medium |
| Validation Scenario | AS-008 — Network Reconnaissance |

---

# Objective

Detect network discovery and service enumeration activity that may indicate an attacker identifying systems and services for subsequent exploitation or lateral movement.

---

# Threat Description

Following initial access, attackers often perform internal network reconnaissance to identify live hosts, open ports, shared resources, and available services. Monitoring abnormal network connection patterns can help detect reconnaissance before more advanced attack stages begin.

---

# SPL Search

```spl
index=sysmon EventCode=3
| bucket span=5m _time
| stats dc(DestinationIp) AS UniqueHosts count BY Computer Image _time
| where UniqueHosts >= 20
| sort -UniqueHosts
```

---

# Required Data Sources

- Sysmon
- Windows Firewall Logs (Optional)

---

# Windows Event IDs

| Event ID | Description |
|----------|-------------|
| Sysmon Event ID 3 | Network Connection |

---

# MITRE ATT&CK Mapping

| Field | Value |
|-------|-------|
| Tactic | Discovery |
| Techniques | T1018 — Remote System Discovery<br>T1046 — Network Service Discovery |

---

# Alert Severity

**Medium**

---

# Detection Threshold

Generate an alert when:

- A host connects to a large number of internal systems within a short period.
- Sequential connections target multiple hosts or services.
- Network scanning activity exceeds the normal baseline.
- Excessive outbound connection attempts are detected.

---

# False Positive Considerations

Potential legitimate activity includes:

- Vulnerability scanners.
- Asset inventory tools.
- Network monitoring platforms.
- Endpoint management solutions.
- Authorized security assessments.

---

# Investigation Guidance

1. Identify the source host initiating the connections.
2. Review the process responsible for the network activity.
3. Determine the destination hosts and services.
4. Verify whether the activity originated from an approved scanning solution.
5. Review subsequent authentication or lateral movement events.
6. Escalate the incident if unauthorized reconnaissance is confirmed.