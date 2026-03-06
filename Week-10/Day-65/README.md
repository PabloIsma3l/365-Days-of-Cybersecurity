# 🔎 Splunk: The Basics — Day 65
## 📌 Overview

This repository documents the completion of the **Splunk: The Basics** room on TryHackMe.

This room introduces **Splunk**, one of the most widely used SIEM platforms in Security Operations Centers (SOC). It focuses on how security analysts search, analyze, and investigate logs to detect suspicious activity.

All tasks have been successfully completed.

---

## 🎯 Learning Objectives Achieved

✔ Understand what Splunk is and how it works
✔ Learn how SOC analysts search logs using SPL
✔ Identify key components of the Splunk interface
✔ Perform basic investigations using log data
✔ Understand how Splunk supports security monitoring

---

## 🧠 What is Splunk?

**Splunk** is a platform used for:

* Log aggregation
* Security monitoring
* Incident investigation
* Data analysis
* SIEM operations

It collects machine data from multiple sources and allows analysts to search and analyze it in real time.

---

## 🏗️ Core Splunk Components

### 🔹 Forwarder

Agents installed on endpoints that **send logs to Splunk**.

Examples of logs collected:

* System logs
* Application logs
* Authentication logs
* Network device logs

---

### 🔹 Indexer

The **Indexer** processes and stores incoming log data.

Responsibilities include:

* Parsing logs
* Indexing events
* Making data searchable

---

### 🔹 Search Head

The **Search Head** is the interface used by analysts to:

* Run searches
* Build dashboards
* Investigate alerts

---

## 🔍 Splunk Search Processing Language (SPL)

Splunk uses **SPL (Search Processing Language)** to query log data.

Basic search example:

```
index=main
```

Search logs from a specific source:

```
index=main source="/var/log/auth.log"
```

Search events related to failed logins:

```
index=main "failed password"
```

---

## 📊 Useful SPL Commands

### stats

Used to aggregate data.

Example:

```
index=main | stats count by source_ip
```

---

### table

Displays selected fields in table format.

```
index=main | table _time host source
```

---

### sort

Sorts search results.

```
index=main | sort -_time
```

---

### top

Shows the most frequent values.

```
index=main | top source_ip
```

---

## 🧠 How SOC Analysts Use Splunk

SOC analysts rely on Splunk to:

* Investigate alerts
* Analyze login activity
* Detect brute-force attempts
* Identify suspicious IP addresses
* Track attacker behavior

Splunk allows analysts to correlate logs across multiple systems.

---

## 🚨 Example Security Investigation

Typical workflow:

1️⃣ Alert triggered in SIEM
2️⃣ Analyst searches logs in Splunk
3️⃣ Identify suspicious activity
4️⃣ Correlate events across systems
5️⃣ Determine if activity is malicious
6️⃣ Escalate incident if necessary

---

## 🧰 Common Use Cases

* Brute force detection
* Suspicious login analysis
* Malware investigation
* Network anomaly detection
* Insider threat monitoring

---
