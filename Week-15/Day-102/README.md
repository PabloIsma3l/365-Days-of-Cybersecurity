# 🌊 Detecting Web DDoS Attacks — TryHackMe DAY 102

## 📅 Day X - 365 Days of Cybersecurity

## ✅ Status: Completed

---

## 🧠 Overview

In this room, I learned how to **detect Distributed Denial of Service (DDoS) attacks** targeting web applications by analyzing traffic patterns, logs, and abnormal behavior.

DDoS attacks aim to overwhelm a server or service, making it unavailable to legitimate users. Detecting these attacks is a key responsibility for a **SOC Level 1 Analyst**.

---

## 🎯 Learning Objectives

* Understand how DDoS attacks work
* Identify different types of web-based DDoS attacks
* Detect abnormal traffic patterns
* Analyze logs to identify attack behavior
* Recognize Indicators of Compromise (IoCs)

---

## 🌊 What is a DDoS Attack?

A **Distributed Denial of Service (DDoS)** attack occurs when multiple systems flood a target with traffic, exhausting its resources and causing service disruption.

### 🔹 Goals:

* Make the application unavailable
* Exhaust server resources (CPU, memory, bandwidth)
* Disrupt business operations

---

## ⚙️ Types of Web DDoS Attacks

### 🔹 Volumetric Attacks

* High volume of traffic
* Consumes bandwidth

📌 Example:

* Massive number of HTTP requests

---

### 🔹 Application Layer Attacks (Layer 7)

* Targets specific endpoints (e.g., login pages)
* Harder to detect than volumetric attacks

📌 Examples:

* HTTP GET/POST floods
* Slow requests (Slowloris-style attacks)

---

### 🔹 Protocol Attacks

* Exploit weaknesses in protocols
* Consume server resources

---

## 📊 Detection via Traffic Analysis

### 🔍 Key Indicators:

* Sudden spike in traffic
* High number of requests from multiple IPs
* Repeated requests to the same endpoint
* Unusual traffic patterns

---

## 📄 Log Analysis

### 🔹 Example Log Pattern:

```id="91bq0o"
192.168.1.10 - - [20/Oct/2025:10:00:01] "GET /index.html HTTP/1.1" 200
192.168.1.11 - - [20/Oct/2025:10:00:01] "GET /index.html HTTP/1.1" 200
192.168.1.12 - - [20/Oct/2025:10:00:01] "GET /index.html HTTP/1.1" 200
```

### 🔍 What to Look For:

* High volume of requests in a short time
* Multiple IP addresses targeting the same resource
* Repeated identical requests
* Increased error rates (503, 504)

---

## 🚨 Indicators of Compromise (IoCs)

* Traffic spikes beyond normal baseline
* Multiple IPs sending similar requests
* Repeated access to a single endpoint
* High number of 5xx errors
* Abnormal request rates per second

---

## 🛡️ Detection in a SOC Environment

### 🔹 Monitoring Sources:

* Web server logs (Apache, Nginx)
* WAF logs
* CDN metrics
* SIEM dashboards

---

### 🔹 Detection Strategies:

* Baseline normal traffic behavior
* Identify anomalies in request rate
* Correlate logs across multiple sources
* Monitor response times and error rates

---

## 🌐 Role of CDN and WAF in DDoS Protection

### 🔹 CDN (Content Delivery Network)

* Distributes traffic across multiple servers
* Absorbs high traffic loads
* Helps mitigate volumetric attacks

---

### 🔹 WAF (Web Application Firewall)

* Filters malicious HTTP requests
* Blocks suspicious patterns
* Helps mitigate Layer 7 attacks

📌 SOC Insight:

* Many DDoS attempts are visible in WAF/CDN logs even if mitigated

---

## 🔎 Attacker Behavior

During a DDoS attack, attackers may:

* Use botnets to generate traffic
* Rotate IP addresses
* Target specific endpoints repeatedly
* Attempt to evade detection with varied requests

---

## 🛠️ Tools & Technologies

* SIEM (Splunk / ELK)
* WAF (Cloudflare, AWS WAF, ModSecurity)
* CDN services
* Web server logs
* Network monitoring tools

---

## 🧠 Key Takeaways

* DDoS attacks focus on availability disruption
* Traffic pattern analysis is key for detection
* Baselines are essential to identify anomalies
* Layer 7 attacks are more subtle and targeted
* CDN and WAF play a critical role in mitigation

---

## 📌 Final Thoughts

This room helped me understand:

* How to detect DDoS attacks using logs and traffic analysis
* The difference between volumetric and application-layer attacks
* The importance of monitoring and baselining traffic
* How defensive technologies (CDN, WAF) assist in detection and mitigation

These skills are essential for handling real-world incidents in a SOC environment.
