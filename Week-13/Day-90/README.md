# 🧪 NetworkMiner — TryHackMe (Completed) DAY 90

## 📌 Overview

This repository documents the completion of the **NetworkMiner** room on TryHackMe.

NetworkMiner is a **Network Forensics Analysis Tool (NFAT)** used to analyze captured network traffic (PCAP files) and extract valuable artifacts such as files, credentials, hosts, and sessions without actively generating traffic.

This room focuses on passive network analysis and forensic investigation techniques.

---

## 🎯 Learning Objectives Achieved

✔ Understand NetworkMiner fundamentals
✔ Perform passive network traffic analysis
✔ Extract files and artifacts from PCAPs
✔ Identify hosts, sessions, and credentials
✔ Investigate suspicious network activity
✔ Apply network forensics techniques

---

## 🧠 What is NetworkMiner?

NetworkMiner is a **passive network analysis tool** that:

* Parses PCAP files
* Extracts transmitted files
* Reconstructs sessions
* Identifies hosts and endpoints

Unlike Wireshark, it focuses on **artifact extraction and forensic analysis** rather than packet-by-packet inspection.

---

## ⚙️ Key Features

* File extraction (images, executables, documents)
* Credential harvesting (cleartext protocols)
* Host identification
* Session reconstruction
* DNS and HTTP analysis

---

## 📊 Interface Overview

### 🔹 Hosts Tab

Displays:

* IP addresses
* Hostnames
* MAC addresses
* OS fingerprinting (if available)

📌 Example:

* Internal host communicating with external suspicious IP

---

### 🔹 Files Tab

Shows extracted files from traffic:

* Images
* Executables
* Documents

📌 Example:

* Suspicious `.exe` downloaded over HTTP

---

### 🔹 Credentials Tab

Displays credentials found in plaintext protocols:

* FTP
* HTTP
* Telnet

📌 Example:

* Username: admin
* Password: password123

---

### 🔹 Sessions Tab

* Reconstructed communication sessions
* Helps track conversations between hosts

---

### 🔹 DNS Tab

* Domain queries
* Helps identify suspicious domains

📌 Example:

* Requests to unknown or malicious domains

---

## 🧩 Task Breakdown & Examples

### 🧪 Task 1–2: Introduction

* Installed/launched NetworkMiner
* Loaded PCAP file

📌 Key insight:

* Passive analysis (no network interaction)

---

### 🌐 Task 3: Host Identification

* Identified communicating hosts

📌 Example:

* Internal IP → External IP communication
* Suspicious external IP flagged

---

### 🔐 Task 4: Credential Extraction

* Extracted credentials from traffic

📌 Example:

* HTTP login captured in plaintext

---

### 📦 Task 5: File Extraction

* Recovered transferred files

📌 Example:

* Malicious executable downloaded via HTTP

---

### 🔎 Task 6: Session Analysis

* Investigated sessions between hosts

📌 Example:

* Reconstructed attacker communication

---

### 🌍 Task 7: DNS Analysis

* Reviewed domain requests

📌 Example:

* Suspicious or uncommon domains

---

### 🚨 Task 8: Investigation Scenario

* Combined all analysis techniques

📌 Workflow:

1. Identify suspicious host
2. Analyze sessions
3. Extract files
4. Review credentials
5. Correlate DNS activity

---

## 🚨 Indicators of Compromise (IOCs)

* Suspicious external IPs
* Malicious file downloads
* Cleartext credentials
* Unusual DNS queries
* Unknown communication patterns

---

## 🛠️ Network Forensics Workflow

1. Load PCAP into NetworkMiner
2. Review Hosts tab
3. Check Credentials tab
4. Analyze Sessions
5. Extract Files
6. Investigate DNS queries
7. Correlate findings

---

## ⚖️ NetworkMiner vs Wireshark

| Feature         | NetworkMiner      | Wireshark         |
| --------------- | ----------------- | ----------------- |
| Analysis Type   | Passive Forensics | Packet Inspection |
| Ease of Use     | High              | Medium            |
| File Extraction | Automatic         | Manual            |
| Packet Detail   | Limited           | Deep              |

---

## 🧩 SOC / DFIR Relevance

NetworkMiner is used for:

* Incident response investigations
* Malware analysis (network behavior)
* Data exfiltration detection
* Credential compromise detection

---

## 🏁 Room Completion Status

* ✅ All tasks completed
* 🧠 Strong understanding of network forensics achieved

---

## 🚀 Key Takeaways

* Passive analysis is critical in forensics
* NetworkMiner excels at artifact extraction
* Credentials and files can be recovered from traffic
* Complements tools like Wireshark

---

## 🚀 Next Steps

* Combine with Wireshark analysis
* Practice with real PCAP datasets
* Explore Zeek for advanced network analysis

---

🧠 *Room completed as part of my Blue Team, SOC & Digital Forensics training path.*
