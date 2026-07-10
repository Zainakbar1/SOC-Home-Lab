# SMB Authentication Detection

## Objective

Detect successful SMB authentication using valid credentials.

---

## MITRE ATT&CK

T1078

Valid Accounts

---

## Detection Logic

Monitor:

- SMB authentication

- Administrative access

- Share enumeration

- Remote execution

---

## Splunk Query

```spl
index=sysmon

(Image="*net.exe*"

OR Image="*cmd.exe*")

| table _time User Image CommandLine
```

---

## Severity

Medium

---

## False Positives

- Legitimate administrators

- Backup software

- SCCM

---

## Recommended Response

Review:

Source host

User account

Time

Purpose

Authorization