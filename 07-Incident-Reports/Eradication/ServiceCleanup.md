# Service Cleanup

## Overview

Following containment, all Windows services were reviewed to identify unauthorized or temporary services created during the attack simulation. Particular attention was given to the PsExec service (PSEXESVC), which is commonly created during remote execution.

---

# Objective

- Remove temporary services
- Verify Windows service integrity
- Confirm PsExec service removal
- Ensure no unauthorized services remain

---

# Services Reviewed

- PSEXESVC
- Windows Services
- SplunkForwarder
- Sysmon64
- VMware Tools

---

# Verification Activities

The following PowerShell command was used:

```powershell
Get-Service PSEXESVC -ErrorAction SilentlyContinue
```

Result:

No PSEXESVC service was present after cleanup.

Additional verification included:

- Reviewing running services
- Checking automatic startup services
- Comparing service inventory with baseline

---

# Evidence

Related screenshots:

- Phase8-06 – Services Verification
- Phase8-14 – PsExec Events

---

# Outcome

The endpoint contained only expected Windows and application services. No unauthorized services remained after eradication.