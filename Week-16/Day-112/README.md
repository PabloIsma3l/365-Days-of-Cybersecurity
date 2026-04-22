# 🐧 Linux Threat Detection 2 — TryHackMe

## 📅 Day 112 - 365 Days of Cybersecurity

## ✅ Status: Completed

---

## 🧠 Overview

In this room, I analyzed the **post-compromise activity of an attacker on a Linux system**, focusing on:

* **Discovery techniques**
* **Defense evasion**
* **Malware delivery**
* **Cryptominer deployment**

The objective is to understand **what attackers do after gaining access** and how to detect these actions using logs and process analysis.

📌 Key concept:
Detection is about **reconstructing attacker behavior step-by-step after initial compromise**.

---

## 🎯 Learning Objectives

* Detect attacker **discovery activity**
* Identify **malicious scripts and execution chains**
* Detect **file transfer and malware delivery**
* Analyze **cryptominer behavior**
* Correlate logs to reconstruct a full attack scenario

---

## 🔍 Phase 1: Discovery Activity

After gaining access, attackers perform reconnaissance.

### 🔹 Common Discovery Commands

* `hostname`
* `ps aux`
* `whoami`
* System/environment checks

📌 Example:

```bash
systemd-detect-virt
```

➡️ Used to identify cloud environments (e.g., AWS) ([Medium][1])

---

### 🔎 Detection Clues

* Execution of system enumeration commands
* Scripts automating reconnaissance
* Unusual command execution by non-admin users

---

## 🧬 Script-Based Activity

Attackers often use scripts to automate actions.

### 🔹 Example Finding

* Script path:

```bash
/home/itsupport/debug.sh
```

* Script executed discovery commands like:

```bash
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu
```

📌 SOC Insight:
Scripts = **high signal for malicious automation** ([Medium][1])

---

### 🔎 Detection Indicators

* Unexpected scripts in user directories
* Scripts executing system commands
* Repeated automated actions

---

## 🛡️ Defense Evasion

Attackers check for security tools before proceeding.

### 🔹 Example

Using:

```bash
ps aux
```

To identify EDR/AV processes like:

* `falcon`
* `sentinel`
* `ds_agent`

📌 SOC Insight:
Attackers try to **identify and bypass security controls early** ([Medium][1])

---

## 📦 Malware Delivery

Attackers transfer and download malicious files.

### 🔹 Techniques Observed

* File download via `curl` / `wget`
* File transfer via SCP

---

### 🔹 Example Findings

* Malicious script path:

```bash
/var/tmp/helper.sh
```

* Suspicious archive:

```bash
kernupd.tar.gz
```

📌 Insight:
Files downloaded via `curl` were identified as more suspicious ([Medium][1])

---

### 🔎 Detection Indicators

* File creation after network activity
* Execution from `/tmp` or `/var/tmp`
* Use of scripting tools for downloads

---

## 🔐 Initial Compromise (Observed)

### 🔹 SSH Brute Force

* Attacker IP:

```
45.9.148.125
```

📌 Pattern:

* Multiple failed logins
* Successful login
  ➡️ Account compromise ([Medium][1])

---

## ⚙️ Attacker Actions After Access

### 🔹 User Enumeration

Command used:

```bash
last
```

➡️ Lists previously logged-in users ([Medium][1])

---

### 🔹 Network Scanning

* Target range:

```
10.10.12.1–10.10.12.10
```

➡️ Indicates lateral movement attempts ([Medium][1])

---

## ⛏️ Cryptominer Deployment

Final stage of the attack.

### 🔹 Execution Command

```bash
nohup /tmp/.apt/kernupd/kernupd
```

📌 Behavior:

* Runs in background (`nohup`)
* Hidden directory (`.apt`)
* Persistent execution ([Medium][1])

---

### 🔎 Detection Indicators

* Processes running from `/tmp`
* Hidden directories (dot-prefixed)
* High CPU usage processes
* Long-running unknown binaries

---

## 🔗 Full Attack Chain

1. SSH brute force → initial access
2. Discovery commands executed
3. Script automation (`debug.sh`)
4. Security tools checked (EDR detection)
5. Malware downloaded (`helper.sh`)
6. Archive transferred (`kernupd.tar.gz`)
7. Cryptominer deployed
8. Network scanning performed

➡️ Full compromise lifecycle ([JAWSTAR SEC][2])

---

## 🚨 Indicators of Compromise (IoCs)

* SSH brute force activity
* Suspicious scripts in user directories
* Use of `curl` / `wget` for downloads
* File execution from `/tmp`
* Hidden directories (`.apt`)
* Cryptominer processes
* Network scanning activity
* Enumeration commands execution

---

## 🛡️ SOC Detection Approach

### 🔹 Key Principles

* Detect **post-compromise behavior**
* Correlate logs across multiple sources
* Focus on attacker intent (not just commands)
* Reconstruct full attack timeline

---

### 🔹 Investigation Workflow

1. Detect suspicious login
2. Analyze discovery activity
3. Identify executed scripts
4. Trace file downloads
5. Detect malware execution
6. Analyze persistence and impact

---

## 🛠️ Tools & Technologies

* `ps`, `grep`, `cat`
* `ausearch` (auditd)
* Linux logs (`auth.log`, `audit.log`)
* SIEM (Splunk / ELK)

---

## 🧠 Key Takeaways

* Attackers perform **structured post-compromise actions**
* Discovery phase is highly detectable
* Scripts are strong indicators of malicious automation
* `/tmp` directory is a common attacker workspace
* Cryptominers are a common post-exploitation payload
* Detection requires **full attack chain visibility**

---

## 📌 Final Thoughts

This room helped me:

* Understand attacker behavior after initial access
* Detect discovery, evasion, and execution phases
* Identify malware delivery techniques
* Analyze a real cryptominer attack
* Strengthen my **SOC investigation and correlation skills**

This represents a strong step toward detecting **real-world Linux compromises and post-exploitation activity**.

[1]: https://medium.com/%40oomensusan/linux-threat-detection-2-walkthrough-tryhackme-69d2cb8a2741?utm_source=chatgpt.com "Linux Threat Detection 2 Walkthrough. TryHackMe | by Lintu Oommen | Medium"
[2]: https://jawstarsec.in/linux-threat-detection-1-or-linux-threat-detection-2-or-linux-threat-detection-3-or-tryhackme-walkthrough-answers-or-all-parts?utm_source=chatgpt.com "Linux Threat Detection 1 , 2, 3 | Tryhackme Walkthrough Answers | JAWSTAR SEC"
