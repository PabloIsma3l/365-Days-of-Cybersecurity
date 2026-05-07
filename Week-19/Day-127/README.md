# 🕷️ ItsyBitsy — TryHackMe

## 📅 Day 127 - 365 Days of Cybersecurity

## ✅ Status: Completed

---

# 🧠 Overview

In this room, I investigated a security incident involving:

* Phishing delivery
* Malicious attachments
* PowerShell abuse
* Malware execution
* Persistence mechanisms

The room simulated a real SOC investigation where multiple artifacts had to be analyzed and correlated to reconstruct attacker activity.

📌 Key Concept:

Incident response is about **connecting events into a complete attack timeline**.

---

# 🎯 Learning Objectives

* Investigate phishing-based attacks
* Analyze malicious PowerShell activity
* Detect persistence mechanisms
* Correlate logs and artifacts
* Reconstruct attacker behavior

---

# 📧 Initial Access — Phishing

The attack started with a phishing email containing a malicious attachment.

---

## 🚨 Common Indicators

* Suspicious sender
* Social engineering language
* Malicious attachment
* User interaction leading to execution

---

📌 SOC Insight:

Phishing remains one of the most common initial access vectors.

---

# ⚙️ Malicious Execution

After execution, suspicious activity was observed involving PowerShell.

---

## 🔹 PowerShell Abuse

Indicators included:

* Encoded commands
* Script execution
* Suspicious child processes

---

## Example Suspicious Activity

```powershell id="r7p3xm"
powershell.exe -enc <base64_payload>
```

---

📌 PowerShell is frequently abused because it is:

* Trusted
* Powerful
* Present by default on Windows systems

---

# 🔗 Process Chain Analysis

A critical investigation skill practiced in this room was:

➡️ Parent-child process analysis

---

## Example Attack Chain

```text id="m8x4ct"
outlook.exe
 └── winword.exe
      └── powershell.exe
```

---

📌 This process lineage strongly indicates phishing-based compromise.

---

# 🧬 Persistence Mechanisms

The attacker established persistence after execution.

---

## 🔹 Common Persistence Indicators

* Registry Run keys
* Startup folder modifications
* Scheduled tasks

---

## Investigation Focus

* What was modified?
* When was persistence created?
* Which process initiated it?

---

📌 Persistence allows attackers to survive reboots and maintain access.

---

# 🌐 Network Activity

The malware generated outbound communication.

---

## Indicators Investigated

* Suspicious domains
* External IP connections
* Potential C2 traffic

---

📌 Outbound connections can reveal:

* Payload delivery
* Beaconing
* Data exfiltration

---

# 🔍 Log & Artifact Correlation

This room required correlating multiple evidence sources:

* Process execution
* PowerShell logs
* Network indicators
* Persistence artifacts

---

## 🧠 Investigation Workflow

1. Analyze phishing entry point
2. Review process execution
3. Identify PowerShell abuse
4. Investigate persistence
5. Correlate network activity
6. Build attack timeline

---

📌 Core SOC Skill:

➡️ **Correlation across multiple telemetry sources**

---

# 🚨 Indicators of Compromise (IoCs)

## File-Based

* Suspicious attachment
* Malicious scripts

---

## Process-Based

* PowerShell execution
* Encoded commands
* Suspicious child processes

---

## Network-Based

* External malicious domains
* Suspicious outbound traffic

---

## Persistence-Based

* Registry modifications
* Startup persistence

---

# 🛡️ Detection Opportunities

Possible detection logic:

* Office applications spawning PowerShell
* Encoded PowerShell commands
* Persistence modifications
* Suspicious outbound communication

---

# 🧪 Concepts Practiced

* Phishing investigation
* Process tree analysis
* PowerShell abuse detection
* Persistence analysis
* Attack-chain reconstruction
* SOC investigation workflow

---

# 🛠️ Tools & Technologies

* Windows logs
* PowerShell analysis
* Process investigation
* Threat intelligence concepts
* SIEM-style investigation workflow

---

# 🧠 Key Takeaways

* Phishing often leads to PowerShell abuse
* Process lineage is critical in investigations
* Persistence mechanisms reveal attacker objectives
* Correlation is essential for accurate incident analysis
* Incident response requires timeline reconstruction

---

