# DR-001 — Brute Force Authentication

## Rule Information

| Field | Value |
|-------|-------|
| Rule Name | Brute Force Authentication Detection |
| Detection ID | DR-001 |
| Category | Authentication |
| Severity | High |
| Validation Scenario | AS-001 — Password Brute Force |

---

# Objective

Detect repeated failed authentication attempts that may indicate a password guessing or brute force attack against Windows local or Active Directory accounts.

---

# Threat Description

Brute force attacks attempt to gain unauthorized access by repeatedly trying different passwords until valid credentials are found. Successful attacks can lead to unauthorized access, privilege escalation, lateral movement, and further compromise of the environment.

---

# SPL Search

```spl
(index=windows OR index=ad)
sourcetype="XmlWinEventLog:Security"
EventCode=4625
| bucket span=5m _time
| stats count values(host) AS Hosts values(IpAddress) AS SourceIPs by TargetUserName _time
| where count>=10
| rename TargetUserName AS User
| sort -count
```

---

# Required Data Sources

- Windows Security Log

---

# Windows Event IDs

| Event ID | Description |
|----------|-------------|
| 4625 | Failed Logon |
| 4624 | Successful Logon |
| 4740 | User Account Locked |

---

# MITRE ATT&CK Mapping

| Field | Value |
|-------|-------|
| Tactic | Credential Access |
| Technique | T1110 — Brute Force |

---

# Alert Severity

**High**

---

# Detection Threshold

Generate an alert when:

- Ten or more failed logon attempts occur against the same account within five minutes.
- Failed logon attempts originate from the same host or IP address.
- Multiple failed logons are followed by a successful authentication or account lockout.

---

# False Positive Considerations

Potential legitimate activity includes:

- Users entering incorrect passwords multiple times.
- Password synchronization failures.
- Services using expired credentials.
- Misconfigured scheduled tasks.
- Authorized vulnerability scanning.

---

# Investigation Guidance

1. Identify the targeted account.
2. Review the originating workstation and source IP address.
3. Check for successful logons following the failed attempts.
4. Determine whether the account was locked.
5. Investigate additional authentication attempts from the same source.
6. Escalate the incident if malicious activity is confirmed.