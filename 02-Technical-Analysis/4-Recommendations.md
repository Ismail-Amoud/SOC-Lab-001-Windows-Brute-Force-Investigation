# Security Recommendations

# Overview

This document provides security recommendations based on the findings of the Windows Remote Desktop (RDP) brute force investigation.

Although the attack was intentionally performed in a controlled laboratory environment, the recommendations below reflect industry best practices for protecting production environments against credential-based attacks.

---

# Investigation Summary

The investigation confirmed that:

- Fifteen failed Remote Desktop authentication attempts were generated.
- Windows recorded all authentication failures as Event ID 4625.
- The Wazuh Agent successfully collected the events.
- The Wazuh Manager processed and correlated the activity.
- Wazuh generated Rule 60122 and Rule 60204.
- The attack was mapped to MITRE ATT&CK Technique T1110 (Brute Force).

No unauthorized access was obtained.

---

# Risk Assessment

Without appropriate security controls, brute force attacks may result in:

- Unauthorized access to systems
- Account compromise
- Privilege escalation
- Lateral movement
- Data theft
- Ransomware deployment
- Service disruption

Implementing multiple defensive controls significantly reduces these risks.

---

# Recommended Security Controls

## 1. Enable Multi-Factor Authentication (MFA)

### Priority

Critical

### Description

Require Multi-Factor Authentication for all Remote Desktop and administrative accounts.

### Benefit

Even if an attacker discovers a valid password, access is denied without the second authentication factor.

---

## 2. Implement Account Lockout Policies

### Priority

Critical

### Description

Automatically lock user accounts after a defined number of failed authentication attempts.

Example:

- Lock after 5 failed attempts
- Lock duration: 15–30 minutes

### Benefit

Prevents attackers from continuously guessing passwords.

---

## 3. Enforce Strong Password Policies

### Priority

High

### Description

Require passwords that are:

- At least 14 characters
- Complex
- Unique
- Changed when compromised

Avoid predictable passwords.

### Benefit

Makes brute force attacks significantly more difficult.

---

## 4. Restrict Remote Desktop Access

### Priority

Critical

### Description

Limit Remote Desktop access to authorized users and trusted networks only.

Avoid exposing RDP directly to the Internet.

### Benefit

Reduces the attack surface.

---

## 5. Enable Network Level Authentication (NLA)

### Priority

High

### Description

Require authentication before establishing an RDP session.

### Benefit

Prevents unnecessary resource consumption and reduces exposure to unauthorized users.

---

## 6. Monitor Failed Authentication Attempts

### Priority

High

### Description

Continuously monitor Windows Security Event ID 4625.

Investigate:

- Repeated failures
- High-frequency authentication attempts
- Multiple targeted accounts

### Benefit

Allows early detection of brute force attacks.

---

## 7. Correlate Security Events

### Priority

High

### Description

Use SIEM correlation rules, such as Wazuh Rule 60204, to group related failed authentication events.

### Benefit

Reduces alert fatigue while improving incident visibility.

---

## 8. Restrict Administrative Accounts

### Priority

High

### Description

Avoid using built-in administrative accounts for daily activities.

Implement separate administrative accounts.

### Benefit

Reduces the impact of credential compromise.

---

## 9. Review Windows Audit Policies

### Priority

Medium

### Description

Ensure that Windows logs both:

- Successful logons
- Failed logons

Regularly review audit configurations.

### Benefit

Provides complete forensic visibility.

---

## 10. Perform Continuous Security Monitoring

### Priority

High

### Description

Continuously monitor:

- Windows Security Logs
- Sysmon Events
- Authentication activity
- Privilege changes
- PowerShell execution
- Registry modifications

### Benefit

Improves early threat detection.

---

# SOC Analyst Recommendations

During every brute force investigation, analysts should verify:

- Source IP address
- Target host
- Target account
- Number of failed attempts
- Successful authentication after failures
- Lateral movement
- Privilege escalation
- Newly created accounts
- Suspicious PowerShell activity
- Persistence mechanisms

These checks help determine whether the attack was unsuccessful or resulted in a compromise.

---

# Long-Term Improvements

To further strengthen the security posture, organizations should consider implementing:

- Endpoint Detection and Response (EDR)
- Threat Intelligence integration
- Security Orchestration, Automation and Response (SOAR)
- Privileged Access Management (PAM)
- Just-In-Time Administration (JIT)
- Passwordless Authentication
- Security Awareness Training

These technologies improve both prevention and incident response capabilities.

---

# Lessons for Future SOC Investigations

Future investigations should also examine:

- Event ID 4624 (Successful Logon)
- Event ID 4720 (User Account Created)
- Event ID 4728 (Group Membership Changes)
- Event ID 4688 (Process Creation)
- PowerShell Operational Logs
- Sysmon Process Creation Events
- Registry Modifications
- Scheduled Tasks
- Windows Services

This broader investigation helps determine whether attackers progressed beyond the initial brute force attempt.

---

# Recommendations Summary

| Recommendation | Priority |
|---------------|----------|
| Enable Multi-Factor Authentication | Critical |
| Configure Account Lockout Policies | Critical |
| Restrict Remote Desktop Access | Critical |
| Enforce Strong Password Policies | High |
| Enable Network Level Authentication | High |
| Monitor Event ID 4625 | High |
| Use SIEM Correlation Rules | High |
| Limit Administrative Accounts | High |
| Review Audit Policies | Medium |
| Continuous Security Monitoring | High |

---

# Conclusion

The brute force attack was successfully detected before any unauthorized access occurred.

Although the laboratory was intentionally designed for defensive training, the investigation demonstrates the importance of combining preventive controls, continuous monitoring, and effective event correlation.

Implementing the recommendations described in this document will significantly improve an organization's ability to prevent, detect, and respond to credential-based attacks while reducing overall security risk.
