# 🔎 Splunk: The Basics Day 66
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

## 🏁 Room Completion Status

* ✅ All tasks completed
* 🧠 Practical understanding of Splunk for SOC investigations achieved

---

## 🚀 Next Steps

* Practice advanced SPL queries
* Build Splunk dashboards
* Learn detection rule creation
* Perform threat hunting with Splunk

---

🧠 *Room completed as part of my structured SOC Analyst, Blue Team, and DFIR training path.*

---

# 🔎 Elastic Stack: The Basics — TryHackMe (Completed)

## 📌 Overview

This section documents the completion of the **Elastic Stack: The Basics** room on TryHackMe.

The room introduces the **Elastic Stack (ELK)**, another widely used platform for **log aggregation, monitoring, and security investigations** in SOC environments.

ELK stands for:

* **Elasticsearch**
* **Logstash**
* **Kibana**

All tasks in the room were successfully completed.

---

## 🎯 Learning Objectives Achieved

✔ Understand the architecture of the Elastic Stack
✔ Learn how logs are ingested and indexed
✔ Explore Kibana dashboards used by SOC analysts
✔ Perform basic log searches and investigations
✔ Understand how ELK supports threat detection

---

## 🧠 What is the Elastic Stack?

The **Elastic Stack (ELK)** is a platform used for:

* Log collection
* Data indexing
* Security monitoring
* Threat investigation
* Visualization of security data

It allows analysts to **collect, search, and visualize large volumes of machine data** in real time.

---

## 🏗️ Elastic Stack Components

### 🔹 Elasticsearch

**Elasticsearch** is the core search and analytics engine.

Responsibilities:

* Store indexed log data
* Perform fast searches
* Analyze large datasets

---

### 🔹 Logstash

**Logstash** is responsible for **collecting and processing logs**.

Capabilities include:

* Parsing log data
* Transforming events
* Sending processed logs to Elasticsearch

---

### 🔹 Kibana

**Kibana** is the **visual interface** used by analysts.

With Kibana, SOC analysts can:

* Search logs
* Build dashboards
* Investigate alerts
* Visualize security events

---

## 🔍 How SOC Analysts Use ELK

SOC analysts commonly use the Elastic Stack to:

* Investigate suspicious log activity
* Detect anomalies in authentication logs
* Identify unusual network connections
* Correlate events across systems
* Visualize attack patterns

---

## 📊 Kibana Features for Security Investigations

Important Kibana capabilities include:

* **Discover** → Explore raw log data
* **Dashboards** → Visualize security metrics
* **Visualizations** → Graph and analyze trends
* **Search & filtering** → Investigate specific events

These tools help analysts quickly identify **suspicious patterns and anomalies**.

---

## 🚨 Example Investigation Workflow

Typical SOC workflow using ELK:

1️⃣ Alert detected by monitoring tools
2️⃣ Analyst searches logs in Kibana
3️⃣ Filter events by IP, host, or user
4️⃣ Identify suspicious patterns
5️⃣ Correlate logs from multiple sources
6️⃣ Escalate incident if confirmed

---

## 🧰 Common Security Use Cases

* Failed login monitoring
* Detection of brute-force attacks
* Network traffic analysis
* Malware communication detection
* Threat hunting across log datasets

---
