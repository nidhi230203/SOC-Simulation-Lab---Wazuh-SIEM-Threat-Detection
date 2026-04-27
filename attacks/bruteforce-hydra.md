# 🔐 Brute Force Attack Analysis (Hydra)

## 📌 Objective

This test was performed to simulate a **credential brute-force attack** against the Windows endpoint and observe how effectively the SIEM detects repeated authentication failures.

The focus was to understand:

* How attack activity appears in logs
* How alerts are generated
* How patterns can be identified during analysis

---

## ⚙️ Attack Setup

* **Attacker:** Kali Linux
* **Target:** Windows 11 (Wazuh Agent + Sysmon)
* **Tool Used:** Hydra

### Command Used

```bash
hydra -l administrator -P passwords.txt <TARGET_IP> ssh
```

> `<TARGET_IP>` represents the IP address of the target Windows machine.

---

## 🧪 Attack Behavior

During execution:

* Multiple login attempts were generated rapidly
* Requests were automated using a wordlist
* Activity originated from a single source system

This behavior is clearly different from normal user login activity.

---

## 🔍 Observed Logs

### Key Indicators

* **Event ID:** 4625 (Failed Login)
* Repeated authentication failures
* High frequency of events within a short time

### SIEM Observation

* Noticeable spike in alerts during the attack
* Authentication failures dominated the dashboard
* Same source IP observed across multiple events

---

## 📊 Detection Summary

| Parameter        | Observation           |
| ---------------- | --------------------- |
| Detection Status | Successfully detected |
| Alert Volume     | High                  |
| Log Visibility   | Clear                 |
| Attack Pattern   | Identifiable          |

---

## 🧠 Analysis

The pattern of repeated failed logins indicates automated credential attempts.

Key characteristics:

* Same source system generating repeated requests
* Rapid execution with minimal delay
* No successful authentication observed

This confirms typical brute-force behavior rather than legitimate usage.

---

## 🔗 Event Correlation

```
Repeated Failed Logins (Event ID 4625)
        +
High Frequency Attempts
        +
Single Source IP
        ↓
Brute Force Attack Pattern
```

---

## 🎯 SOC Perspective

From a monitoring standpoint:

* The attack was clearly visible in both logs and alerts
* Detection worked effectively for authentication-based threats
* No signs of system compromise were observed

---

## ⚠️ Notes

* Detection relies heavily on authentication logs
* This simulation does not include evasion techniques
* Real-world attacks may use slower or distributed methods

---

## 🧾 Conclusion

The brute-force attack was successfully detected using Wazuh SIEM.

The combination of:

* Failed login events
* Alert spikes
* Repeated source activity

made it straightforward to identify the attack pattern.

This scenario demonstrates the effectiveness of SIEM systems in detecting **credential-based attacks**, while also highlighting the importance of continuous monitoring and analysis.
