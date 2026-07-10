# High Severity SMB Alert

## Alert Name

SMB Lateral Movement Detection

---

## Description

This alert identifies possible lateral movement through SMB using administrative credentials.

---

## Trigger Conditions

- PsExec detected

OR

- SMB share enumeration

OR

- Administrative share access

OR

- Remote cmd.exe execution

---

## Alert Severity

High

---

## MITRE ATT&CK

T1021.002

T1078

T1569.002

T1059.003

---

## SOC Response

1. Validate source IP

2. Validate user account

3. Review authentication logs

4. Check running processes

5. Isolate affected endpoint if malicious

6. Acquire forensic evidence

7. Block attacker account

8. Document incident

---

## Escalation

Notify:

SOC Lead

Incident Response Team

System Administrator

---

## Priority

P1