# Implementation Status

# Overview

This document summarizes the implementation status of the security controls deployed within the Home SOC Laboratory following the Windows Remote Desktop (RDP) Brute Force Investigation.

The purpose of this document is to distinguish between:

- Security controls that are already implemented.
- Controls currently under development.
- Planned future improvements.

This provides a clear overview of the laboratory's current security posture.

---

# Laboratory Summary

| Property | Value |
|----------|-------|
| Laboratory | Home SOC Lab |
| Investigation | Windows RDP Brute Force |
| Status | Completed |
| Wazuh Version | 4.14 |
| Monitoring Platform | Wazuh SIEM |
| Environment | Proxmox Virtualization |

---

# Current Security Controls

| Security Control | Status |
|------------------|--------|
| Windows Event Monitoring | ✅ Implemented |
| Wazuh Agent | ✅ Implemented |
| Wazuh Manager | ✅ Implemented |
| Wazuh Dashboard | ✅ Implemented |
| Windows Security Log Collection | ✅ Implemented |
| Event Correlation | ✅ Implemented |
| MITRE ATT&CK Mapping | ✅ Implemented |
| Active Directory Monitoring | ✅ Implemented |
| Sysmon Deployment | ✅ Implemented |
| Remote Desktop Monitoring | ✅ Implemented |

---

# Windows Security Configuration

## Windows Security Auditing

Status

✅ Implemented

Description

Windows successfully records both successful and failed authentication attempts.

Evidence

- Event ID 4624
- Event ID 4625

---

## Audit Policy

Status

✅ Implemented

Description

Windows Logon auditing is configured for:

- Success
- Failure

This allows the detection of successful and failed authentication attempts.

---

## Remote Desktop Services

Status

✅ Implemented

Description

Remote Desktop is enabled to allow realistic attack simulations inside the laboratory.

The service is monitored by Wazuh.

---

# Wazuh Components

## Wazuh Agent

Status

✅ Implemented

Responsibilities

- Collect Windows Security Events
- Collect Sysmon Events
- Forward events to the Wazuh Manager

Validation

Successfully transmitting events.

---

## Wazuh Manager

Status

✅ Implemented

Responsibilities

- Receive events
- Decode logs
- Apply detection rules
- Correlate alerts
- Store security events

Validation

Successfully processed Windows Event ID 4625.

---

## Event Storage

Status

✅ Implemented

Description

Raw security events are successfully stored in:

archives.json

Validation

The investigation confirmed all fifteen failed authentication events were present.

---

## Detection Rules

Status

✅ Implemented

Validated Rules

- Rule 60122
- Rule 60204

Validation

Both rules successfully detected and correlated the simulated brute force attack.

---

## MITRE ATT&CK Mapping

Status

✅ Implemented

Technique

T1110 – Brute Force

Sub-technique

T1110.001 – Password Guessing

Validation

The attack was automatically mapped by Wazuh.

---

# Sysmon

Status

✅ Implemented

Description

Microsoft Sysmon has been deployed on the Windows 11 workstation.

Purpose

- Process monitoring
- Network monitoring
- Registry monitoring
- File monitoring

Current Status

Operational.

---

# Active Directory

Status

✅ Implemented

Environment

Windows Server 2022

Features

- Active Directory Domain Services
- Domain Authentication
- Windows Accounts
- Domain Controller

Purpose

Provide realistic enterprise authentication.

---

# Laboratory Validation

The following components were successfully validated during the investigation.

| Validation | Status |
|------------|--------|
| Windows Event ID 4625 Generated | ✅ |
| Wazuh Agent Received Events | ✅ |
| archives.json Stored Events | ✅ |
| Rule 60122 Triggered | ✅ |
| Rule 60204 Triggered | ✅ |
| MITRE ATT&CK Mapping | ✅ |
| Dashboard Alert Display | ✅ |

---

# Planned Improvements

The following security enhancements are planned for future laboratory investigations.

| Improvement | Status |
|-------------|--------|
| Multi-Factor Authentication (MFA) | 🔄 Planned |
| Account Lockout Policy | 🔄 Planned |
| Suricata IDS | 🔄 Planned |
| Zeek Network Monitoring | 🔄 Planned |
| TheHive Integration | 🔄 Planned |
| Shuffle SOAR | 🔄 Planned |
| Threat Intelligence Integration | 🔄 Planned |
| Sigma Rule Testing | 🔄 Planned |
| YARA Rule Validation | 🔄 Planned |

---

# Security Maturity

| Area | Status |
|------|--------|
| Windows Monitoring | 🟢 Operational |
| Wazuh SIEM | 🟢 Operational |
| Active Directory | 🟢 Operational |
| Sysmon | 🟢 Operational |
| Incident Investigation | 🟢 Operational |
| Threat Hunting | 🟡 In Development |
| Network Detection | 🟡 In Development |
| Incident Response Automation | ⚪ Planned |
| Threat Intelligence | ⚪ Planned |

Legend

- 🟢 Operational
- 🟡 In Development
- 🔄 Planned
- ⚪ Future

---

# Compliance with Investigation Objectives

| Objective | Status |
|-----------|--------|
| Simulate an RDP brute force attack | ✅ Completed |
| Generate Windows Event ID 4625 | ✅ Completed |
| Validate Wazuh event collection | ✅ Completed |
| Validate event correlation | ✅ Completed |
| Verify MITRE ATT&CK mapping | ✅ Completed |
| Produce a professional investigation report | ✅ Completed |
| Preserve forensic evidence | ✅ Completed |

---

# Overall Assessment

The current Home SOC Laboratory successfully reproduces a realistic enterprise monitoring environment for Windows authentication investigations.

The implemented security controls allow the complete lifecycle of a brute force attack to be observed, from the initial failed authentication attempts to the final correlated alert generated by Wazuh.

The environment is considered stable and ready for more advanced investigations involving persistence, privilege escalation, Active Directory attacks, PowerShell monitoring, Sysmon analysis, and threat hunting scenarios.

---

# Conclusion

The implementation status confirms that the laboratory has achieved the primary objectives of this investigation.

Core monitoring, event collection, correlation, and analysis capabilities are fully operational.

Future laboratories will build upon this foundation by introducing additional detection technologies, advanced attack scenarios, and automated incident response capabilities.
