# Lateral Movement

## T1021.002 - SMB/Windows Admin Shares

### Activity

Administrative share access

### Commands

```bash
netexec smb 10.10.10.30 -u socadmin -p root --shares
```

### Detection

```spl
index=sysmon
CommandLine="*ADMIN$*"
```

---

## Phase

Phase 6