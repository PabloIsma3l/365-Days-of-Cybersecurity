# 📧 Phishing Emails in Action — TryHackMe DAY 78

## 📌 Overview

This document summarizes the completion of the **"Phishing Emails in Action"** room on TryHackMe.

This room builds on phishing fundamentals by analyzing **real-world phishing email examples**. The focus is on identifying indicators of compromise (IOCs), recognizing social engineering tactics, and understanding how attackers craft convincing phishing campaigns.

---

## 🎯 Learning Objectives

* Analyze real phishing email samples
* Identify indicators of phishing attempts
* Recognize social engineering techniques in practice
* Extract IOCs from malicious emails
* Improve detection skills for SOC environments

---

## 🧠 Practical Phishing Analysis

Unlike theoretical rooms, this lab focuses on **hands-on analysis of actual phishing emails**.

Analysts must evaluate:

* Email structure
* Sender information
* Links and attachments
* Language and intent

---

## 🔎 Key Indicators Identified

### 🔹 Suspicious Sender

* Domains that mimic legitimate companies
* Slight misspellings (typosquatting)
* External addresses pretending to be internal

---

### 🔹 Malicious Links

* URLs that do not match the displayed text
* Use of shortened or obfuscated links
* Domains designed to look legitimate

---

### 🔹 Social Engineering Techniques

Attackers commonly use:

* Urgency ("Immediate action required")
* Fear ("Your account will be suspended")
* Authority impersonation (IT, banks, managers)

---

### 🔹 Attachments

* Malicious documents (.docm, .xlsm)
* Executable files disguised as legitimate documents

---

## 📊 IOC Extraction

During analysis, analysts extract Indicators of Compromise such as:

* Malicious domains
* Suspicious IP addresses
* File hashes (if available)

These IOCs can then be used to:

* Block threats
* Enrich SIEM alerts
* Support threat hunting

---

## 🛡️ SOC Perspective

In a SOC environment, phishing investigations typically involve:

1. Receiving a reported email
2. Analyzing headers and content
3. Extracting IOCs
4. Blocking malicious indicators
5. Notifying affected users

---

## 🏁 Room Completion Status

* ✅ All tasks completed

---

## 🚀 Key Takeaways

* Real phishing emails often appear highly convincing
* Small details can reveal malicious intent
* Social engineering is a critical component of phishing attacks
* IOC extraction is essential for defense and detection

---

🚀 *This room strengthens practical phishing detection skills by exposing analysts to real-world attack scenarios and teaching how to identify them effectively.*
