# 🧨 Gobuster — Offensive Security Tools (TryHackMe)

## 📌 Overview

This repository documents my hands-on practice with **Gobuster**, completed as part of **Day 40** in my TryHackMe learning path.

Gobuster is a **directory, file, DNS, and virtual host brute-forcing tool** written in Go. It is widely used during the **reconnaissance and enumeration phase** of web application penetration testing and Red Team operations.

---

## 🎯 Learning Objectives

* Understand what Gobuster is and when to use it
* Perform directory and file enumeration
* Use wordlists effectively
* Interpret Gobuster results correctly
* Apply Gobuster during web reconnaissance

---

## 🧠 What is Gobuster?

Gobuster is a fast brute-force enumeration tool used to discover:

* Hidden directories and files
* DNS subdomains
* Virtual hosts

It is commonly used after identifying a web service with tools like **Nmap**.

---

## ⚙️ Installation

Gobuster comes pre-installed on Kali Linux. If needed:

```bash
sudo apt install gobuster
```

---

## 🧩 Gobuster Modes

### 📂 Directory / File Enumeration (dir)

Used to discover hidden directories and files.

```bash
gobuster dir -u http://target.com -w wordlist.txt
```

Common options:

* `-u` → Target URL
* `-w` → Wordlist
* `-x` → File extensions (e.g. php, txt, html)
* `-t` → Threads
* `-o` → Output file

Example:

```bash
gobuster dir -u http://10.10.10.10 -w /usr/share/wordlists/dirb/common.txt -x php,txt
```

---

### 🌐 DNS Enumeration (dns)

```bash
gobuster dns -d target.com -w subdomains.txt
```

---

### 🧭 Virtual Host Enumeration (vhost)

```bash
gobuster vhost -u http://target.com -w vhosts.txt
```

---

## 📤 Output Interpretation

Gobuster outputs discovered paths and status codes:

```
/admin (Status: 301)
/login.php (Status: 200)
/backup.txt (Status: 200)
```

Important:

* Status codes **200 / 301 / 302** are usually interesting
* Always manually verify findings in a browser or Burp Suite

---

## 🧠 Key Concepts Learned (Day 40)

✔ Web enumeration methodology
✔ Importance of wordlists
✔ File extension fuzzing
✔ Recon before exploitation

---

## 🔐 Security Relevance (Red Team)

Gobuster is critical for:

* Discovering hidden attack surfaces
* Finding admin panels and backup files
* Identifying misconfigurations
* Supporting further exploitation (SQLi, LFI, RCE)

---

## 🖼️ Proof of Completion

* Day 40 completed
* Tool: Gobuster
* Screenshot evidence stored in repository (image)

---

## 📚 Learning Sources

* TryHackMe — Tools for Offensive Security
* Gobuster documentation

---

