# 📅 Day 21 – Tcpdump: The Basics

## 🎯 Daily Objective

Learn how to use **tcpdump** to capture, filter, and analyze network packets from the command line, and understand its importance for traffic analysis and security investigations.

---

## 🐧 What is tcpdump?

tcpdump is a **command-line packet analyzer** that allows capturing and inspecting network traffic directly from the terminal.

It is widely used because:

* It is lightweight and fast
* Works on servers without GUI
* Ideal for quick troubleshooting and forensic analysis

---

## 📦 Packet Capture Basics

Basic syntax:

```bash
tcpdump -i <interface>
```

Common examples:

```bash
tcpdump -i eth0
tcpdump -i any
```

---

## 💾 Saving Traffic to PCAP Files

Captured traffic can be saved for later analysis in Wireshark.

```bash
tcpdump -i eth0 -w capture.pcap
```

To read a PCAP file:

```bash
tcpdump -r capture.pcap
```

---

## 🔍 Filtering Traffic (Basics)

Filters help reduce noise and focus on relevant packets.

### By Protocol

```bash
tcpdump icmp
tcpdump tcp
tcpdump udp
```

### By Port

```bash
tcpdump port 80
tcpdump tcp port 443
```

### By Host

```bash
tcpdump host 192.168.1.10
tcpdump src host 10.0.0.5
tcpdump dst host 8.8.8.8
```

---

## 🌐 Observing Clear-Text vs Encrypted Traffic

* Clear-text protocols (HTTP, FTP, Telnet) may expose payload data
* Encrypted protocols (HTTPS, SSH) hide content but not metadata

tcpdump can still reveal:

* Source and destination IPs
* Ports and protocols
* Traffic patterns

---

## 🔍 Red Team Perspective

From an offensive security viewpoint, tcpdump helps:

* Understand network behavior
* Verify encryption usage
* Identify sensitive data leaks
* Support MITM and pivoting techniques

---

## 🛠️ Key Takeaways

* tcpdump is essential for low-level network visibility
* Filters are critical for effective analysis
* PCAPs enable offline and collaborative investigation

