# 🧩 DAY 53 CAPA: The Basics 

## 📌 Overview

This repository documents the completion of the **CAPA: The Basics** room on TryHackMe.

This room introduces CAPA, a tool used in malware analysis to automatically identify suspicious capabilities within executable files. It focuses on understanding how CAPA works, how to interpret its output, and how it assists analysts in identifying malicious behavior.

All tasks have been successfully completed.

---

## 🎯 Learning Objectives Achieved

✔ Understand what CAPA is and its purpose
✔ Learn how CAPA detects malware capabilities
✔ Interpret CAPA output results
✔ Identify common malicious behaviors
✔ Understand CAPA’s role in malware triage

---

## 🧠 What is CAPA?

CAPA is an open-source tool developed to automatically identify capabilities in executable files.

Instead of simply detecting malware families, CAPA answers the question:

> "What can this binary do?"

It analyzes binaries and matches patterns against a ruleset to identify behaviors such as:

* Network communication
* Process injection
* Credential dumping
* File system modification
* Persistence mechanisms

---

## ⚙️ How CAPA Works

CAPA works by:

1️⃣ Disassembling the binary
2️⃣ Matching code patterns against predefined rules
3️⃣ Mapping findings to higher-level capabilities
4️⃣ Generating structured output

It does not execute malware — it performs static analysis.

---

## 🛠️ Basic CAPA Usage

### 🔹 Run CAPA Against a File

```bash
capa suspicious.exe
```

This analyzes the binary and outputs detected capabilities.

---

### 🔹 JSON Output Format

```bash
capa suspicious.exe -j
```

Generates structured JSON output for automation or integration with other tools.

---

### 🔹 Verbose Mode

```bash
capa suspicious.exe -v
```

Provides more detailed output during analysis.

---

## 📊 Understanding CAPA Output

CAPA output typically includes:

* Capability name
* Associated MITRE ATT&CK technique
* Namespace/category
* Matched code locations

Example capabilities:

* Create process
* Modify registry
* Encode data using Base64
* HTTP communication
* Inject into another process

This helps analysts quickly understand malware behavior without deep manual reverse engineering.

---

## 🎯 CAPA in Malware Analysis Workflow

Typical triage process:

1️⃣ Obtain suspicious binary
2️⃣ Calculate hash (SHA256)
3️⃣ Run strings analysis
4️⃣ Execute CAPA
5️⃣ Map capabilities to MITRE ATT&CK
6️⃣ Decide on deeper reverse engineering if needed

CAPA significantly speeds up initial malware triage.

---

## 🛡️ CAPA Use Cases

* SOC malware investigation
* Incident response analysis
* Threat intelligence research
* Rapid malware triage
* CTF reverse engineering challenges

---

## ⚠️ Limitations

* Static analysis only
* May miss heavily obfuscated malware
* Rule-based detection requires updated rule sets
* Does not replace dynamic analysis (sandboxing)

CAPA is best used alongside other tools such as sandboxes and disassemblers.

---

