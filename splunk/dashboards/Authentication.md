# Authentication Dashboard

## Overview

The Authentication Dashboard provides real-time visibility into Windows and Active Directory authentication activity. It enables SOC analysts to monitor login behavior, identify authentication anomalies, detect brute force attacks, and investigate account-related security events.

This dashboard primarily supports authentication monitoring, incident triage, and detection validation.

---

# Purpose

- Monitor user authentication activity.
- Detect failed and successful logons.
- Identify brute force attacks and account lockouts.
- Visualize authentication trends across the environment.
- Support incident response and security investigations.

---

# Data Sources

- Windows Security Log
- Active Directory

---

# Dashboard Panels

## Successful Logons

**Purpose**

Display successful user authentication events.

**Event IDs**

- 4624

---

## Failed Logons

**Purpose**

Monitor failed authentication attempts that may indicate password guessing or user mistakes.

**Event IDs**

- 4625

---

## Account Lockouts

**Purpose**

Identify accounts locked due to excessive failed authentication attempts.

**Event IDs**

- 4740

---

## Authentication Timeline

**Purpose**

Visualize authentication activity over time to identify spikes or unusual patterns.

---

## Top Targeted Users

**Purpose**

Display user accounts receiving the highest number of authentication attempts.

---

## Top Source Hosts

**Purpose**

Identify systems generating the highest number of authentication events.

---

## Logon Type Distribution

**Purpose**

Visualize authentication events by Windows Logon Type.

---

## Authentication Activity by Host

**Purpose**

Display authentication volume for each monitored endpoint.

---

# Related Detection Rules

- DR-001 — Brute Force Authentication
- DR-002 — Authentication Anomaly

---

# Dashboard Validation

The dashboard is considered successfully implemented when:

- Authentication events are successfully indexed in Splunk.
- All dashboard panels display accurate data.
- Detection alerts are visible during attack simulations.
- Dashboard results support authentication investigations.