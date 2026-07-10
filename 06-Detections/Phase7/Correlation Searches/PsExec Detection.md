# PsExec Detection

## Objective

Detect remote execution performed through PsExec.

---

## MITRE ATT&CK

| Technique | ID |
|-----------|----|
| Service Execution | T1569.002 |
| Windows Command Shell | T1059.003 |

---

## Detection Logic

The detection identifies:

- cmd.exe
- services.exe
- PSEXESVC
- whoami
- hostname
- ipconfig

executed shortly after SMB authentication.

---

## Splunk Query

```spl
index=sysmon

(Image="*cmd.exe"

OR ParentImage="*services.exe"

OR ParentImage="*PSEXESVC*")

| table _time Image ParentImage CommandLine User
```

---

## Severity

High

---

## False Positives

- Administrative activity
- Helpdesk support
- Remote maintenance

---

## Recommended Response

1. Identify source host

2. Verify administrator activity

3. Isolate endpoint if unauthorized

4. Review lateral movement

5. Collect forensic evidence