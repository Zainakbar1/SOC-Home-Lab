# Scheduled Task Persistence Alert

## Alert Name

Windows Scheduled Task Persistence Detection

---

# Description

This alert detects the creation or modification of Windows Scheduled Tasks that may be used by attackers to establish persistence on a compromised endpoint.

Scheduled Tasks are frequently abused by adversaries because they provide a reliable mechanism for executing payloads automatically at system startup, user logon, or predefined intervals.

This alert monitors execution of **schtasks.exe** and identifies suspicious task names, payloads, and command-line arguments associated with persistence.

---

# MITRE ATT&CK

| Tactic | Technique | ATT&CK ID |
|----------|--------------------------|------------|
| Persistence | Scheduled Task / Job | T1053.005 |

---

# Severity

**High**

Escalate to **Critical** if:

- Scheduled Task executes a suspicious executable or script.
- Task is created immediately after Registry persistence.
- Parent process is **PowerShell**, **cmd.exe**, or **PsExec**.
- Multiple persistence mechanisms are observed together.

---

# Data Source

- Sysmon Event ID 1
- Splunk Enterprise

---

# Detection Logic

Monitor execution of:

- schtasks.exe

Search for:

- ChromeUpdate
- payload.bat
- /create
- /sc
- /tn

---

# SPL Search

```spl
index=sysmon earliest=-15m
(
Image="*schtasks.exe"
OR CommandLine="*ChromeUpdate*"
OR CommandLine="*payload.bat*"
)
| table _time Computer User ParentImage Image CommandLine
```

---

# Trigger Condition

Generate an alert when:

- A Scheduled Task is created.
- A Scheduled Task references a batch file or executable.
- A Scheduled Task is created by an unusual parent process.
- The task name is previously unseen.
- Scheduled Task persistence follows attacker discovery activity.

---

# Alert Schedule

Run Every

```
15 Minutes
```

Search Window

```
Last 15 Minutes
```

---

# Risk Score

| Risk | Score |
|------|------:|
| Medium | 45 |
| High | 75 |
| Critical | 95 |

---

# Indicators of Compromise

## Scheduled Task

```
ChromeUpdate
```

---

## Payload

```
payload.bat
```

---

## Process

```
schtasks.exe
```

---

# Investigation Steps

1. Identify the endpoint where the task was created.
2. Verify the scheduled task configuration.
3. Review the configured payload.
4. Determine who created the task.
5. Review parent-child process relationships.
6. Check for Registry Run Key persistence.
7. Review Startup Folder entries.
8. Search for additional attacker activity.
9. Determine whether remote execution occurred before persistence.

---

# Recommended Response

If malicious:

- Disable the Scheduled Task.
- Remove the persistence mechanism.
- Preserve forensic evidence.
- Perform IOC hunting.
- Review Registry Run Keys.
- Investigate additional persistence mechanisms.
- Continue timeline reconstruction.

---

# False Positives

- Enterprise software deployment
- Windows Updates
- Backup software
- Administrative maintenance scripts
- Approved automation tools

---

# Recommended Tuning

Whitelist trusted:

- Microsoft
- VMware
- Enterprise management software
- Backup solutions

Prioritize:

- New Scheduled Tasks
- Unknown payloads
- PowerShell-created tasks
- cmd.exe-created tasks
- PsExec-created tasks
- SYSTEM account activity

---

# Validation

## Lab Status

✅ Successfully Validated

Detected:

- schtasks.exe
- ChromeUpdate
- payload.bat

Evidence:

- Screenshot 25
- Screenshot 26
- Screenshot 32

---

# Outcome

The alert successfully detected the Scheduled Task persistence mechanism created during Phase 8. Sysmon process creation telemetry was forwarded to Splunk Enterprise, where the alert identified task creation, associated payload references, and parent process information. This alert provides an effective mechanism for identifying persistence established through Windows Task Scheduler.