# Registry Persistence Alert

## Alert Name

Windows Registry Run Key Persistence

---

# Description

This alert detects attempts to establish persistence through Windows Registry Run Keys.

Registry Run Keys are one of the most commonly abused persistence mechanisms because programs configured within these Registry locations execute automatically when a user logs on.

This alert identifies Registry modifications performed through **reg.exe** and searches for suspicious Registry values referencing executables or batch files.

---

# MITRE ATT&CK

| Tactic | Technique | ATT&CK ID |
|----------|-------------------------------|------------|
| Persistence | Registry Run Keys / Startup Folder | T1547.001 |
| Discovery | Query Registry | T1012 |

---

# Severity

**High**

Escalate to **Critical** if:

- Registry persistence is followed by remote execution
- Multiple persistence mechanisms are observed
- The parent process is PowerShell or PsExec

---

# Data Source

- Sysmon Event ID 1
- Splunk Enterprise

---

# Detection Logic

Detect execution of:

- reg.exe

Search for:

- CurrentVersion\Run
- ChromeUpdater
- payload.bat

---

# SPL Search

```spl
index=sysmon earliest=-15m
(
Image="*reg.exe"
OR CommandLine="*CurrentVersion\\Run*"
OR CommandLine="*ChromeUpdater*"
OR CommandLine="*payload.bat*"
)
| table _time Computer User ParentImage Image CommandLine
```

---

# Trigger Condition

Trigger an alert when:

- A new Registry Run Key is created.
- An existing Run Key is modified.
- A Registry value references an executable or batch file.
- Persistence is created by PowerShell or cmd.exe.

---

# Alert Schedule

Run Every:

```
15 Minutes
```

Time Range:

```
Last 15 Minutes
```

---

# Risk Score

| Risk | Score |
|------|------:|
| Medium | 40 |
| High | 70 |
| Critical | 90 |

---

# Response Actions

Upon alert generation:

1. Identify the affected endpoint.
2. Verify the Registry Run Key.
3. Review the referenced executable.
4. Search for additional persistence.
5. Review Scheduled Tasks.
6. Collect forensic evidence.
7. Remove unauthorized Registry entries.
8. Continue IOC hunting.

---

# False Positives

- Software installers
- Enterprise deployment tools
- Approved administrator activity
- Windows Updates

---

# Tuning Recommendations

Exclude:

- Microsoft installers
- VMware Tools
- Enterprise deployment software

Prioritize:

- PowerShell
- cmd.exe
- PsExec
- Unknown parent processes

---

# Validation

## Status

✅ Successfully Validated

Evidence:

- Screenshot 23
- Screenshot 24

---

# Outcome

The alert successfully detected Registry Run Key persistence created during Phase 8. Sysmon process creation telemetry combined with Splunk correlation enabled rapid identification of Registry modifications associated with attacker persistence.