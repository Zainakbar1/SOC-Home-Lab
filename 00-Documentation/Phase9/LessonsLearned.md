# Project Lessons Learned

## Project

SOC Home Lab – Attack Simulation, Detection Engineering, Threat Hunting, and Incident Response

---

# Overview

This document summarizes the knowledge gained, technical achievements, challenges encountered, and future improvements identified during the development of the SOC Home Lab.

The project was completed over nine structured phases covering infrastructure deployment, attack simulation, SIEM implementation, detection engineering, threat hunting, incident response, and portfolio documentation.

The completed lab demonstrates practical Security Operations Center (SOC) workflows using enterprise-inspired technologies and methodologies.

---

# Project Objectives

The primary objectives of the project were to:

- Build a realistic SOC environment using virtual machines.
- Centralize endpoint telemetry using Splunk Enterprise.
- Simulate attacker activity in an isolated environment.
- Develop custom detection rules using Splunk SPL.
- Perform proactive threat hunting.
- Investigate incidents using structured methodologies.
- Map attacker behavior to the MITRE ATT&CK framework.
- Produce professional documentation suitable for a cybersecurity portfolio.

All objectives were successfully completed.

---

# Major Achievements

## Infrastructure

Successfully deployed:

- Ubuntu SOC Server
- Windows 11 Endpoint
- Kali Linux Attack Platform

Implemented:

- VMware NAT networking
- Host-Only SOC network
- Static IP addressing
- Snapshot strategy

---

## SIEM Deployment

Successfully configured:

- Splunk Enterprise
- Splunk Universal Forwarder
- Sysmon

Validated:

- Endpoint log collection
- Centralized logging
- Search functionality
- Detection queries

---

## Attack Simulation

Successfully simulated:

- Host Discovery
- Account Enumeration
- Process Enumeration
- Service Enumeration
- Registry Enumeration
- Registry Run Key Persistence
- Scheduled Task Persistence
- Remote Command Execution

---

## Detection Engineering

Created:

- 7 SPL Detection Queries
- 3 Correlation Searches
- 2 Production-style Alerts

Validated detection coverage against generated telemetry.

---

## Threat Hunting

Performed investigations covering:

- Discovery activity
- Registry persistence
- Scheduled Task persistence
- IOC hunting
- Timeline reconstruction
- Process analysis
- Parent-child relationships

---

## Incident Response

Produced:

- Incident Report
- IOC Analysis
- Timeline
- Evidence Report
- Lessons Learned

---

## Documentation

Completed documentation for every project phase including:

- Installation
- Architecture
- Network Design
- Troubleshooting
- Detection Engineering
- Incident Response
- Portfolio Documentation

---

# Skills Developed

## Security Operations

- SOC Monitoring
- Log Analysis
- Detection Engineering
- Threat Hunting
- Incident Response

---

## Windows Security

- Sysmon
- Registry Analysis
- Scheduled Tasks
- Process Investigation
- Windows Services

---

## Linux Administration

- Ubuntu Server
- SSH
- Package Management
- System Administration

---

## Splunk

- Search Processing Language (SPL)
- Index Management
- Data Ingestion
- Correlation Searches
- Alert Development
- Dashboard Investigation

---

## VMware

- Virtual Machine Deployment
- Snapshot Management
- Virtual Networking
- Resource Planning

---

## Frameworks

Applied:

- MITRE ATT&CK
- NIST Incident Response Lifecycle

---

# Technical Challenges

The project included several realistic engineering challenges:

- VMware networking configuration
- Splunk data ingestion troubleshooting
- Sysmon configuration validation
- Windows firewall restrictions
- Detection tuning
- False positive reduction
- IOC correlation
- Attack timeline reconstruction

Each challenge was documented and resolved during implementation.

---

# Key Lessons

The project reinforced several important cybersecurity principles:

## Visibility

Effective detection depends on comprehensive endpoint telemetry.

---

## Correlation

Individual events often appear harmless, but correlating multiple events reveals attacker behavior.

---

## Documentation

High-quality documentation is as important as technical implementation.

---

## Detection Engineering

Detection logic requires continuous testing and tuning to balance coverage with false positives.

---

## Threat Hunting

Proactive investigations can uncover suspicious activity before alerts are generated.

---

## Incident Response

Structured investigations improve consistency, evidence collection, and reporting quality.

---

# Future Improvements

Potential future enhancements include:

## Infrastructure

- Windows Server Domain Controller
- Active Directory
- Additional Windows Clients
- Linux Endpoints

---

## Security Tools

- Zeek
- Suricata
- Wazuh
- Velociraptor
- TheHive
- Cortex
- MISP

---

## Detection Engineering

Expand coverage for:

- Credential Access
- Lateral Movement
- Defense Evasion
- Command and Control
- Exfiltration

---

## Automation

Future improvements include:

- SOAR playbooks
- Automated IOC enrichment
- Automated containment
- Automated reporting

---

# Portfolio Value

This project demonstrates practical experience in:

- Building enterprise-style SOC infrastructure
- Deploying SIEM solutions
- Configuring endpoint telemetry
- Simulating attacker behavior
- Writing detection rules
- Conducting threat hunts
- Performing incident response
- Producing professional technical documentation

These skills closely align with responsibilities expected of:

- SOC Analyst (Tier 1 / Tier 2)
- Blue Team Analyst
- Detection Engineer
- Threat Hunter
- Security Operations Engineer

---

# Final Statistics

| Category | Count |
|-----------|------:|
| Project Phases | 9 |
| Virtual Machines | 3 |
| Operating Systems | 3 |
| Detection Queries | 7 |
| Correlation Searches | 3 |
| Alerts | 2 |
| Incident Reports | 5 |
| MITRE Techniques | 11 |
| Documentation Files | 60+ |
| Screenshots | 100+ |

---

# Final Reflection

This project provided end-to-end experience with the complete lifecycle of security operations. Beginning with infrastructure deployment and ending with incident reporting, each phase built upon the previous one to create a realistic and repeatable SOC environment.

Beyond technical implementation, the project emphasized disciplined documentation, structured investigations, and alignment with industry frameworks such as MITRE ATT&CK and the NIST Incident Response Lifecycle.

The completed repository serves as both a learning resource and a professional portfolio demonstrating practical blue-team capabilities.

---

# Project Status

## SOC Home Lab

**Status:** ✅ Completed

All planned phases have been implemented, validated, documented, and organized into a portfolio-ready repository.

The project is suitable for:

- GitHub portfolio publication
- Technical interviews
- Resume project experience
- Cybersecurity demonstrations
- Continuous expansion with future enhancements

---

# Acknowledgements

This project was completed as a hands-on learning initiative to develop practical cybersecurity skills through realistic laboratory exercises, emphasizing detection engineering, threat hunting, incident response, and security operations best practices.