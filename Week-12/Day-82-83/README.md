# 🎯 The Greenholt Phish — TryHackMe (Completed) DAY 83

## 📌 Overview

This document summarizes the completion of **"The Greenholt Phish"** room on TryHackMe.

This lab simulates a **real-world phishing incident investigation**, where an analyst must identify the initial access vector, analyze email artifacts, extract indicators of compromise (IOCs), and determine the scope and impact of the attack.

---

## 🎯 Learning Objectives Achieved

✔ Investigate a phishing incident end-to-end
✔ Analyze malicious emails and attachments
✔ Extract and validate IOCs
✔ Understand attacker techniques and intent
✔ Apply a structured SOC investigation workflow

---

## 🧠 Investigation Approach

A structured methodology was applied:

1. **Alert Intake** → Review reported phishing email
2. **Email Analysis** → Inspect headers, sender, and content
3. **Artifact Extraction** → URLs, domains, attachments
4. **Enrichment** → Reputation checks and context gathering
5. **Correlation** → Link artifacts across the incident
6. **Impact Assessment** → Determine affected users/systems
7. **Response Actions** → Recommend containment and remediation

---

## 🔎 Key Analysis Findings

### 🔹 Email Analysis

* Identified **sender spoofing / lookalike domain**
* Detected **social engineering techniques** (urgency, impersonation)
* Inconsistencies between display name and actual domain

---

### 🔹 URL & Domain Analysis

* Suspicious / newly registered domains
* Mismatch between visible link and actual URL
* Potential redirection behavior

---

### 🔹 Attachment Analysis

* Presence of potentially malicious document
* Indicators of macro-enabled or payload delivery

---

### 🔹 Indicators of Compromise (IOCs)

Examples of extracted IOCs:

* Malicious domains
* Suspicious IP addresses
* File hashes (if applicable)

These can be used for:

* Blocking at firewall / proxy level
* SIEM correlation
* Threat hunting activities

---

## 📊 Attack Flow (Simplified)

1. Phishing email delivered to target
2. User interaction (link click or attachment open)
3. Redirection or payload execution
4. Potential credential harvesting or malware delivery

---

## 🛡️ SOC Response Actions

Recommended actions based on findings:

* Block malicious domains and IPs
* Quarantine similar emails across the organization
* Reset compromised user credentials
* Perform endpoint checks for malware
* Update detection rules (SIEM / EDR)

---

## 🧩 MITRE ATT&CK Mapping

* **Initial Access** → Phishing (T1566)
* **Credential Access** → Credential Harvesting (if applicable)
* **Execution** → Malicious attachment / script

---

## 🛡️ SOC Perspective

This lab reflects a real SOC workflow:

* Alert triage
* Email investigation
* IOC extraction and enrichment
* Incident scoping
* Containment and reporting

---

## 🏁 Room Completion Status

* ✅ All tasks completed

---

## 🚀 Key Takeaways

* Phishing remains a primary initial access vector
* Small inconsistencies in emails reveal attacker intent
* Structured investigation is critical for efficiency
* IOC extraction enables broader organizational defense
* Real-world scenarios require both technical and analytical skills

---

🚀 *This room demonstrates practical SOC-level phishing investigation skills, simulating a real incident response scenario from detection to containment.*
