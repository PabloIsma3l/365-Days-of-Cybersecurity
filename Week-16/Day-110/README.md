# 🐧 Linux Logging for SOC — TryHackMe

## 📅 Day 110 - 365 Days of Cybersecurity

## ✅ Status: Completed

---

## 🧠 Overview

In this room, I learned how to **analyze Linux logs from a SOC perspective**, focusing on authentication events, system logs, and runtime monitoring using tools like **auditd**.

Unlike Windows, Linux logging is **less structured and highly customizable**, requiring strong filtering and investigation skills.

📌 Key concept:
Detection in Linux is not about event IDs — it's about **log hunting and pattern recognition**.

---

## 🎯 Learning Objectives

* Understand Linux logging structure and limitations
* Analyze authentication, system, and application logs
* Use command-line tools to filter and investigate logs
* Understand **runtime monitoring via system calls**
* Use **auditd** for advanced detection

---

## 📂 Linux Logging Fundamentals

* Logs are stored in:

```bash
/var/log/
```

* Logs are:

  * Plain text
  * Unstructured (no event IDs like Windows)
  * Distributed across multiple files

📌 SOC Insight:
You must **know where to look + filter aggressively**, otherwise logs become noise. ([Medium][1])

---

## 🔎 Working with Logs (SOC Skills)

### 🔹 Reading Logs

```bash
cat /var/log/syslog
```

### 🔹 Filtering Logs

```bash
cat /var/log/syslog | grep CRON
```

### 🔹 Searching Across Logs

```bash
grep -R -E "auth|login|session" /var/log
```

📌 Key Skill:

* Linux detection = **grep + filtering + pattern recognition** ([Medium][1])

---

## 🔐 Authentication Logs (CRITICAL)

### 📍 File:

```bash
/var/log/auth.log
```

### 🔍 What it contains:

* SSH logins (success/failure)
* User activity
* `sudo` commands
* User creation/modification

---

### 🔹 Detection Use Cases

#### Brute Force Attack

```bash
grep "Failed password" /var/log/auth.log
```

#### SSH Activity

```bash
grep "sshd" /var/log/auth.log
```

#### User Management

```bash
grep -E "(useradd|usermod|userdel)" /var/log/auth.log
```

#### Sudo Commands

```bash
grep "COMMAND=" /var/log/auth.log
```

📌 SOC Insight:
Auth logs are the **#1 source for detecting compromise in Linux** ([Medium][1])

---

## 📊 Common Linux Logs (Important Context)

* `/var/log/syslog` → General system activity
* `/var/log/kern.log` → Kernel events
* `/var/log/dpkg.log` / `apt` → Package installations
* `/var/log/messages` → System-wide logs

📌 These logs are useful but often **noisy and harder to parse** in daily SOC work. ([Medium][1])

---

## ⚠️ Key Limitation (VERY IMPORTANT)

By default, Linux **does NOT log**:

* Process execution
* File access
* Network activity

📌 Meaning:
You **cannot fully detect attacks with default logs alone** ([Medium][1])

---

## ⚙️ System Calls (Core Concept)

Linux operates using **system calls**:

* Example:

```bash
execve
```

📌 Key Insight:

* Every action (process, file, network) uses system calls
* Attackers **cannot bypass system calls** ([Medium][1])

➡️ This is the foundation of advanced detection tools

---

## 🛡️ Auditd (CRITICAL FOR SOC)

### 🔹 What is Auditd?

A Linux auditing tool used to monitor:

* Process execution
* File access
* System changes

---

### 📍 Logs:

```bash
/var/log/audit/audit.log
```

---

### 🔹 Example Command:

```bash
ausearch -i -k proc_wget
```

---

### 🔍 Key Fields in Auditd Logs:

* `pid / ppid` → Process relationships
* `auid` → Original user
* `uid` → Effective user
* `exe` → Executed binary
* `tty` → Session identifier

📌 SOC Insight:
Auditd allows you to **reconstruct attacker activity step-by-step** ([Medium][1])

---

## 🔄 Runtime Monitoring (GAME CHANGER)

Auditd enables detection of:

* File modifications (e.g., SSH config changes)
* Command execution
* Tool usage (e.g., wget downloads)

📌 Example Detection:

* Downloaded malware via `wget`
* File access tracking
* Network scanning activity

---

## ⚠️ Logging Challenges

* Logs are inconsistent across distributions
* Format and location may change
* High volume of noise

📌 Key Rule:
More logs ≠ better detection
Filtering is critical ([Medium][1])

---

## 🚨 Indicators of Compromise (IoCs)

* Multiple failed SSH logins
* Successful login after failures
* Unauthorized `sudo` usage
* New users added
* Suspicious command execution
* File changes in critical locations
* Use of tools like `wget` for downloads

---

## 🛡️ SOC Detection Approach

### 🔹 Linux Detection =

* Log hunting (not event IDs)
* Pattern recognition
* Command-line analysis
* Event correlation

---

### 🔹 Example Attack Chain

1. SSH brute force
2. Successful login
3. `sudo` privilege escalation
4. File download via `wget`
5. Tool execution
6. Network scan

➡️ Full compromise detected via logs

---

## 🛠️ Tools & Technologies

* `grep`, `cat`, `less`
* Auditd
* Syslog
* SIEM (Splunk / ELK)
* Linux CLI

---

## 🧠 Key Takeaways

* Linux logs are **powerful but unstructured**
* Authentication logs are the most critical source
* Default logging is **not enough for detection**
* Auditd provides essential runtime visibility
* Detection relies on **filtering + correlation + investigation**

---

## 📌 Final Thoughts

This room helped me:

* Understand how Linux logging differs from Windows
* Develop log hunting skills using CLI tools
* Detect real attack patterns in authentication logs
* Use auditd to monitor runtime activity
* Think like a SOC analyst when investigating Linux systems
