# 📅 Day 19 – Networking Secure Protocols

## 🎯 Daily Objective

Learn how **TLS, SSH, and VPNs** secure network traffic and understand their role in protecting data confidentiality, integrity, and authentication.

---

## 🔐 TLS (Transport Layer Security)

TLS is a cryptographic protocol that secures communication between clients and servers.

* Commonly used in **HTTPS**
* Encrypts data in transit
* Prevents eavesdropping and tampering

### 📊 Common Clear-Text vs Secure Ports

| Protocol | Default Port (Clear Text) | Secure Version | Secure Port |
| -------- | ------------------------- | -------------- | ----------- |
| HTTP     | 80                        | HTTPS          | 443         |
| SMTP     | 25                        | SMTPS          | 465 / 587   |
| POP3     | 110                       | POP3S          | 995         |
| IMAP     | 143                       | IMAPS          | 993         |

Understanding these ports is critical during **reconnaissance and service identification**.

**Basic interaction / inspection:**

```bash
openssl s_client -connect <IP>:443
```

This allows manual inspection of:

* TLS handshake
* Certificates
* Cipher suites

**Security relevance:**

* Certificate misconfigurations
* Weak cipher suites
* Expired or self-signed certificates

---

## 🔑 SSH (Secure Shell)

SSH provides encrypted remote access to systems.

* Port **22** by default
* Supports password and key-based authentication

**Basic interaction:**

```bash
ssh user@<IP>
```

**Security relevance:**

* Brute-force attempts
* Weak credentials
* Key mismanagement

---

## 🌐 VPN (Virtual Private Network)

VPNs create an **encrypted tunnel** between devices or networks.

* Protect traffic over untrusted networks
* Hide internal IP addressing

**Basic interaction (example):**

```bash
openvpn config.ovpn
```

**Security relevance:**

* Misconfigured VPNs expose internal networks
* Split tunneling risks
* VPN access often equals network-level trust

---

## 🔍 Red Team Perspective

Understanding secure protocols allows:

* Identifying weak or outdated encryption
* Detecting trust assumptions
* Targeting misconfigurations rather than encryption itself

Encryption is rarely broken — **implementations are**.

---

## 📌 Key Takeaways

* Secure protocols protect data in transit
* Misconfiguration undermines strong cryptography
* Attackers focus on endpoints and configuration flaws

---
