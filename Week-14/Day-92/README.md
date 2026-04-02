##  Network Discovery Detection — TryHackMe (Completed) DAY 92

## 📌 Overview

This repository documents the completion of the **Network Discovery Detection** room on TryHackMe.

This room focuses on identifying and detecting adversary techniques used during the **discovery phase** of an attack, where attackers attempt to map the network, identify hosts, services, and gather information for lateral movement.

---

## 🎯 Learning Objectives Achieved

✔ Understand network discovery techniques used by attackers
✔ Identify indicators of scanning and enumeration
✔ Detect reconnaissance activity in network traffic
✔ Use filters and logs to investigate suspicious behavior
✔ Map activity to MITRE ATT&CK techniques

---

## 🧠 What is Network Discovery?

Network discovery is a phase where attackers gather information about:

* Active hosts
* Open ports and services
* Network topology
* Domain information

This aligns with **MITRE ATT&CK Discovery (TA0007)**.

---

## 🔎 Common Discovery Techniques

### 🔹 ICMP Scanning (Ping Sweep)

* Identifies live hosts

📌 Indicator:

* Multiple ICMP echo requests across a subnet

```wireshark
icmp
```

---

### 🔹 Port Scanning

* Identifies open ports/services

📌 Indicator:

* Multiple SYN packets to different ports

```wireshark
tcp.flags.syn == 1 and tcp.flags.ack == 0
```

---

### 🔹 Service Enumeration

* Identifies running services (HTTP, FTP, SSH, SMB)

📌 Indicator:

* Connection attempts to common service ports (21, 22, 80, 445)

---

### 🔹 DNS Enumeration

* Queries to discover domains and subdomains

📌 Indicator:

* High volume of DNS queries
* Unusual domain patterns

```wireshark
dns
```

---

## 📊 Task Breakdown & Examples

### 🧩 Task 1–2: Introduction to Discovery

* Understood attacker reconnaissance phase
* Reviewed MITRE ATT&CK mapping

📌 Example:

* TA0007 – Discovery

---

### 🌐 Task 3: Identifying Host Discovery

* Observed ICMP traffic patterns

📌 Example:

* Sequential ping requests across IP range → ping sweep

---

### 🔍 Task 4: Detecting Port Scans

* Analyzed TCP flags

📌 Example:

* SYN scan behavior (no ACK responses)

---

### 🧪 Task 5: Service Enumeration

* Identified connections to multiple services

📌 Example:

* Repeated attempts to connect to SSH and SMB

---

### 🌍 Task 6: DNS-Based Discovery

* Investigated DNS queries

📌 Example:

* Enumeration of internal/external domains

---

### 🚨 Task 7: Suspicious Activity Detection

* Correlated multiple indicators

📌 Example:

* Host performing ICMP sweep + port scan → likely attacker

---

### 🧠 Task 8: Investigation Scenario

* Applied full workflow

📌 Workflow:

1. Identify suspicious host
2. Analyze traffic patterns
3. Detect scanning behavior
4. Map to MITRE technique
5. Document findings

---

## 🚨 Indicators of Compromise (IOCs)

* ICMP sweeps across multiple hosts
* High number of SYN packets
* Connections to multiple ports/services
* Unusual DNS query patterns
* Short-lived connections across many hosts

---

## 🛠️ Detection Techniques

* Network traffic analysis (Wireshark)
* IDS/IPS alerts (Snort/Suricata)
* SIEM correlation (Splunk/ELK)

---

## 🧩 MITRE ATT&CK Mapping

* **TA0007 – Discovery**

  * T1046 → Network Service Discovery
  * T1018 → Remote System Discovery
  * T1049 → System Network Connections Discovery

---

## 🧠 SOC Perspective

SOC analysts use these detections to:

* Identify early-stage attacks
* Prevent lateral movement
* Trigger alerts for reconnaissance activity

Early detection at this stage can stop attacks before exploitation.

---

## 🏁 Room Completion Status

* ✅ All tasks completed
* 🧠 Strong understanding of discovery detection achieved

---

## 🚀 Key Takeaways

* Discovery is a critical early attack phase
* Scanning behavior is highly detectable
* Combining indicators improves accuracy
* Mapping to MITRE enhances detection capability

---

🧠 *Room completed as part of my Blue Team, SOC & Threat Detection training path.*
