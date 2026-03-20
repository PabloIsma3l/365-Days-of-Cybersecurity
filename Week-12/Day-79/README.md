# 🛠️ Phishing Analysis Tools — TryHackMe day 79

## 📌 Overview

This document summarizes the completion of the **"Phishing Analysis Tools"** room on TryHackMe.

This room focuses on the tools commonly used by security analysts to investigate phishing emails, extract indicators of compromise (IOCs), and validate suspicious content.

Understanding these tools is essential for **SOC Analysts and Incident Responders**, as phishing is one of the most frequent entry points for cyber attacks.

---

## 🎯 Learning Objectives

* Learn the tools used for phishing analysis
* Understand how to analyze email headers
* Extract and validate IOCs
* Investigate suspicious URLs and attachments

---

## 🧰 Common Phishing Analysis Tools

### 🔹 Email Header Analyzers

Used to analyze email headers and trace the origin of messages.

Examples:

* Identify sender spoofing
* Validate SPF, DKIM, and DMARC
* Trace mail servers involved

---

### 🔹 URL Analysis Tools

Used to inspect suspicious links safely.

Capabilities:

* Detect malicious domains
* Identify redirects
* Analyze domain reputation

---

### 🔹 File Analysis Tools

Used to analyze suspicious attachments.

Examples:

* Check file hashes
* Identify malware signatures
* Perform static analysis

---

### 🔹 Threat Intelligence Platforms

Provide context about indicators such as IPs, domains, and hashes.

Examples:

* Reputation checks
* Historical data on threats
* Known malicious campaigns

---

## 🔎 Practical Workflow

Typical phishing investigation workflow:

1. Analyze the email header
2. Extract URLs and attachments
3. Check domain and IP reputation
4. Analyze attachments (if present)
5. Correlate findings with threat intelligence

---

## 🛡️ SOC Use Case

In a SOC environment, analysts use these tools to:

* Investigate reported phishing emails
* Validate suspicious indicators
* Block malicious domains and IPs
* Prevent further compromise

---

## 🏁 Room Completion Status

* ✅ All tasks completed

---

## 🚀 Key Takeaways

* Tools are essential for efficient phishing analysis
* Email headers provide critical technical evidence
* URLs and attachments must always be validated
* Threat intelligence enhances investigation accuracy

---

🚀 *This room strengthens practical skills in using real-world tools to analyze a
