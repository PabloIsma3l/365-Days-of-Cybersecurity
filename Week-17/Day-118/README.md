# 🕵️ Shadow Trace — TryHackMe

## 📅 Day 118 - 365 Days of Cybersecurity

## ✅ Status: Completed

---

# 🧠 Overview

In this room, I worked through a **SOC triage and malware investigation scenario**, analyzing a suspicious binary and correlating EDR alerts to identify malicious activity.

Focus areas included:

* Static malware triage
* IOC extraction
* Alert analysis
* Obfuscated payload decoding
* Correlation of suspicious activity

📌 Key Concept:

This room felt like a mini **SOC investigation case**, moving from suspicious file → indicators → alerts → attack reconstruction.

---

# 🎯 Learning Objectives

* Perform initial malware triage on a suspicious executable
* Extract Indicators of Compromise (IOCs)
* Analyze suspicious EDR alerts
* Decode obfuscated attacker activity
* Correlate evidence into an attack narrative

---

# 🔬 Static File Analysis

Suspicious sample investigated:

```text id="ax4p72"
windows-update.exe
```

Masquerading as a legitimate updater.

---

## 🧱 Binary Triage with PEStudio

Analysis revealed:

### Architecture

```text id="g4m9ra"
64-bit
```

---

## SHA-256 Hash

```text id="qn6kfr"
b2a88de3e3bcfae4a4b38fa36e884c586b5cb2c2c283e71fba59efdb9ea64bfc
```

Used for:

* Threat intel lookup
* Sample identification
* IOC enrichment

---

## Suspicious URL Discovered

```text id="dfm8oc"
http://tryhatme.com/update/security-update.exe
```

Domain IOC:

```text id="g1tpr8"
responses.tryhatme.com
```

📌 Static analysis can often reveal network indicators without execution. ([Medium][1])

---

## Network-Capable Imports

Interesting imported library:

```text id="t3ca8e"
WS2_32.dll
```

Indicates:

* Socket communications
* Potential beaconing / downloads

---

# 🔎 IOC Extraction

Indicators recovered:

* SHA-256 hash
* Malicious URLs
* Domain IOC
* Networking DLL imports
* Encoded embedded artifacts

---

## Base64 Decoding

Encoded artifact recovered and decoded using CyberChef.

Technique:

```text id="q8yl0p"
From Base64
```

📌 Good example of lightweight malware triage + artifact extraction.

---

# 🚨 Alert Analysis (EDR Investigation)

Two critical alerts analyzed:

* powershell.exe
* chrome.exe

---

## 🔹 PowerShell Alert

Observed:

* `FromBase64String()` usage
* Encoded PowerShell activity

Decoded malicious URL:

```text id="d5rc3m"
https://tryhatme.com/dev/main.exe
```

Indicators:

* Obfuscation
* Download cradle behavior
* Suspicious PowerShell execution

---

## 🔹 Browser-Based Payload Delivery

Chrome alert revealed obfuscated JavaScript building a malicious URL through ASCII values.

Decoded URL:

```text id="s6uq0a"
https://reallysecureupdate.tryhatme.com/update.exe
```

Saved payload:

```text id="c7nkwr"
test.txt
```

📌 Great example of suspicious browser activity generating malicious downloads. ([Medium][2])

---

# 🧬 Obfuscation Techniques Observed

## PowerShell

* Base64 encoding
* Hidden malicious URL

---

## JavaScript

* ASCII character arrays
* String reconstruction

Used to hide:

* Payload locations
* Malicious intent

Classic defense evasion pattern.

---

# 🔗 Attack Chain Reconstruction

1. Suspicious fake updater discovered
2. Static analysis reveals malicious IOCs
3. PowerShell attempts payload retrieval
4. Browser-based JavaScript downloads additional payload
5. Potential multi-stage malware delivery

➡️ Suspected downloader / staged infection chain

---

# 🚨 Indicators of Compromise (IoCs)

## File-Based

* SHA256 hash
* Suspicious binary name
* Network-capable imports

---

## Network-Based

* tryhatme.com
* responses.tryhatme.com
* reallysecureupdate.tryhatme.com

---

## Behavioral

* Encoded PowerShell
* Browser-driven payload download
* Suspicious child-process activity
* Obfuscated script execution

---

# 🛡️ SOC Investigation Workflow

This room reinforced a practical workflow:

1. Triage suspicious file
2. Extract artifacts / IOCs
3. Analyze EDR alerts
4. Decode obfuscated content
5. Correlate evidence
6. Reconstruct attack story

---

# 🧪 Concepts Practiced

* Static malware triage
* PE analysis
* IOC extraction
* EDR alert investigation
* Base64 decoding
* Obfuscated JavaScript analysis
* Attack-chain correlation

---

# 🛠️ Tools Used

* PEStudio
* CyberChef
* PowerShell
* EDR alert console
* Basic Python decoding logic

---

# 🧠 Key Takeaways

* Initial triage can reveal valuable IOCs quickly
* Obfuscation often hides infrastructure, not intent
* EDR alerts require context and correlation
* Browser activity can be part of malware delivery
* File analysis + alert analysis provides stronger investigations
* This mirrors real SOC alert triage work

---

# 📌 Final Thoughts

This room helped me:

* Practice real-world SOC triage methodology
* Extract and analyze malware indicators
* Investigate suspicious EDR alerts
* Decode obfuscated attacker activity
* Strengthen incident correlation skills
