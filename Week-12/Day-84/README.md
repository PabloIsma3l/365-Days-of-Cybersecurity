# 🎣 Snapped Phish-ing Line — TryHackMe DAY 84

## 📌 Overview

This document summarizes the completion of the **"Snapped Phish-ing Line"** room on TryHackMe.

This lab focuses on analyzing a **large-scale phishing campaign**, where multiple malicious emails and URLs are investigated to uncover attacker infrastructure, techniques, and impact.

It builds on previous phishing knowledge and emphasizes **correlation, IOC enrichment, and campaign analysis**.

---

## 🎯 Learning Objectives

* Investigate phishing campaigns at scale
* Analyze multiple malicious emails and URLs
* Correlate indicators across different artifacts
* Identify attacker infrastructure
* Apply SOC investigation techniques

---

## 🧠 Investigation Approach

A structured workflow was followed:

1. **Email Review** → Identify suspicious messages
2. **Artifact Extraction** → URLs, domains, attachments
3. **IOC Enrichment** → Reputation checks and analysis
4. **Correlation** → Link indicators across multiple samples
5. **Campaign Identification** → Understand attacker scope

---

## 🔎 Key Analysis Areas

### 🔹 Email Analysis

* Identification of phishing patterns
* Reused templates across campaigns
* Social engineering techniques

---

### 🔹 URL & Domain Analysis

* Detection of malicious domains
* Identification of phishing infrastructure
* Analysis of redirects and landing pages

---

### 🔹 Campaign Correlation

* Linking multiple phishing emails
* Identifying shared infrastructure
* Recognizing patterns across attacks

---

### 🔹 IOC Identification

Examples:

* Malicious domains
* Suspicious IP addresses
* URLs used in phishing emails

---

## 📊 Attack Campaign Insights

* Attackers often reuse infrastructure
* Campaigns may target multiple users or organizations
* Patterns help detect future attacks

---

## 🛡️ SOC Response Actions

* Block identified domains and IPs
* Add IOCs to SIEM and detection tools
* Alert users about phishing attempts
* Monitor for similar activity

---

## 🧩 MITRE ATT&CK Mapping

* **Initial Access** → Phishing (T1566)
* **Credential Access** → Credential Harvesting
* **Command and Control** → Malicious domains (if applicable)

---

## 🏁 Room Completion Status

* ✅ All tasks completed

---

## 🚀 Key Takeaways

* Phishing campaigns often reuse infrastructure
* Correlating indicators is key to identifying campaigns
* IOC enrichment improves detection capabilities
* Campaign-level analysis is critical in SOC environments

---

🚀 *This room strengthens the ability to analyze phishing campaigns at scale and apply real-world SOC investigation techniques.*
