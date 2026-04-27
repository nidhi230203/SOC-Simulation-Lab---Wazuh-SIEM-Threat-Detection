# SOC-Simulation-Lab---Wazuh-SIEM-Threat-Detection
Hands-on SOC lab using Wazuh SIEM for threat detection, log analysis, and event correlation across 100,000+ security events.
# 🛡️ SOC Simulation Lab – SIEM-Based Threat Detection

## 📌 Overview

This project demonstrates a **Security Operations Center (SOC) simulation lab** designed to analyze real-world attack behavior using Wazuh SIEM.

The lab environment collects endpoint telemetry, generates security events, and enables investigation of attack patterns through dashboards and log analysis.

> 🎯 Goal: Understand how attacks appear in logs and how SIEM tools help in detecting them.

---

## 🚨 Key Highlights

* Analyzed **75,000+ security events over ~1 month**
* Successfully detected **brute-force authentication activity**
* Identified **detection gaps in reconnaissance and execution stages**
* Focused on **log analysis and alert correlation**

---

## 🏗️ Architecture

```
Kali Linux (Attacker)
        ↓
Windows 11 (Sysmon + Wazuh Agent)
        ↓
Wazuh Manager (Amazon Linux 2023)
        ↓
Wazuh Dashboard (SIEM)
        ↓
Log Analysis & Monitoring
```

---

## ⚙️ Tech Stack

| Layer               | Technology        |
| ------------------- | ----------------- |
| SIEM                | Wazuh             |
| Endpoint Monitoring | Sysmon            |
| Target System       | Windows 11        |
| Attacker System     | Kali Linux        |
| Server OS           | Amazon Linux 2023 |
| Virtualization      | VMware            |

---

## 🚨 Attack Scenarios

### 🔐 Brute Force (Hydra)

* High-frequency login attempts
* Event ID **4625 (Failed Login)**
* Clear alert spikes observed

**Result:**
✔ Successfully detected

---

### 🌐 Reconnaissance (Nmap)

* Port scanning activity
* Sequential probing behavior

**Result:**
⚠ Limited detection observed

**Insight:**
Highlights the need for SIEM rule tuning

---

### ⚡ PowerShell Activity

* Sysmon Event ID **1 (Process Creation)**
* Limited number of events recorded

**Result:**
⚠ Low detection visibility

**Insight:**
Baseline logging exists, but detection coverage is limited

---

## 📊 Dashboard Preview

![Alerts Over Time](screenshots/Alerts%20Over%20Time.png)

![Alerts by Severity](screenshots/Alerts%20by%20Severity.png)

![Top Attack Types](screenshots/Top%20Attack%20Types.png)

---

## 🔍 Key Findings

* Stable log generation under normal activity
* Significant spikes during brute-force attacks
* Authentication failures dominated alert data

---

## ⚠️ Detection Limitations

* Nmap reconnaissance not clearly detected
* PowerShell activity produced limited alerts

### Analysis

Detection effectiveness depends on:

* Rule configuration
* Log quality
* SIEM tuning

---

## 🧠 Event Correlation

```
Repeated Failed Logins (4625)
        +
High Frequency
        +
Same Source IP
        ↓
Brute Force Pattern
```

---

## 🧬 MITRE ATT&CK Mapping

| Technique         | ID    |
| ----------------- | ----- |
| Brute Force       | T1110 |
| Command Execution | T1059 |
| Network Discovery | T1046 |

---

## 📂 Project Structure

```
.
├── architecture/
├── setup/
├── attacks/
├── analysis/
├── screenshots/
├── report/
└── README.md
```

---

## 🛠️ Setup Summary

* Wazuh deployed using OVA
* Windows agent configured and connected
* Sysmon enabled for endpoint visibility
* Kali Linux used for attack simulation

---

## 📄 Detailed Report

📥 [Download SOC Incident Report](report//SOC%20INCIDENT%20ANALYSIS%20REPORT.docx)

---

## 🎯 Why This Project Matters

This lab demonstrates:

* Practical SIEM usage
* Log-based threat detection
* Understanding of detection gaps

> Reflects how real SOC environments rely on continuous monitoring and tuning

---

## 📈 Future Improvements

* Custom detection rules
* Enhanced PowerShell monitoring
* Threat intelligence integration
* Network-level visibility (Zeek)

---

## ⭐ Final Note

This project highlights both detection capabilities and limitations, providing a realistic view of SOC operations and SIEM-based monitoring.
