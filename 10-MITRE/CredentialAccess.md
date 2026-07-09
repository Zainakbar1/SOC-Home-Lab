# Credential Access

## T1078 - Valid Accounts

### Description

Use valid credentials to authenticate.

### Activity

SMB Authentication

### Command

```bash
netexec smb 10.10.10.30 -u socadmin -p root
```

### Detection

```spl
index=sysmon DestinationPort=445
```

### Phase

Phase 6