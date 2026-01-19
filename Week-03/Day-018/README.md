# 📅 Day 18 – Networking Core Protocols

## 🎯 Daily Objective

Understand the **core networking protocols** that enable communication across networks and how they are leveraged or abused from a cybersecurity perspective.

---

## 🔑 Core Networking Protocols

### 🌐 HTTP / HTTPS

Protocols used for web communication.

* **HTTP**: clear-text communication
* **HTTPS**: encrypted using TLS

**Basic interaction (manual):**

```bash
telnet <IP> <PORT>
GET / HTTP/1.1
Host: <IP>
```

**Security relevance:**

* Target of most web attacks
* Traffic inspection and interception
* Misconfigurations can expose sensitive data

---

### 📁 FTP

File Transfer Protocol used to transfer files between hosts.

* Uses port **21**

**Basic interaction:**

```bash
ftp <IP>
```

**Security relevance:**

* Clear-text credentials
* Anonymous access risks

---

### 🔐 SSH

Secure Shell protocol for remote administration.

* Port **22**

**Basic interaction:**

```bash
ssh user@<IP>
```

**Security relevance:**

* Brute-force attacks
* Key-based authentication
* Common entry point in compromised systems

---

### 📧 SMTP / POP3 / IMAP

Email-related protocols.

* **SMTP**: sending emails (25)
* **POP3**: receiving emails (110)
* **IMAP**: receiving emails (143)

**Basic interaction (SMTP example):**

```bash
telnet <IP> 25
HELO example.com
```

**Security relevance:**

* Phishing campaigns
* Credential harvesting
* Misconfigured mail servers

---

### 🧭 DNS

Domain Name System translates domain names into IP addresses.

**Basic interaction:**

```bash
dig example.com
nslookup example.com
```

**Security relevance:**

* DNS enumeration
* DNS spoofing
* Data exfiltration via DNS

---

## 🔍 Red Team Perspective

Understanding these protocols enables:

* Service identification during scans
* Target prioritization
* Choosing correct attack vectors
* Post-exploitation movement

---

## 🛠️ Tools Related

* `curl`, `wget`
* `ftp`
* `ssh`
* `dig`, `nslookup`
* `nmap`

---

## 📌 Key Takeaways

* Protocols define how services communicate
* Misuse or misconfiguration creates attack surfaces
* Protocol knowledge is mandatory for offensive operations

---
