# DR-003 — Malicious PowerShell

## Rule Information

| Field | Value |
|-------|-------|
| Rule Name | Malicious PowerShell Execution Detection |
| Detection ID | DR-003 |
| Category | Execution |
| Severity | High |
| Validation Scenario | AS-003 — Malicious PowerShell |

---

# Objective

Detect suspicious PowerShell execution commonly associated with post-exploitation, malware, and attacker tradecraft.

---

# Threat Description

PowerShell is a legitimate Windows administration tool that is frequently abused by attackers to execute malicious commands, download payloads, bypass security controls, and establish persistence. Detecting suspicious PowerShell activity provides early visibility into post-exploitation behavior.

---

# SPL Search

```spl
index=sysmon EventCode=1 Image="*\\powershell.exe"
(CommandLine="*EncodedCommand*" OR
 CommandLine="*-enc*" OR
 CommandLine="*Invoke-Expression*" OR
 CommandLine="*IEX*" OR
 CommandLine="*DownloadString*" OR
 CommandLine="*ExecutionPolicy Bypass*" OR
 CommandLine="*-nop*" OR
 CommandLine="*-w hidden*")
| table _time Computer User Image ParentImage CommandLine
| sort -_time
```

---

# Required Data Sources

- Sysmon
- Windows PowerShell Operational Log

---

# Windows Event IDs

| Event ID | Description |
|----------|-------------|
| Sysmon Event ID 1 | Process Creation |
| 4103 | PowerShell Module Logging |
| 4104 | PowerShell Script Block Logging |

---

# MITRE ATT&CK Mapping

| Field | Value |
|-------|-------|
| Tactic | Execution |
| Technique | T1059.001 — PowerShell |

---

# Alert Severity

**High**

PowerShell is commonly leveraged during post-exploitation. Suspicious command-line arguments should be investigated immediately.

---

# Detection Threshold

Generate an alert whenever PowerShell execution contains one or more of the following indicators:

- EncodedCommand
- Invoke-Expression (IEX)
- DownloadString
- ExecutionPolicy Bypass
- Hidden Window
- NoProfile
- NonInteractive

---

# False Positive Considerations

Potential legitimate activity includes:

- Administrative PowerShell scripts
- Configuration management tools
- Endpoint management solutions
- Security monitoring software
- Approved automation scripts

---

# Investigation Guidance

1. Review the full PowerShell command line.
2. Identify the parent process that launched PowerShell.
3. Verify the user who executed the command.
4. Check for network connections or payload downloads.
5. Review additional process creation events.
6. Investigate persistence or credential access activity following execution.