# ⚔️ Cyber Kill Chain — Day 69

## 📌 Overview

This document summarizes the concepts learned in the **"Cyber Kill Chain"** room on TryHackMe.

The **Cyber Kill Chain**, developed by Lockheed Martin, is a framework used to understand the stages of a cyber attack. It helps defenders detect, analyze, and prevent intrusions by identifying attacker behavior at each phase of the attack lifecycle.

Understanding the kill chain allows SOC analysts and security teams to detect threats earlier and disrupt attacks before they succeed.

---

## 🎯 Learning Objectives

* Understand the Cyber Kill Chain framework
* Learn the different phases of a cyber attack
* Identify attacker behavior during each stage
* Understand how defenders can disrupt attacks at different phases

---

## 🧠 What is the Cyber Kill Chain?

The **Cyber Kill Chain** is a model that describes the stages an attacker typically follows when carrying out a cyber intrusion.

By understanding these stages, defenders can detect malicious activity earlier and stop attacks before they reach their objective.

The model contains **seven phases**.

---

## 🔗 The 7 Phases of the Cyber Kill Chain

### 1️⃣ Reconnaissance

The attacker gathers information about the target.

Examples:

* Collecting employee information
* Scanning networks
* Identifying exposed services

Common techniques:

* OSINT
* Network scanning
* Social media research

---

### 2️⃣ Weaponization

The attacker creates the malicious payload used in the attack.

Examples:

* Malware development
* Exploit creation
* Malicious document preparation

Often combines:

* Exploit + malware

---

### 3️⃣ Delivery

The attacker delivers the malicious payload to the victim.

Common delivery methods:

* Phishing emails
* Malicious attachments
* Drive‑by downloads
* USB devices

---

### 4️⃣ Exploitation

The vulnerability is exploited to execute the malicious payload.

Examples:

* Exploiting software vulnerabilities
* Running malicious macros
* Exploiting browser vulnerabilities

---

### 5️⃣ Installation

Malware is installed on the victim system.

Examples:

* Backdoors
* Remote access trojans (RATs)
* Persistence mechanisms

The attacker ensures continued access to the compromised system.

---

### 6️⃣ Command and Control (C2)

The compromised system communicates with the attacker's infrastructure.

Examples:

* Connecting to a C2 server
* Receiving attacker commands
* Sending stolen data

---

### 7️⃣ Actions on Objectives

The attacker performs the final actions to achieve their goals.

Examples:

* Data exfiltration
* Privilege escalation
* Lateral movement
* System destruction

---

## 🛡️ How Defenders Use the Kill Chain

Security teams use the Cyber Kill Chain to:

* Detect threats early in the attack lifecycle
* Improve threat hunting strategies
* Design defensive security controls
* Disrupt attacks before they succeed

Examples:

* Email filtering to stop **Delivery**
* Vulnerability patching to prevent **Exploitation**
* Network monitoring to detect **Command and Control**

---

## 📊 Cyber Kill Chain vs Modern Frameworks

While the Cyber Kill Chain focuses on the **attack lifecycle**, modern frameworks like **MITRE ATT&CK** provide a more detailed view of attacker techniques.

Both models are often used together in security operations.

---
