# Windows Brute Force Investigation Report

## Incident Information

| Item | Value |
|------|-------|
| Incident ID | SOC-LAB-001 |
| Incident Name | Windows RDP Brute Force Investigation |
| Analyst | Gouled Houssein |
| Detection Platform | Wazuh 4.14 |
| Environment | Home SOC Laboratory |
| MITRE ATT&CK | T1110 – Brute Force |
| Severity | High (Level 10) |
| Status | Closed |

---

# 1. Incident Overview

This investigation documents the complete lifecycle of a simulated Windows Remote Desktop brute force attack detected by Wazuh.

Unlike a traditional laboratory where the objective is only to trigger an alert, this investigation focuses on validating every component involved in the detection pipeline.

The objective was to answer the following questions:

- Was the attack successfully generated?
- Did Windows record the attack?
- Did the Wazuh Agent collect the events?
- Did the Wazuh Manager receive the events?
- Which detection rules were triggered?
- Why did Wazuh classify the activity as MITRE ATT&CK T1110?

---

# 2. Lab Environment

## Hypervisor

Proxmox VE

## SIEM

Wazuh 4.14

## Manager

Ubuntu Server

## Domain Controller

Windows Server 2022

## Target

Windows 11 Enterprise

## Monitoring

Sysmon

## Authentication Protocol

Remote Desktop Protocol (RDP)

---

# 3. Attack Scenario

A brute force attack was simulated using Microsoft Remote Desktop.

The attacker repeatedly attempted to authenticate to the Windows 11 workstation using an invalid password.

The attack originated from the Domain Controller.

### Source Host

DC01-AD

### Source IP

192.168.10.10

### Target Host

WIN11-Lab

### Target User

Administrator

### Number of Attempts

15

---

# 4. Initial Investigation

Immediately after generating the attack, the Wazuh Dashboard was inspected.

The initial search focused on Event ID 4625.

No matching events were immediately visible.

At this stage it appeared that Wazuh had failed to detect the attack.

Instead of assuming that detection had failed, the investigation continued by validating every component individually.

---

# 5. Windows Investigation

The Windows Event Viewer was examined.

Navigation:

Windows Logs

↓

Security

↓

Event ID 4625

Result:

Windows successfully recorded all failed authentication attempts.

A total of fifteen Event ID 4625 entries were identified.

This proved that Windows correctly detected every failed login attempt.

---

# 6. Wazuh Agent Verification

The Wazuh Agent status was verified.

The investigation confirmed:

- Agent connected
- Agent operational
- Sysmon operational
- Windows events successfully forwarded

Additional Windows events such as Event ID 7040 and Event ID 4616 were successfully received.

This confirmed that communication between Windows and the Wazuh Manager was functioning correctly.

---

# 7. Windows Audit Policy Verification

The Windows audit policy was inspected.

The "Logon" category was configured to audit both:

- Success
- Failure

Therefore Windows was expected to generate Event ID 4625 for every failed authentication attempt.

This configuration was verified successfully.

---

# 8. Wazuh Manager Investigation

The investigation then moved from the Dashboard to the Ubuntu Wazuh Manager.

The file inspected was:

/var/ossec/logs/archives/archives.json

A search was performed for Event ID 4625.

The search confirmed that every authentication failure had been received by the manager.

The events were then filtered by timestamp.

Exactly fifteen Event ID 4625 entries were found for the attack timeframe.

This demonstrated that the Wazuh Agent successfully forwarded every Windows security event.

---

# 9. Detection Rules Investigation

After confirming that the events reached the manager, the investigation focused on the Wazuh detection engine.

Two detection rules were identified.

## Rule 60122

Description:

Logon Failure – Unknown user or bad password

Purpose:

Detect every failed authentication attempt individually.

Each Windows Event ID 4625 generated one Rule 60122 alert.

---

## Rule 60204

Description:

Multiple Windows Logon Failures

Purpose:

Correlate multiple failed authentication attempts into a single security incident.

This rule generated one Level 10 alert.

The rule automatically mapped the activity to MITRE ATT&CK Technique T1110.

---

# 10. Understanding Event Correlation

The investigation demonstrated the difference between Windows events and Wazuh incidents.

Windows generated:

15 Event ID 4625

↓

Wazuh generated:

Multiple Rule 60122 alerts

↓

Correlation Engine

↓

One Rule 60204 alert

This behavior prevents analysts from receiving hundreds of identical alerts during a brute force attack.

Instead, Wazuh groups related events into a single security incident.

---

# 11. MITRE ATT&CK Analysis

Technique

T1110

Name

Brute Force

Tactic

Credential Access

Reason

The attacker repeatedly attempted authentication using an invalid password.

The frequency of failed logon events matched the detection logic implemented by Rule 60204.

---

# 12. Indicators of Compromise

| Indicator | Value |
|------------|-------|
| Attack Type | Brute Force |
| Protocol | RDP |
| Windows Event ID | 4625 |
| Detection Rule | 60122 |
| Correlation Rule | 60204 |
| Source IP | 192.168.10.10 |
| Source Host | DC01-AD |
| Target Host | WIN11-Lab |
| Target User | Administrator |

---

# 13. Analyst Assessment

The investigation confirms that the brute force attack was successfully detected.

Windows generated the expected Event ID 4625 entries.

The Wazuh Agent successfully collected these events.

The Wazuh Manager successfully received the events.

The Wazuh correlation engine correctly generated Rule 60204.

The incident was accurately mapped to MITRE ATT&CK Technique T1110.

No unauthorized access was achieved.

The activity was classified as a controlled laboratory exercise.

---

# 14. Lessons Learned

This investigation demonstrated the importance of validating every stage of the detection pipeline.

Initially, the absence of visible events in the Dashboard suggested that the attack had not been detected.

However, further investigation proved that the events were present in Windows, successfully collected by the Wazuh Agent, received by the Wazuh Manager, and processed by the detection engine.

This reinforces an important SOC principle:

**Never assume detection has failed before validating every layer of the monitoring infrastructure.**

---

# 15. Conclusion

This investigation successfully reproduced a realistic Windows brute force attack within a controlled SOC laboratory.

Every phase of the detection pipeline was validated, including Windows logging, Wazuh event collection, alert generation, rule correlation, and MITRE ATT&CK mapping.

The exercise provided practical experience in professional SOC investigation techniques and demonstrated the complete workflow used by security analysts to validate authentication-based attacks.
