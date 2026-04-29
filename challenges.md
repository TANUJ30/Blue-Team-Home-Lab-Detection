# Challenges Faced and Solutions

This document summarizes key technical challenges encountered while building the Blue Team homelab and how they were resolved.

---

# 1. Network Visibility Issue (NAT vs Bridged)

## Challenge
Initially the lab used NAT networking, which limited visibility between systems and prevented proper network monitoring through Suricata.

Issues observed:
- Windows and Ubuntu were on different subnets
- Suricata could not reliably inspect endpoint traffic
- ICMP detection testing was inconsistent

## Solution
The lab network was migrated from NAT to Bridged networking.

Actions taken:
- Reconfigured both virtual machines to use Bridged Adapter
- Placed Ubuntu and Windows hosts in same subnet
- Verified connectivity and packet visibility

## Outcome
- Suricata gained proper traffic visibility
- Network-based detections began functioning as expected

---

# 2. HOME_NET Misconfiguration

## Challenge
Initial Suricata configuration used incorrect HOME_NET values, preventing detection rules from matching expected traffic.

## Solution
Updated HOME_NET to correct monitored subnet:

```yaml
HOME_NET: "[192.168.0.0/24]"
```

## Outcome
- Custom ICMP detection rule began triggering correctly
- Traffic was properly monitored

---

# 3. Sysmon Log Visibility Troubleshooting

## Challenge
Sysmon generated events locally but initial visibility inside Wazuh required troubleshooting.

Issues investigated:
- Event channel collection
- Agent configuration validation
- Process creation event visibility

## Solution
Validated Sysmon configuration and confirmed event collection pipeline.

Verified:
- Sysmon Event ID 1 process creation logs
- Wazuh agent log forwarding
- Event visibility in Wazuh dashboard

## Outcome
- Endpoint telemetry collection confirmed
- Process monitoring functioning correctly

---

# 4. Suricata Rule Loading Issues

## Challenge
During Suricata configuration, duplicate signatures and rule path conflicts caused parsing errors.

Issues encountered:
- Rule path confusion
- Duplicate signature errors
- suricata-update package problems

## Solution
Simplified the ruleset and used custom local rule testing.

Implemented:

```suricata
alert icmp any any -> $HOME_NET any (msg:"ICMP Ping Detected"; sid:1000001; rev:1;)
```

## Outcome
- Successful alert generation
- Stable custom detection testing

---

# 5. Wazuh + Suricata Integration Troubleshooting

## Challenge
Ensuring Suricata alerts were ingested correctly into Wazuh required validation.

## Solution
Integrated eve.json into Wazuh:

```xml
<localfile>
 <location>/var/log/suricata/eve.json</location>
 <log_format>json</log_format>
</localfile>
```
Restarted Wazuh manager and verified alert ingestion.

## Outcome
- Suricata alerts visible in Wazuh
- End-to-end IDS pipeline validated
---
