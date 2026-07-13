# Executive Summary

## Incident Title

Windows Remote Desktop Brute Force Investigation

---

## Incident Identifier

SOC-LAB-001

---

## Incident Date

July 12, 2026

---

## Severity

High (Level 10)

---

## MITRE ATT&CK

**Technique:** T1110 – Brute Force

**Tactic:** Credential Access

---

# Executive Overview

This laboratory simulates a Windows Remote Desktop Protocol (RDP) brute force attack against a Windows 11 workstation monitored by Wazuh.

The primary objective was to reproduce a realistic SOC investigation by following the complete detection pipeline, from attack generation to incident validation.

Instead of simply verifying that an alert was generated, the investigation focused on understanding every stage of the detection process, including Windows Security Logs, Wazuh event collection, alert generation, rule correlation, and MITRE ATT&CK mapping.

---

# Incident Description

A series of failed Remote Desktop authentication attempts were intentionally generated from the Domain Controller (DC01-AD) toward the Windows 11 workstation (WIN11-Lab).

The attack targeted the local **Administrator** account using an incorrect password.

A total of **15 authentication failures** were generated during the simulation.

Windows recorded every failed authentication attempt as **Security Event ID 4625**.

The Wazuh Agent collected these events and forwarded them to the Wazuh Manager.

The manager generated multiple **Rule 60122** alerts before correlating the activity into a single **Rule 60204** brute force incident.

The incident was automatically mapped to **MITRE ATT&CK Technique T1110 (Brute Force).**

---

# Investigation Scope

The investigation covered the following components:

- Windows Security Event Logs
- Windows Event Viewer
- Wazuh Agent
- Wazuh Manager
- archives.json
- Detection Rules
- Correlation Rules
- MITRE ATT&CK Mapping

---

# Key Findings

The investigation confirmed that:

- The brute force attack successfully generated Windows Security Event ID 4625.
- Fifteen failed authentication attempts were recorded.
- All authentication failures were received by the Wazuh Manager.
- Individual failed logons generated Rule 60122 alerts.
- Wazuh correlated these events into a single Rule 60204 incident.
- The attack was correctly classified as MITRE ATT&CK Technique T1110.

---

# Evidence Summary

| Evidence | Result |
|-----------|--------|
| Attack Type | Windows RDP Brute Force |
| Source Host | DC01-AD |
| Target Host | WIN11-Lab |
| Target Account | Administrator |
| Failed Attempts | 15 |
| Windows Event ID | 4625 |
| Detection Rule | 60122 |
| Correlation Rule | 60204 |
| Severity | Level 10 |
| MITRE Technique | T1110 |

---

# Business Impact

This investigation was performed in a controlled laboratory environment.

No production systems were affected.

No unauthorized access was obtained.

The exercise successfully demonstrated the complete detection and investigation workflow used by a Security Operations Center (SOC).

---

# Analyst Assessment

The incident was classified as a **simulated brute force attack** performed for defensive training purposes.

All monitoring components operated as expected.

Windows generated the required security events.

The Wazuh Agent successfully collected the events.

The Wazuh Manager correctly processed and correlated the events into a high-severity brute force alert.

The investigation confirms that the laboratory is capable of detecting and investigating Windows authentication attacks in a manner comparable to a production SOC environment.

---

# Executive Conclusion

This laboratory demonstrates the complete lifecycle of a Windows brute force investigation.

Beginning with attack simulation and ending with incident validation, every stage of the SOC investigation process was successfully reproduced.

The exercise validates the effectiveness of Windows Security Logging, Wazuh event collection, rule correlation, and MITRE ATT&CK mapping while providing practical experience in professional incident investigation.
