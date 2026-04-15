# 🛡️ Windows Threat Detection 1 — TryHackMe

## 📅 Day 105 - 365 Days of Cybersecurity

## ✅ Status: Completed

---

## 🧠 Overview

In this room, I learned how to **detect threats on Windows systems** using event logs, Sysmon data, and event correlation techniques.

The focus is on identifying attacker behavior rather than isolated events, which is a critical mindset for a **SOC Level 1 Analyst**.

This room builds on Windows logging fundamentals and introduces real-world detection scenarios.

---

## 🎯 Learning Objectives

* Detect malicious activity using Windows Event Logs
* Leverage **Sysmon** for deeper visibility
* Correlate multiple events to identify attacks
* Understand attacker techniques on Windows systems
* Identify Indicators of Compromise (IoCs)

---

## 🪟 Key Log Sources

### 🔹 Windows Security Logs

Provide visibility into:

* Authentication activity
* Account changes
* Privilege usage

---

### 🔹 Sysmon Logs

Provide enhanced telemetry:

* Process execution
* Network connections
* File creation
* Registry changes

📌 SOC Insight:
Sysmon is essential for detecting **advanced threats and attacker behavior**.

---

## 🔢 Important Event IDs

### 🔐 Authentication Events

* **4624** → Successful logon
* **4625** → Failed logon

📌 Detection:

* Brute force attacks
* Unauthorized access attempts

---

### ⚙️ Process Execution

* **4688 (Windows)** → Process creation
* **Sysmon Event ID 1** → Detailed process creation

📌 Detection:

* Suspicious processes
* Malicious scripts or binaries

---

### 🌐 Network Connections

* **Sysmon Event ID 3**

📌 Detection:

* Outbound connections
* Command & Control (C2) activity

---

### 📁 File & Persistence Activity

* **Sysmon Event ID 11** → File creation
* **Sysmon Event ID 13** → Registry modification

📌 Detection:

* Malware drops
* Persistence mechanisms

---

## 🔎 Detection Techniques

### 🔹 Event Correlation

Single events are not enough — detection comes from combining multiple events.

📌 Example:

* Multiple **4625** (failed logins)
* Followed by **4624** (successful login)

➡️ Indicates a **brute force attack**

---

### 🔹 Parent-Child Process Analysis

Analyzing process relationships is key:

📌 Example:

* `winword.exe` → `powershell.exe`

➡️ Suspicious behavior (possible macro-based attack)

---

### 🔹 Behavioral Analysis

Focus on anomalies such as:

* Unusual login times
* Unexpected processes
* Unknown network connections

---

## 🚨 Indicators of Compromise (IoCs)

* High number of failed login attempts
* Successful login after multiple failures
* Suspicious command-line executions
* Unknown processes spawning from legitimate ones
* Outbound connections to external IPs
* Registry modifications for persistence

---

## 🛡️ Detection Scenarios

### 🔹 Brute Force Attack

* Multiple **4625**
* Followed by **4624**

---

### 🔹 Malicious Execution

* Suspicious **4688 / Sysmon Event 1**
* Abnormal parent-child processes

---

### 🔹 C2 Communication

* **Sysmon Event 3**
* Repeated outbound connections

---

### 🔹 Persistence Mechanism

* **Sysmon Event 13**
* Registry autorun keys modified

---

## 🔎 SOC Perspective

In a real SOC environment:

* Logs are centralized in a **SIEM**
* Alerts are generated based on correlation rules
* Analysts investigate patterns, not isolated events
* Context is critical for accurate detection

---

## 🛠️ Tools & Technologies

* Windows Event Viewer
* Sysmon
* SIEM (Splunk / ELK)
* EDR solutions

---

## 🧠 Key Takeaways

* Threat detection is based on **event correlation**
* Sysmon significantly improves visibility
* Process and network activity are critical indicators
* Understanding attacker behavior is essential
* Logs are the foundation of detection and response

---

## 📌 Final Thoughts

This room helped me:

* Think like a SOC Analyst when analyzing Windows systems
* Detect real attack patterns using logs
* Understand how attackers operate and persist
* Correlate multiple data sources to identify threats

This is a key step toward performing real-world threat detection in a SOC environment.
