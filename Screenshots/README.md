# Screenshot Evidence

This folder contains evidence captured during testing and validation of the Blue Team Homelab Detection project.

The screenshots document host detections, network intrusion alerts, authentication monitoring, and attack simulation activity observed through Wazuh, Sysmon and Suricata.

---

# Windows / Sysmon Detections

## New-User.png
Demonstrates Windows user creation activity monitored through Wazuh.

## sysmon-useradd-logs.png
Shows Sysmon process and user creation telemetry generated during account creation testing.

## sysmon-logs-useradd.png
Additional Sysmon event evidence validating host telemetry collection.

## User group into administrators.png
Shows detection related to privilege escalation simulation by adding a user into the Administrators group.

## sysmon-logs-user-as-administrators.png
Shows Sysmon telemetry generated from privilege modification activity.

---

# Linux / Authentication Monitoring

## Login Failure.png
Authentication monitoring showing failed login activity.

## SSH Failed login.png
Simulated multiple failed SSH login attempts used to validate authentication-related detections.

## user-add-in-linux.png
Shows Linux user creation monitoring through Wazuh agent telemetry.

## linux-user-move-to-sudo-group.png
Demonstrates privilege escalation style activity by moving a user into the sudo group.

## pkg-install-alert.png
Shows package installation activity detected and monitored through Linux telemetry.

---

# Network Intrusion Detection (Suricata)

## Ping.png
Simulated ICMP traffic generated for IDS testing.

## suricata-icmp-alert.png
Custom Suricata alert generated from ICMP detection rule.

## Suricata-alert-on-nmap.png
Suricata alert triggered during Nmap scan simulation to validate network intrusion detection.

---

# Summary
These screenshots provide evidence for:

- Host-based detection monitoring
- Network intrusion detection
- Authentication monitoring
- Privilege escalation simulations
- Attack simulation validation
- Multi-agent security monitoring
