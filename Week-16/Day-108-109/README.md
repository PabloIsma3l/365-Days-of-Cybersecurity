# 🛡️ Windows Threat Detection 3 — TryHackMe

## 📅 Day 109 - 365 Days of Cybersecurity

## ✅ Status: Completed

---

## 🧠 Overview

In this room, I developed advanced skills in **Windows threat detection**, focusing on identifying complete attack chains through **event correlation, behavioral analysis, and timeline reconstruction**.

This stage represents a transition from basic detection to a **full SOC investigation mindset**, where the objective is to understand attacker behavior across multiple stages of an intrusion.

---

## 🎯 Learning Objectives

* Detect complex, multi-stage attacks on Windows systems
* Correlate events across multiple log sources
* Analyze attacker behavior in depth
* Identify lateral movement and persistence techniques
* Perform timeline-based investigations

---

## 🪟 Key Log Sources

### 🔹 Windows Security Logs

Provide visibility into:

* Authentication activity
* Account usage
* Privilege escalation

---

### 🔹 Sysmon Logs

Provide detailed system telemetry:

* **Event ID 1** → Process creation
* **Event ID 3** → Network connections
* **Event ID 11** → File creation
* **Event ID 13** → Registry changes

📌 SOC Insight:
Sysmon enables visibility into **attacker actions across the entire attack lifecycle**.

---

## 🔎 Core Detection Concepts

### 🔹 Attack Chain Analysis

Modern detection focuses on identifying the full attack lifecycle:

1. Initial Access
2. Execution
3. Persistence
4. Lateral Movement
5. Command & Control
6. Data Exfiltration

📌 Detection requires correlating events across these stages.

---

### 🔹 Event Correlation

Single logs are not enough — detection comes from combining events.

📌 Example:

* Sysmon Event 1 → Suspicious process
* Sysmon Event 3 → External connection
* Sysmon Event 11 → File creation

➡️ Indicates **malware execution + payload delivery**

---

### 🔹 Parent-Child Process Analysis

Understanding process relationships is critical:

📌 Example:

* `winword.exe` → `powershell.exe` → `cmd.exe`

➡️ Likely malicious macro execution chain

---

### 🔹 Lateral Movement Detection

Attackers often move across systems after initial compromise.

📌 Indicators:

* Logins across multiple hosts
* Use of administrative tools
* Unusual authentication patterns

---

### 🔹 Persistence Mechanisms

Attackers maintain access through:

* Registry modifications (Sysmon 13)
* Autorun entries
* Scheduled tasks

---

### 🔹 Data Exfiltration Detection

Attackers may attempt to extract sensitive data:

* Large outbound traffic
* Repeated external connections
* Suspicious file transfers

---

## 🚨 Indicators of Compromise (IoCs)

* Suspicious multi-stage process chains
* Abnormal parent-child relationships
* Unexpected outbound network connections
* Unauthorized file creation
* Registry changes for persistence
* Unusual authentication activity across systems

---

## 🛡️ Detection Scenarios

### 🔹 Initial Compromise

* Office application spawning PowerShell
* Suspicious command-line execution

---

### 🔹 Malware Execution

* Sysmon Event 1 + abnormal process behavior
* Followed by file creation (Sysmon 11)

---

### 🔹 Lateral Movement

* Multiple logins across hosts
* Use of administrative tools

---

### 🔹 Persistence

* Registry modifications (Sysmon 13)

---

### 🔹 Command & Control (C2)

* Repeated outbound connections (Sysmon 3)

---

### 🔹 Data Exfiltration

* Large or unusual outbound traffic
* External data transfers

---

## 🔎 SOC Investigation Workflow

1. Identify suspicious activity (alert/log)
2. Correlate related events
3. Build a timeline of attacker actions
4. Identify techniques and objectives
5. Determine scope and impact

📌 Key Principle:
Detection → Correlation → Investigation → Response

---

## 🛠️ Tools & Technologies

* Windows Event Viewer
* Sysmon
* SIEM (Splunk / ELK)
* EDR solutions

---

## 🧠 Key Takeaways

* Advanced threat detection requires **full attack chain visibility**
* Event correlation is essential for accurate detection
* Sysmon provides critical insight into attacker behavior
* Lateral movement and persistence are key stages to detect
* Investigation skills are as important as detection

---

## 📌 Final Thoughts

This room helped me:

* Develop a **complete SOC investigation mindset**
* Understand how attackers move through a system
* Detect multi-stage attacks using behavioral analysis
* Reconstruct attack timelines using logs
* Think like a real SOC Analyst during incident investigations

This marks a significant step toward performing **real-world threat detection and incident response** in a SOC environment.
