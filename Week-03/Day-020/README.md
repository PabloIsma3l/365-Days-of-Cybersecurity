# 📅 Day 20 – Wireshark: The Basics

## 🎯 Daily Objective

Learn the **fundamentals of Wireshark** and how to analyze network traffic and **PCAP files** to understand how protocols behave at packet level.

---

## 🦈 What is Wireshark?

Wireshark is a **network protocol analyzer** used to capture and inspect packets traveling across a network.

It allows:

* Deep inspection of network traffic
* Protocol analysis
* Troubleshooting and security investigations

---

## 📦 Packets & PCAP Files

* **Packets**: small units of data transmitted over a network
* **PCAP**: file format that stores captured network traffic

PCAPs are commonly used for:

* Incident response
* Malware analysis
* Network forensics
* Learning how protocols work

---

## 🧱 Wireshark Interface Basics

Key sections:

* **Packet List Pane**: summary of captured packets
* **Packet Details Pane**: protocol breakdown by OSI layers
* **Packet Bytes Pane**: raw packet data (hex + ASCII)

Understanding these panes is essential for effective analysis.

---

## 🔍 Display Filters (Basics)

Display filters allow focusing on specific traffic.

Examples:

```text
http
ip.addr == 192.168.1.10
tcp.port == 80
icmp
```

Filters are critical when working with large PCAP files.

---

## 🌐 Protocol Analysis Examples

### HTTP

* Inspect requests and responses
* View headers and methods (GET, POST)

### DNS

* Observe queries and responses
* Identify domains being resolved

### TCP

* Analyze handshakes (SYN, SYN-ACK, ACK)
* Identify retransmissions and issues

---

## 🔐 Clear-Text vs Encrypted Traffic

* **Clear-text protocols** (HTTP, FTP, Telnet) expose data
* **Encrypted protocols** (HTTPS, SSH) hide payload content

Wireshark can still reveal:

* IPs and ports
* Protocols in use
* Metadata and timing

---

## 🔍 Red Team Perspective

Wireshark is useful for:

* Understanding protocol behavior
* Learning what information leaks over the network
* Verifying encryption usage
* Supporting MITM and traffic analysis techniques

---

## 🛠️ Key Takeaways

* Wireshark is essential for network visibility
* PCAP analysis builds protocol intuition
* Not all sensitive data is hidden by encryption

---

