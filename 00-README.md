# 🛡️ SOC Lab 001 – Windows Brute Force Investigation with Wazuh (MITRE ATT&CK T1110)

![Wazuh](https://img.shields.io/badge/Wazuh-4.14-blue)
![Windows](https://img.shields.io/badge/Windows-11%20Enterprise-0078D6)
![Ubuntu](https://img.shields.io/badge/Ubuntu-24.04-E95420)
![MITRE ATT&CK](https://img.shields.io/badge/MITRE-T1110-red)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

---

# 📖 Project Overview

This project documents a complete Security Operations Center (SOC) investigation of a simulated Remote Desktop Protocol (RDP) brute force attack in a Windows Active Directory lab monitored by Wazuh.

Unlike a simple alert demonstration, this investigation follows the complete incident response workflow performed by a SOC Analyst:

- Attack simulation
- Evidence collection
- Windows Event Log analysis
- Wazuh investigation
- Alert correlation
- MITRE ATT&CK mapping
- Incident conclusion
- Security recommendations

The objective was to understand not only **how Wazuh detects a brute force attack**, but **why** the alert is generated and how an analyst validates every stage of the detection pipeline.

---

# 🎯 Objectives

The objectives of this laboratory were to:

- Simulate a Windows RDP brute force attack
- Generate multiple failed authentication attempts
- Investigate Windows Security Events
- Validate event collection by the Wazuh Agent
- Verify event reception by the Wazuh Manager
- Understand Wazuh correlation rules
- Investigate Rule 60122 and Rule 60204
- Map the attack to MITRE ATT&CK
- Produce a complete SOC investigation report

---

# 🏗️ Lab Environment

| Component | Technology |
|------------|------------|
| Hypervisor | Proxmox VE |
| SIEM | Wazuh 4.14 |
| Manager | Ubuntu Server 24.04 |
| Domain Controller | Windows Server 2022 |
| Target Machine | Windows 11 Enterprise |
| Monitoring | Sysmon |
| Protocol | Remote Desktop (RDP) |

---

# 🖥️ Lab Architecture

> *(Insert Architecture.png here)*

```
Attacker (DC01-AD)
        │
        ▼
Remote Desktop (RDP)
        │
        ▼
WIN11-Lab
        │
Windows Security Logs
        │
        ▼
Wazuh Agent
        │
        ▼
Ubuntu Wazuh Manager
        │
        ▼
archives.json
        │
        ▼
Detection Rules
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

# ⚔️ Attack Scenario

A brute force attack was simulated by repeatedly attempting Remote Desktop authentication with an incorrect password.

### Source Host

DC01-AD

### Target Host

WIN11-Lab

### Target User

Administrator

### Authentication Method

Remote Desktop Protocol (RDP)

### Failed Attempts

15

---

# 🔍 Investigation Workflow

The investigation followed the same methodology used by professional SOC analysts.

## Step 1

Generate the attack.

## Step 2

Verify Windows Event Viewer.

## Step 3

Confirm Event ID 4625.

## Step 4

Verify Wazuh Agent collection.

## Step 5

Verify archives.json.

## Step 6

Investigate Rule 60122.

## Step 7

Investigate Rule 60204.

## Step 8

Map the attack to MITRE ATT&CK.

## Step 9

Write the incident report.

---

# 🚨 Detection Results

| Evidence | Result |
|-----------|---------|
| Attack Type | Brute Force |
| Protocol | RDP |
| Failed Attempts | 15 |
| Windows Event ID | 4625 |
| Wazuh Rule | 60122 |
| Correlation Rule | 60204 |
| Severity | Level 10 |
| MITRE ATT&CK | T1110 |
| MITRE Tactic | Credential Access |

---

# 📊 Investigation Timeline

| Step | Evidence |
|--------|-----------|
| Attack generated | 15 invalid RDP logins |
| Windows detected | Event ID 4625 |
| Wazuh received | archives.json |
| Individual alerts | Rule 60122 |
| Correlation alert | Rule 60204 |
| Incident confirmed | Brute Force |

---

# 🛡️ MITRE ATT&CK Mapping

| Framework | Value |
|------------|--------|
| Technique | T1110 |
| Name | Brute Force |
| Tactic | Credential Access |

---

# 🧠 Skills Demonstrated

- Security Operations Center (SOC)
- Windows Security Log Analysis
- Windows Event ID 4625 Investigation
- Wazuh SIEM
- Wazuh Correlation Rules
- Sysmon
- Incident Investigation
- MITRE ATT&CK Mapping
- Digital Forensics
- Threat Detection
- Incident Analysis
- Security Monitoring

---

# 📂 Repository Structure

```
SOC-Lab-001-Windows-Brute-Force-Investigation/

README.md

executive_summary.md

investigation_report.md

timeline.md

lab_environment.md

detection_rules.md

mitre_mapping.md

iocs.md

recommendations.md

lessons_learned.md

screenshots_guide.md

LICENSE

screenshots/

diagrams/
```

---

# 📚 Lessons Learned

This investigation demonstrated the complete detection pipeline used by Wazuh.

The investigation highlighted the difference between:

- Windows Events
- Wazuh Archives
- Individual Detection Rules
- Correlation Rules
- MITRE ATT&CK Mapping

It also demonstrated how a SOC analyst validates evidence before concluding that a brute force attack occurred.

---

# 📌 Conclusion

The simulated brute force attack successfully generated Windows Security Event ID 4625 entries.

The Wazuh Agent collected these events and forwarded them to the Wazuh Manager.

The manager stored the events in **archives.json**, generated multiple **Rule 60122** alerts, and finally correlated the activity into a single **Rule 60204** incident mapped to **MITRE ATT&CK T1110 (Brute Force)**.

This project demonstrates a complete SOC investigation workflow from attack generation to incident validation.
