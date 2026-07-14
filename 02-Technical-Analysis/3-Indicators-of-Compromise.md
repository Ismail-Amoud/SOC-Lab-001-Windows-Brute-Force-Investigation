# Indicators of Compromise (IOCs)

# Overview

This document summarizes all Indicators of Compromise (IOCs) identified during the Windows Remote Desktop (RDP) brute force investigation.

Although this attack was intentionally simulated in a controlled laboratory environment, the indicators documented below are identical to those that could be observed during a real brute force attack against a Windows system.

---

# Incident Summary

| Field | Value |
|--------|-------|
| Incident ID | SOC-LAB-001 |
| Incident Type | Windows RDP Brute Force |
| MITRE ATT&CK | T1110 – Brute Force |
| MITRE Sub-technique | T1110.001 – Password Guessing |
| Severity | High (Level 10) |
| Status | Closed |
| Environment | Home SOC Laboratory |

---

# Source Information

| Indicator | Value |
|-----------|-------|
| Source Host | DC01-AD |
| Source IP Address | 192.168.10.10 |
| Attack Origin | Internal Laboratory Network |
| Protocol | Remote Desktop Protocol (RDP) |
| Destination Port | TCP 3389 |

---

# Target Information

| Indicator | Value |
|-----------|-------|
| Target Host | WIN11-Lab |
| Operating System | Windows 11 Enterprise |
| Target Account | Administrator |
| Authentication Type | Interactive Logon (RDP) |

---

# Windows Indicators

| Indicator | Value |
|-----------|-------|
| Windows Event ID | 4625 |
| Event Description | An account failed to log on |
| Log Source | Windows Security Log |
| Audit Category | Logon Failure |

---

# Wazuh Indicators

| Indicator | Value |
|-----------|-------|
| Detection Rule | 60122 |
| Correlation Rule | 60204 |
| Wazuh Agent | WIN11-Lab |
| Wazuh Manager | Ubuntu Server |
| Event Collection | Successful |
| Correlation | Successful |

---

# Authentication Indicators

| Indicator | Value |
|-----------|-------|
| Authentication Protocol | RDP |
| Login Result | Failed |
| Failed Attempts | 15 |
| Successful Logins | None |

---

# Timeline Indicators

| Indicator | Value |
|-----------|-------|
| Attack Duration | Approximately 30–40 seconds |
| Authentication Attempts | 15 |
| Correlation Alert | 1 |
| Time Zone | EDT (UTC-4) |
| UTC Timestamp | 2026-07-13T01:48 |

---

# MITRE ATT&CK Indicators

| Indicator | Value |
|-----------|-------|
| Framework | MITRE ATT&CK |
| Tactic | Credential Access |
| Technique | T1110 – Brute Force |
| Sub-technique | T1110.001 – Password Guessing |

---

# Detection Chain

The following indicators were observed during the investigation.

```
Attack Generated
        │
        ▼
Remote Desktop Authentication
        │
        ▼
Windows Event ID 4625
        │
        ▼
Wazuh Agent
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

# Primary Evidence

The following evidence confirmed the brute force activity.

- Fifteen failed Remote Desktop authentication attempts.
- Windows Security Event ID 4625 generated for each failed authentication.
- Events successfully collected by the Wazuh Agent.
- Events successfully received by the Wazuh Manager.
- Rule 60122 triggered for failed logon events.
- Rule 60204 generated a correlated brute force alert.
- MITRE ATT&CK Technique T1110 assigned.

---

# Observed Security Artifacts

| Artifact | Purpose |
|----------|---------|
| Windows Event Viewer | Confirm failed logons |
| Security Log | Original evidence |
| archives.json | Raw event validation |
| Wazuh Dashboard | Alert investigation |
| Rule 60122 | Individual failed authentication |
| Rule 60204 | Correlated brute force incident |

---

# Analyst Assessment

The collected Indicators of Compromise clearly demonstrate a Windows Remote Desktop brute force attack.

No evidence of a successful authentication was identified.

The investigation confirmed that every authentication attempt failed and that the attack was successfully detected by the Wazuh correlation engine.

Because this exercise was performed inside a controlled laboratory, the incident is classified as a simulated attack used for defensive training.

---

# IOC Summary

| Category | Indicator |
|----------|-----------|
| Attack Type | Windows RDP Brute Force |
| Protocol | TCP 3389 (RDP) |
| Source Host | DC01-AD |
| Source IP | 192.168.10.10 |
| Target Host | WIN11-Lab |
| Target User | Administrator |
| Event ID | 4625 |
| Detection Rule | 60122 |
| Correlation Rule | 60204 |
| MITRE Technique | T1110 |
| MITRE Sub-technique | T1110.001 |
| Severity | High |
| Outcome | Authentication Failed |

---

# Conclusion

The Indicators of Compromise collected during this investigation provide a complete forensic record of the simulated brute force attack.

Documenting these indicators enables security analysts to quickly identify similar attacks, validate future detections, and support incident response activities using standardized evidence.
