# 🧬 Unified Kill Chain  Day 70

## 📌 Overview

This document summarizes the knowledge gained from completing the **"Unified Kill Chain"** room on TryHackMe.

The **Unified Kill Chain (UKC)** is a modern cybersecurity framework that expands on the traditional Cyber Kill Chain by combining multiple attacker models. It provides a more comprehensive view of how cyber attacks progress across different phases and environments.

The framework helps defenders detect and disrupt attackers at multiple stages of an intrusion.

---

## 🎯 Learning Objectives

* Understand the concept of the Unified Kill Chain
* Learn how it expands the traditional Cyber Kill Chain
* Identify attacker behavior across different stages
* Understand how defenders can interrupt attacks earlier

---

## 🧠 What is the Unified Kill Chain?

The **Unified Kill Chain** is a security model designed to describe the full lifecycle of modern cyber attacks.

Unlike the traditional Cyber Kill Chain, the Unified Kill Chain integrates:

* The **Cyber Kill Chain**
* The **MITRE ATT&CK framework**

This provides defenders with a broader view of attacker behavior and helps improve threat detection and response.

---

## 🔗 Main Phases of the Unified Kill Chain

The Unified Kill Chain organizes attacker activity into **three major stages**.

### 1️⃣ Initial Foothold

This stage represents how attackers gain their first access to a system or network.

Examples:

* Phishing attacks
* Exploiting public-facing applications
* Credential theft
* Drive-by downloads

Security controls at this stage may include:

* Email security gateways
* Web filtering
* Endpoint protection

---

### 2️⃣ Network Propagation

After gaining access, attackers attempt to move through the network and expand their control.

Examples:

* Privilege escalation
* Lateral movement
* Credential dumping
* Persistence mechanisms

Detection at this stage often relies on:

* EDR solutions
* SIEM monitoring
* Behavioral detection

---

### 3️⃣ Action on Objectives

This final phase represents the attacker achieving their ultimate goals.

Examples:

* Data exfiltration
* Ransomware deployment
* System sabotage
* Intelligence collection

Defensive strategies focus on:

* Data loss prevention (DLP)
* Network monitoring
* Incident response procedures

---

## 🛡️ Why the Unified Kill Chain Matters

The Unified Kill Chain helps security teams:

* Understand modern attacker behavior
* Detect attacks earlier in the lifecycle
* Improve threat hunting capabilities
* Align detection with MITRE ATT&CK techniques

It provides a **more realistic representation of modern attacks** compared to older models.

---

## 📊 Cyber Kill Chain vs Unified Kill Chain

| Feature     | Cyber Kill Chain     | Unified Kill Chain          |
| ----------- | -------------------- | --------------------------- |
| Focus       | Linear attack stages | Expanded attacker lifecycle |
| Model Type  | Traditional          | Modern hybrid framework     |
| Integration | Standalone           | Integrates MITRE ATT&CK     |
| Detection   | Stage-based          | Behavior-based              |

---
