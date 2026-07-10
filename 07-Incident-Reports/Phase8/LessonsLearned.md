# Lessons Learned

## Incident ID

IR-009

---

# Overview

This document summarizes the key observations, lessons learned, and recommendations identified during the Phase 8 threat hunting and incident response exercise.

The purpose of this review is to evaluate the effectiveness of the implemented detection engineering, threat hunting methodology, incident response process, and overall SOC workflow. These findings help improve future investigations and strengthen defensive capabilities.

---

# Incident Summary

| Category | Status |
|----------|--------|
| Incident Type | Threat Hunting |
| Severity | High |
| Environment | SOC Home Lab |
| Investigation Status | Closed |
| Detection Status | Successful |
| Recovery Status | Successful |

---

# Investigation Objectives

The objectives of this exercise were to:

- Investigate simulated attacker activity
- Collect endpoint evidence
- Detect persistence mechanisms
- Perform IOC hunting
- Reconstruct the attack timeline
- Validate Splunk detections
- Map activity to the MITRE ATT&CK Framework
- Produce complete incident documentation

All objectives were successfully achieved.

---

# What Worked Well

## Sysmon Visibility

Sysmon generated detailed endpoint telemetry throughout the attack simulation.

Collected information included:

- Process creation
- Parent-child relationships
- Command-line arguments
- User context
- Registry activity
- Scheduled task execution

This telemetry significantly improved investigation quality.

---

## Splunk Enterprise

Splunk successfully centralized endpoint logs and enabled efficient searching, correlation, and timeline reconstruction.

Capabilities demonstrated:

- IOC hunting
- Detection engineering
- Timeline analysis
- MITRE ATT&CK mapping
- Correlation searches
- Alert validation

---

## Detection Engineering

Custom SPL queries successfully detected:

- Discovery commands
- Registry persistence
- Scheduled task persistence
- IOC artifacts
- Remote execution
- Attack timeline events

Detection coverage aligned with the simulated attack techniques.

---

## Threat Hunting

Rather than relying only on alerts, proactive hunting identified attacker activity through:

- Process analysis
- Registry analysis
- Scheduled task analysis
- IOC searches
- Timeline reconstruction

This demonstrated the value of hypothesis-driven investigations.

---

## Incident Documentation

Maintaining documentation throughout the investigation improved consistency and ensured that all evidence, findings, and decisions were recorded in a structured manner.

---

# Challenges Encountered

Several practical issues were encountered during implementation:

- Some Windows Security Event IDs were unavailable because advanced auditing was not enabled.
- Remote execution simulations required adjustments to generate reliable telemetry.
- Certain administrative commands generated similar events to attacker activity, requiring careful analysis to distinguish legitimate actions from simulated attacks.
- Detection logic required tuning to reduce potential false positives.

These challenges reflect realistic conditions that SOC analysts encounter in production environments.

---

# Improvements for Future Phases

The following enhancements are recommended:

### Endpoint Logging

- Enable additional Windows Advanced Audit Policies.
- Expand Sysmon configuration to capture more event types, such as network connections and file creation.

### Detection Engineering

- Develop behavior-based detections in addition to command-based detections.
- Add risk scoring and severity classification.
- Expand MITRE ATT&CK coverage to additional tactics and techniques.

### Threat Hunting

- Incorporate network telemetry where available.
- Correlate endpoint events with authentication and DNS activity.
- Build reusable hunting playbooks.

### Incident Response

- Standardize evidence collection procedures.
- Develop containment checklists.
- Automate portions of IOC validation.

---

# Skills Demonstrated

This phase demonstrated practical experience in:

- Threat Hunting
- Incident Response
- Detection Engineering
- Splunk Search Processing Language (SPL)
- Sysmon Analysis
- Windows Endpoint Investigation
- IOC Analysis
- Timeline Reconstruction
- Registry Forensics
- Scheduled Task Analysis
- MITRE ATT&CK Mapping
- Security Documentation

---

# Key Takeaways

The investigation reinforced several important principles:

- High-quality telemetry is essential for effective investigations.
- Small attacker actions can be correlated into a complete attack narrative.
- Persistence mechanisms are easier to identify when combined with contextual process information.
- Structured documentation improves investigation quality and repeatability.
- MITRE ATT&CK provides a common language for describing adversary behavior.
- Threat hunting complements traditional alert-based monitoring.

---

# Recommendations

Based on the investigation, the following recommendations are made for future SOC operations:

1. Continuously review and tune detection rules.
2. Expand endpoint logging coverage.
3. Develop additional correlation searches for lateral movement and credential access.
4. Perform regular threat hunting exercises.
5. Maintain up-to-date incident response playbooks.
6. Validate detections through controlled attack simulations.
7. Document all investigations using a standardized reporting format.

---

# Overall Assessment

The Phase 8 exercise successfully demonstrated a complete threat hunting and incident response workflow within a controlled SOC environment.

The investigation covered the full lifecycle of a security incident:

- Detection
- Investigation
- Evidence Collection
- IOC Analysis
- Timeline Reconstruction
- MITRE ATT&CK Mapping
- Containment Validation
- Recovery Verification
- Documentation

The custom detection logic and structured reporting provided strong visibility into attacker behavior while reinforcing best practices for Security Operations Center (SOC) analysts.

---

# Phase 8 Outcome

**Status:** ✅ Successfully Completed

The Phase 8 objectives were fully achieved. The lab now includes:

- Comprehensive attack simulations
- Validated Splunk detections
- Threat hunting workflows
- Correlation searches
- Alert definitions
- Incident reports
- MITRE ATT&CK mappings
- Complete documentation

This phase represents a production-style incident investigation and demonstrates practical SOC analyst, threat hunting, and detection engineering skills suitable for portfolio presentation.