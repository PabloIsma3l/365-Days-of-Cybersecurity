# 📊 Log Analysis with SIEM — TryHackMe

## 📅 Day 124 - 365 Days of Cybersecurity

## ✅ Status: Completed

---

# 🧠 Overview

In this room, I learned how to perform **log analysis using a SIEM platform**, focusing on detecting suspicious activity through querying and event correlation.

The lab simulated a real SOC environment where logs are ingested and analyzed to:

* Detect threats
* Investigate alerts
* Identify attacker behavior

📌 Key Concept:

A SIEM is not just a log viewer —
➡️ **It is a detection and investigation engine.**

---

# 🎯 Learning Objectives

* Understand SIEM fundamentals
* Perform log searches using queries
* Identify suspicious patterns in logs
* Correlate events across multiple sources
* Investigate potential security incidents

---

# 🧱 What is a SIEM?

SIEM (Security Information and Event Management):

* Collects logs from multiple sources
* Normalizes and indexes data
* Enables searching and correlation
* Generates alerts based on detection rules

---

## 🔹 Common Log Sources

* Windows Event Logs
* Linux logs
* Web server logs
* Firewall logs
* Authentication logs

---

📌 SOC Insight:

More logs = more visibility → better detection capability.

---

# 🔍 Log Analysis Fundamentals

Logs contain structured data such as:

* Timestamp
* Source IP
* Destination IP
* Username
* Process
* Event type

---

## 🔹 Analyst Goal

Find:

* Anomalies
* Suspicious behavior
* Indicators of compromise

---

# 🔎 Querying in SIEM

Core skill developed in this room:

➡️ Writing queries to filter and analyze logs

---

## 🔹 Basic Query Examples

Search for failed logins:

```text id="q7k2dz"
event_type=authentication AND status=failed
```

---

Search for specific IP:

```text id="n3x8vm"
src_ip=192.168.1.10
```

---

Search for suspicious activity:

```text id="p9c1tw"
process=powershell.exe AND command=*encoded*
```

---

📌 Queries allow analysts to **slice large datasets into actionable insights**.

---

# 🚨 Detecting Suspicious Activity

---

## 🔹 Authentication Anomalies

* Multiple failed login attempts
* Login attempts from unusual locations
* Brute-force patterns

---

## 🔹 Process-Based Indicators

* PowerShell execution
* Encoded commands
* Suspicious parent-child relationships

---

## 🔹 Network Indicators

* Connections to unknown IPs
* Unusual outbound traffic
* Rare destinations

---

# 🔗 Event Correlation

A single log rarely tells the full story.

---

## 🧠 Example Correlation

1. Failed logins detected
2. Successful login occurs
3. Suspicious process execution
4. Outbound connection

➡️ Indicates possible compromise

---

📌 Key Skill:

➡️ **Link multiple events into a coherent attack narrative**

---

# 🛡️ SOC Investigation Workflow

---

## Step-by-Step

1. Identify alert or suspicious indicator
2. Query logs for related events
3. Filter relevant data
4. Correlate events across sources
5. Identify attacker behavior
6. Confirm or dismiss threat

---

📌 Core Principle:

➡️ **Search → Filter → Correlate → Investigate**

---

# 🧪 Detection Use Cases

Practiced scenarios included:

* Brute-force login detection
* Suspicious PowerShell usage
* Unauthorized access patterns
* Network anomalies

---

# 🛠️ SIEM Capabilities Used

* Log ingestion
* Query engine
* Filtering
* Event correlation
* Timeline analysis

---

# 🚨 Indicators of Compromise (IoCs)

* Multiple failed logins
* Suspicious login patterns
* Encoded PowerShell commands
* Unusual process execution
* Unexpected network connections

---

# 🧠 Key Takeaways

* SIEM is central to SOC operations
* Querying is a critical analyst skill
* Logs must be correlated, not analyzed in isolation
* Detection requires identifying patterns, not single events
* Efficient filtering is key to handling large datasets

---

