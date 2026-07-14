# Wazuh Detection Rules Analysis

# Overview

This document explains how Wazuh detected and correlated the simulated Windows Remote Desktop brute force attack.

The investigation focuses on the detection logic behind Rule 60122 and Rule 60204.

Understanding these rules is essential for SOC analysts because they demonstrate how Wazuh transforms raw Windows events into actionable security incidents.

---

# Detection Pipeline

The attack followed the detection pipeline below.

```

Attacker
│
▼
Remote Desktop (RDP)
│
▼
Windows Authentication
│
▼
Windows Security Log
│
▼
Event ID 4625
│
▼
Wazuh Agent
│
▼
Wazuh Manager
│
▼
archives.json
│
▼
Rule 60122
│
▼
Rule 60204
│
▼
MITRE ATT&CK T1110

```

---

# Windows Event ID 4625

## Description

Windows Event ID **4625** is generated whenever an authentication attempt fails.

This event is recorded inside the Windows Security log.

It is one of the most important events monitored by Security Operations Centers because it provides evidence of failed authentication attempts.

---

## Evidence Found

| Item | Value |
|------|-------|
| Windows Event ID | 4625 |
| Description | Failed Logon |
| Authentication | NTLM |
| Target Account | Administrator |
| Source Host | DC01-AD |

---

# Rule 60122

## Rule Information

| Property | Value |
|----------|-------|
| Rule ID | 60122 |
| Level | 5 |
| Description | Logon Failure – Unknown user or bad password |

---

## Purpose

Rule 60122 is responsible for detecting **each failed Windows authentication attempt**.

Every time Windows generates Event ID 4625, Wazuh evaluates the event against its rules.

If the event matches the detection logic, Rule 60122 generates an alert.

---

## Evidence

During this investigation:

- Windows generated 15 failed logons.
- Wazuh generated multiple Rule 60122 alerts.
- Each alert corresponded to a failed authentication attempt.

---

## Why Multiple Alerts?

Every authentication failure represents an independent security event.

Therefore:

```

15 Failed Logons

↓

15 Windows Event ID 4625

↓

Multiple Rule 60122 Alerts

```

This behavior allows analysts to investigate every failed authentication individually.

---

# Rule 60204

## Rule Information

| Property | Value |
|----------|-------|
| Rule ID | 60204 |
| Level | 10 |
| Description | Multiple Windows Logon Failures |

---

## Purpose

Rule 60204 is a **correlation rule**.

Unlike Rule 60122, it does not detect individual authentication failures.

Instead, it analyzes multiple Rule 60122 alerts occurring within a short period of time.

When the defined threshold is exceeded, Wazuh creates a single brute force incident.

---

## Why Only One Alert?

Although the attack generated many failed logons, Wazuh intentionally produced only one Rule 60204 alert.

This prevents alert fatigue.

Without correlation, a brute force attack generating thousands of failed logons would also generate thousands of critical alerts.

Instead:

```

15 Failed Logons

↓

Multiple Rule 60122 Alerts

↓

One Rule 60204 Incident

```

This behavior is typical of modern SIEM platforms.

---

# Alert Correlation

The investigation confirmed the following correlation workflow.

```

Windows Event 4625

↓

Rule 60122

↓

Rule 60122

↓

Rule 60122

↓

Rule 60122

↓

Rule 60122

↓

Correlation Engine

↓

Rule 60204

↓

SOC Investigation

```

---

# MITRE ATT&CK Mapping

The correlation rule automatically mapped the activity to:

| Framework | Value |
|-----------|--------|
| Technique | T1110 |
| Name | Brute Force |
| Tactic | Credential Access |

---

# Severity Analysis

## Rule 60122

Severity Level:

5

Purpose:

Detect individual failed logons.

---

## Rule 60204

Severity Level:

10

Purpose:

Detect an ongoing brute force attack.

---

# Analyst Interpretation

An analyst should not investigate Rule 60122 alerts independently when they occur in large numbers.

Instead, the analyst should identify whether Wazuh has generated a correlation alert such as Rule 60204.

The investigation should then focus on:

- Source IP
- Target Host
- Target Account
- Number of Attempts
- Time Window
- MITRE Technique

This approach significantly reduces investigation time.

---

# Investigation Results

| Evidence | Result |
|----------|---------|
| Windows Event | 4625 |
| Rule 60122 | Triggered |
| Rule 60204 | Triggered |
| Correlation | Successful |
| MITRE Mapping | Successful |
| Severity | High |

---

# Lessons Learned

This investigation demonstrated an important SOC concept.

Not every security alert represents an incident.

Rule 60122 represents **individual evidence**.

Rule 60204 represents **the incident itself**.

Understanding the difference between detection rules and correlation rules is fundamental for Security Operations Center analysts.

---

# Conclusion

The investigation successfully validated the Wazuh detection engine.

Individual Windows authentication failures were correctly detected through Rule 60122.

The correlation engine grouped these events into a single Rule 60204 incident, accurately identifying the attack as a Windows Remote Desktop brute force attack mapped to MITRE ATT&CK Technique T1110.

This investigation demonstrates how Wazuh reduces alert fatigue while preserving complete forensic visibility.
