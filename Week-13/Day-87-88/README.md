# 🦈 Wireshark: Packet Operations — TryHackMe (Completed) DAY 88 

## 📌 Overview

This document summarizes the completion of the **"Wireshark: Packet Operations"** room on TryHackMe.

The room focuses on practical packet-level analysis using Wireshark, including capturing traffic, applying filters, following streams, and extracting meaningful information from packets to support investigations.

---

## 🎯 Learning Objectives Achieved

✔ Capture and inspect network packets
✔ Use display and capture filters effectively
✔ Follow TCP/UDP streams
✔ Extract useful data from packet payloads
✔ Identify suspicious network behavior

---

## 🧠 Core Concepts

### 🔹 Packets & Frames

* Packets carry data across networks
* Frames are the link-layer encapsulation of packets
* Analysis focuses on headers + payload

---

### 🔹 Capture vs Display Filters

* **Capture filters (BPF)** → limit what is captured (e.g., `port 80`)
* **Display filters (Wireshark)** → refine what is shown (e.g., `http`, `ip.addr == 10.10.10.10`)

Using both correctly improves efficiency and visibility.

---

## 🔎 Key Wireshark Operations

### 🔹 Basic Navigation

* Packet list pane
* Packet details pane
* Packet bytes pane

---

### 🔹 Filtering Examples

```bash
http
ip.addr == 192.168.1.10
tcp.port == 80
dns
```

---

### 🔹 Follow Streams

* **Follow TCP Stream** → reconstruct conversations
* **Follow UDP Stream** → inspect datagrams

Useful for:

* Extracting credentials
* Viewing HTTP requests/responses
* Rebuilding sessions

---

### 🔹 Packet Inspection

* Analyze headers (IP, TCP, UDP)
* Check flags (SYN, ACK, FIN)
* Inspect payload content

---

## 🛠️ Practical Use Cases

* Identify suspicious connections
* Detect cleartext credentials
* Investigate malware communication
* Analyze DNS queries
* Troubleshoot network issues

---

## 🚨 Indicators of Suspicious Activity

* Unusual ports or protocols
* Repeated connection attempts
* Suspicious DNS queries
* Cleartext sensitive data

---

## 🛡️ SOC Perspective

Wireshark is used in SOC/DFIR to:

* Perform deep packet inspection (DPI)
* Investigate alerts from IDS/IPS
* Reconstruct attacker activity
* Support incident response

---

## 🏁 Room Completion Status

* ✅ All tasks completed

---

## 🚀 Key Takeaways

* Filtering is essential for efficient analysis
* Following streams reveals full conversations
* Packet-level visibility is critical for investigations
* Wireshark is a core tool for network forensics

---

🚀 *This room strengthens hands-on packet analysis skills using Wireshark, a fundamental tool for SOC analysts and incident responders.*
