# 🐧 Linux Threat Detection 1 — TryHackMe

## 📅 Day 111 - 365 Days of Cybersecurity

## ✅ Status: Completed

---

## 🧠 Overview

In this room, I learned how to **detect real attacks on Linux systems**, focusing on:

* **Initial Access via SSH**
* **Service exploitation**
* **Process tree analysis for investigation**

The main goal is to move from simple log analysis to **understanding how an attack happened and tracing its origin**, which is essential in a SOC environment.

---

## 🎯 Learning Objectives

* Detect SSH-based attacks (brute force & unauthorized access)
* Identify compromised accounts and attacker IPs
* Analyze web/service logs for exploitation attempts
* Use **process tree analysis** to trace attacker activity
* Understand real-world initial access techniques

---

## 🔐 Initial Access via SSH

SSH is one of the most common entry points in Linux environments.

📌 Key Risk:

* Internet-exposed SSH = high attack surface ([Medium][1])

---

### 🔍 Key Detection Indicators

* Multiple failed login attempts
* Successful login after failures
* Logins from external/untrusted IPs
* Use of password authentication instead of SSH keys

---

### 🔎 Example Detection

```bash
grep "Failed password" /var/log/auth.log
grep "Accepted" /var/log/auth.log
```

---

### 📌 SOC Insight

A common attack pattern:

1. Brute force attempts (many failed logins)
2. Successful login
3. Account compromise

➡️ Classic **SSH brute force attack** ([Medium][1])

---

## 🚨 Detecting SSH Attacks

### 🔹 Indicators of Compromise (IoCs)

* High volume of failed login attempts
* Multiple users targeted (botnet behavior)
* External IP performing login attempts
* Successful login to privileged account (e.g., root)

---

### 🔹 Example Attack Pattern

* Botnet targets multiple users
* Eventually compromises a privileged account
* Gains full system access

📌 SOC Insight:
Attackers often **rotate usernames and IPs** during brute force attempts ([Medium][1])

---

## 🌐 Initial Access via Services

Attackers may exploit **public-facing services**.

### 🔹 Example: Command Injection

* Application allows execution of system commands
* Attacker injects commands (e.g., `whoami`, `cat`)

---

### 🔍 Detection Clues

* Suspicious commands in logs
* Unexpected file access
* Application behavior anomalies

---

### 📌 Example Scenario

* Attacker interacts with a vulnerable service
* Executes commands via injection
* Reads sensitive files

➡️ Leads to **remote code execution (RCE)** ([Medium][1])

---

## 🧬 Process Tree Analysis (CRITICAL)

This is the **most important concept in this room**.

### 🔹 What is it?

Tracing:

➡️ **Which process started another process**

---

### 🔹 Why it matters

Instead of asking:

❌ “What happened?”
✅ Ask: **“What triggered this?”**

---

### 🔍 Example Investigation

1. Suspicious command detected (`whoami`)
2. Identify its **parent process (PPID)**
3. Trace back to original application
4. Identify attacker entry point

---

### 🔹 Tools Used

```bash
ausearch -i -x whoami
ausearch -i --pid <PID>
```

---

### 📌 Key Insight

Process tree analysis allows you to:

* Trace attacks back to origin
* Identify exploited applications
* Understand full attack flow

➡️ This is **core SOC investigation skill** ([Medium][1])

---

## 🐍 Reverse Shell Detection

Attackers may spawn shells using legitimate tools.

### 🔹 Indicators:

* Unusual process execution
* Interpreter usage (e.g., Python, Bash)
* Network connections after execution

---

### 📌 Example Behavior

* Vulnerable app exploited
* Spawns shell via Python
* Attacker gains remote control

➡️ Typical **post-exploitation behavior** ([Medium][1])

---

## ⚔️ Advanced Initial Access Techniques

### 🔹 Supply Chain Compromise

* Trusted application executes malicious code

📌 Example:

* Legit app suddenly runs suspicious commands

---

### 🔹 Detection Method

➡️ **Process Tree Analysis**

📌 Why:

* Reveals abnormal execution chains
* Identifies compromised applications

---

## 🚨 Indicators of Compromise (IoCs)

* Multiple failed SSH logins
* Successful login after brute force
* External IP accessing system
* Suspicious command execution (`whoami`, `cat`, etc.)
* Unexpected file access
* Abnormal process chains
* Reverse shell activity

---

## 🔗 Example Attack Chain

1. SSH brute force attack
2. Successful login (account compromised)
3. Access to vulnerable service
4. Command injection
5. Execution of system commands
6. Reverse shell established

➡️ Full system compromise

---

## 🛡️ SOC Detection Approach

### 🔹 Key Principles

* Detect **patterns, not single events**
* Correlate logs across sources
* Trace activity using **process trees**
* Focus on attacker behavior

---

### 🔹 Investigation Workflow

1. Detect suspicious activity
2. Analyze logs (auth.log, service logs)
3. Identify attacker IP / user
4. Trace process execution (auditd)
5. Reconstruct attack chain

---

## 🛠️ Tools & Technologies

* `grep`, `cat`, `less`
* `ausearch` (auditd)
* Linux logs (`auth.log`)
* SIEM (Splunk / ELK)

---

## 🧠 Key Takeaways

* SSH is a major attack vector in Linux environments
* Brute force attacks follow predictable patterns
* Service vulnerabilities can lead to full compromise
* **Process tree analysis is essential for investigation**
* Detection requires correlation + context

---

## 📌 Final Thoughts

This room helped me:

* Detect real-world Linux attacks (SSH + services)
* Identify compromised users and attacker behavior
* Use process tree analysis to trace attacks
* Understand how initial access leads to full compromise
* Develop a **SOC investigation mindset in Linux environments**

