# DR-007 — Lateral Movement

## Rule Information

| Field | Value |
|-------|-------|
| Rule Name | Lateral Movement Detection |
| Detection ID | DR-007 |
| Category | Lateral Movement |
| Severity | High |
| Validation Scenario | AS-007 — Lateral Movement |

---

# Objective

Detect remote administration and lateral movement techniques used by attackers to move between systems after gaining initial access.

---

# Threat Description

After compromising a system, attackers commonly use legitimate remote administration protocols such as RDP, SMB, PsExec, Windows Remote Management (WinRM), or explicit credentials to move laterally across the network. Monitoring these activities helps identify unauthorized access before additional systems are compromised.

---

# SPL Search

```spl
index=windows
(EventCode=4624 Logon_Type=3 OR
 EventCode=4624 Logon_Type=10 OR
 EventCode=4648 OR
 EventCode=5140)
| table _time Account_Name ComputerName IpAddress Logon_Type EventCode
| sort -_time
```

---

# Required Data Sources

- Windows Security Log
- Sysmon

---

# Windows Event IDs

| Event ID | Description |
|----------|-------------|
| 4624 | Successful Logon |
| 4648 | Logon Using Explicit Credentials |
| 4672 | Special Privileges Assigned to New Logon |
| 5140 | Network Share Access |
| Sysmon Event ID 1 | Process Creation |

---

# MITRE ATT&CK Mapping

| Field | Value |
|-------|-------|
| Tactic | Lateral Movement |
| Techniques | T1021.001 — Remote Desktop Protocol (RDP)<br>T1021.002 — SMB/Windows Admin Shares<br>T1021.006 — Windows Remote Management (WinRM) |

---

# Alert Severity

**High**

---

# Detection Threshold

Generate an alert when:

- A remote interactive (RDP) logon occurs.
- Explicit credentials are used for remote authentication.
- Administrative shares are accessed.
- Multiple remote logons originate from the same source host within a short period.

---

# False Positive Considerations

Potential legitimate activity includes:

- System administrator maintenance.
- Help desk remote support.
- Software deployment tools.
- Patch management solutions.
- Backup and monitoring platforms.

---

# Investigation Guidance

1. Identify the source and destination hosts.
2. Verify the account used for remote authentication.
3. Review the authentication method and logon type.
4. Check for privilege escalation before or after the remote session.
5. Review process creation events on the destination host.
6. Investigate additional lateral movement from the same source system.
7. Escalate the incident if unauthorized remote access is confirmed.