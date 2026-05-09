# 🌩️ Tempest Incident — TryHackMe

## 📅 Day 129 - 365 Days of Cybersecurity

## ✅ Status: Completed

---

# 🧠 Overview

In this room, I investigated a realistic **security incident scenario** involving suspicious activity across a Windows environment.

The investigation focused on:

* Incident response workflow
* Log and telemetry analysis
* PowerShell activity
* Process correlation
* Network investigation
* Timeline reconstruction

📌 Key Concept:

Incident response is not just about detecting malware —
➡️ it is about understanding **what happened, how it happened, and what the attacker achieved**.

---

# 🎯 Learning Objectives

* Investigate a Windows security incident
* Analyze attacker behavior through logs
* Correlate process and network activity
* Identify persistence and execution techniques
* Reconstruct an attack timeline

---

# 🚨 Initial Incident Investigation

The scenario began with suspicious activity detected on a host system.

The investigation required determining:

* Initial access vector
* Commands executed
* Attacker objectives
* Scope of compromise

---

# 🔍 Windows Telemetry Analysis

Multiple telemetry sources were analyzed during the investigation.

---

## 🔹 Key Artifacts Reviewed

* Process creation events
* PowerShell logs
* Authentication activity
* Network connections
* System events

---

📌 SOC Insight:

Windows telemetry provides visibility into attacker actions and system behavior.

---

# ⚙️ PowerShell Analysis

A major focus of the investigation involved suspicious PowerShell execution.

---

## 🚨 Suspicious Indicators

* Encoded commands
* Script execution
* Obfuscation techniques
* Remote download behavior

---

## Example Suspicious Execution

```powershell id="q7m3cx"
powershell.exe -enc <base64_payload>
```

---

📌 PowerShell is frequently abused because it enables:

* In-memory execution
* Fileless techniques
* Administrative automation
* Payload delivery

---

# 🔗 Process Tree Investigation

Process lineage analysis was critical for understanding execution flow.

---

## Example Process Chain

```text id="d9t4ra"
explorer.exe
 └── powershell.exe
      └── cmd.exe
```

---

## Why It Matters

Parent-child process relationships help identify:

* Malicious execution chains
* User-driven activity
* LOLBin abuse

---

📌 Process trees are one of the most valuable investigation artifacts in SOC environments.

---

# 🌐 Network Investigation

The investigation included analysis of outbound communications.

---

## Indicators Reviewed

* Suspicious IP addresses
* Unknown domains
* External network connections
* Possible C2 traffic

---

## Investigation Goals

* Identify malicious infrastructure
* Detect beaconing behavior
* Correlate network activity with execution events

---

📌 Network telemetry often exposes attacker infrastructure and objectives.

---

# 🧬 Persistence Investigation

The attacker attempted to maintain access to the system.

---

## Common Persistence Areas Investigated

* Registry Run keys
* Startup folder entries
* Scheduled tasks
* Service creation

---

📌 Persistence analysis helps determine attacker intent and dwell time.

---

# 🔎 Timeline Reconstruction

A key DFIR skill practiced in this room:

➡️ Rebuilding the sequence of attacker actions

---

## Investigation Workflow

1. Review initial alert
2. Analyze suspicious processes
3. Investigate PowerShell execution
4. Correlate network activity
5. Identify persistence mechanisms
6. Reconstruct attacker timeline
7. Determine impact

---

📌 Core Principle:

➡️ **Events gain meaning through correlation and chronology**

---

# 🚨 Indicators of Compromise (IoCs)

## Process-Based

* Suspicious PowerShell execution
* Encoded commands
* Abnormal parent-child processes

---

## Network-Based

* External suspicious connections
* Unknown domains/IPs
* Beaconing behavior

---

## Persistence-Based

* Registry modifications
* Scheduled task creation
* Startup persistence

---

# 🛡️ Detection Opportunities

Potential detections include:

* Encoded PowerShell execution
* Office applications spawning shells
* Rare outbound connections
* Persistence modifications
* LOLBin abuse

---

# 🧪 Concepts Practiced

* Incident response workflow
* Windows telemetry analysis
* PowerShell investigation
* Process tree analysis
* Network correlation
* Timeline reconstruction
* Persistence detection

---

# 🛠️ Tools & Technologies

* Windows Event Logs
* PowerShell logging
* Process investigation techniques
* SIEM-style analysis
* Threat hunting methodology

---

# 🧠 Key Takeaways

* Correlation is essential in incident response
* PowerShell remains a major attacker tool
* Process lineage reveals execution context
* Timeline reconstruction exposes attacker behavior
* Multiple telemetry sources improve investigation accuracy

---

