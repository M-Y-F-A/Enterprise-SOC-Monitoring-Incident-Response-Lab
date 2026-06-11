# Attack Scenario

## Scenario Summary
A controlled adversary simulation traverses from an external host through VPN access into an internal Windows/AD environment.

## Attack Stages
1. Initial access through controlled VPN path
2. Endpoint authentication attempts and account targeting
3. Internal movement and privileged access simulation
4. Security event generation for SOC detection and triage

## Expected Evidence
- Authentication failures/successes
- Process and network telemetry from endpoint
- Domain controller authentication events
