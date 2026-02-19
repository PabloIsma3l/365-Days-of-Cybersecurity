# 🛡️ IDS Fundamentals — TryHackMe Day 50

## 📌 Overview

This repository documents the completion of the **IDS Fundamentals** room on TryHackMe.

This room introduces Intrusion Detection Systems (IDS), how they function, detection methodologies, deployment types, and their role within SOC and Incident Response environments.

All tasks have been successfully completed.

---

## 🎯 Learning Objectives Achieved

✔ Understand what an IDS is
✔ Learn the difference between IDS and IPS
✔ Identify different types of IDS
✔ Understand detection methodologies
✔ Recognize how IDS integrates with SIEM and SOC workflows
✔ Understand alert handling and false positives

---

## 🧠 What is an IDS?

An **Intrusion Detection System (IDS)** is a security solution that monitors network traffic or host activity to detect suspicious behavior, malicious activity, or policy violations.

Unlike a firewall, an IDS:

* Does not block traffic by default
* Operates passively
* Generates alerts for analysts
* Provides visibility into threats

It is primarily a detection tool used in SOC environments.

---

## 🔍 IDS vs IPS

| IDS                   | IPS                                 |
| --------------------- | ----------------------------------- |
| Detects threats       | Detects and blocks threats          |
| Passive monitoring    | Inline protection                   |
| Generates alerts      | Actively prevents attacks           |
| No traffic disruption | Can impact traffic if misconfigured |

Many modern solutions combine both capabilities.

---

## 🏗️ Types of IDS

### 🌐 1️⃣ NIDS (Network-Based IDS)

* Monitors network traffic
* Placed at strategic network segments
* Analyzes packets in real-time

Detects:

* Port scanning
* Brute force attempts
* Exploit traffic
* Suspicious outbound connections

Common deployment areas:

* Perimeter network
* Between VLANs
* Data center core

---

### 🖥️ 2️⃣ HIDS (Host-Based IDS)

* Installed on endpoints or servers
* Monitors system logs
* Tracks file integrity
* Detects suspicious processes

Detects:

* Privilege escalation
* File tampering
* Unauthorized configuration changes
* Suspicious service execution

---

## 🧠 Detection Methodologies

### 1️⃣ Signature-Based Detection

* Matches traffic against known attack patterns
* Highly effective for known threats
* Fast and precise
* Cannot detect zero-day attacks

Example:

* Known SQL injection payload
* Known malware hash signature

---

### 2️⃣ Anomaly-Based Detection

* Establishes a baseline of normal behavior
* Detects deviations from normal activity
* Can identify unknown threats
* Higher false positive rate

Example:

* Unusual outbound traffic volume
* Login attempts outside business hours

---

### 3️⃣ Hybrid Detection

* Combines signature + anomaly detection
* Used in most modern IDS platforms

---

## 🚨 Common Attacks Detected by IDS

* Port scanning
* Brute force attacks
* SQL Injection attempts
* Cross-site scripting attempts
* Malware beaconing
* DNS tunneling
* Lateral movement activity

---

## 📊 IDS in SOC & SIEM Environments

IDS logs are typically:

* Forwarded to a SIEM
* Correlated with firewall logs
* Combined with EDR telemetry
* Used in incident investigations

### 🔎 Example SOC Workflow

1. IDS detects brute force activity
2. Alert sent to SIEM
3. Correlation with authentication logs
4. Analyst validates malicious activity
5. IP blocked via firewall
6. Incident documented

---

## 🛠️ Common Open-Source IDS Tools

* **Snort** (Signature-based NIDS)
* **Suricata** (High-performance NIDS/IPS)
* **OSSEC** (Host-based IDS)
* **Wazuh** (Advanced HIDS + SIEM integration)

These are widely used in labs and enterprise environments.

---

## ⚠️ IDS Challenges

* False positives
* Alert fatigue
* Encrypted traffic visibility limitations
* Signature maintenance
* High-volume log management

Proper tuning and integration with other tools is critical.

---

## 🐗 Basic Snort Usage (NIDS Example)

**Snort** is one of the most widely used open-source Network Intrusion Detection Systems.

### 🔹 Run Snort in Sniffer Mode

```bash
snort -v
```

Displays live packet information.

---

### 🔹 Run Snort in Packet Logger Mode

```bash
snort -dev -l ./log
```

* `-d` → Show application layer data
* `-e` → Show link layer headers
* `-v` → Verbose mode
* `-l` → Log directory

---

### 🔹 Run Snort in IDS Mode

```bash
snort -c /etc/snort/snort.conf -i eth0
```

* `-c` → Specify configuration file
* `-i` → Network interface

This enables full IDS functionality using rule-based detection.

---

### 🔹 Basic Snort Rule Example

```bash
alert tcp any any -> any 80 (msg:"HTTP Traffic Detected"; sid:1000001;)
```

Rule breakdown:

* `alert` → Action
* `tcp` → Protocol
* `any any` → Source IP and port
* `->` → Direction
* `any 80` → Destination (HTTP port)
* `msg` → Alert message
* `sid` → Unique rule ID

Custom rules are typically stored in:

```bash
/etc/snort/rules/local.rules
```

---

Snort is commonly integrated with:

* SIEM platforms
* Log management systems
* SOC monitoring dashboards

---


