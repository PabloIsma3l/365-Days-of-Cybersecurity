# 🎣 Phishing Analysis Fundamentals — TryHackMe DAY 77

## 📌 Overview

This document summarizes the completion of the **"Phishing Analysis Fundamentals"** room on TryHackMe.

Phishing is one of the most common initial access vectors used by attackers. This room introduces the fundamentals of analyzing phishing emails, identifying malicious indicators, and understanding how attackers trick users into compromising systems.

This knowledge is essential for **SOC Analysts, Incident Responders, and Blue Team professionals**.

---

## 🎯 Learning Objectives

* Understand what phishing is and how it works
* Identify different types of phishing attacks
* Analyze email headers and content
* Detect malicious links and attachments
* Recognize common phishing indicators

---

## 🧠 What is Phishing?

Phishing is a **social engineering attack** where attackers impersonate legitimate entities to trick victims into:

* Revealing credentials
* Clicking malicious links
* Downloading malware

Phishing is commonly delivered via:

* Email
* SMS (Smishing)
* Voice calls (Vishing)

---

## 🎯 Types of Phishing Attacks

### 🔹 Generic Phishing

* Mass emails sent to many users
* Low personalization

### 🔹 Spear Phishing

* Targeted attacks against specific individuals
* Uses personal or organizational context

### 🔹 Whaling

* Targets high-value individuals (executives)

---

## 📧 Email Analysis Basics

When analyzing phishing emails, key components include:

### 🔹 Sender Address

* Check for spoofed or suspicious domains

### 🔹 Subject Line

* Urgency or fear tactics

### 🔹 Email Body

* Grammar mistakes
* Suspicious requests
* Social engineering techniques

---

## 🔎 Email Headers Analysis

Headers provide technical details about the email’s origin.

Important fields:

* **From** – claimed sender
* **Return-Path** – actual sending address
* **Received** – mail servers involved
* **SPF/DKIM/DMARC** – authentication checks

Headers help determine if the email is **spoofed or legitimate**.

---

## 🔗 Malicious Links & Attachments

### Links

* Hover to inspect URLs
* Look for domain spoofing
* Shortened or obfuscated URLs

### Attachments

* Suspicious file types (.exe, .js, .docm)
* May contain malware or macros

---

## 🚨 Common Phishing Indicators

* Urgent language ("Act now!")
* Unexpected attachments
* Requests for credentials
* Mismatched URLs
* Poor grammar or formatting

---

## 🛡️ Phishing in SOC Operations

SOC analysts:

* Investigate reported phishing emails
* Extract IOCs (IPs, domains, hashes)
* Block malicious domains
* Educate users

Phishing analysis is often the **first step in detecting an attack**.

---

## 🏁 Room Completion Status

* ✅ All tasks completed

---

## 🚀 Key Takeaways

* Phishing is a primary initial access vector
* Email headers are critical for verification
* Links and attachments must always be analyzed
* Social engineering plays a key role in attacks

---

🚀 *This room builds foundational skills required to analyze phishing attempts and detect initial access techniques used by attackers.*
