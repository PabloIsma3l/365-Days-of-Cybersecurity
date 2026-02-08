# 🐍DAY-039 Hydra — Offensive Security Tools (TryHackMe)

## 📌 Overview

This repository documents my hands-on practice with **Hydra**, completed as part of **Day 39** in my TryHackMe learning path, within the room **"Tools for Offensive Security / Hydra"**.

Hydra is a **fast and flexible online password cracking tool** used to perform **brute-force and credential attacks** against various network services. It is a fundamental tool for **Red Team operations** and **offensive security assessments**.

---

## 🎯 Learning Objectives

* Understand what Hydra is and when to use it
* Learn Hydra syntax and command structure
* Perform brute-force attacks against common services
* Interpret Hydra output correctly
* Understand ethical and legal boundaries of password attacks

---

## 🧠 What is Hydra?

Hydra (also known as **THC-Hydra**) is a **login cracker** that supports numerous protocols and services.

### Commonly Supported Services

* SSH
* FTP
* HTTP / HTTPS (basic, form-based)
* SMB
* RDP
* Telnet
* MySQL / PostgreSQL

Hydra is commonly used during:

* Initial access attempts
* Password auditing
* CTF challenges
* Red Team engagements

---

## ⚙️ Basic Syntax

```bash
hydra [options] <target> <service>
```

### Common Options

* `-l` → Single username
* `-L` → Username wordlist
* `-p` → Single password
* `-P` → Password wordlist
* `-s` → Specify port
* `-t` → Number of parallel threads
* `-f` → Stop after first valid login
* `-V` → Verbose output

---

## 🔐 Example Attacks

### 🔑 SSH Brute Force

```bash
hydra -l root -P passwords.txt ssh://10.10.10.10
```

### 📂 FTP Brute Force

```bash
hydra -l admin -P passwords.txt ftp://10.10.10.10
```

### 🌐 HTTP POST Form

```bash
hydra -l admin -P passwords.txt 10.10.10.10 http-post-form \
"/login.php:username=^USER^&password=^PASS^:Invalid login"
```

---

## 📤 Output Interpretation

Successful login attempts are shown clearly:

```
[22][ssh] host: 10.10.10.10   login: admin   password: password123
```

Important:

* Always verify credentials manually
* False positives can occur with misconfigured failure messages

---

## 🧠 Key Concepts Learned (Day 39)

✔ Hydra workflow and syntax
✔ Difference between services and modules
✔ Importance of correct failure messages (HTTP forms)
✔ Ethical usage and scope awareness

---

## 🔐 Security Relevance (Red Team)

Hydra is a **core offensive tool** used for:

* Credential-based attacks
* Weak password discovery
* Validating security controls
* Gaining initial access during engagements

Used incorrectly, it can cause:

* Account lockouts
* Service disruption

---

## 🖼️ Proof of Completion

* Day 39 completed
* Room: *Tools for Offensive Security — Hydra*
* Screenshot evidence stored in repository (image)

---

## 📚 Learning Sources

* TryHackMe — Tools for Offensive Security
* THC-Hydra documentation

---

