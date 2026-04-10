# 🕵️ Detecting Web Attacks — TryHackMe

## 📅 Day 99 - 365 Days of Cybersecurity

## 🚧 Progress: 50%

---

## 🧠 Overview

In this room, I am learning how to **detect web-based attacks** by analyzing HTTP traffic, logs, and identifying malicious patterns.

This is a critical skill for a **SOC Level 1 Analyst**, as many real-world attacks target web applications and can be identified through log analysis and traffic inspection.

---

## 🎯 Learning Objectives (So far)

* Understand how web attacks appear in HTTP traffic
* Identify suspicious patterns in requests
* Analyze logs to detect malicious activity
* Recognize common attack techniques in real scenarios

---

## 🌐 HTTP Traffic Analysis

Web attacks are often visible in HTTP requests. Key elements to analyze:

* **URL / Endpoint**
* **Request Method (GET, POST)**
* **Headers (User-Agent, Cookies, etc.)**
* **Parameters (Query strings / Body data)**

📌 SOC Insight:
Attackers often manipulate these fields to inject malicious payloads.

---

## ⚠️ Common Attack Patterns (Observed)

### 🔹 SQL Injection (SQLi)

**Example payloads:**

```
' OR 1=1 --
' UNION SELECT NULL,NULL --
```

📌 Indicators:

* Unexpected SQL keywords in parameters
* Authentication bypass attempts
* Abnormal query structures

---

### 🔹 Cross-Site Scripting (XSS)

**Example payloads:**

```
<script>alert('XSS')</script>
<img src=x onerror=alert(1)>
```

📌 Indicators:

* JavaScript inside input fields
* Encoded payloads (%3Cscript%3E)

---

### 🔹 Directory Traversal

**Example:**

```
../../../../etc/passwd
```

📌 Indicators:

* Use of `../`
* Attempts to access system files

---

### 🔹 Command Injection

**Example:**

```
; whoami
&& ls
```

📌 Indicators:

* Shell operators (`;`, `&&`, `|`)
* System command execution attempts

---

## 📊 Log Analysis

Logs are a primary source for detecting attacks.

### 🔹 Example Log Entry:

```
192.168.1.10 - - [10/Oct/2025:13:55:36] "GET /login.php?id=1' OR '1'='1 HTTP/1.1" 200
```

### 🔍 What to Look For:

* Suspicious parameters
* Repeated requests (brute force / fuzzing)
* Unusual status codes (401, 403, 500)
* High request frequency

---

## 🚨 Indicators of Compromise (IoCs)

* Injection payloads in URLs
* Abnormal request patterns
* Multiple failed login attempts
* Unusual User-Agent strings
* Access to sensitive files or endpoints

---

## 🛡️ Detection Perspective (SOC)

From a SOC point of view, detection involves:

* Monitoring **web server logs**
* Reviewing **WAF alerts**
* Correlating events in a **SIEM**
* Identifying anomalies in traffic behavior

---

## 🛠️ Tools Mentioned / Used

* Wireshark
* NetworkMiner
* SIEM (Splunk / ELK)
* Web server logs (Apache / Nginx)

---

## 🧠 Key Takeaways (So far)

* Web attacks leave identifiable traces in HTTP traffic
* Understanding payload patterns is essential for detection
* Logs are a critical source of evidence
* Early detection can prevent exploitation

---

## 🚧 Status

Currently halfway through the room. Continuing to build skills in:

* Advanced detection techniques
* Real-world attack scenarios
* Log-based investigation
