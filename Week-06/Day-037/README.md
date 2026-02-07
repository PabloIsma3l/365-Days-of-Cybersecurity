# 🕷️ Burp Suite — TryHackMe (Day 37)

## 📌 Overview

This section corresponds to **Day 37** of my TryHackMe learning path, focused on **Burp Suite**, one of the most important tools for **web application security testing**. In this part, I completed all tasks **up to Task 8 (Part 1)**.

Burp Suite is widely used by penetration testers to intercept, analyze, and manipulate HTTP/S traffic between the browser and the target application.

---

## 🎯 Learning Objectives

* Understand what Burp Suite is and how it fits into web pentesting
* Learn how a proxy works in web security
* Configure a browser to work with Burp Suite
* Intercept and analyze HTTP requests and responses
* Become familiar with Burp Suite's main tabs and workflow

---

## 🧠 Burp Suite Basics

### What is Burp Suite?

Burp Suite is a **web proxy tool** that allows you to sit between your browser and a web server. This makes it possible to inspect, modify, and replay web traffic.

It is commonly used for:

* Web application testing
* Finding vulnerabilities such as SQL Injection, XSS, IDOR, etc.
* Understanding how web applications communicate

---

## 🌐 How the Proxy Works

When Burp Suite is running as a proxy:

```
Browser  <-->  Burp Suite  <-->  Web Server
```

All HTTP/S traffic passes through Burp, allowing full visibility and control over requests and responses.

---

## ⚙️ Initial Setup

### Burp Suite Configuration

* Burp Suite Community Edition was used
* Proxy listener running on:

  * `127.0.0.1:8080`

### Browser Configuration

* Browser traffic configured to go through Burp
* Burp CA certificate installed to intercept HTTPS traffic

---

## 🔎 Proxy Tab

The **Proxy** tab is the core of Burp Suite.

### Intercept

* Allows interception of HTTP requests before they are sent to the server
* Requests can be:

  * Forwarded
  * Dropped
  * Modified

Example of intercepted request:

```http
GET / HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0
```

---

## 📂 Target Tab

The **Target** tab provides a structured view of the application:

* Site map of discovered endpoints
* Helps understand application structure
* Useful for planning attacks and testing scope

---

## 🧪 Repeater (Introduction)

Repeater allows:

* Manual modification of requests
* Re-sending requests multiple times
* Observing how the server responds to changes

This is extremely useful for:

* Parameter manipulation
* Authentication testing
* Input validation analysis

---

## 🧠 Key Concepts Learned (Up to Task 8 – Part 1)

✔ How Burp Suite intercepts traffic
✔ How to configure proxy settings
✔ Difference between request and response
✔ Importance of HTTPS certificate installation
✔ Understanding Burp's workflow and UI

---

## 🔐 Security Relevance

Burp Suite is a **core Red Team tool**. Mastering it is essential for:

* Web application pentesting
* Bug bounty hunting
* CTF challenges
* Real-world offensive security assessments

---

## 📚 Next Steps

* Continue with Burp Suite tasks (rest tasks – Part 2)
* Deep dive into Repeater and Intruder
* Apply Burp Suite in SQLi and XSS labs

---

🧠 *Progress logged as part of my daily cybersecurity practice — Day 37.*
