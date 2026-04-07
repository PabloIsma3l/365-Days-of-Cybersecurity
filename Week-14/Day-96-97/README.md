##  🐷 Snort Fundamentals — TryHackMe (Completed) DAY 97

## 📌 Overview

This repository documents the completion of the **Snort Fundamentals** room on TryHackMe.

This room focuses on using **Snort**, an open-source Network Intrusion Detection and Prevention System (IDS/IPS), to detect malicious network activity through rule-based analysis.

---

## 🎯 Learning Objectives Achieved

✔ Understand how Snort works
✔ Learn IDS vs IPS concepts
✔ Analyze traffic using Snort
✔ Write and understand Snort rules
✔ Detect malicious activity using signatures

---

## 🧠 What is Snort?

Snort is a **signature-based IDS/IPS** that analyzes network traffic and generates alerts when it detects suspicious patterns.

It can operate in three modes:

* Sniffer Mode → Reads packets and displays them
* Packet Logger Mode → Logs packets to files
* IDS Mode → Detects malicious traffic using rules

---

## ⚙️ Snort Modes Examples

### 🔹 Sniffer Mode

```bash
snort -v
```

Displays packet headers in real time.

---

### 🔹 Packet Logger Mode

```bash
snort -dev -l ./logs
```

Logs packets for later analysis.

---

### 🔹 IDS Mode

```bash
snort -c /etc/snort/snort.conf -A console
```

Uses rules to detect suspicious activity.

---

## 🧩 Snort Rule Structure

Basic rule format:

```bash
action protocol src_ip src_port -> dst_ip dst_port (options)
```

### 🔹 Example Rule

```bash
alert tcp any any -> any 80 (msg:"HTTP Traffic Detected"; sid:1000001;)
```

📌 Explanation:

* alert → generate alert
* tcp → protocol
* any any → any source
* -> → direction
* any 80 → destination port 80

---

## 📊 Task Breakdown & Examples

### 🧩 Task 1–2: Introduction

* Understood Snort purpose
* Learned IDS vs IPS differences

---

### 🌐 Task 3: Running Snort

📌 Example:

* Captured live traffic
* Observed packet headers

---

### 🔎 Task 4: Logging Traffic

📌 Example:

* Saved packets to logs
* Reviewed captured data

---

### 🧪 Task 5: Rule-Based Detection

📌 Example:

* Detected HTTP traffic using rule

---

### 🚨 Task 6: Writing Custom Rules

📌 Example:

```bash
alert icmp any any -> any any (msg:"ICMP Detected"; sid:1000002;)
```

---

### 🧠 Task 7: Detecting Attacks

📌 Example:

* Detected port scan attempts
* Identified suspicious traffic patterns

---

## 🚨 Indicators of Compromise (IOCs)

* Repeated connection attempts
* Suspicious protocol usage
* Traffic matching known malicious signatures

---

## 🛠️ Detection Capabilities

* Signature-based detection
* Real-time alerting
* Packet logging

---

## ⚖️ IDS vs IPS

| Feature    | IDS     | IPS    |
| ---------- | ------- | ------ |
| Detection  | Yes     | Yes    |
| Blocking   | No      | Yes    |
| Deployment | Passive | Inline |

---

## 🧩 MITRE ATT&CK Mapping

* **TA0001 – Initial Access**
* **TA0007 – Discovery**
* **TA0011 – Command and Control**

Snort helps detect activity across multiple stages.

---

## 🧠 SOC Perspective

SOC analysts use Snort to:

* Detect known attack patterns
* Generate alerts for investigation
* Monitor network traffic in real time

---

## 🏁 Room Completion Status

* ✅ All tasks completed
* 🧠 Strong understanding of Snort and IDS concepts achieved

---

## 🚀 Key Takeaways

* Snort is a powerful signature-based IDS/IPS
* Rules are the core of detection
* Real-time monitoring is critical in SOC environments
* Complements tools like Wireshark and SIEM

---

🧠 *Room completed as part of my Blue Team, SOC & Network Defense training path.*
