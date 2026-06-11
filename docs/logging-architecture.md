# Logging Architecture

## Telemetry Sources
- Windows Endpoint (Sysmon, Security logs)
- Domain Controller (AD authentication and policy logs)
- VPN gateway logs (connection activity)

## Collection and Forwarding
- Endpoint and server logs forwarded to Splunk indexers
- Parsing/normalization handled by Splunk configurations

## SOC Outcomes
- Alert generation for key detections
- Search, investigation, and response workflow support
