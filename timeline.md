# Attack Timeline

## Incident

Windows Remote Desktop Brute Force Investigation

---

# Timeline Overview

The following timeline reconstructs the brute force attack from the initial authentication attempt until the final Wazuh correlation alert.

All timestamps are based on evidence collected from Windows Security Logs and Wazuh.

---

# Timeline

| Time (EDT) | Event | Evidence |
|------------|-------|----------|
| 20:48:08 | First failed RDP authentication attempt | Windows Event ID 4625 |
| 20:48:09 | Failed authentication | Windows Event ID 4625 |
| 20:48:11 | Failed authentication | Windows Event ID 4625 |
| 20:48:13 | Failed authentication | Windows Event ID 4625 |
| 20:48:15 | Failed authentication | Windows Event ID 4625 |
| 20:48:17 | Failed authentication | Windows Event ID 4625 |
| 20:48:19 | Failed authentication | Windows Event ID 4625 |
| 20:48:21 | Failed authentication | Windows Event ID 4625 |
| 20:48:23 | Failed authentication | Windows Event ID 4625 |
| 20:48:24 | Wazuh Rule 60122 generated | Individual detection |
| 20:48:25 | Additional failed logons detected | Rule 60122 |
| 20:48:27 | Wazuh correlation engine triggered | Rule 60204 |
| 20:48:28 | Incident classified as Brute Force | MITRE T1110 |
| 20:48:40 | Last failed authentication recorded | Windows Event ID 4625 |

---

# Investigation Flow

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

# Event Summary

## Total Failed Logons

15

---

## Windows Security Events

15 Event ID 4625

---

## Individual Wazuh Alerts

Rule 60122

---

## Correlation Alerts

Rule 60204

---

## MITRE ATT&CK

Technique:

T1110

Tactic:

Credential Access

---

# Analyst Observations

The attack was completed within a very short period of time.

Because multiple authentication failures occurred in rapid succession, Wazuh correlated the events into a single brute force incident instead of generating multiple high-severity alerts.

This correlation significantly reduces alert fatigue while preserving all forensic evidence.

---

# Timeline Validation

The investigation validated the following sequence:

✓ Attack generated

↓

✓ Windows Security Event created

↓

✓ Event collected by Wazuh Agent

↓

✓ Event stored in archives.json

↓

✓ Rule 60122 triggered

↓

✓ Rule 60204 triggered

↓

✓ MITRE ATT&CK mapping completed

↓

✓ Incident confirmed

---

# Conclusion

The reconstructed timeline demonstrates the complete lifecycle of a Windows brute force attack.

Every stage of the attack was successfully validated using Windows Security Logs, Wazuh event collection, correlation rules, and MITRE ATT&CK mapping.

This timeline provides a clear forensic reconstruction of the incident and can be used as supporting evidence during a professional SOC investigation.
