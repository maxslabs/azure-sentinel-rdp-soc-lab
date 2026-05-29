# Azure Sentinel RDP SOC Detection Lab

## Overview

This project simulates a Security Operations Center (SOC) investigation of a Remote Desktop Protocol (RDP) brute-force attack using Microsoft Sentinel.

It demonstrates end-to-end SOC workflows including telemetry ingestion, detection engineering, and incident investigation using Windows Event Logs and KQL queries.

---

## Architecture

The lab simulates an enterprise attack scenario:

- Windows 11 generates RDP authentication attempts
- Windows Server 2022 logs authentication events (Security Logs)
- Logs are forwarded to Azure Log Analytics
- Microsoft Sentinel analyzes telemetry and triggers detections

![SOC Architecture](architecture/soc-architecture.png)

---

## Data Sources

### Windows Server 2022
- Event ID 4624 → Successful logon
- Event ID 4625 → Failed logon attempts
- Event ID 4688 → Process creation

---

## Detection Engineering (KQL)

The following detection use cases were implemented in Microsoft Sentinel:

- Multiple failed RDP authentication attempts (4625 spike)
- Suspicious login success following repeated failures
- Unusual authentication patterns from single source
- Process-level anomaly correlation (4688)

KQL queries are located in the `detections/` directory.

---

## Investigation Workflow

1. RDP brute-force simulation initiated from Windows 11
2. Failed authentication attempts generated on Windows Server 2022
3. Security logs collected and forwarded to Log Analytics Workspace
4. Microsoft Sentinel processes telemetry using KQL rules
5. Alerts generated for abnormal authentication patterns
6. SOC investigation performed using event correlation and timeline analysis

---

## Evidence

All supporting artifacts are stored in the `evidence/` directory, including:

- Log Analytics query outputs
- Windows Event Viewer logs
- Authentication failure spikes
- Successful and failed RDP sessions

---

## Key Skills Demonstrated

- SIEM operations using Microsoft Sentinel
- KQL-based detection engineering
- Windows Event Log analysis
- RDP attack simulation and analysis
- SOC incident investigation workflows

---

## SOC Summary

The investigation identified a brute-force authentication attempt against a Windows Server 2022 system. Detection was successfully performed using Microsoft Sentinel with Windows Event Log telemetry.

No persistence or lateral movement was observed in this simulation.

---

## Notes

This environment is fully isolated and used strictly for cybersecurity learning and SOC simulation.

All attack activity is simulated and controlled.
