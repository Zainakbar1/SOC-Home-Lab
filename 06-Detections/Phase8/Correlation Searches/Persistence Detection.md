# Persistence Detection Correlation Search

## Detection Name

Windows Persistence Detection – Registry Run Keys & Scheduled Tasks

---

# Purpose

This correlation search identifies common Windows persistence mechanisms frequently abused by attackers after gaining initial access.

The detection combines Registry Run Key modifications and Scheduled Task creation into a single high-confidence detection, allowing SOC analysts to quickly identify attempts to maintain long-term access on compromised endpoints.

---

# Detection Objectives

Detect the following persistence techniques:

- Registry Run Key creation
- Registry Run Key modification
- Scheduled Task creation
- Scheduled Task modification
- Payload references
- Registry persistence combined with scheduled task persistence

---

# MITRE ATT&CK

| Tactic | Technique | ATT&CK ID |
|----------|-------------------------------|------------|
| Persistence | Registry Run Keys / Startup Folder | T1547.001 |
| Persistence | Scheduled Task / Job | T1053.005 |
| Discovery | Query Registry | T1012 |

---

# Data Sources

- Sysmon Event ID 1
- Windows Registry
- Windows Task Scheduler
- Splunk Universal Forwarder
- Splunk Enterprise

---

# Detection Logic

The search monitors execution of:

- reg.exe
- schtasks.exe

and searches for:

- CurrentVersion\Run
- ChromeUpdater
- ChromeUpdate
- payload.bat

---

# SPL Detection

```spl
index=sysmon earliest=-15m
(
Image="*reg.exe"
OR Image="*schtasks.exe"
OR CommandLine="*CurrentVersion\\Run*"
OR CommandLine="*ChromeUpdater*"
OR CommandLine="*ChromeUpdate*"
OR CommandLine="*payload.bat*"
)
| stats
count
values(CommandLine) as Commands
values(Image) as Processes
by Computer User ParentImage
```

---

# Alert Trigger

Generate an alert when:

- A new Registry Run Key is created.
- A Scheduled Task is created.
- A Registry Run Key references an executable or batch file.
- A Scheduled Task references an unknown executable.
- Registry persistence and Scheduled Task persistence occur within the same investigation window.

---

# Alert Severity

**High**

Increase to **Critical** when:

- Parent process is PowerShell
- Parent process is cmd.exe
- Activity originates from PsExec
- Multiple persistence techniques are observed together

---

# Investigation Steps

1. Review Registry Run Keys.
2. Verify Scheduled Tasks.
3. Examine the referenced executable.
4. Review parent-child process relationships.
5. Search for additional persistence mechanisms.
6. Determine whether remote execution preceded persistence.
7. Verify whether persistence has been removed.

---

# Indicators of Compromise

## Registry

```
HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

Registry Value

```
ChromeUpdater
```

---

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

# Expected False Positives

- Enterprise software installers
- Software updates
- Windows Update
- Backup software
- Approved administrative scripts

---

# Recommended Tuning

Whitelist trusted:

- Microsoft
- VMware
- Enterprise deployment tools
- Endpoint management software

Generate alerts only for:

- Newly created Run Keys
- Newly created Scheduled Tasks
- Unknown payload paths
- Non-standard parent processes

---

# Response Actions

Upon detection:

1. Isolate the endpoint.
2. Export Registry Run Keys.
3. Export Scheduled Tasks.
4. Preserve forensic evidence.
5. Remove unauthorized persistence.
6. Hunt for additional attacker activity.
7. Perform IOC search across the environment.

---

# Validation

## Lab Status

✅ Successfully Validated

Persistence Created:

- Registry Run Key
- Scheduled Task

Successfully Detected:

- reg.exe
- schtasks.exe
- ChromeUpdater
- ChromeUpdate
- payload.bat

Evidence

- Screenshot 23
- Screenshot 24
- Screenshot 25
- Screenshot 26

---

# Outcome

This correlation search successfully detected the persistence mechanisms simulated during Phase 8. Registry Run Keys and Scheduled Task creation were identified through Sysmon process creation telemetry and correlated into a high-confidence persistence detection. The search demonstrates how multiple persistence indicators can be combined to improve detection fidelity while reducing false positives.