# DR-005 — Windows Persistence

## Rule Information

| Field | Value |
|-------|-------|
| Rule Name | Windows Persistence Detection |
| Detection ID | DR-005 |
| Category | Persistence |
| Severity | High |
| Validation Scenario | AS-005 — Windows Persistence |

---

# Objective

Detect common Windows persistence techniques used by attackers to maintain access after compromising a system.

---

# Threat Description

Attackers often establish persistence by creating scheduled tasks or installing Windows services that automatically execute after system startup or user logon. Monitoring these events helps identify unauthorized persistence mechanisms before they can be used for continued access.

---

# SPL Search

```spl
index=windows
(EventCode=4698 OR EventCode=4699 OR EventCode=4700 OR EventCode=4701 OR EventCode=7045)
| table _time ComputerName EventCode SubjectUserName Service_Name Task_Name
| sort -_time
```

---

# Required Data Sources

- Windows Security Log
- Windows System Log
- Sysmon

---

# Windows Event IDs

| Event ID | Description |
|----------|-------------|
| 4698 | Scheduled Task Created |
| 4699 | Scheduled Task Deleted |
| 4700 | Scheduled Task Enabled |
| 4701 | Scheduled Task Disabled |
| 7045 | Windows Service Installed |

---

# MITRE ATT&CK Mapping

| Field | Value |
|-------|-------|
| Tactic | Persistence |
| Techniques | T1053.005 — Scheduled Task<br>T1543.003 — Windows Service |

---

# Alert Severity

**High**

---

# Detection Threshold

Generate an alert when:

- A new scheduled task is created.
- A Windows service is installed.
- A scheduled task is enabled or modified unexpectedly.
- A service is installed outside approved maintenance windows.

---

# False Positive Considerations

Potential legitimate activity includes:

- Software installation.
- Windows updates.
- Enterprise management tools.
- Backup solutions.
- Approved administrative maintenance.

---

# Investigation Guidance

1. Identify the user or process responsible for creating the task or service.
2. Review the associated executable or command.
3. Verify whether the executable is trusted or digitally signed.
4. Determine whether the activity was authorized.
5. Review related process creation and PowerShell events.
6. Escalate the incident if unauthorized persistence is confirmed.