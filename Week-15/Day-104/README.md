# 🛡️ Windows Threat Detection 1 — TryHackMe 

## 📅 Day 104 - 365 Days of Cybersecurity

## 🚧 Progress: 50%

---

## 🧠 Overview

In this room, I am learning how to **detect threats on Windows systems** using log analysis, event correlation, and behavioral detection techniques.

This builds on previous knowledge of **Windows Event Logs and Sysmon**, focusing on identifying real attack patterns and attacker behavior.

---

## 🎯 Learning Objectives (So far)

* Detect suspicious activity using Windows logs
* Analyze attacker behavior on Windows systems
* Correlate multiple events to identify threats
* Identify Indicators of Compromise (IoCs)
* Understand common attack techniques on Windows

---

## 🪟 Windows Threat Detection Basics

Threat detection in Windows relies on:

* **Event Logs (Security, System, Application)**
* **Sysmon Logs**
* **Behavioral Analysis**
* **Event Correlation**

📌 SOC Insight:
Single events are not enough — detection comes from **patterns and correlations**.

---

## 🔢 Key Events Used in Detection

### 🔐 Authentication Activity

* **4624** → Successful logon
* **4625** → Failed logon

📌 Detection:

* Brute force attacks
* Suspicious login activity

---

### ⚙️ Process Activity

* **4688 (Windows)** → Process creation
* **Sysmon Event ID 1** → Detailed process creation

📌 Detection:

* Suspicious processes
* Unusual parent-child relationships

---

### 🌐 Network Activity

* **Sysmon Event ID 3**

📌 Detection:

* Outbound connections
* Possible C2 communication

---

## 🔎 Detection Concepts (So far)

### 🔹 Event Correlation

Instead of analyzing single logs:

📌 Example:

* Multiple **4625** → Failed logins
* Followed by **4624** → Successful login

➡️ Indicates possible **brute force attack**

---

### 🔹 Behavioral Analysis

Focus on anomalies:

* Unusual login times
* Unknown processes
* Unexpected network connections

---

### 🔹 Parent-Child Process Relationships

Important for detecting malicious execution:

📌 Example:

* `winword.exe` → spawning `powershell.exe`

➡️ Highly suspicious behavior

---

## ⚠️ Early Indicators of Compromise (IoCs)

* Multiple failed logins
* Suspicious process execution
* Unexpected network connections
* Abnormal user behavior
* Use of administrative tools in unusual contexts

---

## 🛡️ Detection Mindset (SOC Perspective)

* Focus on **patterns, not isolated events**
* Understand **normal behavior (baseline)**
* Identify **anomalies**
* Correlate logs across different sources

---

## 🛠️ Tools & Technologies

* Windows Event Viewer
* Sysmon
* SIEM (Splunk / ELK)
* EDR tools

---

## 🧠 Key Takeaways (So far)

* Threat detection requires correlation, not single events
* Sysmon provides deeper visibility than default logs
* Process behavior is a key indicator of compromise
* Understanding attacker techniques improves detection

---

## 🚧 Status

Currently halfway through the room. Continuing to develop skills in:

* Advanced threat detection techniques
* Real-world attack scenarios
* Deep log correlation and investigation
