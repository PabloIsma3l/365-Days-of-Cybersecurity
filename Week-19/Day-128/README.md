# 🛡️ Benign — TryHackMe

## 📅 Day 128 - 365 Days of Cybersecurity

## ✅ Status: Completed

---

# 🧠 Overview

In this room, I performed a full **SOC/DFIR-style investigation** focused on identifying suspicious activity within a Windows environment.

The investigation involved:

* Log analysis
* PowerShell investigation
* Process correlation
* Threat hunting techniques
* Timeline reconstruction

📌 Key Concept:

Not all suspicious activity is immediately malicious —
➡️ analysts must investigate deeply before reaching conclusions.

---

# 🎯 Learning Objectives

* Investigate suspicious Windows activity
* Analyze PowerShell execution
* Correlate logs and process activity
* Perform threat hunting techniques
* Reconstruct attacker behavior through telemetry

---

# 🔍 Investigation Scenario

The room simulated a real-world SOC case where analysts needed to determine whether observed activity was:

* Benign
* Suspicious
* Malicious

This required:

* Reviewing logs
* Investigating process execution
* Correlating multiple artifacts

---

# ⚙️ PowerShell Investigation

A major focus of the room was analyzing PowerShell activity.

---

## 🚨 Suspicious Indicators

* Encoded commands
* Obfuscated scripts
* Unusual execution patterns
* Network-related PowerShell activity

---

## Example Suspicious Command

```powershell id="u7m3ra"
powershell.exe -enc <base64_payload>
```

---

📌 SOC Insight:

PowerShell is one of the most abused Windows tools because it enables:

* Remote execution
* Automation
* Fileless attacks
* In-memory payload execution

---

# 🔗 Process Correlation

The investigation required analyzing process relationships.

---

## Example Process Tree

```text id="n4c8xt"
explorer.exe
 └── powershell.exe
```

Additional suspicious chains may indicate:

* User execution
* Script launch
* Malware activity

---

📌 Parent-child process analysis is critical for understanding attacker behavior.

---

# 🧬 Threat Hunting Concepts

This room introduced practical threat hunting techniques.

---

## 🔹 Hunting Goals

* Identify abnormal behavior
* Detect suspicious execution patterns
* Search for indicators across logs

---

## Example Hunting Areas

* PowerShell logs
* Process creation events
* User activity
* Network indicators

---

📌 Threat hunting focuses on proactively identifying malicious behavior.

---

# 🌐 Network Activity Analysis

Investigation included reviewing:

* External connections
* Suspicious IPs/domains
* Potential command-and-control activity

---

## Indicators Reviewed

* Rare destinations
* Unexpected outbound communication
* Connections initiated by suspicious processes

---

📌 Network telemetry often reveals attacker infrastructure.

---

# 🛠️ Log Analysis

Logs analyzed included:

* Process execution logs
* PowerShell logs
* Authentication events
* System activity

---

## Key Investigation Questions

* What executed?
* Who executed it?
* When did it happen?
* Was the activity expected?

---

# 🔎 Timeline Reconstruction

A major SOC skill practiced:

➡️ Building a sequence of events

---

## Investigation Flow

1. Identify suspicious activity
2. Analyze PowerShell execution
3. Correlate process activity
4. Investigate network connections
5. Reconstruct attacker timeline
6. Determine impact

---

📌 Timeline reconstruction is essential in incident response.

---

# 🚨 Indicators of Suspicious Activity

## Process-Based

* PowerShell execution
* Encoded commands
* Unusual child processes

---

## Network-Based

* Connections to suspicious IPs
* Rare outbound communication

---

## Behavioral

* Obfuscation
* Script execution anomalies
* Suspicious execution context

---

# 🛡️ Detection Opportunities

Potential detection logic:

* Encoded PowerShell execution
* PowerShell spawned from unusual parents
* Suspicious outbound traffic
* Rare process execution patterns

---

# 🧪 Concepts Practiced

* Threat hunting
* PowerShell analysis
* Process tree investigation
* Log correlation
* Timeline reconstruction
* SOC investigation methodology

---

# 🛠️ Tools & Technologies

* Windows logs
* PowerShell logging
* SIEM-style analysis
* Process investigation techniques
* Threat hunting concepts

---

# 🧠 Key Takeaways

* PowerShell activity requires careful investigation
* Correlation is essential for accurate conclusions
* Threat hunting is proactive, not reactive
* Timeline reconstruction helps reveal attacker behavior
* Analysts must distinguish benign from malicious activity

---

