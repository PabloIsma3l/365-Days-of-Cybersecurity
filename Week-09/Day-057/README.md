# 🌐 OWASP Top 10 2025 — IAAA Failures & Application Design Flaws Day 57

## 📌 Overview

This repository documents the completion of the following TryHackMe rooms:

* **OWASP Top 10 2025: IAAA Failures**
* **OWASP Top 10 2025: Application Design Flaws**

These rooms focus on understanding critical web application vulnerabilities and how weaknesses in authentication, authorization, and application design lead to real-world security breaches.

All tasks have been successfully completed.

---

# 🔐 OWASP Top 10 2025 — IAAA Failures

IAAA stands for:

* **Identification**
* **Authentication**
* **Authorization**
* **Accountability**

This section covers vulnerabilities related to improper implementation of these controls.

---

## 🎯 Covered Categories

### 🔹 A01 – Broken Access Control

Occurs when users can access resources or perform actions outside their intended permissions.

Examples:

* Accessing another user's account data
* IDOR (Insecure Direct Object Reference)
* Privilege escalation
* Forced browsing

Impact:

* Data exposure
* Unauthorized modifications

Prevention:

* Enforce server-side authorization checks
* Apply least privilege
* Use proper access control validation

---

### 🔹 A07 – Identification & Authentication Failures

Weak authentication mechanisms allow attackers to compromise user accounts.

Examples:

* Weak password policies
* Credential stuffing
* Brute force attacks
* Session fixation

Impact:

* Account takeover
* Data breaches

Prevention:

* Multi-factor authentication (MFA)
* Secure session management
* Rate limiting

---

### 🔹 A09 – Security Logging & Monitoring Failures

Occurs when applications fail to properly log and monitor suspicious activity.

Examples:

* No logging of failed login attempts
* Missing alerts for privilege escalation
* Lack of centralized monitoring

Impact:

* Delayed incident detection
* Extended attacker dwell time

Prevention:

* Centralized logging
* SIEM integration
* Real-time alerting

---

# 🏗️ OWASP Top 10 2025 — Application Design Flaws

This section focuses on vulnerabilities caused by poor architectural decisions or insecure design practices.

---

## 🎯 Covered Categories

### 🔹 A02 – Cryptographic Failures

Occurs when sensitive data is not properly protected.

Examples:

* Weak encryption algorithms
* Hardcoded cryptographic keys
* No HTTPS implementation

Impact:

* Data exposure
* Credential leakage

Prevention:

* Strong encryption standards
* Secure key management
* TLS implementation

---

### 🔹 A03 – Injection

Occurs when untrusted input is interpreted as commands or queries.

Examples:

* SQL Injection
* Command Injection
* LDAP Injection

Impact:

* Data exfiltration
* Remote code execution

Prevention:

* Input validation
* Parameterized queries
* Least privilege database accounts

---

### 🔹 A06 – Vulnerable & Outdated Components

Using outdated libraries or software with known vulnerabilities.

Examples:

* Unpatched frameworks
* Unsupported software versions

Impact:

* Exploitable known CVEs
* System compromise

Prevention:

* Patch management
* Dependency tracking
* Regular vulnerability scanning

---

### 🔹 A10 – Server-Side Request Forgery (SSRF)

Occurs when an application fetches remote resources without validating user-supplied URLs.

Examples:

* Accessing internal services
* Cloud metadata exposure

Impact:

* Internal network exposure
* Privilege escalation

Prevention:

* Input validation
* Network segmentation
* Allowlist-based URL filtering

---

# 🛡️ Practical Security Impact

Understanding these vulnerabilities is critical for:

* Secure application development
* Web penetration testing
* SOC monitoring and detection
* Incident response investigations

These categories represent the most critical web security risks in modern environments.

---

## 🏁 Room Completion Status

* ✅ Both rooms completed
* 🧠 Strong understanding of modern OWASP Top 10 web application risks achieved

---

