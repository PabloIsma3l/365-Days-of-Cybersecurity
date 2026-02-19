# 🔥 DAY 49 Firewall Fundamentals — TryHackMe 

## 📌 Overview

This repository documents the completion of the **Firewall Fundamentals** room on TryHackMe.

This room introduces the core concepts of firewalls, how they function in network security, different firewall types, rule configuration logic, and their role in protecting infrastructure.

All tasks have been successfully completed.

---

## 🎯 Learning Objectives Achieved

✔ Understand what a firewall is and its purpose
✔ Learn how firewalls filter traffic
✔ Identify different types of firewalls
✔ Understand rule configuration and policy logic
✔ Recognize how firewalls support Incident Response and SOC operations

---

## 🧠 What is a Firewall?

A **firewall** is a network security device or software that monitors and controls incoming and outgoing network traffic based on predefined security rules.

Its main goal is to:

* Prevent unauthorized access
* Block malicious traffic
* Enforce security policies
* Segment internal networks

---

## 🏗️ Types of Firewalls

### 1️⃣ Packet Filtering Firewall

* Operates at Network Layer (Layer 3)
* Filters traffic based on:

  * Source IP
  * Destination IP
  * Port numbers
  * Protocol

Fast but limited in context awareness.

---

### 2️⃣ Stateful Inspection Firewall

* Tracks active connections
* Understands session state
* More secure than simple packet filtering

Most modern enterprise firewalls are stateful.

---

### 3️⃣ Application Layer Firewall (Proxy Firewall)

* Operates at Application Layer (Layer 7)
* Inspects application-level traffic
* Can filter HTTP, FTP, SMTP traffic

Provides deeper inspection and control.

---

### 4️⃣ Next-Generation Firewall (NGFW)

* Deep Packet Inspection (DPI)
* Integrated IDS/IPS
* Application awareness
* SSL inspection
* Threat intelligence integration

Common in enterprise environments.

---

## 📜 Firewall Rules & Policies

Firewall rules typically include:

* Source IP
* Destination IP
* Source Port
* Destination Port
* Protocol (TCP/UDP/ICMP)
* Action (ALLOW / DENY)

### 🔑 Rule Evaluation Logic

* Rules are processed top-to-bottom
* First match applies
* Implicit deny at the end (default block rule)

Misconfigured rules can create security gaps.

---

## 🌐 Common Firewall Use Cases

* Block unauthorized inbound traffic
* Restrict outbound internet access
* Protect web servers (port 80/443)
* Control SSH access (port 22)
* Segment internal networks (VLAN isolation)

---

## 🚨 Firewalls in Incident Response

During an investigation, firewall logs help to:

* Identify suspicious IP addresses
* Detect port scanning attempts
* Detect brute force attacks
* Identify data exfiltration
* Block malicious command-and-control traffic

Firewall logs are often integrated into SIEM platforms for centralized analysis.

---

## 🛡️ Firewall vs IDS/IPS

* **Firewall** → Controls traffic flow based on rules
* **IDS (Intrusion Detection System)** → Detects suspicious activity
* **IPS (Intrusion Prevention System)** → Detects and blocks malicious activity

Modern NGFW solutions often combine these capabilities.

---

## 🐧 Basic Firewall Usage in Linux

In Linux environments, firewall management is commonly handled using tools such as **iptables**, **ufw (Uncomplicated Firewall)**, or **firewalld**.

### 🔹 UFW (Ubuntu/Debian)

Enable firewall:

```bash
sudo ufw enable
```

Allow SSH:

```bash
sudo ufw allow 22/tcp
```

Check status:

```bash
sudo ufw status verbose
```

---

### 🔹 iptables (Advanced)

Allow SSH traffic:

```bash
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

Drop all incoming traffic (example default deny):

```bash
sudo iptables -P INPUT DROP
```

iptables provides granular rule control but requires deeper networking knowledge.

---

## 🛡️ Firewall Usage in Windows Defender

Windows systems use **Windows Defender Firewall** (now Microsoft Defender Firewall) for host-based protection.

Key features:

* Inbound and outbound traffic filtering
* Domain, Private, and Public network profiles
* Advanced Security Rules (port, program, IP-based)
* Integration with Active Directory policies (GPO)

### 🔹 PowerShell Example

Allow inbound TCP port 3389 (RDP):

```powershell
New-NetFirewallRule -DisplayName "Allow RDP" -Direction Inbound -Protocol TCP -LocalPort 3389 -Action Allow
```

List firewall rules:

```powershell
Get-NetFirewallRule
```

Host-based firewalls are critical in limiting lateral movement during incidents.

---
