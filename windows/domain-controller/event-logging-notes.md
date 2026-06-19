# Active Directory Event Logging

## Overview

This document describes the Windows event logs collected from the Active Directory Domain Controller using Splunk Universal Forwarder.

The selected log sources provide visibility into domain authentication, directory services, and DNS activity, enabling centralized monitoring and detection of identity-based attacks within the enterprise environment.

---

## Log Sources

### Security Log

**Log Name**

```text
Security
```

**Index**

```text
ad
```

**Purpose**

Collects Windows Security auditing events related to Active Directory, including:

* Successful and failed user logons
* Kerberos authentication events
* Account lockouts
* Privileged logons
* User account creation and deletion
* Group membership changes
* Account management events
* Security policy modifications

---

### Directory Service Log

**Log Name**

```text
Directory Service
```

**Index**

```text
ad
```

**Purpose**

Captures Active Directory service events, including:

* Directory replication
* LDAP operations
* Active Directory database events
* Domain service warnings and errors
* Object creation, modification, and deletion

---

### DNS Server Log

**Log Name**

```text
DNS Server
```

**Index**

```text
ad
```

**Purpose**

Collects DNS server activity, including:

* DNS query processing
* Zone updates
* Dynamic DNS registrations
* DNS server warnings and errors
* Name resolution events

---

## Event Collection Summary

| Log Source        | Index | Security Value                      |
| ----------------- | ----- | ----------------------------------- |
| Security          | ad    | Authentication and account auditing |
| Directory Service | ad    | Active Directory operations         |
| DNS Server        | ad    | DNS activity and name resolution    |

---

## Detection Coverage

The collected logs support detection of:

* Brute force attacks
* Password spraying
* Kerberos authentication anomalies
* Account lockouts
* User and group modifications
* Privileged account activity
* Suspicious Active Directory changes
* DNS-based reconnaissance
* Lateral movement indicators

---

## Data Collection Method

Logs are collected locally by Splunk Universal Forwarder and forwarded to the central Splunk Enterprise server, where they are indexed in the **ad** index for correlation, investigation, and detection.

---

## Notes

* All Domain Controller logs are stored in the dedicated **ad** index.
* XML rendering is enabled for the Security log to preserve complete event details.
* Centralizing identity-related events in a dedicated index simplifies threat hunting, detection engineering, and incident response.
