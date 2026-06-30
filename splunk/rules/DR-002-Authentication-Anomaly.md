# DR-002 — Authentication Anomaly

## Rule Information

| Field | Value |
|-------|-------|
| Rule Name | Authentication Anomaly Detection |
| Detection ID | DR-002 |
| Category | Authentication |
| Severity | Medium |
| Validation Scenario | AS-002 — Authentication Validation |

---

# Objective

Detect authentication activity that deviates from normal user behavior and may indicate compromised credentials or unauthorized account usage.

---

# Threat Description

Attackers frequently use valid credentials to blend into legitimate network activity. Unusual authentication patterns—such as logons from unfamiliar workstations, abnormal logon types, or activity outside normal business hours—can indicate account compromise.

---

# SPL Search

```spl
index=windows sourcetype="WinEventLog:Security" EventCode=4624
| eval Hour=strftime(_time,"%H")
| where Hour<6 OR Hour>20
| table _time Account_Name Workstation_Name IpAddress Logon_Type
| sort -_time
```

---

# Required Data Sources

- Windows Security Log
- Active Directory Authentication Logs

---

# Windows Event IDs

| Event ID | Description |
|----------|-------------|
| 4624 | Successful Logon |
| 4625 | Failed Logon |
| 4648 | Logon Using Explicit Credentials |
| 4768 | Kerberos Authentication Ticket Request |
| 4769 | Kerberos Service Ticket Request |

---

# MITRE ATT&CK Mapping

| Field | Value |
|-------|-------|
| Tactic | Defense Evasion |
| Technique | T1078 — Valid Accounts |

---

# Alert Severity

**Medium**

---

# Detection Threshold

Generate an alert when one or more of the following conditions occur:

- Authentication outside business hours.
- Authentication from a previously unseen workstation.
- Multiple source hosts authenticate to the same account within a short period.
- Unusual logon type for the user.
- Excessive Kerberos authentication requests.

---

# False Positive Considerations

Possible legitimate activity includes:

- Remote work or VPN connections.
- Shift-based employees.
- Administrative maintenance.
- Newly deployed workstations.
- Help desk or IT support activities.

---

# Investigation Guidance

1. Verify whether the user initiated the authentication.
2. Identify the source workstation and IP address.
3. Compare the activity with the user's historical behavior.
4. Review logon type and authentication method.
5. Check for privilege escalation or lateral movement after authentication.
6. Investigate any additional suspicious activity related to the account.