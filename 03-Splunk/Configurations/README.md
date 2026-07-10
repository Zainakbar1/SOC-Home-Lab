# Splunk Configuration Files

## Overview

This directory contains the configuration files used throughout the SOC Home Lab deployment. These files define how Splunk Enterprise stores data, receives logs, communicates with forwarders, and manages server-level settings.

The configurations are based on the implementation performed during the project and have been sanitized for publication. Environment-specific values such as passwords, hostnames, and unique identifiers have been removed where appropriate.

---

# Configuration Files

| File | Purpose |
|------|---------|
| indexes.conf | Defines custom Splunk indexes |
| inputs.conf | Configures data inputs and receiving ports |
| outputs.conf | Configures forwarding destinations |
| server.conf | Server-level configuration settings |

---

# Environment

| Component | Value |
|-----------|-------|
| SIEM | Splunk Enterprise |
| Operating System | Ubuntu 26.04 LTS |
| Splunk Version | 10.x |
| Hostname | Ubuntu-SOC |
| Management Port | 8089 |
| Web Interface | 8000 |
| Forwarder Port | 9997 |

---

# Directory Structure

```
Configurations/
│
├── README.md
├── indexes.conf
├── inputs.conf
├── outputs.conf
└── server.conf
```

---

# Configuration Summary

## indexes.conf

Defines logical storage locations for indexed data. During this project, a dedicated index was used to separate endpoint telemetry from other data sources.

---

## inputs.conf

Configures the Splunk receiving port used by the Universal Forwarder installed on the Windows endpoint.

Configured services include:

- Splunk Forwarder Receiver
- Syslog Listener (optional)
- Management Inputs

---

## outputs.conf

Defines forwarding destinations for Splunk instances.

Within this project, the Windows Universal Forwarder was configured to forward Sysmon telemetry to the Ubuntu Splunk Enterprise server.

---

## server.conf

Contains server-level configuration including:

- Hostname
- Server identity
- General settings
- Licensing
- Networking parameters

Sensitive values have been omitted.

---

# Security Considerations

The published configuration files do not contain:

- Passwords
- Authentication tokens
- SSL private keys
- Deployment secrets
- License files

Only configuration required to understand the lab architecture has been retained.

---

# Related Documentation

- `00-Documentation/Phase2`
- `00-Documentation/Phase3`
- `00-Documentation/Phase9`
- `04-Sysmon`
- `06-Detections`

---

# Conclusion

These configuration files document the Splunk Enterprise deployment used throughout the SOC Home Lab. Together they provide the foundation for centralized log collection, detection engineering, threat hunting, and incident response activities demonstrated in this repository.