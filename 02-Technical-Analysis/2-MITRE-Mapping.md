# MITRE ATT&CK Mapping

# Overview

This document explains why the simulated attack was mapped to **MITRE ATT&CK Technique T1110 – Brute Force** and how Wazuh identified this behavior during the investigation.

Rather than simply displaying a MITRE identifier, this document explains the reasoning behind the mapping and its importance during Security Operations Center (SOC) investigations.

---

# What is MITRE ATT&CK?

MITRE ATT&CK (Adversarial Tactics, Techniques, and Common Knowledge) is a globally recognized knowledge base that documents the tactics and techniques used by real-world attackers.

It provides a standardized framework that allows security analysts to classify malicious activities consistently across different security platforms.

Instead of describing an attack using vendor-specific terminology, SOC analysts use MITRE ATT&CK techniques to communicate the attacker's behavior.

---

# Technique Identified

| Property | Value |
|----------|-------|
| Framework | MITRE ATT&CK |
| Technique ID | T1110 |
| Technique Name | Brute Force |
| Tactic | Credential Access |

---

# Why Was T1110 Selected?

During the laboratory exercise, multiple Remote Desktop authentication attempts were performed using an incorrect password.

Each authentication failure generated a Windows Security Event ID 4625.

The Wazuh detection engine recognized that multiple failed authentication attempts occurred within a short period of time.

After correlating these events, Wazuh classified the activity as:

**MITRE ATT&CK T1110 – Brute Force**

This mapping accurately represents the attacker's attempt to gain unauthorized access by repeatedly guessing credentials.

---

# Attack Sequence

```
Attacker

↓

Remote Desktop (RDP)

↓

Invalid Password

↓

Windows Authentication Failure

↓

Event ID 4625

↓

Rule 60122

↓

Rule 60204

↓

MITRE ATT&CK T1110
```

---

# Detection Evidence

The investigation produced the following evidence.

| Evidence | Result |
|----------|--------|
| Authentication Attempts | 15 |
| Windows Event ID | 4625 |
| Detection Rule | 60122 |
| Correlation Rule | 60204 |
| MITRE Technique | T1110 |

---

# Understanding Technique T1110

Brute Force attacks attempt to obtain valid credentials by repeatedly submitting authentication requests.

The attacker continues until:

- the correct password is discovered,
- the account is locked,
- or the attack is stopped.

Because authentication systems generate multiple failed logons, this technique produces characteristic security events that can be monitored by SIEM platforms.

---

# Common Variants of T1110

MITRE ATT&CK identifies several forms of brute force attacks.

## T1110.001 – Password Guessing

The attacker repeatedly guesses the password of a single account.

Example:

Administrator

↓

Password1

↓

Password123

↓

Admin123

↓

Welcome1

This laboratory follows this scenario.

---

## T1110.002 – Password Cracking

The attacker attempts to recover passwords from password hashes using offline cracking tools.

Examples:

- Hashcat
- John the Ripper

No authentication attempts are sent to the target system.

---

## T1110.003 – Password Spraying

Instead of trying many passwords against one account, the attacker tries one common password against many different accounts.

Example:

Password:

Spring2026!

Accounts:

Administrator

John

Mary

David

This technique reduces the risk of account lockout.

---

## T1110.004 – Credential Stuffing

Previously leaked usernames and passwords are automatically tested against another service.

The attacker relies on users reusing passwords across multiple systems.

---

# Why This Laboratory Matches T1110.001

The investigation confirmed:

- one target account,
- multiple authentication attempts,
- repeated incorrect passwords,
- repeated Windows Event ID 4625.

Therefore the attack matches:

**T1110.001 – Password Guessing**

while remaining part of the broader technique:

**T1110 – Brute Force**

---

# Why Wazuh Detected the Attack

Windows generated:

Event ID 4625

↓

The Wazuh Agent collected the event.

↓

The Wazuh Manager decoded the event.

↓

Rule 60122 identified each failed authentication.

↓

Rule 60204 correlated multiple failures.

↓

MITRE ATT&CK T1110 was assigned.

---

# Analyst Investigation

When a SOC analyst receives a T1110 alert, the investigation normally focuses on:

- Source IP address
- Source Host
- Target Host
- Target User
- Number of failed attempts
- Authentication protocol
- Time window
- Additional suspicious activity
- Successful logons after the failures
- Lateral movement attempts

These elements help determine whether the attack was successful or prevented.

---

# Defensive Recommendations

Organizations can reduce the risk of brute force attacks by implementing:

- Multi-Factor Authentication (MFA)
- Account Lockout Policies
- Strong Password Policies
- Remote Desktop Restrictions
- Network Level Authentication (NLA)
- IP Allow Lists
- Continuous Security Monitoring
- SIEM Alert Correlation
- Threat Hunting

---

# Lessons Learned

This investigation demonstrated that MITRE ATT&CK is much more than a simple label displayed inside Wazuh.

It provides valuable context that explains:

- the attacker's objective,
- the attack technique,
- the affected security domain,
- the expected behavior,
- and appropriate defensive strategies.

Understanding MITRE ATT&CK allows SOC analysts to investigate incidents more efficiently and communicate findings using a standardized language understood across the cybersecurity industry.

---

# Conclusion

The simulated Windows Remote Desktop brute force attack was correctly mapped to **MITRE ATT&CK Technique T1110**.

The investigation confirmed that repeated authentication failures generated Windows Event ID 4625, triggered Wazuh Rule 60122, activated the Rule 60204 correlation engine, and resulted in a high-severity brute force alert.

This mapping demonstrates how Wazuh integrates Windows Security Logs with the MITRE ATT&CK framework to provide contextualized threat detection for Security Operations Center investigations.
