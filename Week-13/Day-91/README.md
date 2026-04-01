# 🌐 Network Security Essentials — TryHackMe (Completed) DAY 90

## 📌 Overview

This repository documents the completion of the **Network Security Essentials** room on TryHackMe.

This room provides a foundational understanding of how networks are secured, including key defensive mechanisms, monitoring strategies, and common threats faced by modern infrastructures.

---

## 🎯 Learning Objectives Achieved

✔ Understand core network security concepts
✔ Identify common network threats and attack vectors
✔ Learn defensive technologies (Firewall, IDS/IPS)
✔ Understand network monitoring strategies
✔ Recognize malicious activity in network traffic

---

## 🧠 Core Concepts

### 🔹 What is Network Security?

Network security involves protecting network infrastructure from:

* Unauthorized access
* Misuse
* Data exfiltration
* Disruption of services

It combines policies, tools, and monitoring to ensure confidentiality, integrity, and availability.

---

## 🛡️ Key Security Components

### 🔹 Firewalls

* Control inbound and outbound traffic
* Enforce access control policies

📌 Example:

* Blocking external access to internal services except HTTP/HTTPS

---

### 🔹 IDS / IPS

* **IDS** → Detects suspicious activity
* **IPS** → Detects and actively blocks threats

📌 Example:

* Detecting port scans or brute force attempts

---

### 🔹 SIEM

* Centralized log collection and analysis
* Correlates events across systems

📌 Example:

* Detecting multiple failed logins across hosts

---

## 🚨 Common Network Threats

### 🔹 Port Scanning

* Identifies open ports and services

📌 Indicator:

* Multiple SYN packets to different ports

---

### 🔹 Brute Force Attacks

* Repeated login attempts

📌 Indicator:

* High volume of authentication failures

---

### 🔹 Malware Communication (C2)

* Infected hosts communicating with attacker servers

📌 Indicator:

* Unknown outbound connections

---

### 🔹 Data Exfiltration

* Unauthorized data transfer

📌 Indicator:

* Large outbound traffic spikes

---

## 🔍 Network Monitoring

Monitoring helps detect and respond to threats.

### 🔹 What to Monitor

* Network traffic (PCAP)
* Logs (firewall, IDS, servers)
* Authentication events

---

### 🔹 Tools Used

* Wireshark → Packet analysis
* NetworkMiner → Forensics & extraction
* SIEM (Splunk / ELK) → Log correlation

---

## 📊 Practical Examples

### 🧪 Example 1: Detecting a Port Scan

```wireshark
tcp.flags.syn == 1 and tcp.flags.ack == 0
```

Observation:

* Multiple SYN packets to different ports → scanning activity

---

### 🧪 Example 2: Suspicious DNS Traffic

```wireshark
dns
```

Observation:

* Queries to unknown or random domains

---

### 🧪 Example 3: Detecting Cleartext Credentials

```wireshark
http.request.method == "POST"
```

Observation:

* Credentials sent without encryption

---

## 🧩 Defense in Depth

Layered security approach:

* Firewall (perimeter)
* IDS/IPS (detection/prevention)
* Endpoint security (EDR/AV)
* SIEM (visibility & correlation)

No single control is sufficient.

---

## 🧠 SOC Perspective

SOC analysts use these concepts to:

* Monitor network activity
* Detect anomalies
* Investigate alerts
* Respond to incidents

---

## 🏁 Room Completion Status

* ✅ All tasks completed
* 🧠 Strong understanding of network security fundamentals achieved

---

## 🚀 Key Takeaways

* Network security is layered and proactive
* Monitoring is essential for detection
* Understanding traffic patterns is critical
* Tools must be combined for effective defense

---

🧠 *Room completed as part of my Blue Team & SOC training path.*
