# Credential Reset

## Overview

Following the identification of successful SMB authentication and PsExec-based remote execution, the credentials used during the attack simulation were treated as potentially compromised. As part of the containment process, credential rotation procedures were documented to prevent unauthorized reuse and restore trust in the affected accounts.

Within this SOC Home Lab, credential reset activities were simulated using dedicated laboratory accounts. No production accounts or external systems were involved.

---

# Objective

The objectives of credential reset were to:

- Invalidate compromised credentials
- Prevent unauthorized reuse
- Restore account integrity
- Reduce the risk of lateral movement
- Improve authentication security
- Document post-incident recovery actions

---

# Affected Accounts

| Account | Role | Status |
|---------|------|--------|
| socadmin | Local Administrator | Password Reset (Simulated) |
| Administrator | Built-in Administrator | Verified |
| Splunk Service Account | Log Collection | Verified |

---

# Trigger for Credential Reset

Credential reset procedures were initiated after confirming:

- Successful SMB authentication
- Administrative share access
- PsExec remote execution
- Service creation events
- Multiple authentication events from the attack workstation

These indicators suggested that the administrative credentials used during the simulation should no longer be considered trustworthy.

---

# Simulated Response Actions

The following actions were documented as part of the incident response process:

1. Reset the password for the affected administrative account.
2. Verify account membership in privileged groups.
3. Review recent authentication activity.
4. Confirm no unauthorized accounts were created.
5. Verify Remote Desktop Users group membership.
6. Validate local Administrators group membership.
7. Document all credential changes.

---

# Verification Activities

Following credential rotation, the following checks were performed:

- Confirmed successful authentication using updated credentials.
- Reviewed Windows Security Logs for new authentication events.
- Verified that no additional SMB authentication attempts succeeded with the previous credentials.
- Confirmed no unexpected privilege escalation occurred.

---

# Evidence

Evidence supporting this activity included:

- Windows Security Event Logs
- Sysmon Process Creation Events
- Local Users and Groups Review
- Splunk Authentication Searches
- Incident Timeline Documentation

Related screenshots:

- Phase8-10 – Local Users
- Phase8-11 – User Creation Events
- Phase8-12 – RDP Users
- Phase8-17 – Authentication Events

---

# Security Recommendations

Following credential reset, the following improvements were recommended:

- Enforce strong password policies.
- Enable multi-factor authentication where possible.
- Apply the principle of least privilege.
- Restrict administrative account usage.
- Monitor authentication failures and unusual logon patterns.
- Rotate privileged credentials on a regular schedule.

---

# MITRE ATT&CK Mapping

| Tactic | Technique |
|---------|-----------|
| Credential Access | T1110 – Brute Force (Simulation) |
| Lateral Movement | T1021.002 – SMB / Windows Admin Shares |
| Defense Evasion | Mitigated through credential rotation |

---

# Lessons Learned

This exercise demonstrated that credential security plays a critical role in limiting attacker movement. Even in a simulated environment, promptly rotating administrative credentials after suspicious activity is an essential containment measure that reduces the likelihood of continued unauthorized access.

---

# Outcome

Credential reset procedures successfully completed the containment phase of the simulated incident. Administrative account integrity was restored, authentication activity was verified, and the environment was prepared for eradication and recovery activities documented in the following phases.