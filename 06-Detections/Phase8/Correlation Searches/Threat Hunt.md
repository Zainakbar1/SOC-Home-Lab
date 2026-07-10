# Threat Hunting Correlation Search

## Detection Name

Phase 8 Threat Hunting Workflow

---

# Purpose

This correlation search provides a structured workflow for investigating suspicious endpoint activity following an alert. Rather than detecting a single event, it correlates multiple indicators across discovery, persistence, remote execution, and attacker artifacts to reconstruct the full attack lifecycle.

The workflow is intended for SOC analysts performing manual investigations, threat hunting, and incident response.

---

# Threat Hunting Objectives

The investigation aims to:

- Identify attacker discovery activity
- Detect Registry persistence
- Detect Scheduled Task persistence
- Identify remote execution
- Locate Indicators of Compromise (IOCs)
- Reconstruct the attack timeline
- Map activity to the MITRE ATT&CK Framework
- Determine the scope of compromise

---

# Investigation Workflow

```
Alert Generated
       │
       ▼
Initial Triage
       │
       ▼
Discovery Investigation
       │
       ▼
Persistence Investigation
       │
       ▼
IOC Hunting
       │
       ▼
Timeline Reconstruction
       │
       ▼
MITRE ATT&CK Mapping
       │
       ▼
Containment Decision
```

---

# Hunt 1 – Discovery Commands

Purpose

Identify reconnaissance activity.

Commands investigated:

- whoami.exe
- hostname.exe
- systeminfo.exe
- ipconfig.exe
- tasklist.exe
- net.exe
- sc.exe
- schtasks.exe

SPL

```spl
index=sysmon
(Image="*whoami.exe"
OR Image="*hostname.exe"
OR Image="*systeminfo.exe"
OR Image="*ipconfig.exe"
OR Image="*tasklist.exe"
OR Image="*net.exe"
OR Image="*sc.exe"
OR Image="*schtasks.exe")
| table _time User Image ParentImage CommandLine
```

---

# Hunt 2 – Registry Investigation

Purpose

Locate Registry persistence.

SPL

```spl
index=sysmon
(Image="*reg.exe"
OR CommandLine="*CurrentVersion\\Run*")
| table _time User Image CommandLine
```

---

# Hunt 3 – Scheduled Task Investigation

Purpose

Identify persistence created through Windows Task Scheduler.

SPL

```spl
index=sysmon
(Image="*schtasks.exe"
OR CommandLine="*ChromeUpdate*")
| table _time User Image CommandLine
```

---

# Hunt 4 – IOC Search

Indicators

- payload.bat
- ChromeUpdater
- ChromeUpdate

SPL

```spl
index=sysmon
(CommandLine="*payload.bat*"
OR CommandLine="*ChromeUpdater*"
OR CommandLine="*ChromeUpdate*")
| table _time User Image ParentImage CommandLine
```

---

# Hunt 5 – Timeline Reconstruction

Purpose

Reconstruct attacker activity chronologically.

SPL

```spl
index=sysmon
| sort _time
| table _time User ParentImage Image CommandLine
```

---

# Hunt 6 – Remote Execution

Purpose

Identify commands executed remotely through PsExec.

SPL

```spl
index=sysmon
(Image="*tasklist.exe"
OR Image="*systeminfo.exe"
OR Image="*reg.exe"
OR Image="*schtasks.exe")
| table _time User ParentImage Image CommandLine
```

---

# Indicators of Compromise

## Files

```
payload.bat
```

---

## Registry

```
HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

Value

```
ChromeUpdater
```

---

## Scheduled Task

```
ChromeUpdate
```

---

## Processes

- reg.exe
- schtasks.exe
- tasklist.exe
- systeminfo.exe
- whoami.exe
- hostname.exe
- ipconfig.exe

---

# MITRE ATT&CK Mapping

| ATT&CK Tactic | Technique | ATT&CK ID |
|---------------|-----------|-----------|
| Discovery | System Owner/User Discovery | T1033 |
| Discovery | System Information Discovery | T1082 |
| Discovery | Network Configuration Discovery | T1016 |
| Discovery | Account Discovery | T1087 |
| Discovery | Process Discovery | T1057 |
| Discovery | Service Discovery | T1007 |
| Discovery | Query Registry | T1012 |
| Persistence | Registry Run Keys | T1547.001 |
| Persistence | Scheduled Task | T1053.005 |
| Execution | Remote Service Execution | T1569.002 |

---

# Analyst Checklist

- [ ] Confirm the affected endpoint.
- [ ] Identify the executing user.
- [ ] Review parent-child process relationships.
- [ ] Verify Registry Run Keys.
- [ ] Verify Scheduled Tasks.
- [ ] Review IOC hits.
- [ ] Build the attack timeline.
- [ ] Assess scope of compromise.
- [ ] Recommend containment actions.
- [ ] Document findings.

---

# Investigation Outcome

During Phase 8, the threat hunting workflow successfully identified:

- Discovery activity
- Registry persistence
- Scheduled Task persistence
- Remote command execution
- IOC artifacts
- Complete attack timeline

The collected telemetry demonstrated how multiple low-level events can be correlated into a comprehensive incident investigation, allowing analysts to understand attacker behavior, validate detections, and support incident response activities.

---

# Validation

## Status

✅ Successfully Validated

Evidence:

- Screenshot 20 – Discovery Activity
- Screenshot 23 – Registry Investigation
- Screenshot 24 – Registry Persistence
- Screenshot 26 – Scheduled Task Creation
- Screenshot 29 – IOC Hunt
- Screenshot 30 – Attack Timeline
- Screenshot 31 – MITRE Mapping
- Screenshot 32 – Detection Summary