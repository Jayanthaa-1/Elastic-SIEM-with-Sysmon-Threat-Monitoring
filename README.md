# Elastic-SIEM-with-Sysmon-Threat-Monitoring

# Elastic SIEM with Sysmon Threat Monitoring (Windows VM Lab)

## Project Overview
This project demonstrates the implementation of a centralized Security Information and Event Management (SIEM) solution using the Elastic Stack integrated with Sysmon for advanced Windows endpoint monitoring.

The lab simulates a real-world SOC (Security Operations Center) environment where logs from Windows virtual machines are collected, analyzed, and correlated to detect suspicious activity such as malicious processes, persistence techniques, abnormal authentication attempts, and unusual network connections.

This project provides hands-on experience in threat detection, log analysis, and incident investigation using industry-relevant tools.

---

## Architecture

Windows Endpoint (Sysmon Installed)
        ↓
Elastic Agent
        ↓
Fleet Server
        ↓
Elasticsearch
        ↓
Kibana SIEM Dashboard

---

## Technologies Used

SIEM Platform: Elastic Stack  
Search Engine: Elasticsearch  
Visualization: Kibana  
Agent Management: Fleet Server  
Log Forwarding: Elastic Agent  
Endpoint Monitoring: Sysmon  
Virtualization: VirtualBox / VMware  
Operating System: Windows 10 VM  
Log Sources: Windows Event Logs, Sysmon Logs, Security Logs

---

## Lab Environment

Host Machine: Windows / Linux system  
Target Machine: Windows 10 Virtual Machine  
SIEM Server: Elastic Stack running on Linux VM  
RAM Requirement: Minimum 4GB recommended  
Storage Requirement: Minimum 40GB  
Network Mode: NAT / Internal Network

---

## Project Setup

### Step 1 – Create Virtual Machines

Two virtual machines were created:

1. Windows 10 VM (endpoint for monitoring)
2. Linux VM for Elastic SIEM

Recommended configuration:

CPU: 2 cores  
RAM: 4GB minimum  
Storage: 40GB  

---

### Step 2 – Install Elastic Stack

Installed the following components:

Elasticsearch  
Kibana  
Fleet Server  

Commands used:

sudo apt update
sudo apt install elasticsearch
sudo apt install kibana

Start services:

sudo systemctl start elasticsearch
sudo systemctl start kibana

Check service status:

sudo systemctl status elasticsearch
sudo systemctl status kibana

Access Kibana dashboard:

http://localhost:5601

---

### Step 3 – Configure Fleet Server

Fleet Server is used to centrally manage Elastic Agents.

Steps performed:

Enabled Fleet in Kibana  
Created new agent policy  
Generated enrollment token  
Configured Fleet Server integration  

Fleet allows centralized collection and management of endpoint logs.

---

### Step 4 – Install Sysmon on Windows VM

Sysmon provides detailed telemetry of Windows system activity including process creation, network connections, and registry changes.

Download Sysmon from Microsoft Sysinternals website.

Install Sysmon:

sysmon64.exe -accepteula -i sysmonconfig.xml

Verify Sysmon service:

Get-Service Sysmon64

Sysmon logs location:

Event Viewer → Applications and Services Logs → Microsoft → Windows → Sysmon → Operational

---

### Step 5 – Install Elastic Agent on Windows VM

Elastic Agent collects logs and forwards them to Elasticsearch.

Downloaded Elastic Agent from Kibana Fleet interface.

Install agent using enrollment token:

elastic-agent install --url=https://<fleet-server-ip>:8220 --enrollment-token=<token>

Agent sends Windows logs and Sysmon logs to Elastic SIEM.

---

## Log Collection

Elastic Agent collects the following logs:

Sysmon process creation logs  
Windows security logs  
Authentication logs  
PowerShell logs  
Network connection logs  
Registry activity logs  

Logs are visible in Kibana under Security → Hosts → Events.

---

## Detection Use Cases

### Suspicious Process Activity
Detection of unusual parent-child process relationships such as:

cmd.exe spawning powershell.exe

This may indicate malicious script execution.

---

### Failed Login Attempts
Multiple failed login attempts identified using:

Event ID 4625

Indicates possible brute-force attack attempts.

---

### Network Connection Monitoring
Sysmon Event ID 3 logs outbound network connections.

Used to detect connections to suspicious IP addresses.

---

### Persistence Mechanism Detection
Registry modifications monitored in locations such as:

HKCU\Software\Microsoft\Windows\CurrentVersion\Run

Attackers use these registry keys for persistence.

---

## Kibana Dashboards

Kibana provides visualization of collected logs including:

Host activity timeline  
Process execution logs  
Authentication events  
Network connection logs  
Alert severity overview  

Dashboards help analysts quickly identify suspicious behavior.

---

## Screenshots

Add screenshots to improve project presentation:

Kibana dashboard  
Sysmon logs in Event Viewer  
Fleet agent status page  
Security alerts page  

Suggested folder structure:

screenshots/
dashboard.png
alerts.png
sysmon_logs.png
fleet_status.png

---

## Skills Demonstrated

SIEM deployment  
Log analysis  
Threat detection  
Windows security monitoring  
Incident investigation  
Endpoint monitoring  
Security event correlation  
SOC workflow understanding  

---

## Learning Outcomes

Gained practical experience with SIEM tools  
Improved understanding of Windows logging mechanisms  
Learned how to detect suspicious activities  
Developed log analysis and investigation skills  
Understood SOC analyst workflow  
Configured centralized log collection  

---

## Future Improvements

Integrate Suricata IDS  
Add Sigma detection rules  
Simulate attacks using Atomic Red Team  
Create custom dashboards  
Integrate threat intelligence feeds  
Automate alert generation  

---

## Project Structure

Elastic-SIEM-Sysmon-Lab/

README.md  
sysmon-config.xml  
screenshots/  
detection-rules/  
notes/  

---

## References

Elastic Documentation  
https://www.elastic.co/guide

Sysmon Documentation  
https://learn.microsoft.com/sysinternals

MITRE ATT&CK Framework  
https://attack.mitre.org/

---

## Author

Your Name  
Cybersecurity Enthusiast  
SOC Analyst Aspirant  

---

## Project Summary

This project demonstrates practical implementation of a SIEM solution integrated with Sysmon to monitor Windows endpoint activity. It showcases the ability to collect logs, detect suspicious behavior, and analyze security events using Elastic Stack.

The project reflects real-world SOC analyst responsibilities including log monitoring, threat detection, and incident investigation.
