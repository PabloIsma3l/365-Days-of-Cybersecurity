# 🐧 REMnux: Getting Started — Day 54

## 📌 Overview

This repository documents the completion of the **REMnux: Getting Started** room on TryHackMe.

This room introduces REMnux, a Linux distribution specifically designed for malware analysis and reverse engineering. It focuses on understanding the available tools inside the virtual machine and how they assist in static, network, and memory analysis scenarios.

All tasks have been successfully completed.

---

## 🎯 Learning Objectives Achieved

✔ Understand what REMnux is
✔ Explore core malware analysis tools
✔ Perform static analysis on suspicious files
✔ Simulate network services safely
✔ Perform basic memory analysis with Volatility
✔ Understand how REMnux supports DFIR workflows

---

## 🧠 What is REMnux?

REMnux is a Linux-based toolkit distribution built for malware analysts.

It includes pre-installed tools for:

* Static malware analysis
* Network traffic simulation & analysis
* Reverse engineering
* Memory forensics
* File format inspection

It provides a controlled lab environment for safely investigating malicious files.

---

# 🔎 Static Analysis Tools

## 🔹 Hashing & File Identification

```bash
sha256sum suspicious.exe
file suspicious.exe
```

Used to identify file type and calculate hashes for threat intelligence comparison.

---

## 🔹 Strings Extraction

```bash
strings suspicious.exe
```

Helps identify:

* Hardcoded domains
* IP addresses
* Registry paths
* Suspicious commands

---

## 🔹 oledump (Office Malware Analysis)

Used to analyze malicious Microsoft Office documents.

```bash
oledump.py suspicious.doc
```

List macro streams:

```bash
oledump.py suspicious.doc -s A
```

Extract specific stream:

```bash
oledump.py suspicious.doc -s A -v
```

Useful for detecting embedded VBA macros and malicious payloads.

---

# 🌐 Network Simulation & Analysis

## 🔹 INetSim (Internet Simulation)

INetSim simulates common internet services to safely analyze malware network behavior without exposing it to the real internet.

Start INetSim:

```bash
sudo inetsim
```

It simulates services like:

* HTTP
* HTTPS
* DNS
* FTP
* SMTP

This allows analysts to observe:

* Command-and-control callbacks
* Malware download attempts
* DNS requests

INetSim is critical for safe dynamic behavior observation.

---

# 🧬 Malware Capability Analysis

## 🔹 YARA Scanning

```bash
yara rules.yar suspicious.exe
```

Used to detect known malware patterns.

---

## 🔹 CAPA

```bash
capa suspicious.exe
```

Identifies high-level malware capabilities.

---

# 🧠 Memory Analysis with Volatility

Volatility is used for memory forensics analysis.

Example basic usage:

```bash
volatility -f memory.img --profile=Win7SP1x64 pslist
```

---

## 🔹 pslist

Lists active processes at the time of memory capture.

```bash
volatility -f memory.img --profile=Win7SP1x64 pslist
```

---

## 🔹 pstree

Displays parent-child process relationships.

```bash
volatility -f memory.img --profile=Win7SP1x64 pstree
```

Helps detect:

* Suspicious parent processes
* Process injection chains

---

## 🔹 filescan

Scans memory for file objects.

```bash
volatility -f memory.img --profile=Win7SP1x64 filescan
```

Useful to detect:

* Hidden files
* Suspicious dropped payloads

---

## 🔹 netscan (additional useful plugin)

```bash
volatility -f memory.img --profile=Win7SP1x64 netscan
```

Identifies active and closed network connections.

---

# 🔐 Basic Malware Triage Workflow in REMnux

1️⃣ Calculate file hash
2️⃣ Identify file type
3️⃣ Extract strings
4️⃣ Analyze Office documents with oledump
5️⃣ Run YARA scan
6️⃣ Execute CAPA
7️⃣ Simulate network traffic with INetSim
8️⃣ Perform memory analysis with Volatility

This structured approach allows safe and efficient malware investigation.

---

## ⚠️ Best Practices

* Never analyze malware on your host machine
* Use isolated lab environments
* Take VM snapshots before analysis
* Disable shared folders when possible
* Keep rules and signatures updated

---

## 🏁 Room Completion Status

* ✅ All tasks completed
* 🧠 Solid understanding of REMnux environment and malware triage workflow achieved

---

## 🚀 Next Steps

* Practice full malware triage scenarios
* Combine REMnux with Windows sandbox VMs
* Study advanced Volatility plugins
* Explore reverse engineering with Ghidra

---

🧠 *Room completed as part of my structured Blue Team, DFIR & Malware Analysis training path.*


