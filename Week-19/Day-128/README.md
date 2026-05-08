# 📊 Alert Triage with Elastic — TryHackMe

## 📅 Day 128 - 365 Days of Cybersecurity

## ✅ Status: Completed

---

# 🧠 Overview

In this room, I performed **alert triage using Elastic (ELK Stack)**, focusing on how SOC analysts investigate alerts and analyze logs within an Elastic-based SIEM environment.

The lab simulated real-world workflows involving:

* Alert investigation
* Log analysis
* Event correlation
* Decision-making in SOC environments

📌 Key Concept:

SIEM tools may differ in interface —
➡️ **but the investigation mindset remains the same.**

---

# 🎯 Learning Objectives

* Understand alert triage in Elastic
* Investigate alerts using Kibana
* Analyze logs and events
* Correlate activity across multiple data sources
* Classify alerts based on evidence

---

# 🧱 Elastic Stack (ELK)

Elastic SIEM is built on:

* **Elasticsearch** → data storage and indexing
* **Logstash** → data ingestion and processing
* **Kibana** → visualization and analysis

---

## 🔹 Key Components Used

* Discover (log search)
* Dashboards
* Alerts
* Timeline view

---

📌 SOC Insight:

Elastic provides powerful **search + visualization + correlation capabilities**.

---

# 🔎 Alert Triage Process

---

## 🛡️ Step-by-Step

1. Review alert details
2. Identify key indicators (IP, user, host, process)
3. Search logs in Kibana
4. Filter relevant events
5. Analyze timeline
6. Correlate related activity
7. Classify alert

---

📌 Core Principle:

➡️ **Investigate → Correlate → Decide**

---

# 🔍 Log Analysis in Kibana

---

## 🔹 Key Fields Analyzed

* `@timestamp`
* `host.name`
* `user.name`
* `process.name`
* `source.ip`
* `destination.ip`

---

## 🔹 Filtering Examples

Search for specific user activity:

```text id="h7k2xp"
user.name: "admin"
```

---

Search for PowerShell execution:

```text id="c9p4rm"
process.name: "powershell.exe"
```

---

Search for specific IP:

```text id="v5t1zs"
source.ip: "192.168.1.10"
```

---

📌 Filtering allows narrowing down large datasets into relevant evidence.

---

# 🔗 Event Correlation

---

## Example Investigation

* Alert triggered for suspicious activity
* Logs show unusual login
* Followed by process execution
* Followed by network connection

➡️ Indicates possible compromise

---

📌 Key Skill:

➡️ **Connecting multiple events into a single narrative**

---

# 🚨 Detection Use Cases

---

## 🔹 Authentication Events

* Failed login attempts
* Suspicious login times
* Unusual locations

---

## 🔹 Process Activity

* PowerShell execution
* Encoded commands
* Unknown binaries

---

## 🔹 Network Activity

* Outbound connections
* Rare destinations
* Possible C2 communication

---

# 🧠 Triage Decision Making

---

## 🔹 Classification

* ✅ True Positive → confirmed malicious activity
* ⚠️ Suspicious → requires further investigation
* ❌ False Positive → benign

---

## 🔹 Key Questions

* Is the activity expected?
* Is there malicious behavior?
* Are multiple indicators present?
* What is the risk level?

---

📌 Decision-making is the most important SOC skill.

---

# 🛠️ Elastic Capabilities Used

* Log search (Kibana Discover)
* Filtering and querying
* Timeline analysis
* Event correlation
* Alert investigation

---

# 🚨 Indicators of Suspicious Activity

* Multiple failed logins
* Suspicious process execution
* Unexpected user activity
* Rare network connections
* Anomalous behavior patterns

---

# 🧪 Concepts Practiced

* Alert triage workflow
* Log analysis in Elastic
* Event correlation
* SOC investigation mindset
* Decision-making process

---

# 🧠 Key Takeaways

* Elastic is a powerful SIEM for log analysis
* Triage methodology is tool-independent
* Correlation is key to detecting attacks
* Context determines alert classification
* Efficient filtering is essential for investigation

---

