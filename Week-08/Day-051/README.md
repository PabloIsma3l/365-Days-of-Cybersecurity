# 🔎 Vulnerability Scanner Overview — DAY 51
## 📌 Overview

This repository documents the completion of the **Vulnerability Scanner Overview** room on TryHackMe.

This room introduces vulnerability scanners, how they operate, their role in security assessments, and how they support defensive security operations.

All tasks have been successfully completed.

---

## 🎯 Learning Objectives Achieved

✔ Understand what a vulnerability scanner is
✔ Learn how vulnerability scanning works
✔ Identify different types of scanners
✔ Understand authenticated vs unauthenticated scans
✔ Recognize how scanning supports vulnerability management programs

---

## 🧠 What is a Vulnerability Scanner?

A **vulnerability scanner** is a security tool used to identify weaknesses, misconfigurations, and known vulnerabilities in systems, networks, and applications.

It works by:

* Discovering live hosts
* Enumerating open ports and services
* Identifying software versions
* Matching findings against vulnerability databases (CVE, NVD)

The goal is to detect security weaknesses before attackers exploit them.

---

## ⚙️ How Vulnerability Scanners Work

Typical scanning process:

1️⃣ Host discovery
2️⃣ Port scanning
3️⃣ Service enumeration
4️⃣ Version detection
5️⃣ Vulnerability matching
6️⃣ Risk scoring (CVSS)

Scanners rely heavily on vulnerability feeds and signature databases.

---

## 🏗️ Types of Vulnerability Scanners

### 🌐 Network-Based Scanners

* Scan network devices and servers
* Identify open ports and exposed services
* Detect outdated software

---

### 🖥️ Host-Based Scanners

* Installed locally on systems
* Perform deeper inspection
* Detect missing patches and insecure configurations

---

### 🌍 Web Application Scanners

* Focus on web applications
* Detect vulnerabilities such as:

  * SQL Injection
  * Cross-Site Scripting (XSS)
  * File inclusion vulnerabilities
  * Misconfigured headers

---

## 🔐 Authenticated vs Unauthenticated Scans

### 🔓 Unauthenticated Scan

* Simulates an external attacker
* Limited visibility
* Only detects externally exposed vulnerabilities

---

### 🔑 Authenticated Scan

* Uses valid credentials
* Provides deeper inspection
* Detects missing patches and internal misconfigurations
* More accurate results

Authenticated scans reduce false positives.

---

## 📊 Risk Scoring (CVSS)

Most scanners classify vulnerabilities using the **Common Vulnerability Scoring System (CVSS)**.

Severity levels:

* Low
* Medium
* High
* Critical

CVSS scores help prioritize remediation efforts.

---

## 🛠️ Common Vulnerability Scanning Tools

* Nessus
* OpenVAS
* Qualys
* Nexpose

These tools are widely used in enterprise environments.

---

## 🔄 Vulnerability Management Lifecycle

1️⃣ Asset discovery
2️⃣ Vulnerability scanning
3️⃣ Risk assessment
4️⃣ Remediation (patching/config fixes)
5️⃣ Verification scan
6️⃣ Reporting

Continuous scanning is essential for maintaining security posture.

---

## ⚠️ Limitations of Vulnerability Scanners

* False positives
* False negatives
* Cannot detect zero-day vulnerabilities
* May generate large volumes of findings

Scanners do not replace manual testing or penetration testing.

---

