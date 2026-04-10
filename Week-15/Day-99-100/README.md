# 🕵️ Detecting Web Attacks — TryHackMe

## 📅 Day 100 - 365 Days of Cybersecurity

## ✅ Status: Completed

---

## 🧠 Overview

In this room, I learned how to **detect web-based attacks** by analyzing HTTP traffic, server logs, and identifying malicious patterns in real-world scenarios.

This is a core skill for a **SOC Level 1 Analyst**, as web applications are one of the most common attack vectors, and many attacks can be detected through proper log and traffic analysis.

---

## 🎯 Learning Objectives

* Analyze HTTP requests and responses for malicious activity
* Identify common web attack patterns
* Detect anomalies in web server logs
* Understand how attackers interact with web applications
* Recognize Indicators of Compromise (IoCs)

---

## 🌐 HTTP Traffic Analysis

Web attacks are typically visible within HTTP requests. Key components to analyze:

* **Request Method** (GET, POST, etc.)
* **URL / Endpoint**
* **Query Parameters**
* **Headers** (User-Agent, Cookies, Referrer)
* **Request Body**

📌 SOC Insight:
Attackers manipulate these elements to inject payloads and exploit vulnerabilities.

---

## ⚠️ Common Web Attacks & Detection

### 🔹 SQL Injection (SQLi)

**Example payloads:**

```
' OR 1=1 --
' UNION SELECT username, password FROM users --
```

**Detection Indicators:**

* SQL keywords in user input
* Authentication bypass attempts
* Abnormal query patterns in logs

---

### 🔹 Cross-Site Scripting (XSS)

**Example payloads:**

```
<script>alert('XSS')</script>
<img src=x onerror=alert(1)>
```

**Detection Indicators:**

* JavaScript embedded in parameters
* Encoded payloads (`%3Cscript%3E`)
* Reflected input in responses

---

### 🔹 Directory Traversal

**Example:**

```
../../../../etc/passwd
```

**Detection Indicators:**

* Repeated use of `../`
* Attempts to access system or restricted files

---

### 🔹 Command Injection

**Example:**

```
; whoami
&& cat /etc/passwd
```

**Detection Indicators:**

* Shell operators (`;`, `&&`, `|`)
* Unexpected command execution patterns

---

### 🔹 Brute Force / Credential Attacks

**Indicators:**

* Multiple login attempts in a short period
* Repeated 401/403 responses
* Same IP targeting authentication endpoints

---

## 📊 Web Server Log Analysis

Logs are one of the most important sources for detecting attacks.

### 🔹 Example Log Entry:

```
192.168.1.15 - - [12/Oct/2025:10:15:22] "GET /login.php?user=admin' OR '1'='1 HTTP/1.1" 200
```

### 🔍 What to Analyze:

* **IP Address** → Identify attacker origin
* **Timestamp** → Detect patterns or bursts
* **Request** → Look for malicious payloads
* **Status Code** → Understand server response
* **User-Agent** → Detect automation tools

---

## 🚨 Indicators of Compromise (IoCs)

* Injection payloads in URLs or request bodies
* High number of failed login attempts
* Access to unusual or sensitive endpoints
* Abnormal User-Agent strings (e.g., scripts, scanners)
* High frequency of requests (possible scanning/fuzzing)
* Repeated 4xx and 5xx responses

---

## 🛡️ Detection in a SOC Environment

From a SOC perspective, detecting web attacks involves:

* Monitoring **web server logs** (Apache, Nginx, IIS)
* Reviewing **WAF alerts**
* Correlating events in a **SIEM (Splunk, ELK)**
* Identifying anomalies in traffic behavior
* Investigating suspicious IP addresses and patterns

---

## 🧪 Example Detection Scenarios

### Scenario 1: SQL Injection Attempt

* Suspicious query parameter detected
* Response code 200 (possible bypass)
* Same IP repeating similar payloads

### Scenario 2: Brute Force Attack

* Multiple failed login attempts
* Repeated 401 responses
* High request rate from single IP

### Scenario 3: XSS Attempt

* Script tags detected in parameters
* Encoded payloads in requests

---

## 🛠️ Tools & Technologies

* **Wireshark** → Packet analysis
* **NetworkMiner** → Traffic reconstruction
* **SIEM (Splunk / ELK)** → Log correlation and detection
* **Web Server Logs** → Primary evidence source
* **WAF Logs** → Blocked attack attempts

---

## 🧠 Key Takeaways

* Web attacks leave clear traces in HTTP traffic and logs
* Recognizing payload patterns is essential for detection
* Log analysis is a critical SOC skill
* Many attacks can be detected before exploitation if monitored correctly
* Understanding attacker behavior improves detection capabilities

---

## 📌 Final Thoughts

This room strengthened my ability to:

* Detect real-world web attacks
* Analyze logs from a defensive perspective
* Identify malicious patterns in HTTP traffic
* Think like both an attacker and a defender

This is a fundamental step toward becoming a skilled SOC Analyst.
