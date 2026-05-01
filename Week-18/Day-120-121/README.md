# 🧬 File and Hash Threat Intelligence — TryHackMe

## 📅 Day 121 - 365 Days of Cybersecurity

## ✅ Status: Completed

---

# 🧠 Overview

In this room, I learned how to perform **file-based threat intelligence analysis**, focusing on how SOC analysts investigate suspicious files using hashing, enrichment, and sandboxing.

The room simulates a real-world workflow where a suspicious file is:

* Identified
* Hashed
* Enriched with threat intelligence
* Analyzed in sandbox environments
* Correlated with known malicious behavior

📌 Key Concept:

A file alone is just an artifact —
➡️ **Threat Intelligence transforms it into actionable insight.**

---

# 🎯 Learning Objectives

* Identify suspicious files using heuristics
* Generate file hashes (MD5 / SHA256)
* Enrich hashes using threat intelligence platforms
* Analyze sandbox behavior
* Correlate findings with MITRE ATT&CK
* Make investigation decisions based on evidence

---

# 📂 File Analysis (Initial Triage)

Before hashing, initial indicators can reveal suspicious behavior.

---

## 🔹 Suspicious File Locations

Common attacker-used directories:

* `C:\Windows\Temp\`
* `C:\Users\Public\`
* `C:\ProgramData\`

📌 Used for stealth, persistence, or execution.

---

## 🔹 Filename-Based Indicators

### Common attacker techniques:

* Double extensions
  → `invoice.pdf.exe`

* Masquerading
  → `svch0st.exe`

* Randomized names
  → `a8F3k2.exe`

* Legitimate-looking names
  → `update-service.exe`

📌 These are early warning signals — not proof of compromise.

---

# 🔐 File Hashing

A hash acts as a **unique fingerprint of a file**.

---

## 🔹 Why Hashing Matters

* Identifies files regardless of name
* Enables threat intel lookup
* Supports correlation across systems

---

## 🔹 Common Algorithms

* MD5 (fast but less secure)
* SHA256 (preferred)

---

## 🔹 Example Commands

### Windows

```bash id="k1r8mz"
certutil -hashfile file.exe SHA256
Get-FileHash file.exe
```

### Linux

```bash id="o5d3pa"
sha256sum file.exe
```

---

## 📌 SOC Insight

Attackers can rename files —
➡️ **Hashes remain consistent across systems**

---

# 🌐 Hash Enrichment (Threat Intelligence)

After generating a hash, analysts enrich it using external intelligence sources.

---

## 🔍 Key Platforms

* VirusTotal
* MalwareBazaar
* Hybrid Analysis

---

## 🔹 Information Gathered

* Detection score (AV engines)
* Malware classification
* Associated domains / IPs
* Related samples
* Behavioral summaries

---

## 📌 Example Use Case

Hash lookup reveals:

* Known malware family
* Associated C2 infrastructure
* Previous campaign activity

➡️ Immediate context for investigation

---

# 🧪 Sandbox Analysis

Sandboxing allows safe execution of suspicious files.

---

## 🔹 Goals

* Observe runtime behavior
* Identify malicious actions
* Extract IOCs
* Confirm intent

---

## 🔍 Behavioral Indicators

* Process creation
* Registry modifications
* File drops
* Network connections
* Persistence mechanisms

---

## 📌 Key Insight

Static analysis shows **what the file is**
Sandboxing shows **what the file does**

---

# ⚠️ Sandbox Limitations

* Malware may detect sandbox environments
* Limited execution time
* Encrypted traffic may hide activity
* Fileless attacks may evade detection

📌 SOC Rule:

➡️ Never rely on a single source — always correlate.

---

# 🧬 MITRE ATT&CK Mapping

Behavior observed in sandbox can be mapped to ATT&CK techniques.

---

## Example Techniques

* Execution (T1059)
* Persistence (T1547)
* Command & Control (T1071)

📌 Mapping behavior improves:

* Detection rules
* Threat hunting
* Incident response

---

# 🔗 Full SOC Investigation Workflow

This room reflects a real SOC process:

---

## 🛡️ Step-by-Step

1. Detect suspicious file
2. Analyze filename and location
3. Generate hash
4. Enrich hash using threat intel
5. Analyze sandbox results
6. Extract IOCs
7. Map behavior to ATT&CK
8. Decide → benign / suspicious / malicious

---

📌 Core Principle:

➡️ **Collect → Enrich → Analyze → Decide**

---

# 🚨 Indicators of Compromise (IoCs)

## File-Based

* Suspicious filenames
* Unknown hashes
* Execution from temp directories

---

## Network-Based

* Malicious domains
* Suspicious IP connections

---

## Behavioral

* PowerShell execution
* Persistence mechanisms
* Unexpected child processes
* Outbound connections

---

# 🛡️ SOC Decision Making

Final step in the process:

* Benign → close alert
* Suspicious → monitor / escalate
* Malicious → incident response

📌 Intelligence supports **decision-making, not just detection**.

---

# 🛠️ Tools & Technologies

* `certutil`, `Get-FileHash`
* `sha256sum`
* VirusTotal
* MalwareBazaar
* Hybrid Analysis
* Sandbox environments
* MITRE ATT&CK

---

# 🧠 Key Takeaways

* File analysis starts with simple heuristics
* Hashing is essential for identification
* Threat intel platforms provide critical context
* Sandbox analysis reveals real behavior
* Detection requires correlation of multiple data sources
* SOC work is about making informed decisions

---

