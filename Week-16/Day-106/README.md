# 🛡️ Windows Threat Detection 2 — TryHackMe

## 📅 Day 106 - 365 Days of Cybersecurity

## 🚧 Progress: 50%

---

## 🧠 Overview

In this room, I am advancing my skills in **Windows threat detection**, focusing on deeper analysis of attacker techniques, event correlation, and identifying more sophisticated behaviors.

This builds upon previous knowledge of **Windows Event Logs, Sysmon, and basic detection techniques**, moving toward a more **real-world SOC investigation approach**.

---

## 🎯 Learning Objectives (So far)

* Detect advanced threats on Windows systems
* Correlate multiple log sources for investigation
* Identify attacker techniques and behaviors
* Analyze complex attack patterns
* Improve detection accuracy using context

---

## 🪟 Detection Approach

Threat detection at this stage focuses on:

* **Event correlation**
* **Behavioral analysis**
* **Process relationships**
* **Timeline reconstruction**

📌 SOC Insight:
Detection is no longer about “what happened”, but **how and why it happened**.

---

## 🔢 Key Log Sources

### 🔹 Windows Security Logs

* Authentication events
* Account changes
* Privilege usage

---

### 🔹 Sysmon Logs

* Process creation (Event ID 1)
* Network connections (Event ID 3)
* File creation (Event ID 11)
* Registry changes (Event ID 13)

📌 Critical for detecting advanced attacker activity

---

## 🔎 Detection Concepts (So far)

### 🔹 Event Correlation

Combining multiple events to identify an attack chain.

📌 Example:

* Sysmon Event 1 → Suspicious process
* Sysmon Event 3 → External connection

➡️ Possible malware execution with C2 communication

---

### 🔹 Process Injection & Abuse

Attackers may:

* Inject code into legitimate processes
* Abuse trusted binaries (LOLBins)

📌 Indicators:

* Unusual parent-child relationships
* Unexpected process behavior

---

### 🔹 Living-off-the-Land (LOLBins)

Use of legitimate tools for malicious purposes:

Examples:

* `powershell.exe`
* `cmd.exe`
* `wmic.exe`

📌 Detection:

* Suspicious command-line usage
* Execution in unusual contexts

---

### 🔹 Timeline Analysis

Understanding attack flow:

1. Initial access
2. Execution
3. Persistence
4. Communication

📌 SOC Insight:
Building timelines helps identify the full scope of compromise

---

## ⚠️ Early Indicators of Compromise (IoCs)

* Suspicious command-line arguments
* Execution of administrative tools in unusual contexts
* Unexpected outbound connections
* Multiple related suspicious events
* Abnormal process chains

---

## 🛡️ Detection Mindset

* Focus on **behavior over signatures**
* Look for **chains of activity**
* Identify **anomalies vs baseline**
* Understand attacker intent

---

## 🛠️ Tools & Technologies

* Windows Event Viewer
* Sysmon
* SIEM (Splunk / ELK)
* EDR tools

---

## 🧠 Key Takeaways (So far)

* Advanced detection requires correlation and context
* Attackers often use legitimate tools (LOLBins)
* Process relationships are critical for detection
* Timeline analysis is key for investigations
* Detection is about understanding attacker behavior

---

## 🚧 Status

Currently halfway through the room. Continuing to develop skills in:

* Advanced attack detection techniques
* Full attack chain analysis
* Real-world investigation scenarios
