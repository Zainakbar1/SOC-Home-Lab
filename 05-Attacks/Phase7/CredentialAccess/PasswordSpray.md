# Password Spray Attempt

## Objective

Simulate a password spraying attack against the SMB service using Hydra.

---

## MITRE ATT&CK

| Technique | ID |
|-----------|----|
| Password Spraying | T1110.003 |

---

## Tool

Hydra

---

## Wordlist

```
password
Password123
admin
administrator
root
```

---

## Command

```bash
hydra -l socadmin -P passwords.txt smb://10.10.10.30
```

---

## Result

Hydra returned:

```
invalid reply from target
```

The authentication attempt was unsuccessful.

---

## Security Significance

Although authentication failed, repeated login attempts can indicate:

- Password spraying
- Brute force attacks
- Credential guessing

---

## Detection Opportunities

Monitor:

- Failed authentication attempts
- SMB login failures
- Multiple login attempts from one host

---

## MITRE Mapping

T1110.003

---

## Conclusion

Hydra generated SMB authentication attempts that can be used to validate defensive detections.