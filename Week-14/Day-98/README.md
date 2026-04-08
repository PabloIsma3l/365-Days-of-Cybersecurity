# 🌐 Web Security Essentials — TryHackMe DAY 98

## 📅 Day X - 365 Days of Cybersecurity

## 🧠 Overview

In this room, I learned the fundamentals of web security, including how web applications work, their main components, and the most common vulnerabilities exploited by attackers.

This knowledge is essential for a **SOC Level 1 Analyst**, as it helps identify suspicious activity in HTTP/HTTPS traffic, logs, and alerts related to web applications.

---

## 🌍 How the Web Works

A web application is based on communication between:

- **Client (Browser)** → The user
- **Web Server** → Processes requests and returns responses
- **HTTP/HTTPS Protocol** → Communication method

### 🔹 Basic Flow:
1. The client sends a request (GET, POST, etc.)
2. The server processes the request
3. The server returns a response (HTML, JSON, etc.)

---

## 🖥️ Web Application vs Web Server vs Host Machine

Understanding these differences is critical for both security analysis and incident detection:

### 🔹 Web Application
- The **software users interact with**
- Includes frontend and backend logic
- Example: login forms, dashboards, APIs

📌 Focus:
- Business logic
- Vulnerabilities like SQLi, XSS, CSRF

---

### 🔹 Web Server
- Software that **handles HTTP/HTTPS requests**
- Serves content to users

Examples:
- Apache
- Nginx
- IIS

📌 Focus:
- Request/response handling
- Logs (very important for SOC)
- Misconfigurations

---

### 🔹 Host Machine
- The **physical or virtual machine** where everything runs

📌 Includes:
- Operating System (Linux/Windows)
- Services and processes

📌 Focus:
- OS-level attacks
- Privilege escalation
- Persistence mechanisms

---

## 📡 HTTP vs HTTPS

### HTTP
- Unencrypted protocol
- Vulnerable to **Man-in-the-Middle (MITM)** attacks

### HTTPS
- Uses **TLS/SSL encryption**
- Protects confidentiality and integrity

---

## 🔍 HTTP Methods

Key methods learned:

- **GET** → Retrieve data
- **POST** → Send data to the server
- **PUT** → Update resources
- **DELETE** → Remove resources

📌 Notes:
- GET → Parameters visible in URL
- POST → Data sent in request body

---

## 📦 HTTP Status Codes

### ✅ 2xx (Success)
- 200 OK
- 201 Created

### ⚠️ 3xx (Redirection)
- 301 Moved Permanently
- 302 Found

### ❌ 4xx (Client Errors)
- 400 Bad Request
- 401 Unauthorized
- 403 Forbidden
- 404 Not Found

### 💥 5xx (Server Errors)
- 500 Internal Server Error
- 503 Service Unavailable

---

## 🍪 Cookies and Sessions

### Cookies
- Stored in the browser
- Maintain session state

### Risks:
- **Session Hijacking**
- **Session Fixation**

📌 SOC Relevance:
- Detect abnormal session usage

---

## 🌐 Content Delivery Network (CDN)

A **CDN** is a distributed network of servers that deliver web content based on the user's geographic location.

### 🔹 Purpose:
- Improve performance (faster load times)
- Reduce latency
- Increase availability

### 🔹 Security Benefits:
- Absorbs traffic spikes
- Helps mitigate **DDoS attacks**
- Hides the origin server

📌 SOC Insight:
- Traffic may come from CDN IPs instead of real clients
- Important when analyzing logs and identifying sources

---

## 🛡️ Web Application Firewall (WAF)

A **WAF** protects web applications by filtering and monitoring HTTP traffic.

### 🔹 Functions:
- Blocks malicious requests
- Detects attack patterns (SQLi, XSS, etc.)
- Applies security rules

### 🔹 Examples:
- Cloudflare WAF
- AWS WAF
- ModSecurity

📌 SOC Insight:
- Alerts may come from WAF logs
- False positives are common
- Useful for detecting attack attempts even if blocked

---

## ⚠️ Common Web Vulnerabilities

### 1. SQL Injection (SQLi)
- Manipulates SQL queries
- Can expose or modify data

### 2. Cross-Site Scripting (XSS)
- Injects malicious scripts
- Can steal cookies or sessions

### 3. Cross-Site Request Forgery (CSRF)
- Forces users to perform unwanted actions

### 4. File Inclusion (LFI/RFI)
- Includes unauthorized files

### 5. Command Injection
- Executes system commands

---

## 🛡️ OWASP Top 10

- Broken Access Control
- Cryptographic Failures
- Injection
- Security Misconfiguration
- Vulnerable Components
- Authentication Failures

📌 Important for:
- Threat detection
- Risk prioritization

---

## 🔐 Authentication vs Authorization

- **Authentication** → Who you are
- **Authorization** → What you can do

---

## 📊 SOC Level 1 Relevance

This knowledge is essential for:

- Analyzing web server logs (Apache, Nginx)
- Detecting attack patterns (SQLi, XSS)
- Investigating alerts from:
  - WAF
  - SIEM
  - IDS/IPS

- Interpreting HTTP traffic using:
  - Wireshark
  - NetworkMiner

---

## 🧪 Indicators of Compromise (IoCs)

- `' OR 1=1` payloads
- `<script>` injections
- Repeated access attempts
- Suspicious User-Agents
- High volume of 4xx/5xx responses

---

## 🛠️ Related Tools

- Burp Suite
- OWASP ZAP
- Wireshark
- NetworkMiner
- Browser Developer Tools

---

## 🧠 Key Takeaways

- Web applications are a primary attack surface
- Understanding infrastructure layers is critical (App, Server, Host)
- CDNs and WAFs play a major role in modern web security
- Web traffic analysis is a core SOC skill
- Detecting anomalies in HTTP requests is essential for threat detection