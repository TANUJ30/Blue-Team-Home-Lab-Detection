# Detection Scenarios Tested

This document contains detection scenarios validated during the Blue Team homelab project to test host-based monitoring, network intrusion detection, and multi-source log visibility through Wazuh, Sysmon, and Suricata.

---

# 1. Windows User Creation Detection

## Test Performed
A new local Windows user was intentionally created to simulate administrative account creation activity and verify whether endpoint telemetry was captured and forwarded into the monitoring stack.

```powershell
net user testuser /add
```

## Data Sources Used
- Wazuh Agent  
- Sysmon  
- Windows Security Event Logs  

## Detection Observed
The activity generated user account creation events which were collected by Wazuh and correlated with Windows/Sysmon telemetry. The event was successfully visible through the Wazuh dashboard and confirmed proper host monitoring.

---

# 2. Sysmon Process Creation Detection

## Test Performed
Several native reconnaissance commands were executed to simulate simple attacker enumeration behavior and validate Sysmon process creation monitoring.

```powershell
whoami
ipconfig /all
netstat -ano
```

## Data Sources Used
- Sysmon Event ID 1  
- Wazuh Monitoring  

## Detection Observed
Command executions generated process creation telemetry and were successfully observed through Sysmon-generated logs in Wazuh, validating endpoint command visibility and process monitoring.

---

# 3. ICMP Ping Detection (Suricata)

## Custom Rule Used

```suricata
alert icmp any any -> $HOME_NET any (msg:"ICMP Ping Detected"; sid:1000001; rev:1;)
```

## Test Performed
ICMP traffic was generated from a monitored system to validate custom Suricata rule detection and alert forwarding into Wazuh.

```bash
ping <target-ip>
```

## Data Sources Used
- Suricata IDS  
- eve.json  
- Wazuh Integration  

## Detection Observed
The custom rule successfully generated ICMP alerts in Suricata, and those alerts were forwarded into Wazuh, validating the network intrusion detection pipeline.

---

# 4. SSH Alert Detection

## Test Performed
SSH-related activity was generated from Linux/Kali systems to verify monitoring of authentication and remote-access related events.

## Data Sources Used
- Wazuh Linux Agent  
- Linux Authentication Logs  

## Detection Observed
SSH security-related events were collected and visible in Wazuh, demonstrating Linux log ingestion and basic authentication monitoring.

---

# 5. Network Flow Monitoring

## Test Performed
General network activity was observed through Suricata flow logging to validate visibility beyond alert-based detections.

## Observed
Suricata successfully captured:

- Flow events  
- Traffic metadata  
- Alert events  
- Basic protocol activity  

This provided additional network telemetry and validated packet-level monitoring in the lab.

---

# Summary of Validated Detections

| Detection | Source | Status |
|---------|--------|--------|
| User Creation | Wazuh/Sysmon | Success |
| Process Creation | Sysmon | Success |
| ICMP Ping Detection | Suricata | Success |
| SSH Alerts | Wazuh Linux Agent | Success |
| Flow Monitoring | Suricata | Success |

---

# Future Detection Tests

Planned improvements and future detection scenarios include:

- Port scan detection testing  
- Brute-force simulation detections  
- Additional custom Wazuh rules  
- Correlation-based detections  
- Expanded Suricata signature testing  
