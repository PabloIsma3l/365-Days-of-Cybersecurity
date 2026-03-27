# 🌐 Network Traffic Basics — TryHackMe (Completed) Day 86

## 📌 Overview

This document summarizes the completion of the **"Network Traffic Basics"** room on TryHackMe.

This room introduces the fundamentals of network traffic analysis, focusing on how data moves across networks and how analysts can inspect and interpret traffic to detect suspicious or malicious activity.

Understanding network traffic is essential for **SOC Analysts, Threat Hunters, and Incident Responders**.

---

## 🎯 Learning Objectives Achieved

✔ Understand how network traffic works
✔ Learn basic networking protocols
✔ Analyze packets and traffic flows
✔ Identify normal vs suspicious network behavior

---

## 🧠 What is Network Traffic?

Network traffic refers to the **data transmitted between devices** over a network.

It consists of packets that contain:

* Source and destination IP addresses
* Protocol information
* Payload (actual data)

Analyzing this traffic helps detect anomalies and potential threats.

---

## 📡 Common Network Protocols

### 🔹 TCP (Transmission Control Protocol)

* Connection-oriented
* Reliable data transfer
* Used for web, email, SSH

---

### 🔹 UDP (User Datagram Protocol)

* Connectionless
* Faster but less reliable
* Used for streaming, DNS

---

### 🔹 ICMP

* Used for diagnostics (e.g., ping)

---

### 🔹 HTTP / HTTPS

* Web traffic protocols
* HTTPS provides encryption

---

## 🔎 Packet Analysis Basics

Each packet includes:

* Headers (network and transport layers)
* Payload (data)

Analysts inspect packets to:

* Identify suspicious communication
* Detect anomalies
* Investigate incidents

---

## 🛠️ Common Tools

### 🔹 Wireshark

* Packet capture and analysis
* Deep inspection of network traffic

### 🔹 tcpdump

* Command-line packet analyzer
* Useful for quick captures and filtering

---

## 🚨 Indicators of Suspicious Traffic

* Unusual ports or protocols
* Unexpected external connections
* High volume of traffic (possible exfiltration or DDoS)
* Repeated failed connections

---

## 🛡️ SOC Perspective

Network traffic analysis is used to:

* Detect intrusions
* Identify command-and-control (C2) traffic
* Investigate incidents
* Support threat hunting

---

## 🏁 Room Completion Status

* ✅ All tasks completed

---

## 🚀 Key Takeaways

* Network traffic analysis provides visibility into attacker activity
* Understanding protocols is essential for investigations
* Packet analysis helps detect anomalies and threats
* Tools like Wireshark and tcpdump are fundamental for analysts

---

🚀 *This room builds foundational knowledge required to analyze network traffic and detect suspicious activity in real-world envir
