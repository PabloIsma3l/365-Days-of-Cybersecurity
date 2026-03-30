# 🦈 Wireshark: Traffic Analysis — TryHackMe (Completed) DAY 89

## 📌 Overview

This repository documents the completion of the **Wireshark: Traffic Analysis** room on TryHackMe.

This room focuses on analyzing network traffic to detect anomalies, identify suspicious behavior, and investigate potential security incidents using Wireshark.

All tasks have been successfully completed.

---

## 🎯 Learning Objectives Achieved

✔ Understand traffic analysis fundamentals
✔ Identify normal vs suspicious network behavior
✔ Use Wireshark filters for investigation
✔ Analyze protocols and detect anomalies
✔ Extract useful data from packet captures
✔ Investigate potential security incidents using PCAP files

---

## 🧠 What is Traffic Analysis?

Traffic analysis involves examining network packets to:

* Detect anomalies
* Identify malicious activity
* Understand communication patterns
* Investigate incidents

Wireshark allows deep inspection of packets at multiple layers.

---

## 🔍 Key Wireshark Filters Used

### 🔹 Basic Filters

```wireshark
ip.addr == 192.168.1.1
tcp.port == 80
udp.port == 53
```

### 🔹 Protocol Filters

```wireshark
http
dns
tcp
icmp
```

### 🔹 Suspicious Activity Filters

```wireshark
tcp.flags.syn == 1 and tcp.flags.ack == 0   # Possible scan
http.request                                # HTTP requests
frame contains "password"                  # Sensitive data
```

---

## 📊 Task Breakdown & Examples

### 🧩 Task 1–2: Introduction to Traffic Analysis

* Learned how to open PCAP files
* Understood packet structure
* Identified source/destination IPs

📌 Example:

* Source: 192.168.0.10 → Destination: 8.8.8.8
* Protocol: DNS

---

### 🌐 Task 3: Identifying Protocols

* Analyzed common protocols:

  * HTTP
  * DNS
  * TCP
  * ICMP

📌 Example:

* DNS query to resolve a domain
* HTTP GET request to a web server

---

### 🔎 Task 4: Detecting Anomalies

* Identified unusual traffic patterns

📌 Examples:

* High number of SYN packets → Possible port scan
* Repeated failed connections → Possible brute force
* Unknown external IPs communicating internally

---

### 🧪 Task 5: HTTP Analysis

* Inspected HTTP traffic
* Used "Follow TCP Stream"

📌 Example:

* Extracted:

  * URLs
  * User-Agents
  * Credentials (if present in plaintext)

```wireshark
http.request.method == "POST"
```

---

### 🧬 Task 6: DNS Analysis

* Investigated DNS queries

📌 Example:

* Suspicious domain resolution
* Possible DNS tunneling indicators:

  * Long/random subdomains

```wireshark
dns
```

---

### 🚨 Task 7: Detecting Suspicious Traffic

* Looked for indicators of compromise

📌 Examples:

* Communication with known malicious IPs
* Data exfiltration patterns
* Unusual ports being used

---

### 📦 Task 8: File Extraction

* Exported objects from traffic

📌 Example:

* Extracted files from HTTP:

  * Images
  * Executables

Steps:

* File → Export Objects → HTTP

---

### 🧠 Task 9: Investigation Scenario

* Combined all previous knowledge

📌 Workflow:

1. Identify suspicious IP
2. Filter traffic
3. Analyze protocol
4. Extract data
5. Determine if malicious

---

## 🚨 Common Indicators of Compromise (IOCs)

* Suspicious IP addresses
* Unknown domains
* Unusual ports
* Repeated connection attempts
* Cleartext credentials

---

## 🛠️ Practical Investigation Workflow

1. Open PCAP file
2. Apply filters
3. Identify anomalies
4. Inspect packets
5. Follow streams
6. Extract files
7. Document findings

---

## 🧩 Real-World Relevance (SOC Perspective)

This room simulates tasks performed by SOC analysts:

* Investigating alerts
* Analyzing packet captures
* Identifying malicious behavior
* Supporting incident response

---

## 🏁 Room Completion Status

* ✅ All tasks completed
* 🧠 Strong understanding of network traffic analysis achieved

---

## 🚀 Next Steps

* Practice advanced Wireshark filtering
* Combine with SIEM analysis
* Explore threat hunting with network data
* Analyze real-world PCAP datasets

---

🧠 *Room completed as part of my Blue Team & SOC training path.*
