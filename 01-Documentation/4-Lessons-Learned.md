# Lessons Learned

# Overview

This document summarizes the key technical and investigative lessons learned during the Windows Remote Desktop (RDP) Brute Force investigation.

Although the attack simulation itself was straightforward, the investigation highlighted several important concepts related to Windows Security Logs, Wazuh event collection, event correlation, and SOC investigation methodology.

---

# Lesson 1 – Never Trust Your First Impression

The first search performed in the Wazuh Dashboard returned no Event ID 4625 results.

At first glance, this suggested that Wazuh had failed to detect the brute force attack.

Instead of assuming that the detection had failed, the investigation continued by validating every component involved in the detection pipeline.

**Lesson learned:**

> Never conclude that a security tool has failed before validating every layer of the monitoring infrastructure.

---

# Lesson 2 – Always Start with the Original Evidence

The investigation moved from Wazuh to Windows Event Viewer.

Windows Security Logs clearly showed fifteen Event ID 4625 entries.

This confirmed that Windows had correctly recorded every failed authentication attempt.

**Lesson learned:**

> During an investigation, always validate the original evidence before analyzing SIEM alerts.

Windows Event Logs are the primary source of truth.

---

# Lesson 3 – Understanding the Detection Pipeline

One of the most valuable lessons learned during this investigation was understanding how security events travel through the monitoring infrastructure.

The complete pipeline was successfully validated.

```
Attack

↓

Windows Security Event

↓

Wazuh Agent

↓

Wazuh Manager

↓

archives.json

↓

Detection Rules

↓

Correlation Rules

↓

SOC Dashboard
```

This investigation demonstrated that each component plays a specific role in the detection process.

---

# Lesson 4 – archives.json Is Extremely Valuable

Initially, the Dashboard did not provide the expected information.

Instead of relying only on the graphical interface, the investigation continued directly on the Ubuntu Wazuh Manager.

Searching **archives.json** confirmed that all fifteen Windows Event ID 4625 entries had been received.

**Lesson learned:**

> The Dashboard is not the only source of evidence.

The Wazuh Manager provides direct access to the raw events collected from monitored systems.

---

# Lesson 5 – Windows Events Are Not Wazuh Alerts

One of the most important concepts learned during this investigation was the distinction between Windows Events and Wazuh Rules.

Windows generated:

- Event ID 4625

Wazuh generated:

- Rule 60122

Finally, Wazuh correlated these events into:

- Rule 60204

Understanding this difference is essential for every SOC analyst.

---

# Lesson 6 – Correlation Reduces Alert Fatigue

Initially, it seemed surprising that only one Rule 60204 alert was generated.

The investigation demonstrated that this behavior is intentional.

Rule 60122 detects every failed authentication attempt.

Rule 60204 correlates multiple failed logons into a single security incident.

This greatly reduces alert fatigue while preserving forensic visibility.

---

# Lesson 7 – Event Correlation Is More Valuable Than Individual Alerts

The investigation demonstrated that analysts should focus on the correlation alert rather than investigating every individual failed authentication.

Instead of reviewing dozens of identical alerts, analysts can begin with the correlation rule and then examine the supporting evidence only if necessary.

This significantly improves investigation efficiency.

---

# Lesson 8 – MITRE ATT&CK Provides Valuable Context

The investigation confirmed that the attack was automatically mapped to:

**MITRE ATT&CK T1110 – Brute Force**

This mapping immediately explains:

- the attacker's objective,
- the attack technique,
- the affected security domain,
- and the appropriate defensive response.

MITRE ATT&CK provides valuable context beyond simple event detection.

---

# Lesson 9 – Investigation Requires Patience

Several assumptions made during the investigation proved to be incorrect.

Examples include:

- assuming that Wazuh had not detected the attack,
- assuming that Event ID 4625 had not been collected,
- assuming that the detection rules had failed.

Each assumption was verified and either confirmed or disproved using technical evidence.

**Lesson learned:**

> Good investigations are based on evidence, not assumptions.

---

# Lesson 10 – Think Like a SOC Analyst

Perhaps the most important lesson learned was the investigative mindset.

Rather than asking:

"Why isn't there an alert?"

The investigation evolved into asking:

- Did Windows record the event?
- Did the Wazuh Agent collect it?
- Did the Manager receive it?
- Was the event stored?
- Which rule processed it?
- Why was MITRE ATT&CK T1110 selected?

This systematic approach is the foundation of professional SOC investigations.

---

# Skills Acquired

This laboratory strengthened practical knowledge in:

- Windows Security Logs
- Windows Event Viewer
- Event ID 4625 analysis
- Wazuh Agent
- Wazuh Manager
- archives.json
- Detection Rules
- Correlation Rules
- MITRE ATT&CK
- SOC Investigation Methodology
- Evidence Validation
- Incident Documentation

---

# Personal Reflection

This investigation was significantly more valuable than simply triggering a Wazuh alert.

It provided a deeper understanding of how Windows, Wazuh, and MITRE ATT&CK interact during a real security investigation.

More importantly, it reinforced the importance of validating evidence before drawing conclusions.

This experience represents an important milestone toward developing practical SOC Analyst skills and will serve as a foundation for future investigations involving Active Directory, PowerShell, Scheduled Tasks, Registry modifications, File Integrity Monitoring, and other Windows attack techniques.

---

# Final Takeaway

The most important lesson learned from this investigation is:

> **A SOC analyst does not investigate alerts. A SOC analyst investigates evidence.**

Alerts are only the starting point.

Professional investigations require validating every stage of the detection pipeline before reaching a conclusion.
