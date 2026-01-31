# soc-suricata-nmap-detection
SOC-style detection lab using Suricata IDS to detect Nmap reconnaissance activity in a virtualized home lab. Includes custom rules, traffic analysis, alert validation, and attack simulation from Kali Linux .

# SOC Suricata Nmap Detection Lab

## Overview
This project demonstrates a SOC-style intrusion detection scenario using **Suricata IDS** to detect **Nmap reconnaissance activity** within a virtualized home lab. The goal of this lab was to simulate an attacker performing network scanning and validate that defensive monitoring correctly detects and logs the activity.

This lab focuses on **detection, alert analysis, and validation**, mirroring real-world Tier 1 SOC responsibilities.

---

## Lab Architecture

**Attacker Machine**
- Kali Linux
- Tool used: Nmap

**Defended Host**
- Ubuntu Linux (VMware)
- Suricata IDS running in IDS mode

**Network**
- All systems on the same local subnet
- Suricata monitoring the Ubuntu VM network interface

---

## Attack Simulation

From the Kali Linux system, multiple Nmap scans were executed against the Ubuntu host, including SYN scans targeting common TCP ports.

Example scan:
```bash
nmap -sS -p 1-1000 192.168.8.x

Although the target system had no open services, the scan traffic still generated network probes consistent with reconnaissance behavior.
Detection & Alerts
Suricata successfully detected the scanning activity and generated alerts for TCP-based reconnaissance attempts.
Alerts included:
Source IP (attacker)
Destination IP (Ubuntu host)
Destination ports scanned
Protocol (TCP)
Alert signature and severity
Alerts were logged in JSON format via eve.json, confirming successful detection.

## Example alert output:
{
  "event_type": "alert",
  "attacker_ip": "192.168.8.x",
  "internal_host_ip": "192.168.8.x",
  "proto": "TCP",
  "signature": "TEST TCP ALERT",
  "severity": 3,
  "direction": "to_server"
}

## Analysis
Although Nmap reported scanned ports as closed or filtered, Suricata still generated alerts. This behavior is expected and reflects real-world conditions, where attackers frequently probe hosts with no exposed services.
The purpose of this lab was not exploitation, but early-stage detection, which is a core SOC function.
Key Takeaways
IDS systems detect behavior, not service availability
Reconnaissance activity is valuable early-warning data
Closed ports do not equal “no threat”
Proper alerting enables SOC analysts to identify potential threats before escalation

## Skills Demonstrated
	•	Suricata IDS deployment and configuration
	•	Custom rule testing and validation
	•	Network traffic analysis
	•	Reconnaissance detection
	•	SOC-style documentation and reporting
	•	Future Improvements
	•	Add threshold-based scan detection rules
	•	Integrate alerts into a SIEM (Splunk / Elastic)
	•	Visualize alerts with dashboards
	•	Expand detection to UDP and service version scans

## Future Improvements
	•	Add threshold-based scan detection rules
	•	Integrate alerts into a SIEM (Splunk / Elastic)
	•	Visualize alerts with dashboards
	•	Expand detection to UDP and service version scans

