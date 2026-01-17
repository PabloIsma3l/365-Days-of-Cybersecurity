# 📅 Day 17 – Networking Fundamentals: ICMP, ARP, DHCP & NAT

## 🎯 Daily Objective

Understand and complete the **core networking protocols and mechanisms** covered in the TryHackMe *Networking Concepts* room: **ICMP, ARP, DHCP, and NAT**, and their relevance to cybersecurity.

---

## 📡 ICMP (Internet Control Message Protocol)

ICMP is used for **network diagnostics and error reporting**. It does not transport application data but provides critical feedback about network connectivity.

### Common ICMP Uses

* `ping` → check host availability
* `traceroute` → map network paths

### Security Relevance

* Used for host discovery during reconnaissance
* Can be abused for network mapping
* Often filtered by firewalls due to information leakage

---

## 🔁 ARP (Address Resolution Protocol)

ARP maps **IP addresses to MAC addresses** within a local network.

### How ARP Works

* A device broadcasts an ARP request
* The target host replies with its MAC address

### Security Relevance

* Critical for local network communication
* Vulnerable to **ARP spoofing / poisoning**
* Enables Man-in-the-Middle (MITM) attacks

---

## 📦 DHCP (Dynamic Host Configuration Protocol)

DHCP automatically assigns network configuration to hosts.

### Information Provided by DHCP

* IP address
* Subnet mask
* Default gateway
* DNS servers

### Security Relevance

* Simplifies network management
* Rogue DHCP servers can redirect traffic
* Useful during initial network enumeration

---

## 🌍 NAT (Network Address Translation)

NAT allows multiple private IP addresses to share a **single public IP**.

### Why NAT Is Used

* Conserves public IP addresses
* Adds a basic layer of obscurity

### Security Relevance

* Hides internal network structure
* Can limit inbound connections
* Requires port forwarding for exposed services

---

## 🔍 Red Team Perspective

Understanding these protocols enables:

* Effective host discovery (ICMP)
* Local network attacks (ARP poisoning)
* Identifying misconfigurations (DHCP)
* Understanding perimeter limitations (NAT)

---

## 🛠️ Related Tools

* `ping`, `traceroute`
* `arp`, `arp -a`
* `ip`, `ifconfig`
* `tcpdump`, `wireshark`
* `nmap` (host discovery techniques)

---

## 📌 Key Takeaways

* Networking protocols expose valuable information
* Misconfigurations are common attack vectors
* These fundamentals are essential before advancing to Red Team topics

---

## ✅ Status

**Networking Fundamentals (ICMP, ARP, DHCP, NAT): COMPLETED** ✅

---

📁 **Path:** TryHackMe – Cyber Security 101
📆 **Progress:** Week 03 – Day 17
👤 **Author:** Pablo Ismael
🔗 **Repository:** 365-Days-of-Cybersecurity

---

➡️ *Next: moving deeper into network security and offensive techniques*
