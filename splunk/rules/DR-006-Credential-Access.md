# DR-006 — Credential Access

## Rule Information

| Field | Value |
|-------|-------|
| Rule Name | Credential Access Detection |
| Detection ID | DR-006 |
| Category | Credential Access |
| Severity | Critical |
| Validation Scenario | AS-006 — Credential Access |

---

# Objective

Detect attempts to access or dump credentials from the Local Security Authority Subsystem Service (LSASS) or other Windows credential stores.

---

# Threat Description

Credential dumping is a common post-exploitation technique used by attackers to obtain plaintext credentials, password hashes, and Kerberos tickets. Access to LSASS memory is often associated with tools such as Mimikatz and may indicate an attempt to facilitate privilege escalation or lateral movement.

---

# SPL Search

```spl
index=sysmon EventCode=10
TargetImage="*\\lsass.exe"
| table _time Computer SourceImage TargetImage GrantedAccess SourceProcessGUID
| sort -_time
```

---

# Required Data Sources

- Sysmon

---

# Windows Event IDs

| Event ID | Description |
|----------|-------------|
| Sysmon Event ID 10 | Process Access |
| Sysmon Event ID 1 | Process Creation |
| Sysmon Event ID 7 | Image Loaded (Optional) |

---

# MITRE ATT&CK Mapping

| Field | Value |
|-------|-------|
| Tactic | Credential Access |
| Technique | T1003.001 — LSASS Memory |

---

# Alert Severity

**Critical**

---

# Detection Threshold

Generate an alert when:

- A non-system process accesses `lsass.exe`.
- A process requests high-privilege access to LSASS memory.
- Known credential dumping tools interact with LSASS.

---

# False Positive Considerations

Potential legitimate activity includes:

- Endpoint Detection and Response (EDR) solutions.
- Antivirus software.
- Windows Defender.
- Authorized forensic tools.
- Approved security monitoring applications.

---

# Investigation Guidance

1. Identify the process accessing `lsass.exe`.
2. Review the full command line of the source process.
3. Verify the parent process and executing user.
4. Determine whether the process is trusted or digitally signed.
5. Review related PowerShell or process creation events.
6. Investigate subsequent authentication or lateral movement activity.
7. Escalate the incident if unauthorized credential access is confirmed.