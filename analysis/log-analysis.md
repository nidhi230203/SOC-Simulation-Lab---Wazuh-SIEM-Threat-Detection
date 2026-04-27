# 🧠 Log Analysis & Security Insights

## 📌 Overview

This section presents the analysis of security logs collected during the SOC lab simulation.
The goal was to examine system activity, identify abnormal patterns, and understand how different attack behaviors appear within a SIEM environment.

The dataset includes logs generated from:

* Windows 11 endpoint (Sysmon + Security Logs)
* Wazuh SIEM platform

---

## 📊 Log Volume & Activity

* Total logs analyzed: **75,000+ events**
* Observation period: **~1 month**
* Continuous event generation observed

### 🧠 Insight

* Normal system activity produced consistent logs
* Attack simulations resulted in noticeable spikes
* Log ingestion remained stable throughout

---

## ⏱️ Activity Trends

* Regular activity showed predictable logging behavior
* Brute-force attempts created sharp spikes in event volume

### Interpretation

This contrast between baseline and attack activity helps in identifying suspicious patterns during monitoring.

---

## 🔐 Authentication Event Analysis

### Observations

* Multiple failed login attempts recorded
* Event ID: **4625 (Failed Login)**
* Attempts originated repeatedly from the same source

### 🧠 Interpretation

The pattern suggests automated login attempts, consistent with a **brute-force attack scenario**.

---

## ⚡ Process Activity (PowerShell)

### Observations

* Sysmon captured process creation events
* PowerShell execution detected
* Limited number of related logs (~5–7 events)

### 🧠 Interpretation

* Indicates that process monitoring is active
* Low alert volume highlights limited detection capability under default rules

---

## 🌐 Network Activity (Reconnaissance)

### Observations

* Scanning activity performed (Nmap)
* Minimal alerts observed in SIEM

### 🧠 Interpretation

* Detection for reconnaissance activity was weak
* Suggests need for enhanced monitoring or custom rules

---

## 📊 Dashboard Correlation

From dashboard analysis:

* Alert spikes aligned with brute-force activity
* Authentication failures were the most frequent alert type

### 🧠 Insight

Visualizations help quickly identify:

* Attack timing
* Alert concentration
* Behavior patterns

---

## 🔗 Event Correlation

```text
Repeated Failed Logins (Event ID 4625)
        +
High Frequency
        +
Same Source System
        ↓
Brute Force Attack Pattern
```

---

## 🧬 MITRE ATT&CK Mapping

| Activity             | Technique         | ID    |
| -------------------- | ----------------- | ----- |
| Brute Force          | Credential Access | T1110 |
| PowerShell Execution | Command Execution | T1059 |
| Nmap Scan            | Network Discovery | T1046 |

---

## ⚠️ Detection Observations

* Brute-force activity was clearly detected
* PowerShell activity showed limited visibility
* Nmap scanning was not effectively identified

### Analysis

Detection depends on:

* SIEM rule configuration
* Log depth
* Monitoring coverage

---

## 🎯 SOC Perspective

* Authentication-based attacks are easier to detect
* Execution and reconnaissance require deeper monitoring
* SIEM effectiveness improves with tuning

---

## 🧠 Analyst Notes

From an analysis standpoint:

* The system successfully captured relevant logs
* Detection gaps were observed in certain attack phases
* These gaps are expected in default SIEM configurations

---

## 🧾 Conclusion

The log analysis demonstrates how different attack behaviors appear within a monitored environment.

While brute-force activity was clearly visible, limited detection in other areas highlights the importance of continuous tuning and deeper visibility.

This reinforces a key SOC concept:

> Effective detection is built over time through analysis and refinement.

---

## 📸 Reference

```md
![Wazuh Logs](../screenshots/logs/wazuh-discover.png)
```
