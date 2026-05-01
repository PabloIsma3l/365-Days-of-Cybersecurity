# 🧬 File and Hash Threat Intelligence — TryHackMe

## 📅 Day 120 - 365 Days of Cybersecurity

## 🚧 Progress: 50%

---

# 🧠 Overview

In this room, I am learning how to perform **file-based threat intelligence and enrichment**, a core task in SOC operations.

The focus is on transforming a **suspicious file or hash into actionable intelligence** using:

* Filepath and filename analysis
* Hash generation (SHA256 / MD5)
* Threat intelligence platforms (VirusTotal, MalwareBazaar)
* Sandbox analysis

📌 Key Concept:

SOC analysts don’t just see files — they **enrich them into intelligence to make decisions**. ([TryHackMe][1])

---

# 🎯 Learning Objectives (So far)

* Identify suspicious files using heuristics
* Generate and validate file hashes
* Enrich hashes using threat intelligence platforms
* Analyze sandbox results
* Map behavior to MITRE ATT&CK

---

# 📂 Filepath & Filename Analysis

Before hashing, analysts use **heuristics** to detect suspicious files.

---

## 🔹 Suspicious File Locations

Common attacker patterns:

* `C:\Windows\Temp\` → temporary payloads
* `C:\Users\Public\` → shared access / stealth
* `C:\ProgramData\` → persistence

📌 These locations are often abused to reduce visibility. ([TryHackMe][1])

---

## 🔹 Filename-Based Indicators

### ⚠️ Common Techniques

* Double extensions
  → `invoice.pdf.exe`

* Masquerading
  → `svch0st.exe`

* High entropy names
  → `jh8F21.exe`

* Legitimate-looking names
  → `backup-2024.exe`

📌 Filenames alone don’t confirm malware — but they **signal investigation priority**. ([TryHackMe][1])

---

# 🔐 File Hashing (Core Concept)

Hash = **unique fingerprint of a file**

---

## 🔹 Why It Matters

* Identifies malware regardless of filename
* Enables threat intel lookup
* Supports correlation across systems

---

## 🔹 Common Algorithms

* MD5
* SHA256 (preferred)

---

## 🔹 Example Commands

### Windows

```bash id="n2p8as"
certutil -hashfile file.exe SHA256
Get-FileHash file.exe
```

### Linux

```bash id="o8f9ds"
sha256sum file.exe
```

---

## 📌 SOC Insight

Even if attackers rename malware:

➡️ The hash remains the same

---

# 🌐 Hash Enrichment (Threat Intel)

Once a hash is obtained, analysts enrich it using:

* VirusTotal
* MalwareBazaar
* Internal threat intel

---

## 🔍 Key Data from VirusTotal

### 🔹 Detection Score

* Ratio of AV detections
* High score → higher confidence malicious

---

### 🔹 Threat Labels

* Malware family names
* Classification (Trojan, stealer, etc.)

---
