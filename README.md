# Wazuh Security Monitoring Project

![Wazuh](https://img.shields.io/badge/Wazuh-v4.14.3-blue)
![Platform](https://img.shields.io/badge/platform-Linux-lightgrey)
![Status](https://img.shields.io/badge/status-complete-brightgreen)
![Author](https://img.shields.io/badge/author-Satheesh-orange)

A hands-on home lab project demonstrating real-time security monitoring 
and threat detection using Wazuh SIEM.

## Author
**Satheesh Nithiananthan**  
satheeshnithiananthan@gmail.com  
SOC Operations | Blue Team | Threat Detection

## Lab Setup
| Machine | OS | Role |
|---------|-----|------|
| Manager | Kali Linux | Wazuh Manager + Dashboard |
| Agent | Debian/Ubuntu | Monitored Endpoint |

## What Was Done
- Installed and configured Wazuh Manager on Kali Linux
- Connected Debian/Ubuntu as a monitored agent
- Configured log collection and security monitoring
- Analyzed security alerts in Wazuh dashboard

## Features Explored
| Feature | Description |
|---------|-------------|
| Log Monitoring | Real-time system and security log collection |
| Intrusion Detection | Alerts on suspicious activity |
| File Integrity Monitoring | Detects unauthorized file changes |
| Vulnerability Detection | Identifies known CVEs on endpoints |
| Dashboard | Visual alert investigation via Wazuh UI |

## Technologies Used
- **Wazuh** - SIEM and XDR platform
- **Kali Linux** - Manager machine
- **Debian/Ubuntu** - Agent machine
- **Elastic Stack** - Log storage and search
- **Kibana** - Data visualization

## Key Learnings
- How SIEM agents communicate with a manager
- How to read and investigate security alerts
- How Wazuh rules and decoders work
- Real-world SOC monitoring workflow

## Related Projects
- [Wazuh Nmap Detection](https://github.com/Satz-N-Sentry/wazuh-nmap-detection) 
  - Custom rules to detect Nmap port scans in real time

## Documentation
Full setup and configuration steps are in [Wazuh.md](Wazuh.md)
```
