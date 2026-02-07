# 🕷️ Burp Suite — Master README (TryHackMe)

## 📌 Overview

This repository documents my **hands-on learning and practice with Burp Suite**, one of the most essential tools for **web application penetration testing**.

Burp Suite acts as an **intercepting proxy** that allows full visibility and control over HTTP and HTTPS traffic between a client (browser) and a server (web application). It is a core tool for **Red Team operations**, **bug bounty**, and **CTF challenges**.

This README serves as a **master reference**, while daily progress (e.g. Day 37) is tracked in separate logs.

---

## 🎯 Objectives

* Understand how web traffic works at the HTTP level
* Learn to intercept, analyze, and manipulate requests and responses
* Use Burp Suite modules effectively during web assessments
* Build a strong foundation for exploiting web vulnerabilities

---

## 🧠 What is Burp Suite?

Burp Suite is a **web security testing platform** developed by PortSwigger. It is designed to help security professionals identify vulnerabilities in web applications.

### Common Use Cases

* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Insecure Direct Object References (IDOR)
* Authentication and session testing
* Parameter tampering

---

## 🌐 How Burp Suite Works

```
Browser  <-->  Burp Suite (Proxy)  <-->  Web Server
```

All HTTP/S traffic flows through Burp, allowing:

* Inspection of raw requests and responses
* Modification before forwarding
* Replay and automation of attacks

---

## ⚙️ Installation & Setup

### Requirements

* Burp Suite Community or Professional
* Web browser (Firefox / Chromium)

### Proxy Configuration

* Proxy listener: `127.0.0.1:8080`
* Browser configured to route traffic through Burp
* Burp CA certificate installed for HTTPS interception

---

## 🧩 Burp Suite Main Components

### 🔎 Proxy

The **Proxy** module is the core of Burp Suite.

* Intercepts HTTP/S requests
* Allows forwarding, dropping, or modifying traffic
* Useful for understanding application behavior

---

### 🎯 Target

* Displays the application structure as a site map
* Helps define testing scope
* Allows better attack planning

---

### 🔁 Repeater

Repeater is used for **manual request manipulation**.

* Modify parameters and headers
* Send requests multiple times
* Analyze server responses

Ideal for:

* Authentication testing
* Input validation checks
* Logic flaws

---

### ⚡ Intruder

Intruder automates attacks against parameters.

* Brute force attacks
* Fuzzing inputs
* Payload injection

Common uses:

* Password attacks
* Parameter discovery
* Rate-limit testing

---

### 📊 Logger / HTTP History

* Stores all captured requests and responses
* Useful for reviewing traffic
* Helps identify hidden endpoints

---

## 🧪 Example HTTP Request

```http
POST /login HTTP/1.1
Host: target.com
Content-Type: application/x-www-form-urlencoded

username=admin&password=admin
```

Understanding raw requests is critical for exploiting vulnerabilities.

---

## 🔐 Security Relevance (Red Team Perspective)

Burp Suite is indispensable for:

✔ Web application penetration testing
✔ Bug bounty programs
✔ CTF competitions
✔ Real-world Red Team engagements

Most web vulnerabilities **cannot be reliably exploited without Burp Suite**.

---
## 📚 Learning Source

* TryHackMe — Burp Suite rooms

