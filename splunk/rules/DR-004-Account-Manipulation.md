# DR-004 — Account Manipulation

## Rule Information

| Field | Value |
|-------|-------|
| Rule Name | Account Manipulation Detection |
| Detection ID | DR-004 |
| Category | Persistence / Privilege Escalation |
| Severity | High |
| Validation Scenario | AS-004 — Account Manipulation |

---

# Objective

Detect unauthorized account creation, modification, and privilege assignment that may indicate persistence or privilege escalation within a Windows environment.

---

# Threat Description

Attackers often create new accounts or modify existing ones to maintain persistence and gain elevated privileges after compromising a system. Monitoring account management events helps identify unauthorized administrative actions before they can be leveraged for further attacks.

---

# SPL Search

```spl
index=windows sourcetype="WinEventLog:Security"
(EventCode=4720 OR EventCode=4722 OR EventCode=4724 OR EventCode=4728 OR EventCode=4732 OR EventCode=4756)
| table _time ComputerName SubjectUserName TargetUserName GroupName EventCode
| sort -_time
```

---

# Required Data Sources

- Windows Security Log
- Sysmon (Optional)

---

# Windows Event IDs

| Event ID | Description |
|----------|-------------|
| 4720 | User Account Created |
| 4722 | User Account Enabled |
| 4724 | Password Reset Attempt |
| 4728 | Member Added to Global Security Group |
| 4732 | Member Added to Local Security Group |
| 4756 | Member Added to Universal Security Group |

---

# MITRE ATT&CK Mapping

| Field | Value |
|-------|-------|
| Tactic | Persistence / Privilege Escalation |
| Techniques | T1136 — Create Account<br>T1098 — Account Manipulation |

---

# Alert Severity

**High**

---

# Detection Threshold

Generate an alert when:

- A new user account is created.
- An existing account is enabled unexpectedly.
- A user is added to a privileged security group.
- Administrative privileges are assigned outside approved change windows.

---

# False Positive Considerations

Potential legitimate activity includes:

- User onboarding and offboarding.
- Help desk password resets.
- Active Directory administration.
- Scheduled maintenance.
- Approved privilege assignments.

---

# Investigation Guidance

1. Identify the administrator who performed the action.
2. Verify that the activity was authorized.
3. Review recent changes made to the affected account.
4. Check whether privileged groups were modified.
5. Investigate subsequent authentication or privilege escalation activity.
6. Escalate the incident if unauthorized account changes are confirmed.