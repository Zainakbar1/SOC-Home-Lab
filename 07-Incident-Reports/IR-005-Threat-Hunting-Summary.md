# Incident Report IR-005

# Threat Hunting Summary

---

## Objective

Summarize the threat hunting activities performed during Phase 7.

---

## Hunts Performed

### Hunt 1

Network Reconnaissance

Status

Completed

---

### Hunt 2

Service Enumeration

Completed

---

### Hunt 3

SMB Enumeration

Completed

---

### Hunt 4

Credential Validation

Completed

---

### Hunt 5

Administrative Share Enumeration

Completed

---

### Hunt 6

Remote Execution

Completed

---

### Hunt 7

Process Creation Analysis

Completed

---

### Hunt 8

Timeline Reconstruction

Completed

---

## Evidence Sources

Sysmon

Splunk

Windows Event Logs

SMB

NetExec

Impacket

---

## MITRE Coverage

- T1046

- T1021.002

- T1078

- T1569.002

- T1059.003

- T1033

- T1082

---

## Key Findings

Administrative credentials were successfully used.

Remote command execution was observed.

Process creation events were successfully collected.

Threat hunting queries identified attacker activity.

Timeline reconstruction confirmed the attack sequence.

---

## Analyst Assessment

The environment generated sufficient telemetry to detect and investigate the simulated attack.

The combination of Sysmon and Splunk provided excellent endpoint visibility.

---

## Recommendations

Enable Windows Security log forwarding.

Create correlation searches.

Configure real-time alerts.

Deploy Sysmon to additional endpoints.

Expand coverage to PowerShell and WMI.

---

## Overall Assessment

Threat hunting objectives achieved successfully.

Incident closed.