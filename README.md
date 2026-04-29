# Blue-Team-Home-Lab-Detection
Blue Team homelab project demonstrating host-based and network-based detection engineering using Wazuh, Suricata, Sysmon, Windows, Ubuntu and Kali Linux.
## Overview
This project documents the design and implementation of a practical Blue Team homelab built to simulate host and network monitoring using :

- Wazuh for SIEM, log analysis and security monitoring
- Suricata for Network Intrusion Detection (NIDS)
- Sysmon for Windows host telemetry and process monitoring
- Ubuntu Server as Wazuh Manager and Suricata sensor
- Windows as monitored endpoint with Wazuh agent + Sysmon
- Kali Linux as monitored Linux agent 

## Objective
This homelab was built to: 
- Deploy a working SIEM + IDS environment, collect and analyze endpoint telemetry ,generate and validate security alerts, simulate attacker activity in a controlled lab, integrate host and network detections into one monitoring stack, and practice practical SOC analyst skills

## Implemented

### Wazuh Deployment
#### Configured:
- Installed Wazuh manager on Ubuntu
- Enrolled Windows agent
- Added Kali Linux as additional agent
- Verified agent connectivity
- Enabled centralized monitoring
#### Monitored log sources:
- Windows Security logs
- Sysmon event logs
- Linux authentication logs
- SSH-related events
- File integrity monitoring events
### Network Monitoring
- Suricata deployment
- Custom ICMP ping detection
- Suricata alerts forwarded into Wazuh
- Traffic flow monitoring

### Sysmon Integration (Windows)
Integrated Sysmon to improve Windows telemetry.
###Collected events included:
- Process Creation (Event ID 1)
- Process Termination (Event ID 5)
- User account activity
- Scheduled task activity
- Command execution visibility
### Custom Suricata Rule
```suricata
alert icmp any any -> $HOME_NET any (msg:"ICMP Ping Detected"; sid:1000001; rev:1;)
```
## Lab Architecture
```text
Windows Endpoint (Wazuh + Sysmon)
Kali Linux (Wazuh Agent / Attack Simulation)
             |
             v
Ubuntu Server (Wazuh Manager + Suricata IDS)
```
