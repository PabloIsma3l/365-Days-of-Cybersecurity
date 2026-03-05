# 🛡️ Introduction to EDR — Day 64
## 📌 Overview

This repository documents the completion of the **Introduction to EDR** room on TryHackMe.

This room introduces the fundamentals of **Endpoint Detection and Response (EDR)** technologies, explaining how they monitor endpoint activity, detect threats, and help security teams investigate and respond to attacks.

All tasks have been successfully completed.

---

## 🎯 Learning Objectives Achieved

✔ Understand what EDR is and why it is important
✔ Learn how EDR detects malicious activity
✔ Identify key EDR features and capabilities
✔ Understand how EDR supports SOC investigations
✔ Explore endpoint telemetry and behavioral analysis

---

## 🧠 What is EDR?

**Endpoint Detection and Response (EDR)** is a security solution that continuously monitors endpoint devices such as:

* Workstations
* Servers
* Laptops
* Virtual machines

EDR tools collect telemetry from these endpoints and analyze activity to detect suspicious or malicious behavior.

---

## 🎯 Goals of EDR

EDR solutions aim to:

* Detect advanced threats on endpoints
* Provide visibility into endpoint activity
* Investigate security incidents
* Respond quickly to attacks
* Contain compromised systems

---

## 🔍 Key EDR Capabilities

### 1️⃣ Endpoint Monitoring

EDR continuously collects data such as:

* Process execution
* File modifications
* Registry changes
* Network connections
* User activity

---

### 2️⃣ Threat Detection

Detection methods include:

* Signature-based detection
* Behavioral analysis
* Machine learning detection
* Indicators of Compromise (IOCs)

---

### 3️⃣ Incident Investigation

EDR allows analysts to:

* Trace process execution
* View parent-child process relationships
* Investigate suspicious files
* Analyze command-line activity

---

### 4️⃣ Threat Response

EDR platforms can respond to incidents by:

* Isolating compromised endpoints
* Killing malicious processes
* Quarantining files
* Blocking malicious hashes or domains

---

## 📊 Why EDR is Important for SOC Teams

EDR provides:

* Deep visibility into endpoint activity
* Rapid investigation capabilities
* Faster incident containment
* Stronger threat detection

SOC analysts frequently rely on EDR data when triaging alerts.

---

## 🧰 Common EDR Platforms

Examples of widely used EDR solutions:

* Microsoft Defender for Endpoint
* CrowdStrike Falcon
* SentinelOne
* VMware Carbon Black
* Elastic Security

These platforms provide centralized visibility and response capabilities.

---

## 🔎 Example Investigation with EDR

Typical workflow for SOC analysts:

1️⃣ Alert triggered by SIEM or EDR
2️⃣ Analyst reviews endpoint telemetry
3️⃣ Investigates suspicious processes
4️⃣ Correlates activity with logs
5️⃣ Determines if activity is malicious
6️⃣ Contains the endpoint if necessary

---

## 🚨 Common Threats Detected by EDR

* Malware execution
* Ransomware behavior
* Privilege escalation
* Suspicious PowerShell activity
* Lateral movement attempts

