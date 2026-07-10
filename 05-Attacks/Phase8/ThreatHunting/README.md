# Threat Hunting

## Overview

Following the successful execution of discovery, persistence, and remote execution techniques, a structured threat hunting exercise was performed using Splunk Enterprise.

Rather than relying solely on security alerts, the investigation proactively searched endpoint telemetry to identify attacker behavior, reconstruct the attack timeline, validate persistence mechanisms, and collect Indicators of Compromise (IOCs).

Threat hunting focused primarily on Sysmon process creation events, command-line logging, registry modifications, scheduled task creation, and remote execution artifacts.

---

# Objectives

The objectives of this threat hunting exercise were to:

- Identify attacker discovery activity
- Detect persistence mechanisms
- Locate Indicators of Compromise (IOCs)
- Validate Sysmon telemetry
- Correlate attacker actions
- Reconstruct the attack timeline
- Validate MITRE ATT&CK mappings
- Verify detection engineering rules

---

# Data Sources

The investigation utilized the following telemetry sources:

| Source | Description |
|---------|-------------|
| Sysmon | Process Creation, Command Line Logging |
| Windows Event Logs | Service and System Events |
| Splunk Enterprise | Centralized Log Analysis |
| Splunk Universal Forwarder | Endpoint Log Collection |

---

# Hunting Scenario

The investigation assumed that suspicious activity had already occurred on the Windows endpoint.

Known attacker behaviors included:

- System Discovery
- Account Enumeration
- Registry Queries
- Registry Persistence
- Scheduled Task Creation
- Remote Command Execution
- IOC Generation

The objective was to determine the scope of attacker activity using Splunk.

---

# Hunt 1 – Discovery Activity

The first hunt searched for common discovery commands executed by an attacker.

Commands investigated:

- whoami.exe
- hostname.exe
- systeminfo.exe
- ipconfig.exe
- tasklist.exe
- net.exe
- sc.exe
- schtasks.exe

Splunk Search

```spl
index=sysmon earliest=-10m
(Image="*systeminfo.exe"
OR Image="*tasklist.exe"
OR Image="*schtasks.exe"
OR Image="*sc.exe"
OR Image="*net.exe"
OR Image="*net1.exe")
| table _time Computer User Image CommandLine ParentImage
| sort -_time
```

Result

All discovery commands were successfully detected.

Evidence

Screenshot 20

---

# Hunt 2 – Registry Investigation

The second hunt searched for Registry access and Registry Run Key persistence.

Splunk Search

```spl
index=sysmon
(Image="*reg.exe"
OR CommandLine="*CurrentVersion\\Run*")
| table _time Computer User Image CommandLine ParentImage
```

Result

Registry Run Key activity was successfully identified.

Evidence

Screenshots

23

24

---

# Hunt 3 – Scheduled Task Investigation

Scheduled task creation was investigated.

Splunk Search

```spl
index=sysmon
(Image="*schtasks.exe"
OR CommandLine="*ChromeUpdate*")
| table _time Computer User Image CommandLine ParentImage
```

Result

The scheduled task was successfully detected.

Evidence

Screenshots

25

26

---

# Hunt 4 – Remote Execution

Remote command execution performed through PsExec was investigated.

Commands identified included:

- hostname
- whoami
- systeminfo
- ipconfig
- tasklist
- reg query
- schtasks

Splunk Search

```spl
index=sysmon
(Image="*systeminfo.exe"
OR Image="*tasklist.exe"
OR Image="*reg.exe"
OR Image="*schtasks.exe")
| table _time Computer User ParentImage Image CommandLine
```

Result

Remote command execution generated Sysmon Event ID 1 entries under the SYSTEM security context.

Evidence

Screenshots

27

28

---

# Hunt 5 – IOC Search

Indicators of Compromise investigated:

- payload.bat
- ChromeUpdater
- ChromeUpdate
- reg.exe
- schtasks.exe

Splunk Search

```spl
index=sysmon earliest=-30m
(
CommandLine="*ChromeUpdate*"
OR CommandLine="*payload.bat*"
OR CommandLine="*CurrentVersion\\Run*"
OR Image="*schtasks.exe"
OR Image="*reg.exe"
)
| table _time User Image ParentImage CommandLine
| sort -_time
```

Result

IOC artifacts were successfully identified.

Evidence

Screenshot

29

---

# Hunt 6 – Timeline Reconstruction

A chronological timeline was created to reconstruct attacker activity.

Splunk Search

```spl
index=sysmon earliest=-30m
| sort _time
| table _time Image ParentImage User CommandLine
```

Result

The complete attack lifecycle was successfully reconstructed.

Evidence

Screenshot

30

---

# Hunt 7 – Detection Validation

Detection engineering rules were validated by confirming that all simulated attacker behaviors were present in Splunk.

Activities validated:

- Discovery
- Registry Queries
- Registry Persistence
- Scheduled Tasks
- Remote Execution
- IOC Hunting

Evidence

Screenshot

32

---

# Indicators of Compromise

| IOC | Type |
|------|------|
| payload.bat | File |
| ChromeUpdater | Registry Value |
| ChromeUpdate | Scheduled Task |
| reg.exe | Process |
| schtasks.exe | Process |
| systeminfo.exe | Process |
| tasklist.exe | Process |

---

# MITRE ATT&CK Mapping

| Activity | Technique | ATT&CK ID |
|----------|-----------|-----------|
| User Discovery | Discovery | T1033 |
| System Discovery | Discovery | T1082 |
| Account Discovery | Discovery | T1087 |
| Process Discovery | Discovery | T1057 |
| Service Discovery | Discovery | T1007 |
| Registry Discovery | Discovery | T1012 |
| Registry Run Keys | Persistence | T1547.001 |
| Scheduled Tasks | Persistence | T1053.005 |
| Remote Service Execution | Execution | T1569.002 |

---

# Hunting Outcome

The threat hunting exercise successfully identified all simulated attacker behaviors generated during Phase 8. Endpoint telemetry collected through Sysmon and centralized within Splunk Enterprise enabled investigators to detect discovery commands, registry modifications, scheduled task persistence, remote execution, and attacker-generated indicators of compromise.

The investigation demonstrated how proactive threat hunting complements traditional alert-based monitoring by uncovering malicious activity through telemetry correlation and timeline analysis.