# Wazuh SIEM - Security Monitoring Project

![Wazuh](https://img.shields.io/badge/Wazuh-v4.14.3-blue)
![Platform](https://img.shields.io/badge/platform-Linux-lightgrey)
![Status](https://img.shields.io/badge/status-complete-brightgreen)
![License](https://img.shields.io/badge/license-MIT-green)
![Author](https://img.shields.io/badge/author-Satheesh-orange)

---

## Author
**Satheesh Nithiananthan**
satheeshnithiananthan@gmail.com
SOC Operations | Blue Team | Threat Detection | Cybersecurity

---

## Table of Contents
1. [Introduction](#introduction)
2. [Security Capabilities](#security-capabilities)
3. [System Requirements](#system-requirements)
4. [Wazuh Manager Installation](#wazuh-manager-installation)
5. [Wazuh Agent Installation](#wazuh-agent-installation)
6. [Dashboard Monitoring](#dashboard-monitoring)
7. [Troubleshooting & Mitigation](#troubleshooting--mitigation)
8. [Conclusion](#conclusion)
9. [References](#references)

---

## Introduction

Wazuh is an open-source Security Information and Event Management (SIEM) 
platform designed to provide organizations with comprehensive visibility 
and security monitoring across their IT infrastructure.

It offers features such as:
- Log data analysis
- Intrusion detection
- Vulnerability assessment
- File integrity monitoring
- Active response

All integrated within a centralized management and visualization system.

As a next-generation SIEM, Wazuh collects and analyzes data from endpoints, 
servers, network devices, and cloud environments. It identifies anomalies, 
correlates events, and generates alerts for potential security incidents.

Wazuh integrates seamlessly with **Elastic Stack** (Elasticsearch and Kibana) 
or **OpenSearch Dashboard**, providing powerful search, visualization, and 
reporting capabilities.

### Wazuh Core Components

| Component | Description |
|-----------|-------------|
| **Wazuh Agent** | Installed on monitored endpoints to collect system logs, monitor file integrity, detect intrusions, and execute active responses |
| **Wazuh Manager** | Central analysis engine that processes collected data, applies decoders and rules to detect threats, and generates alerts |
| **Wazuh Dashboard** | Web-based graphical interface for managing agents, viewing alerts, visualizing data, and performing security analysis |

---

## Security Capabilities

Wazuh provides a wide range of security capabilities designed to protect 
systems, detect threats, and support incident response.

| Capability | Description |
|------------|-------------|
| **Threat Detection & Monitoring** | Continuously monitors endpoints and networks for suspicious activity, unauthorized access, malware behavior, and policy violations |
| **Log Collection & Analysis** | Collects logs from Windows, Linux, macOS, network devices, and cloud services |
| **File Integrity Monitoring (FIM)** | Detects changes to critical files, system directories, registry keys, and configurations |
| **Intrusion Detection (HIDS)** | Identifies ransomware behavior, privilege escalation attempts, brute-force attacks, and rootkits |
| **Security Configuration Assessment** | Checks endpoints for compliance with CIS benchmarks, PCI-DSS, HIPAA, and GDPR |
| **Vulnerability Detection** | Scans systems to identify missing patches, outdated software, and known vulnerabilities |
| **Active Response** | Takes automated actions such as blocking malicious IPs or isolating compromised endpoints |
| **Cloud Security Monitoring** | Integrated support for AWS, Azure, GCP, and Docker |
| **Centralized Dashboard** | Allows SOC teams to visualize alerts, view system health, and generate reports |

---

## System Requirements

### Lab Environment

| Machine | OS | Role |
|---------|-----|------|
| Manager | Kali Linux | Wazuh Manager + Dashboard |
| Agent | Parrot OS / Debian | Monitored Endpoint |

### Hardware Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| CPU | 2 cores | 4+ cores |
| RAM | 4 GB | 8-16 GB |
| Storage | 50 GB | 100 GB+ |
| Network | 1 Gbps NIC | Stable high-speed connectivity |

### Software Requirements — Wazuh Manager (Kali Linux)

- Operating System: Kali Linux 2024.x or later
- Python 3.8+
- Packages: `curl`, `wget`, `gnupg`, `apt-transport-https`, `unzip`
- Root or sudo privileges

### Software Requirements — Wazuh Agent

- Debian 10, 11, 12
- Ubuntu 18.04, 20.04, 22.04
- Parrot OS (Debian-based)

| Resource | Minimum | Recommended |
|----------|---------|-------------|
| CPU | 1 core | 2 cores |
| RAM | 512 MB | 1-2 GB |
| Disk | 200 MB | 500 MB |
| Network | Must reach Manager on port 1514 and 1515 | - |

### Environment Requirements

- Stable internet access for downloading Wazuh packages
- Administrative/sudo access to both machines
- NTP time synchronization (important for log correlation)
- Optional: VirtualBox, VMware, or Hyper-V for isolated lab

---

## Wazuh Manager Installation

### Step 1 — Run the installation script:
```bash
curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh && sudo bash ./wazuh-install.sh -a
```

![Installation](screenshots/01_wazuh_install.png)

### Step 2 — Installation complete output:
```
INFO: --- Summary ---
INFO: You can access the web interface https://<WAZUH_DASHBOARD_IP>
    User: admin
    Password: <ADMIN_PASSWORD>
INFO: Installation finished.
```

![Install Complete](screenshots/02_install_complete.png)

### Step 3 — Access the Dashboard:
```
https://<WAZUH_DASHBOARD_IP_ADDRESS>
Username: admin
Password: <ADMIN_PASSWORD>
```

![Dashboard Login](screenshots/03_dashboard_login.png)

> **Note:** To find all passwords run:
> ```bash
> sudo tar -O -xvf wazuh-install-files.tar wazuh-install-files/wazuh-passwords.txt
> ```

---

## Wazuh Agent Installation

The Wazuh agent runs on endpoints you want to monitor. It communicates 
with the Wazuh Manager through an encrypted and authenticated channel.

### Agent Capabilities:
- Log data collection
- File integrity monitoring
- Threat detection
- Security configuration assessment
- Vulnerability detection
- Incident response

![Agent Overview](screenshots/04_agent_overview.png)

### Step 1 — Update package manager:
```bash
sudo apt update
sudo apt upgrade -y
```

### Step 2 — Download and install Wazuh Agent on Parrot OS:
```bash
wget https://packages.wazuh.com/4.x/apt/pool/main/w/wazuh-agent/wazuh-agent_4.14.0-1_amd64.deb && \
sudo WAZUH_MANAGER='192.168.8.166' WAZUH_AGENT_NAME='parrot' \
dpkg -i ./wazuh-agent_4.14.0-1_amd64.deb
```

![Agent Install](screenshots/05_agent_install.png)

### Step 3 — Start the agent:
```bash
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
sudo systemctl status wazuh-agent
```

![Agent Status](screenshots/06_agent_status.png)

---

## Dashboard Monitoring

After successfully installing the Wazuh Manager and connecting the agent, 
the next phase involved monitoring system activity through the Wazuh Dashboard.

![Dashboard Overview](screenshots/07_dashboard_overview.png)

### Key Monitoring Activities

| Activity | Description |
|----------|-------------|
| **Agent Status Monitoring** | Verified agents are registered and communicating with Manager |
| **Security Events & Alerts** | Monitored live alerts including failed logins, process creation, and file access |
| **File Integrity Monitoring** | Observed alerts for unauthorized file modifications in critical directories |
| **System & Network Activity** | Reviewed process execution, network connections, and user activity |
| **Authentication Logs** | Identified repeated authentication failures and login anomalies |
| **Rule Correlation** | Analyzed alerts triggered by Wazuh predefined ruleset |
| **Dashboard Visualization** | Used Kibana to visualize data through bar graphs, pie charts, and timelines |
| **Incident Verification** | Cross-checked triggered alerts to confirm false positives and true incidents |

![Security Events](screenshots/08_security_events.png)

---

## Troubleshooting & Mitigation

### 1. Agent Not Connecting

**Problem:** Agent status shows disconnected or not sending logs.
```bash
# Check agent status
sudo systemctl status wazuh-agent

# Check agent logs
sudo tail -f /var/ossec/logs/ossec.log
```

**Fix:**
- Verify network connectivity to Wazuh Manager
- Check firewall ports 1514 and 1515 are open
- Re-register agent with a new key

---

### 2. Logs Not Arriving

**Problem:** No log data from agent.
```bash
# Check ossec.conf for correct log paths
sudo nano /var/ossec/etc/ossec.conf

# Check permissions
ls -la /var/log/
```

**Fix:**
- Correct file paths in ossec.conf
- Give proper read permissions to log files

---

### 3. Rules Not Triggering

**Problem:** Alerts not generated.
```bash
# Test rules
sudo /var/ossec/bin/wazuh-logtest

# Check for syntax errors
sudo /var/ossec/bin/wazuh-logtest -t
```

**Fix:**
- Fix rule syntax errors
- Restart Wazuh Manager after changes

---

### 4. Dashboard Not Showing Data

**Problem:** Wazuh dashboard shows no logs.
```bash
# Check services
sudo systemctl status wazuh-indexer
sudo systemctl status wazuh-dashboard

# Restart if needed
sudo systemctl restart wazuh-indexer
sudo systemctl restart wazuh-dashboard
```

**Fix:**
- Restart dashboard and indexer services
- Recreate missing indices if needed

---

### 5. File Integrity Monitoring Not Working

**Problem:** No alerts when files change.
```bash
# Check syscheck config
grep -A 10 "syscheck" /var/ossec/etc/ossec.conf

# Check syscheck logs
sudo tail -f /var/ossec/logs/ossec.log | grep syscheck
```

**Fix:**
- Add correct monitored directories in ossec.conf
- Restart the agent after changes

---

### 6. High CPU or Memory Usage

**Problem:** Wazuh runs slowly.
```bash
# Check system load
top
htop

# Check Wazuh processes
ps aux | grep wazuh
```

**Fix:**
- Disable unnecessary rules
- Increase RAM/CPU resources
- Tune log collection frequency

---

### 7. Active Response Not Running

**Problem:** Blocking actions or scripts not executed.
```bash
# Check active response logs
sudo tail -f /var/ossec/logs/active-responses.log

# Check script permissions
ls -la /var/ossec/active-response/bin/
```

**Fix:**
- Enable active response in ossec.conf
- Fix script execute permissions:
```bash
sudo chmod +x /var/ossec/active-response/bin/scriptname.sh
```

---

## Conclusion

Wazuh is a comprehensive open-source SIEM solution suitable for labs, 
small teams, and enterprise deployments. This project provided:

- A full overview of Wazuh architecture and features
- Practical installation steps for Kali Linux (Manager) and Parrot OS (Agent)
- Real-time monitoring and alert analysis through the Wazuh Dashboard
- Troubleshooting guidance for common issues

For production deployments, follow official Wazuh documentation for 
sizing, security hardening, and high-availability setups.

---

## References

| Resource | Link |
|----------|------|
| Wazuh Official Documentation | https://documentation.wazuh.com/ |
| Wazuh Downloads | https://wazuh.com/install/ |
| Wazuh GitHub | https://github.com/wazuh/wazuh |
| Wazuh Rules | https://github.com/wazuh/wazuh-ruleset |
| PCI-DSS Compliance | https://documentation.wazuh.com/current/compliance/pci-dss/ |

---

## Related Projects

- [Wazuh Nmap Detection](https://github.com/Satz-N-Sentry/wazuh-nmap-detection) — Custom rules to detect Nmap port scans in real time

---

*Satheesh Nithiananthan | satheeshnithiananthan@gmail.com | March 2026*
