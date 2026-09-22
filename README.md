# Windows SOC Monitoring Lab Using Splunk

## Overview

This project demonstrates a Windows Security Operations Center monitoring environment built using Splunk Enterprise. Windows Event Logs and Sysmon telemetry were collected from a Windows endpoint and forwarded to a Splunk server for searching, dashboard visualization, and security alerting.

## Architecture

- Windows endpoint
- Splunk Universal Forwarder
- Windows Security, System, and Application event logs
- Sysmon Operational logs
- Ubuntu server running Splunk Enterprise
- Splunk index: `soc_lab`

## Dashboard

The Windows SOC Monitoring Dashboard provides:

- Total Windows event count
- Failed login attempts
- Top Windows security event codes
- Security events over time
- Recent suspicious Windows activity
- Windows events by log source
- Shared time-range filtering

![Dashboard Overview](screenshots/01-dashboard-overview.png)

![Detection Dashboard](screenshots/02-dashboard-detections.png)

## Detection Alerts

The project includes six scheduled detection alerts:

1. Encoded PowerShell Execution Detected
2. Repeated Failed Windows Logins Detected
3. Windows User Account Activity Detected
4. Local Administrators Group Changed
5. Suspicious Windows Utility Execution
6. New Windows Service Installed

The alert SPL queries are available in
[`searches/detection_searches.spl`](searches/detection_searches.spl).

## Detection Validation

A controlled Windows service installation was used to generate Event ID 7045 and validate the New Windows Service Installed detection. The event was successfully forwarded, indexed, displayed on the dashboard, and recorded as a triggered alert.

![Triggered Alerts](screenshots/03-triggered-alerts.png)

![Enabled Alerts](screenshots/04-enabled-alerts.png)

## Key Event IDs

| Event ID | Description |
|---|---|
| 4624 | Successful account login |
| 4625 | Failed account login |
| 4688 | New process created |
| 4720 | User account created |
| 4726 | User account deleted |
| 4732 | Member added to a local security group |
| 4733 | Member removed from a local security group |
| 7045 | New Windows service installed |

## Skills Demonstrated

- Splunk Enterprise administration
- Windows event-log collection
- Sysmon telemetry monitoring
- SPL search development
- Scheduled alert creation
- Detection-rule validation
- SOC dashboard creation
- Basic Windows security investigation

## Repository Structure

```text
splunk-soc-project/
├── README.md
├── dashboard/
│   └── windows_soc_monitoring_dashboard.xml
├── searches/
│   └── detection_searches.spl
└── screenshots/
    ├── 01-dashboard-overview.png
    ├── 02-dashboard-detections.png
    ├── 03-triggered-alerts.png
    └── 04-enabled-alerts.png