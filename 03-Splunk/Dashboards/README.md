# Splunk Dashboards

## Overview

This directory contains the Splunk dashboards developed for the SOC Home Lab.

The dashboards provide visualizations for authentication activity, endpoint telemetry, SOC monitoring, and threat hunting investigations. They are intended to demonstrate how collected telemetry can be transformed into operational dashboards for a Security Operations Center (SOC).

---

# Dashboard List

| Dashboard | Purpose |
|-----------|---------|
| Authentication Dashboard | Monitor authentication successes and failures |
| Endpoint Monitoring | Monitor endpoint telemetry and Sysmon events |
| SOC Overview | High-level SOC monitoring dashboard |
| Threat Hunting | Support proactive investigations and IOC hunting |

---

# Dashboard Sources

The dashboards are based on data collected from:

- Windows Event Logs
- Sysmon Operational Logs
- Security Logs
- Splunk Universal Forwarder
- Custom SPL Detection Queries

---

# Data Flow

```
Windows Endpoint
        │
        ▼
Sysmon
        │
        ▼
Universal Forwarder
        │
        ▼
Splunk Enterprise
        │
        ▼
Dashboards
```

---

# Dashboard Status

| Dashboard | Status |
|-----------|--------|
| Authentication Dashboard | Planned / Export when available |
| Endpoint Monitoring | Planned / Export when available |
| SOC Overview | Planned / Export when available |
| Threat Hunting | Planned / Export when available |

---

# Future Improvements

Future versions of this repository will include:

- Exported Splunk XML dashboards
- Dashboard JSON exports (where supported)
- Additional SOC metrics
- MITRE ATT&CK visualizations
- Alert summary panels

---

# Related Files

- `../Configurations`
- `../../06-Detections`
- `../../07-Incident-Reports`

---

# Note

The XML files in this directory are placeholders for exported dashboards. Once dashboards are created or exported from Splunk Enterprise, they should replace the placeholder files with the actual dashboard definitions.