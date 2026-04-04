# 📤 Data Exfiltration Detection — TryHackMe (Completed) DAY 94

## 📌 Overview

This repository documents the completion of the **Data Exfiltration Detection** room on TryHackMe.

This room focuses on identifying and detecting techniques used by attackers to **steal data from compromised systems**, analyzing different exfiltration channels and recognizing abnormal traffic patterns.

---

## 🎯 Learning Objectives Achieved

✔ Understand data exfiltration techniques
✔ Identify abnormal outbound traffic
✔ Detect exfiltration over multiple protocols
✔ Analyze network traffic for hidden data transfer
✔ Apply detection techniques in SOC environments

---

## 🧠 What is Data Exfiltration?

Data exfiltration is the unauthorized transfer of data from a system to an external destination controlled by an attacker.

It typically occurs after:

* Initial compromise
* Persistence
* Privilege escalation

---

## 🚨 Common Exfiltration Channels

### 🔹 HTTP / HTTPS

* Data sent via web requests

📌 Indicator:

* Large POST requests
* Unusual outbound traffic to unknown domains

```wireshark
http.request.method == "POST"
```

---

### 🔹 DNS Tunneling

* Data encoded in DNS queries

📌 Indicator:

* Long/random subdomains
* High volume of DNS requests

```wireshark
dns
```

---

### 🔹 FTP / File Transfer

* Direct file uploads to external servers

📌 Indicator:

* Unexpected FTP sessions

---

### 🔹 ICMP Tunneling

* Data hidden inside ICMP packets

📌 Indicator:

* Unusual ICMP traffic size or frequency

```wireshark
icmp
```

---

## 📊 Task Breakdown & Examples

### 🧩 Task 1–2: Introduction

* Learned exfiltration concepts
* Understood attacker objectives

---

### 🌐 Task 3: HTTP Exfiltration

📌 Example:

* Large HTTP POST request sending encoded data
* Suspicious domain receiving data

---

### 🔎 Task 4: DNS Exfiltration

📌 Example:

* Repeated DNS queries with encoded strings
* Possible data fragmentation across queries

---

### 🧪 Task 5: ICMP / Covert Channels

📌 Example:

* ICMP packets with abnormal payload sizes

---

### 🚨 Task 6: Identifying Anomalies

📌 Indicators:

* Sudden spike in outbound traffic
* Communication with unknown IPs
* Data transfer outside business hours

---

### 🧠 Task 7: Investigation Scenario

📌 Workflow:

1. Identify abnormal outbound traffic
2. Filter suspicious protocol
3. Analyze packet contents
4. Detect encoding/tunneling
5. Identify destination
6. Confirm exfiltration

---

## 🚨 Indicators of Compromise (IOCs)

* Large outbound data transfers
* Repeated DNS queries with random strings
* Suspicious POST requests
* ICMP anomalies
* Communication with unknown external hosts

---

## 🛠️ Detection Techniques

* Traffic analysis (Wireshark)
* Network forensics (NetworkMiner)
* SIEM correlation (Splunk / ELK)
* IDS/IPS alerts

---

## 🧩 MITRE ATT&CK Mapping

* **TA0010 – Exfiltration**

  * T1041 → Exfiltration Over C2 Channel
  * T1048 → Exfiltration Over Alternative Protocol
  * T1020 → Automated Exfiltration

---

## 🧠 SOC Perspective

SOC analysts must:

* Monitor outbound traffic patterns
* Detect abnormal data flows
* Correlate alerts across tools
* Respond quickly to prevent data loss

---

## 🏁 Room Completion Status

* ✅ All tasks completed
* 🧠 Strong understanding of data exfiltration detection achieved

---

## 🚀 Key Takeaways

* Exfiltration often hides in legitimate protocols
* DNS and HTTP are common attack vectors
* Traffic patterns reveal suspicious behavior
* Early detection reduces impact

---

🧠 *Room completed as part of my Blue Team, SOC & Threat Detection training path.*
