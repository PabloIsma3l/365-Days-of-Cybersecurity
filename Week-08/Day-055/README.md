# 🔥 FlareVM: Arsenal of Tools Day 54
## 📌 Overview

This repository documents the completion of the **FlareVM: Arsenal of Tools** room on TryHackMe.

This room introduces FlareVM, a Windows-based malware analysis environment packed with reverse engineering and forensic tools. It focuses on understanding the investigative toolkit available and how it supports malware triage and advanced analysis.

All tasks have been successfully completed.

---

## 🎯 Learning Objectives Achieved

✔ Understand what FlareVM is
✔ Identify core investigative tools inside FlareVM
✔ Perform static malware analysis
✔ Analyze PE files
✔ Understand reverse engineering workflows
✔ Recognize how FlareVM supports DFIR and malware research

---

## 🧠 What is FlareVM?

FlareVM is a Windows-based malware analysis distribution developed to provide analysts with a fully equipped reverse engineering lab.

It includes:

* Reverse engineering tools
* Debuggers
* PE analysis utilities
* Network analysis tools
* Scripting and automation frameworks

It complements REMnux by providing a Windows-focused analysis environment.

---

# 🛠️ Core Tool Categories in FlareVM

---

## 📊 Key Tools & Investigative Value

| Tool                 | Investigative Value                                                                                                                                                                |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Procmon**          | Tracks detailed system activity including file system, registry, and process events. Extremely useful for malware behavior analysis, troubleshooting, and forensic investigations. |
| **Process Explorer** | Displays parent-child process relationships, loaded DLLs, process paths, and digital signatures. Helps identify suspicious process injection or masquerading.                      |
| **HxD**              | Hex editor used to inspect and modify malicious files at byte level. Useful for analyzing file headers, embedded payloads, and obfuscated content.                                 |
| **Wireshark**        | Captures and analyzes network traffic to detect unusual communications, command-and-control traffic, and data exfiltration attempts.                                               |
| **CFF Explorer**     | PE file analysis tool capable of inspecting headers, verifying integrity, checking digital signatures, and reviewing imports/exports.                                              |
| **PEStudio**         | Performs static analysis of executable properties without execution. Highlights suspicious indicators such as risky imports, anomalies, and indicators of compromise.              |
| **FLOSS**            | Extracts and de-obfuscates strings from malware using advanced static analysis techniques, revealing hidden indicators and payload data.                                           |

---

## 🔎 1️⃣ Static Analysis Tools

### 🔹 PE Analysis

* PE-bear
* PEview
* Detect It Easy (DIE)

Used to inspect:

* PE headers
* Imports/Exports
* Compilation timestamps
* Suspicious sections

---

### 🔹 Strings & Metadata

```powershell
strings.exe suspicious.exe
```

Used to extract:

* Hardcoded URLs
* IP addresses
* Registry keys
* Suspicious commands

---

## 🧬 2️⃣ Reverse Engineering Tools

### 🔹 Ghidra

Used for:

* Disassembly
* Decompilation
* Function analysis
* Control flow analysis

Helps understand malware logic and behavior.

---

### 🔹 x64dbg

Debugger used for:

* Dynamic debugging
* Breakpoint analysis
* API call tracing
* Unpacking malware

Useful for analyzing runtime behavior.

---

## 🌐 3️⃣ Network Analysis Tools

* Wireshark
* Fiddler
* TCPView

Used to:

* Inspect HTTP/HTTPS traffic
* Identify suspicious outbound connections
* Monitor active processes and connections

---

## 🧠 4️⃣ Scripting & Automation

* Python
* PowerShell
* FLOSS (FireEye Labs Obfuscated String Solver)

Example FLOSS usage:

```powershell
floss suspicious.exe
```

Used to recover obfuscated strings from malware.

---

# 🔐 Basic Malware Analysis Workflow in FlareVM

1️⃣ Calculate file hash (SHA256)
2️⃣ Identify file type and packer
3️⃣ Extract strings (strings/FLOSS)
4️⃣ Inspect PE structure
5️⃣ Load into Ghidra for static analysis
6️⃣ Debug with x64dbg if needed
7️⃣ Monitor runtime behavior

This workflow supports structured malware triage and deeper reverse engineering.

---

## 🛡️ FlareVM in DFIR & Malware Research

FlareVM supports:

* Advanced malware analysis
* Reverse engineering investigations
* Exploit analysis
* Threat research
* Incident response investigations

It is commonly used in professional malware research labs.

---

## ⚠️ Best Practices

* Use isolated virtual machines
* Disable network access when not required
* Take VM snapshots before executing samples
* Use controlled lab networks
* Never analyze malware on production systems

---

