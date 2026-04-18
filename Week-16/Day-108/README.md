# 🛡️ Windows Threat Detection 3 — TryHackMe

## 📅 Day 108 - 365 Days of Cybersecurity

## 🚧 Progress: 50%

---

## 🧠 Overview

In this room, I am continuing to develop advanced **Windows threat detection skills**, focusing on deeper investigation techniques, attack chain analysis, and identifying more sophisticated attacker behaviors.

This stage builds on previous knowledge of **Windows logs, Sysmon, and event correlation**, moving closer to a **real-world SOC investigation workflow**.

---

## 🎯 Learning Objectives (So far)

* Detect complex attack patterns on Windows systems
* Correlate multiple events across different log sources
* Analyze attacker behavior in depth
* Identify multi-stage attack chains
* Strengthen investigation and analytical skills

---

## 🪟 Detection Approach

At this level, detection focuses on:

* **Full attack chain visibility**
* **Behavioral analysis**
* **Event correlation across multiple sources**
* **Timeline reconstruction**

📌 SOC Insight:
The goal is not just detecting alerts, but **understanding the entire attack lifecycle**.

---

## 🔢 Key Log Sources

### 🔹 Windows Security Logs

* Authentication events
* Account activity
* Privilege changes

---

### 🔹 Sysmon Logs

* **Event ID 1** → Process creation
* **Event ID 3** → Network connections
* **Event ID 11** → File creation
* **Event ID 13** → Registry changes

📌 Critical for tracking attacker actions step by step

---

## 🔎 Detection Concepts (So far)

### 🔹 Multi-Stage Attack Detection

Attackers operate in phases:

1. Initial access
2. Execution
3. Persistence
4. Lateral movement
5. Command & Control

📌 Detection requires correlating events across all stages

---

### 🔹 Advanced Process Analysis

* Tracking suspicious process chains
* Identifying abnormal parent-child relationships

📌 Example:

* `explorer.exe` → `powershell.exe` → external connection

➡️ Possible malicious execution

---

### 🔹 Lateral Movement Indicators

Attackers may move within the network:

* Use of administrative tools
* Remote execution techniques

📌 Indicators:

* Logins across multiple systems
* Unusual authentication patterns

---

### 🔹 Data Exfiltration Awareness

Attackers may attempt to extract data:

* Large outbound traffic
* Suspicious file transfers
* External connections

---

## ⚠️ Early Indicators of Compromise (IoCs)

* Suspicious process chains
* Multiple related events across systems
* Unusual authentication patterns
* Unexpected outbound connections
* Abnormal user or system behavior

---

## 🛡️ Detection Mindset

* Focus on **attack chains, not isolated alerts**
* Identify **patterns over time**
* Correlate events across different systems
* Understand attacker intent and movement

---

## 🛠️ Tools & Technologies

* Windows Event Viewer
* Sysmon
* SIEM (Splunk / ELK)
* EDR solutions

---

## 🧠 Key Takeaways (So far)

* Advanced detection requires full visibility of attack chains
* Attackers operate in multiple stages
* Correlation across logs is essential
* Behavioral analysis improves detection accuracy
* Investigation skills are critical for SOC roles

---

## 🚧 Status

Currently halfway through the room. Continuing to develop skills in:

* Full attack lifecycle detection
* Lateral movement analysis
* Real-world investigation scenarios
