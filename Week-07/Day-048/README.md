# 📊 Introduction to SIEM — TryHackMe Day 48

## 📌 Overview

This repository documents the completion of the **Introduction to SIEM** room on TryHackMe.

This room focuses on the fundamentals of SIEM (Security Information and Event Management), its architecture, core features, and how it supports security monitoring, detection, and incident response operations.

All tasks have been successfully completed (100%).

---

## 🎯 Learning Objectives Achieved

✔ Understand what a SIEM is and why it is used
✔ Learn how logs are collected and centralized
✔ Understand event normalization and correlation
✔ Explore alerting mechanisms
✔ Recognize SIEM use cases in SOC environments
✔ Understand dashboards and reporting capabilities

---

## 🧠 What is a SIEM?

A **SIEM (Security Information and Event Management)** system is a centralized platform that:

* Collects logs from multiple sources
* Normalizes and parses data
* Correlates events
* Generates alerts
* Provides dashboards and reporting

SIEMs are core components of modern Security Operations Centers (SOC).

---

## 🏗️ SIEM Architecture

A typical SIEM environment includes:

### 1️⃣ Log Collection

Data sources may include:

* Firewalls
* Servers (Linux/Windows)
* Endpoints
* IDS/IPS
* Web servers
* Applications
* Cloud platforms

---

### 2️⃣ Log Parsing & Normalization

Raw logs are:

* Parsed into structured fields
* Normalized into a common format
* Indexed for fast searching

This enables cross-platform correlation.

---

### 3️⃣ Correlation Engine

The SIEM applies detection rules such as:

* Multiple failed logins + successful login
* Suspicious IP access patterns
* Unusual privilege escalation

Correlation reduces noise and improves detection accuracy.

---

### 4️⃣ Alerting & Notifications

When detection rules trigger:

* Alerts are generated
* Analysts are notified
* Tickets may be created automatically

---

### 5️⃣ Dashboards & Reporting

SIEM dashboards provide:

* Real-time monitoring
* Threat trends
* Compliance reporting
* Executive summaries

---

## 🔎 Common SIEM Use Cases

* Detect brute force attacks
* Identify suspicious outbound traffic
* Monitor administrative privilege usage
* Detect malware beaconing
* Identify lateral movement
* Track compliance violations

---

## 🛡️ SIEM vs Traditional Monitoring

Traditional logging:

* Decentralized
* Manual review required

SIEM:

* Centralized visibility
* Automated correlation
* Real-time alerting
* Scalable investigation capability

---

## 🔐 SIEM in Incident Response

During an investigation, SIEM helps to:

1. Identify initial compromise
2. Correlate events across systems
3. Build an attack timeline
4. Extract Indicators of Compromise (IOCs)
5. Validate containment actions

SIEM acts as the investigative backbone of SOC operations.

---

## 🐧 Common Linux Log Paths

In Linux environments, logs are typically stored under `/var/log/`. Below are commonly analyzed paths during investigations and SIEM ingestion:

### 🔐 Authentication Logs

* `/var/log/auth.log` (Debian/Ubuntu)
* `/var/log/secure` (RHEL/CentOS)

Used to detect:

* Failed login attempts
* SSH access
* Privilege escalation (sudo usage)

---

### 🖥️ System Logs

* `/var/log/syslog`
* `/var/log/messages`
* `/var/log/dmesg`
* `/var/log/boot.log`

Used to analyze:

* System events
* Service failures
* Kernel messages

---

### 🌐 Web Server Logs

**Apache:**

* `/var/log/apache2/access.log`
* `/var/log/apache2/error.log`

**Nginx:**

* `/var/log/nginx/access.log`
* `/var/log/nginx/error.log`

Used to detect:

* Brute force attempts
* SQL injection attempts
* Suspicious HTTP requests

---

### 📅 Scheduled Tasks & Audit Logs

* `/var/log/cron`
* `/var/log/audit/audit.log`

Used to detect:

* Malicious scheduled jobs
* Policy violations
* Suspicious system calls

---

### 👤 Login History

* `/var/log/wtmp`
* `/var/log/btmp`
* `/var/run/utmp`

Useful for:

* Reviewing login sessions
* Detecting failed authentication attempts

---

These log sources are frequently integrated into SIEM platforms for centralized monitoring and correlation.

---

## 🏁 Room Completion Status

* ✅ 100% completed
* 🧠 Strong understanding of SIEM fundamentals achieved

---
