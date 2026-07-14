# SOC Laboratory Roadmap

# Overview

This roadmap outlines the planned progression of my Home SOC Laboratory.

The objective is to gradually build practical experience in Security Operations Center (SOC) investigations by simulating realistic cyber attacks, collecting forensic evidence, analyzing security events, and documenting professional incident reports.

Each laboratory focuses on a different attack technique, detection method, or investigation workflow.

---

# Current Progress

| Lab | Investigation | Status |
|------|---------------|--------|
| SOC-Lab-001 | Windows RDP Brute Force Investigation | ✅ Completed |

---

# Planned Investigations

## SOC-Lab-002

### Windows PowerShell Execution Detection

Status

🔄 Planned

Objectives

- Detect PowerShell execution
- Investigate Event ID 4104
- Analyze PowerShell Operational Logs
- Correlate Wazuh alerts
- Map MITRE ATT&CK techniques

Expected MITRE

- T1059.001 – PowerShell

---

## SOC-Lab-003

### Windows Process Creation Investigation

Status

🔄 Planned

Objectives

- Detect suspicious process execution
- Analyze Sysmon Event ID 1
- Investigate Process Creation
- Correlate Windows Security Event 4688

Expected MITRE

- T1059
- T1204

---

## SOC-Lab-004

### Scheduled Task Persistence

Status

🔄 Planned

Objectives

- Detect malicious Scheduled Tasks
- Analyze Windows Task Scheduler logs
- Investigate persistence mechanisms

Expected MITRE

- T1053.005

---

## SOC-Lab-005

### Windows Service Creation

Status

🔄 Planned

Objectives

- Detect malicious services
- Analyze Service Control Manager logs
- Investigate persistence through services

Expected MITRE

- T1543.003

---

## SOC-Lab-006

### Registry Modification Detection

Status

🔄 Planned

Objectives

- Detect Registry changes
- Analyze Sysmon Registry Events
- Investigate persistence techniques

Expected MITRE

- T1112

---

## SOC-Lab-007

### File Integrity Monitoring Investigation

Status

🔄 Planned

Objectives

- Monitor critical files
- Detect unauthorized modifications
- Validate Wazuh File Integrity Monitoring

Expected MITRE

- T1070
- T1565

---

## SOC-Lab-008

### Local User Account Creation

Status

🔄 Planned

Objectives

- Detect unauthorized user creation
- Investigate Windows Account Management Events
- Analyze privilege escalation attempts

Expected MITRE

- T1136

---

## SOC-Lab-009

### Active Directory Investigation

Status

🔄 Planned

Objectives

- Investigate authentication events
- Analyze Kerberos activity
- Detect suspicious domain activity

Expected MITRE

- T1558
- T1550

---

## SOC-Lab-010

### Lateral Movement Investigation

Status

🔄 Planned

Objectives

- Investigate remote administration activity
- Analyze authentication across multiple hosts
- Detect lateral movement techniques

Expected MITRE

- T1021

---

## SOC-Lab-011

### Sysmon Threat Hunting

Status

🔄 Planned

Objectives

- Investigate Sysmon telemetry
- Perform threat hunting
- Correlate multiple event sources

Expected MITRE

Multiple Techniques

---

## SOC-Lab-012

### Ransomware Detection Simulation

Status

🔄 Planned

Objectives

- Detect abnormal file modifications
- Analyze encryption behavior
- Investigate process activity
- Validate Wazuh detection capabilities

Expected MITRE

- T1486

---

# Long-Term Objectives

This laboratory will continue expanding with investigations covering:

- Active Directory attacks
- Credential dumping
- Windows Defender events
- Network monitoring with Suricata
- Network analysis with Zeek
- Sigma Rule validation
- YARA detection
- Threat Hunting scenarios
- Malware behavior analysis
- Incident response workflows
- Digital forensics
- SOAR automation
- Case management with TheHive
- Integration with Shuffle
- Threat Intelligence enrichment

---

# Skills Being Developed

Each completed laboratory strengthens practical experience in:

- Security Operations Center (SOC)
- Incident Investigation
- Digital Forensics
- Windows Event Analysis
- Active Directory Security
- Wazuh SIEM
- Sysmon
- MITRE ATT&CK
- Threat Hunting
- Incident Documentation
- Security Monitoring
- Detection Engineering
- Log Analysis
- Event Correlation

---

# Progress Tracker

| Category | Progress |
|----------|----------|
| Windows Security | 🟢 In Progress |
| Wazuh SIEM | 🟢 In Progress |
| Active Directory | 🟡 Planned |
| Sysmon | 🟡 Planned |
| Threat Hunting | 🟡 Planned |
| Digital Forensics | 🟡 Planned |
| Incident Response | 🟡 Planned |
| Network Detection | 🟡 Planned |
| SOAR Automation | ⚪ Future |
| Threat Intelligence | ⚪ Future |

Legend

- ✅ Completed
- 🟢 In Progress
- 🟡 Planned
- ⚪ Future

---

# Portfolio Vision

The goal of this project is to build a complete portfolio of hands-on SOC investigations that demonstrate practical cybersecurity skills through realistic attack simulations, evidence collection, technical analysis, and professional documentation.

Rather than focusing only on theoretical knowledge, every laboratory is designed to reproduce the workflow of a Security Operations Center analyst, from initial detection to final incident reporting.

This roadmap will continue evolving as new investigations and technologies are added to the Home SOC Laboratory.
