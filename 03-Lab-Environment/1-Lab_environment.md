# Lab Environment

# Overview

This laboratory was designed to simulate a real-world Security Operations Center (SOC) environment for detecting, investigating, and documenting Windows authentication attacks using Wazuh.

The environment consists of a Proxmox virtualization platform hosting multiple virtual machines that emulate a small enterprise Active Directory network.

---

# Objectives

The laboratory was built to:

- Learn Security Operations Center (SOC) workflows
- Investigate Windows security events
- Validate Wazuh detections
- Understand MITRE ATT&CK techniques
- Produce professional incident investigation reports
- Build a practical cybersecurity portfolio

---

# Virtualization Platform

| Component | Value |
|------------|--------|
| Hypervisor | Proxmox VE |
| Virtualization | KVM |
| Host OS | Debian / Proxmox VE |

---

# Virtual Machines

## 1. Wazuh Manager

| Property | Value |
|----------|-------|
| Operating System | Ubuntu Server |
| Role | SIEM Platform |
| Components | Wazuh Manager |
| | Wazuh Indexer |
| | Wazuh Dashboard |

### Responsibilities

- Collect security events
- Store security logs
- Correlate events
- Generate alerts
- Map MITRE ATT&CK techniques

---

## 2. Domain Controller

| Property | Value |
|----------|-------|
| Operating System | Windows Server 2022 |
| Hostname | DC01-AD |

### Installed Roles

- Active Directory Domain Services
- DNS
- Remote Desktop Client

### Responsibilities

- Domain authentication
- User management
- Attack simulation

---

## 3. Target Workstation

| Property | Value |
|----------|-------|
| Operating System | Windows 11 Enterprise |
| Hostname | WIN11-Lab |

### Installed Software

- Wazuh Agent
- Sysmon

### Responsibilities

- Generate Windows Events
- Send security logs to Wazuh
- Receive simulated attacks

---

# Network

The laboratory uses an isolated private network.

| Device | IP Address |
|----------|------------|
| Wazuh Manager | 192.168.10.x |
| DC01-AD | 192.168.10.10 |
| WIN11-Lab | 192.168.10.20 |

*(Replace the Wazuh Manager IP with your actual address if you wish to publish it. Otherwise, mask it.)*

---

# Monitoring Components

## Windows Security Logs

Collected Events include:

- Authentication
- Logon
- Logoff
- Account Management
- Group Membership
- Policy Changes

---

## Sysmon

Sysmon extends Windows logging by recording:

- Process Creation
- Network Connections
- Driver Loading
- Registry Changes
- File Creation
- Image Loading

---

## Wazuh Agent

Responsibilities:

- Monitor Windows Event Logs
- Monitor Sysmon Logs
- Forward events to Wazuh Manager

---

## Wazuh Manager

Responsibilities:

- Receive events
- Decode logs
- Apply detection rules
- Correlate alerts
- Store events
- Display investigations

---

# Communication Flow

```
Windows 11

↓

Windows Security Logs

↓

Sysmon

↓

Wazuh Agent

↓

Ubuntu Wazuh Manager

↓

archives.json

↓

Detection Rules

↓

Correlation Rules

↓

Dashboard

↓

SOC Analyst
```

---

# Technologies Used

- Proxmox VE
- Ubuntu Server
- Windows Server 2022
- Windows 11 Enterprise
- Wazuh 4.14
- Sysmon
- Microsoft Remote Desktop
- Active Directory
- PowerShell
- Event Viewer

---

# Security Monitoring

The following log sources were monitored:

- Windows Security
- Windows System
- Windows Application
- Microsoft Sysmon

---

# Attack Scenario Supported

This environment supports investigations for:

- Brute Force (T1110)
- PowerShell Execution
- Command Prompt Execution
- Scheduled Tasks
- Windows Services
- Registry Modification
- File Integrity Monitoring
- User Creation
- Administrator Group Changes
- USB Activity

---

# Skills Demonstrated

This laboratory demonstrates practical experience with:

- Security Operations Center (SOC)
- Windows Security Monitoring
- Wazuh SIEM
- Windows Event Logs
- Active Directory
- Incident Investigation
- Threat Detection
- Digital Forensics
- MITRE ATT&CK
- Security Monitoring

---

# Conclusion

This laboratory provides a realistic enterprise-like environment for learning Windows threat detection and SOC investigations.

The combination of Active Directory, Windows 11, Sysmon, and Wazuh enables realistic attack simulations and professional incident investigations comparable to those performed in production Security Operations Centers.
