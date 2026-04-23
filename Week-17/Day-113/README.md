# 🐧 Linux Threat Detection 3 — TryHackMe

## 📅 Day 113 - 365 Days of Cybersecurity

## 🚧 Progress: 50%

---

## 🧠 Overview

In this room, I am advancing my Linux threat detection skills by focusing on **full attack investigation, event correlation, and attacker behavior analysis**.

This stage builds on previous rooms by combining:

* Log analysis
* Process investigation
* Attack chain reconstruction

📌 Key concept:
Detection evolves into **understanding the complete intrusion lifecycle**, not just isolated events.

---

## 🎯 Learning Objectives (So far)

* Analyze complex attack scenarios on Linux systems
* Correlate multiple data sources (logs + processes)
* Identify attacker techniques across different phases
* Detect lateral movement and persistence behavior
* Strengthen investigation workflow skills

---

## 🔍 Detection Approach

At this stage, the focus is on:

* **Attack chain reconstruction**
* **Behavioral analysis**
* **Multi-source correlation**
* **Timeline-based investigation**

📌 SOC Insight:
The goal is to answer:
➡️ *How did the attacker get in, what did they do, and what was the impact?*

---

## 🔐 Initial Access Indicators

Attackers may gain access via:

* SSH brute force
* Exploiting vulnerable services
* Stolen credentials

---

### 🔎 Detection Clues

* Failed login attempts followed by success
* Logins from unusual IP addresses
* Unexpected user sessions

---

## 🧬 Process & Execution Analysis

Tracking process execution is critical.

### 🔹 Focus Areas

* Suspicious commands
* Unusual process chains
* Parent-child relationships

📌 Example:

* Web service → shell → system commands

➡️ Indicates exploitation of a service

---

## 📦 Post-Compromise Behavior

Attackers may:

* Execute scripts
* Download tools
* Enumerate the system
* Prepare for persistence

---

### 🔎 Detection Indicators

* Scripts in `/tmp` or user directories
* Use of tools like `wget`, `curl`
* Repeated command execution

---

## 🔄 Event Correlation

Detection requires combining:

* Authentication logs
* Process activity
* File creation events

📌 Example:

1. Suspicious login
2. Script execution
3. File download
4. Command execution

➡️ Indicates active compromise

---

## 🌐 Lateral Movement (Intro)

Attackers may attempt:

* Network scanning
* Access to other systems
* Credential reuse

---

## ⚠️ Early Indicators of Compromise (IoCs)

* Suspicious login activity
* Abnormal process execution
* Unexpected scripts or binaries
* Outbound connections
* Multi-stage activity patterns

---

## 🛡️ Detection Mindset

* Focus on **patterns, not individual logs**
* Identify **attack phases**
* Correlate across multiple sources
* Think in terms of **attacker objectives**

---

## 🛠️ Tools & Technologies

* Linux CLI (`grep`, `ps`, `cat`)
* Auditd (`ausearch`)
* Linux logs (`auth.log`, `audit.log`)
* SIEM (Splunk / ELK)

---

## 🧠 Key Takeaways (So far)

* Detection requires full visibility of attack chains
* Process analysis is critical for investigation
* Correlation across logs improves detection accuracy
* Attackers operate in multiple stages
* Investigation mindset is essential for SOC roles

---

## 🚧 Status

Halfway through the room. Continuing to develop skills in:

* Full attack lifecycle analysis
* Advanced detection techniques
* Real-world SOC investigation scenarios
