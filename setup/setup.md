# ⚙️ SOC Lab Setup Guide

## 📌 Overview

This document describes the setup of a SOC simulation environment using Wazuh SIEM to monitor and analyze security events.

The lab includes:

* A monitored Windows endpoint
* A Wazuh server for log processing
* An attacker system for simulation

---

## 🏗️ Architecture Summary

```
Kali Linux (Attacker)
        ↓
Windows 11 (Sysmon + Wazuh Agent)
        ↓
Wazuh Server (Manager + Indexer)
        ↓
Wazuh Dashboard
```

---

## 🖥️ Environment Setup

| Machine      | Role     | OS                |
| ------------ | -------- | ----------------- |
| Wazuh Server | SIEM     | Amazon Linux 2023 |
| Windows 11   | Endpoint | Windows 11        |
| Kali Linux   | Attacker | Kali Linux        |

---

## 🌐 Network Configuration

* All machines are connected using a **NAT network**
* Ensure connectivity:

```bash
ping <TARGET_IP>
```

---

## ⚙️ Step 1: Wazuh Server Setup

### 1. Import Wazuh OVA

* Import the Wazuh OVA into VMware
* Start the virtual machine

### 2. Access Dashboard

```
https://<WAZUH_SERVER_IP>
```

### 3. Verify Services

Ensure the following are running:

* Wazuh Manager
* Indexer
* Dashboard

---

## 🖥️ Step 2: Windows Endpoint Setup

### 1. Install Wazuh Agent

* Download agent from Wazuh dashboard
* Install on Windows machine

### 2. Configure Agent

Edit:

```
C:\Program Files (x86)\ossec-agent\ossec.conf
```

Add:

```xml
<address><WAZUH_SERVER_IP></address>
```

---

### 3. 🔐 Register Agent

```powershell
"C:\Program Files (x86)\ossec-agent\agent-auth.exe" -m <WAZUH_SERVER_IP>
```

---

### 4. Start Agent

```powershell
net start wazuh-agent
```

---

## 🔍 Step 3: Sysmon Configuration

### 1. Download Sysmon

Download from Microsoft official source.

### 2. Use Recommended Config

https://github.com/SwiftOnSecurity/sysmon-config

### 3. Install Sysmon

```powershell
Sysmon64.exe -i sysmonconfig.xml
```

### 4. Purpose

Sysmon provides:

* Process creation logs
* Network activity
* System-level visibility

---

## 🐉 Step 4: Kali Linux Setup

* Ensure Kali is on the same network
* Verify connectivity with Windows

### Tools Used

* Hydra
* Nmap

---

## 🧠 Step 5: Detection-Oriented Setup

### 🎯 Detection Goals

* Detect brute-force login attempts
* Monitor PowerShell activity
* Observe reconnaissance behavior

---

## 🔍 Verification

* Logs should appear in Wazuh Dashboard
* Check:

  * Event ID 4625 (Failed Login)
  * Sysmon process events

---

## ⚠️ Common Issues

* Agent not connecting → run agent-auth
* No logs visible → check Sysmon + restart agent
* Weak detection → requires tuning

---

## ✅ Final Checklist

* [ ] Dashboard accessible
* [ ] Agent connected
* [ ] Sysmon active
* [ ] Logs visible
* [ ] Alerts generated

---

## 🎯 Conclusion

The setup establishes a working SOC pipeline for log collection, processing, and visualization using Wazuh.

This environment helps in understanding:

* How logs are generated
* How attacks are detected
* How SIEM systems operate in practice
