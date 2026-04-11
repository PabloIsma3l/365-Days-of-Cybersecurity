# 🐚 Detecting Web Shells — TryHackMe

## 📅 Day 101 - 365 Days of Cybersecurity

## ✅ Status: Completed

---

## 🧠 Overview

In this room, I learned how to **identify and detect web shells**, a common persistence mechanism used by attackers after compromising a web server.

Web shells allow attackers to execute commands remotely, maintain access, and perform post-exploitation activities directly through a web interface.

Understanding how to detect them is essential for a **SOC Level 1 Analyst**, especially when monitoring compromised web servers.

---

## 🎯 Learning Objectives

* Understand what a web shell is and how it works
* Identify indicators of web shell activity
* Detect malicious behavior in web server logs
* Recognize common web shell patterns and usage
* Analyze attacker behavior post-compromise

---

## 🐚 What is a Web Shell?

A **web shell** is a malicious script uploaded to a web server that allows an attacker to execute commands remotely via HTTP requests.

### 🔹 Common Characteristics:

* Accessible through a browser
* Executes system commands
* Often hidden within legitimate directories
* Can be written in:

  * PHP
  * ASP
  * JSP
  * Python

---

## ⚙️ How Web Shells Work

1. Attacker exploits a vulnerability (e.g., file upload, RCE)
2. Uploads a malicious script (web shell)
3. Accesses the shell via a URL
4. Sends commands through HTTP requests
5. Server executes commands and returns output

📌 Example:

```
http://target.com/uploads/shell.php?cmd=whoami
```

---

## ⚠️ Common Web Shell Indicators

### 🔹 Suspicious File Names

* `shell.php`
* `cmd.php`
* `backdoor.php`
* Randomized or obfuscated names

---

### 🔹 Unusual File Locations

* Upload directories (`/uploads/`)
* Temporary folders
* Public web directories

---

### 🔹 Abnormal HTTP Requests

* Requests containing command parameters:

```
?cmd=
?exec=
?command=
```

---

### 🔹 Suspicious User Behavior

* Repeated access to a single script
* Requests from uncommon IP addresses
* Use of automated tools

---

## 📊 Log Analysis for Detection

### 🔹 Example Log Entry:

```
192.168.1.25 - - [15/Oct/2025:14:22:10] "GET /uploads/shell.php?cmd=whoami HTTP/1.1" 200
```

### 🔍 What to Look For:

* Repeated access to the same `.php` file
* Query parameters executing commands
* High frequency of requests
* Unusual response sizes (command output)

---

## 🧪 Indicators of Compromise (IoCs)

* Requests with `cmd`, `exec`, or similar parameters
* Access to suspicious scripts
* Unexpected files in web directories
* Repeated command execution patterns
* Unknown IPs interacting with server-side scripts

---

## 🛡️ Detection Techniques

### 🔹 Log Monitoring

* Analyze web server logs (Apache, Nginx)
* Look for suspicious parameters and endpoints

### 🔹 File Integrity Monitoring

* Detect newly added or modified files
* Identify unauthorized scripts

### 🔹 WAF Alerts

* Detect command injection attempts
* Monitor blocked requests

### 🔹 SIEM Correlation

* Combine logs from multiple sources
* Identify patterns across time

---

## 🔎 Attacker Behavior (Post-Exploitation)

Once a web shell is deployed, attackers may:

* Execute system commands (`whoami`, `ls`, `cat`)
* Browse directories
* Upload/download files
* Escalate privileges
* Establish persistence

📌 SOC Insight:
This phase is critical to detect before full compromise.

---

## 🛠️ Tools & Technologies

* Web server logs (Apache / Nginx)
* SIEM (Splunk / ELK)
* WAF (Cloudflare, ModSecurity)
* File monitoring tools
* Network analysis tools (Wireshark, NetworkMiner)

---

## 🧠 Key Takeaways

* Web shells are a common post-exploitation technique
* They allow attackers to maintain persistent access
* Detection relies heavily on log analysis and behavioral patterns
* Monitoring file changes is crucial
* Early detection can prevent deeper compromise

---

## 📌 Final Thoughts

This room helped me understand:

* How attackers maintain access after exploiting a system
* How to detect web shell activity in real-world environments
* What indicators to monitor as a SOC Analyst
* The importance of combining log analysis with behavioral detection

This knowledge is highly relevant for real SOC operations and incident response.
