# 🔐 Security Principles — DAY 56

## 📌 Overview

This repository documents the completion of the **Security Principles** room on TryHackMe.

This room introduces the fundamental concepts of information security, including the CIA Triad, common security models, and core principles that guide defensive security strategies.

All tasks have been successfully completed.

---

## 🎯 Learning Objectives Achieved

✔ Understand the CIA Triad
✔ Learn core security principles
✔ Identify common security models
✔ Understand risk, threats, and vulnerabilities
✔ Recognize how these principles apply to real-world environments

---

# 🧠 The CIA Triad

The CIA Triad is the foundation of information security.

## 🔹 Confidentiality

Ensures that sensitive information is only accessible to authorized individuals.

Examples:

* Encryption
* Access controls
* Multi-factor authentication

---

## 🔹 Integrity

Ensures that data is accurate, consistent, and protected from unauthorized modification.

Examples:

* Hashing (SHA256)
* Digital signatures
* File integrity monitoring

---

## 🔹 Availability

Ensures that systems and data are accessible when needed.

Examples:

* Redundancy
* Backups
* Disaster recovery plans
* DDoS protection

---

# ⚠️ Risk, Threats & Vulnerabilities

## 🔹 Threat

A potential cause of an unwanted incident (e.g., attacker, malware, insider threat).

## 🔹 Vulnerability

A weakness that can be exploited (e.g., outdated software, weak passwords).

## 🔹 Risk

The likelihood that a threat will exploit a vulnerability and cause impact.

Risk = Threat × Vulnerability × Impact

---

# 🏗️ Core Security Principles

## 🔹 Least Privilege

Users and systems should only have the minimum level of access necessary to perform their tasks.

---

## 🔹 Defense in Depth

Layered security approach where multiple controls protect assets.

Examples:

* Firewall
* IDS/IPS
* EDR
* SIEM

---

## 🔹 Separation of Duties

Critical tasks should be divided among multiple individuals to reduce risk of abuse.

---

## 🔹 Zero Trust

Never trust, always verify.

All access requests must be authenticated, authorized, and continuously validated.

---

# 📊 Common Security Models

## 🔹 Bell-LaPadula Model

Focuses on confidentiality.

* No Read Up
* No Write Down

Used in military and classified systems.

---

## 🔹 Biba Model

Focuses on integrity.

* No Read Down
* No Write Up

Prevents data corruption.

---

## 🔹 Clark-Wilson Model

Focuses on integrity through well-formed transactions and separation of duties.

---

# 🛡️ Practical Application in Cybersecurity

These principles apply to:

* Network segmentation
* Access control implementation
* Incident response strategies
* Vulnerability management
* Secure system architecture

Understanding these concepts is essential for SOC analysts, security engineers, and penetration testers.

---

