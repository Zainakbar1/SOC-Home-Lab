# Execution

## T1569.002 - Service Execution

### Activity

Remote execution using Impacket PsExec

### Command

```bash
impacket-psexec WINDOWS-SOC/socadmin:root@10.10.10.30
```

### Detection

```spl
index=sysmon
ParentImage="*services.exe"
```

### Phase

Phase 6