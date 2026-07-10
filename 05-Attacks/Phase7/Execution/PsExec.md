# PsExec Remote Execution

## Objective

Validate remote code execution using Impacket PsExec.

---

## MITRE ATT&CK

| Technique | ID |
|-----------|----|
| Service Execution | T1569.002 |
| Windows Command Shell | T1059.003 |

---

## Tool

Impacket PsExec

---

## Command

```bash
impacket-psexec WINDOWS-SOC/socadmin:root@10.10.10.30
```

---

## Result

Remote shell successfully established.

Example:

```
Microsoft Windows
C:\Windows\System32>
```

---

## Commands Executed

```cmd
whoami
hostname
ipconfig
```

---

## Detection

Splunk detected:

- cmd.exe
- services.exe
- PsExec service creation
- Process creation events

---

## Security Impact

Remote command execution enables attackers to:

- Deploy malware
- Dump credentials
- Execute ransomware
- Establish persistence

---

## MITRE Mapping

T1569.002

T1059.003

---

## Conclusion

PsExec successfully demonstrated authenticated remote execution over SMB.