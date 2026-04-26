# 🔬 Intro to Malware Analysis — TryHackMe

## 📅 Day 116 - 365 Days of Cybersecurity

## ✅ Status: Completed

---

# 🧠 Overview

In this room, I learned the fundamentals of **malware analysis from a defender’s perspective**, focusing on how to triage suspicious files and determine whether a sample is malicious.

The room introduced:

* Static Analysis
* Dynamic Analysis
* PE file basics
* Sandboxing
* Process tree investigation
* Basic anti-analysis concepts

📌 Key concept:

Malware analysis is about collecting enough evidence to answer:

* What is this file?
* What does it do?
* Is it malicious?
* How should defenders detect it?

---

# 🎯 Learning Objectives

* Understand the purpose of malware analysis
* Differentiate static vs dynamic analysis
* Perform basic analysis of a PE sample
* Extract indicators from malware artifacts
* Use sandbox results to understand behavior

---

# 🧪 Malware Analysis Approaches

## 🔹 Static Analysis

Analyzing malware **without executing it**.

Techniques covered:

* File identification
* Strings extraction
* Hashing
* PE header analysis
* Imports review

---

## Example:

Check file type:

```bash id="h7b3ca"
file redline
```

Result:

* PE32 executable
* Nullsoft installer archive

---

## Extract Strings

```bash id="g9j2mx"
strings redline | less
```

Used to find:

* URLs
* Commands
* Suspicious strings
* Potential IoCs

---

## Generate Hash

```bash id="m4tkq1"
md5sum redline
```

Sample MD5:

```text id="7v2npe"
ca2dc5a3f94c4f19334cc8b68f256259
```

Used for:

* VirusTotal / Hybrid Analysis lookup
* Sample identification
* Threat intelligence correlation

---

# 🧱 PE Header Analysis

Analyzed metadata inside the Portable Executable.

---

## Important Sections

* `.text` → Executable code
* `.rdata` → Read-only data
* `.data` → Variables
* `.rsrc` → Resources
* `.ndata` → Unusual custom section

---

## Entropy Analysis

Using:

```bash id="n6fpz0"
pecheck redline
```

Observed `.text` entropy:

```text id="8mvrpt"
6.453919
```

📌 Why it matters:

High entropy may suggest:

* Packing
* Encryption
* Obfuscation

Low/normal entropy may suggest:

* Unpacked sample

([Medium][1])

---

## Imports Analysis

Interesting imported API:

```text id="k2qv8z"
RegOpenKeyExW
```

From:

```text id="d5r2cf"
ADVAPI32.dll
```

Potential indicator:

* Registry interaction

---

# 📦 Packing & Obfuscation Awareness

Learned how malware can evade static analysis through:

* Packers
* Obfuscation
* Compressed payloads

Indicators:

* High entropy
* Garbage strings
* Suspicious PE sections

---

# ⚙️ Dynamic Analysis

Analyzing malware **by executing it in a controlled environment**.

---

## 🧪 Sandbox Analysis

Used:

* Hybrid Analysis

Observed:

* Threat score
* MITRE mappings
* Process behavior
* Network activity
* Behavioral indicators

---

## Process Tree Analysis

Important finding:

First process launched:

```text id="x4twp1"
setup_installer.exe
```

Process relationships revealed:

* `cmd.exe`
* `powershell.exe`

being used by the malware. ([Reddit][2])

---

## 📌 SOC Insight

Process trees reveal:

Parent
→ Child
→ Payload actions

Critical for:

* Detection engineering
* Incident investigation

---

# 🔎 Static vs Dynamic Analysis

## Static Analysis

Finds:

* Strings
* Imports
* Hashes
* Indicators

Fast, safe, low risk.

---

## Dynamic Analysis

Finds:

* Runtime behavior
* Persistence actions
* Network connections
* Child processes

Higher visibility.

---

## 📌 Key Lesson

Best results come from:

Static + Dynamic Analysis

➡️ Hybrid approach.

---

# 🚨 Indicators of Compromise (IoCs)

Potential indicators observed:

* Suspicious hashes
* Registry-related imports
* Packed sections
* PowerShell execution
* Unexpected child processes
* Suspicious network activity

---

# 🛡️ Malware Triage Workflow

Basic workflow learned:

1. Identify suspicious file
2. Collect hashes
3. Run static analysis
4. Inspect PE metadata
5. Check sandbox behavior
6. Analyze process tree
7. Extract indicators

---

# 🛠️ Tools & Concepts Covered

* `file`
* `strings`
* `md5sum`
* `pecheck`
* PE Tree
* Hybrid Analysis
* Entropy analysis
* Process tree investigation

---

# 🧠 Key Takeaways

* Malware analysis starts with triage
* Static analysis can reveal valuable indicators quickly
* Entropy and imports can expose suspicious traits
* Sandboxing reveals runtime behavior static analysis misses
* Process trees are critical for understanding malware execution
* Combining multiple techniques improves confidence

---

# 📌 Final Thoughts

This room helped me:

* Build a foundation in malware triage
* Perform basic static and dynamic analysis
* Understand PE structures and indicators
* Use sandbox reports to investigate behavior
* Strengthen a malware-analysis mindset from a SOC perspective

