# 📅 Day 15 – Cyber Security 101: Networking Concepts

## 🎯 Daily Objective

Understand the **fundamental networking concepts** applied to cybersecurity, required to progress through the **TryHackMe path** and as a foundation for the future **Red Team path**.

---

## 🌐 What is Networking?

**Networking** is the interconnection of devices to share information and resources. In cybersecurity, understanding how data travels is critical to:

* Identify vulnerabilities
* Analyze network traffic
* Exploit exposed services
* Defend infrastructures

---

## 🧱 Basic Network Components

### 🔹 Hosts

Devices connected to a network (PCs, servers, routers, IoT).

### 🔹 Network Interface Card (NIC)

Allows a device to connect to a network.

### 🔹 Transmission Media

* Wired (Ethernet, fiber)
* Wireless (Wi-Fi)

### 🔹 Network Devices

* **Switch**: connects devices within a LAN
* **Router**: connects different networks
* **Firewall**: filters traffic based on rules

---

## 📡 Types of Networks

* **LAN (Local Area Network)**: local network (home, office)
* **WAN (Wide Area Network)**: large networks (Internet)
* **MAN (Metropolitan Area Network)**
* **VPN**: Virtual Private Network (encrypted tunnel)

---

## 🧭 IP Addressing

### 🔹 IPv4

Format: `x.x.x.x` (32 bits)
Example: `192.168.1.10`

### 🔹 IPv6

Hexadecimal format (128 bits)

### 🔹 Public vs Private IP

* **Public**: visible on the Internet
* **Private**: internal use

Common private ranges:

* `10.0.0.0/8`
* `172.16.0.0/12`
* `192.168.0.0/16`

---

## 🧮 Subnetting (Introduction)

Subnetting allows dividing a network into smaller subnets for:

* Better control
* Segmentation
* Improved security

Example:

* `192.168.1.0/24`

---

## 🔌 Ports and Protocols

### 🔹 Ports

Identify services running on a host.

Common examples:

* **22** – SSH
* **80** – HTTP
* **443** – HTTPS
* **21** – FTP
* **25** – SMTP

### 🔹 Protocols

* **TCP**: reliable, connection-oriented
* **UDP**: fast, connectionless
* **ICMP**: diagnostics (ping)

---

## 🗂️ OSI Model (Summary)

1. Physical
2. Data Link
3. Network
4. Transport
5. Session
6. Presentation
7. Application

👉 Fundamental for network analysis and troubleshooting.

---

## 🔍 Red Team Relevance

These concepts are essential for:

* Port scanning (Nmap)
* Service enumeration
* Pivoting
* Packet sniffing
* MITM attacks

---

## 🛠️ Related Tools

* `ip`, `ifconfig`
* `ping`, `traceroute`
* `netstat`, `ss`
* `nmap`
* `tcpdump`, `wireshark`

---

## 📌 Conclusion

Networking is a **critical foundation** for offensive cybersecurity. Mastering these concepts enables understanding how attacks work and how to exploit them in a controlled and ethical manner.

