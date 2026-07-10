# Discovery Activity Correlation Search

## Detection Name

Windows Discovery Activity Detection

---

# Purpose

This correlation search detects common Windows discovery commands that attackers execute immediately after gaining access to a system.

Discovery commands often represent the first observable stage of post-compromise activity and can indicate reconnaissance before privilege escalation, persistence, credential access, or lateral movement.

---

# Detection Objective

Identify execution of common reconnaissance commands including:

- whoami.exe
- hostname.exe
- systeminfo.exe
- ipconfig.exe
- tasklist.exe
- net.exe
- net1.exe
- sc.exe
- schtasks.exe

---

# MITRE ATT&CK

| Tactic | Technique | ID |
|----------|-----------|---------|
| Discovery | System Owner/User Discovery | T1033 |
| Discovery | System Information Discovery | T1082 |
| Discovery | Network Configuration Discovery | T1016 |
| Discovery | Account Discovery | T1087 |
| Discovery | Permission Group Discovery | T1069 |
| Discovery | Process Discovery | T1057 |
| Discovery | System Service Discovery | T1007 |

---

# SPL Detection

```spl
index=sysmon earliest=-15m
(
Image="*whoami.exe"
OR Image="*hostname.exe"
OR Image="*systeminfo.exe"
OR Image="*ipconfig.exe"
OR Image="*tasklist.exe"
OR Image="*net.exe"
OR Image="*net1.exe"
OR Image="*sc.exe"
OR Image="*schtasks.exe"
)
| stats count values(CommandLine) as Commands by Computer User ParentImage
```

---

# Trigger Logic

Generate an alert when:

- Multiple discovery commands are executed within a short time window.
- Discovery commands originate from unusual parent processes.
- Discovery activity occurs outside expected administrative hours.

---

# Severity

**Medium**

Increase to **High** if followed by persistence or remote execution activity.

---

# Data Sources

- Sysmon Event ID 1
- Splunk Universal Forwarder
- Splunk Enterprise

---

# Investigation Steps

1. Review the user account.
2. Determine whether execution was local or remote.
3. Inspect the parent process.
4. Correlate with authentication events.
5. Review subsequent persistence activity.
6. Investigate lateral movement indicators.

---

# Expected False Positives

- Helpdesk engineers
- System administrators
- Inventory software
- Patch management tools

---

# Recommended Tuning

Whitelist approved:

- SCCM
- Intune
- VMware Tools
- Microsoft Defender
- Enterprise inventory agents

---

# Validation

## Lab Status

✅ Successfully Validated

Evidence:

- Screenshot 20
- Screenshot 21
- Screenshot 22

---

# Outcome

The correlation search successfully detected attacker discovery activity generated during Phase 8. Commands associated with host enumeration, account discovery, process enumeration, and service enumeration were identified using Sysmon process creation events and correlated within Splunk Enterprise.