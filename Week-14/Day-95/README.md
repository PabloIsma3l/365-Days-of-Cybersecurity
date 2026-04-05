# 🕶️ Man-in-the-Middle Detection — TryHackMe (Completed)DAY 95

## 📌 Overview

This repository documents the completion of the **Man-in-the-Middle (MitM) Detection** room on TryHackMe.

This room focuses on identifying and detecting MitM attacks, where an attacker intercepts and potentially alters communication between two parties without their knowledge.

---

## 🎯 Learning Objectives Achieved

✔ Understand Man-in-the-Middle attack techniques
✔ Identify indicators of interception in network traffic
✔ Detect ARP spoofing and traffic manipulation
✔ Analyze anomalies in communication patterns
✔ Apply detection techniques in SOC environments

---

## 🧠 What is a Man-in-the-Middle Attack?

A MitM attack occurs when an attacker secretly intercepts and possibly modifies communication between two systems.

Common goals:

* Steal credentials
* Capture sensitive data
* Manipulate communications

---

## ⚠️ Common MitM Techniques

### 🔹 ARP Spoofing / Poisoning

* Attacker associates their MAC with another IP

📌 Indicator:

* Multiple MAC addresses for the same IP

---

### 🔹 DNS Spoofing

* Redirects victims to malicious domains

📌 Indicator:

* Incorrect DNS responses

---

### 🔹 SSL Stripping

* Downgrades HTTPS to HTTP

📌 Indicator:

* Unexpected HTTP traffic instead of HTTPS

---

## 📊 Task Breakdown & Examples

### 🧩 Task 1–2: Introduction

* Understood MitM concepts
* Reviewed attack scenarios

---

### 🌐 Task 3: ARP Analysis

📌 Example:

* Duplicate ARP replies
* Same IP mapped to different MACs

---

### 🔎 Task 4: Traffic Inspection

📌 Example:

* Unexpected traffic routing
* Intercepted packets between hosts

---

### 🧪 Task 5: Protocol Anomalies

📌 Example:

* HTTP instead of HTTPS
* Modified responses

---

### 🚨 Task 6: Detection Indicators

📌 Indicators:

* ARP inconsistencies
* Certificate warnings
* Unexpected traffic paths

---

### 🧠 Task 7: Investigation Scenario

📌 Workflow:

1. Identify suspicious host
2. Analyze ARP traffic
3. Check protocol anomalies
4. Validate certificates
5. Confirm interception

---

## 🚨 Indicators of Compromise (IOCs)

* Duplicate ARP responses
* MAC/IP inconsistencies
* Unexpected HTTP traffic
* Suspicious DNS responses
* Certificate warnings

---

## 🛠️ Detection Techniques

* Wireshark (ARP, DNS, HTTP analysis)
* Network monitoring tools
* SIEM correlation
* IDS/IPS alerts

---

## 🧩 MITRE ATT&CK Mapping

* **TA0006 – Credential Access**
* **TA0009 – Collection**

  * T1557 → Adversary-in-the-Middle

---

## 🧠 SOC Perspective

SOC analysts detect MitM attacks by:

* Monitoring ARP traffic
* Identifying anomalies in communication
* Investigating alerts related to spoofing

---

## 🏁 Room Completion Status

* ✅ All tasks completed
* 🧠 Strong understanding of MitM detection achieved

---

## 🚀 Key Takeaways

* MitM attacks rely on interception and deception
* ARP spoofing is a common technique
* Traffic anomalies reveal attacker presence
* Early detection prevents data compromise

---

🧠 *Room completed as part of my Blue Team, SOC & Network Security training path.*
