# 📊 Intro to Log Analysis — DAY 73 (Part 2)

## 📌 Overview

This document summarizes **Part 2 (Tasks 7–10)** of the **"Intro to Log Analysis"** room on TryHackMe.

This section focuses on the **practical side of log analysis**, introducing investigation techniques used by SOC analysts to identify suspicious activity and reconstruct security incidents.

---

## 🎯 Learning Objectives (Part 2)

* Learn how analysts filter large log datasets
* Identify suspicious patterns within logs
* Understand event correlation
* Learn how to reconstruct incident timelines

---

## 🔎 Filtering Log Events

In real environments, logs can contain **thousands or millions of events**. Analysts must filter the data to focus on relevant activity.

Common filtering methods include:

* Searching by **IP address**
* Filtering by **username**
* Searching for specific **Event IDs**
* Limiting events to a **time range**

Filtering allows analysts to quickly isolate suspicious activity from large log datasets.

---

## 🚨 Identifying Suspicious Patterns

One of the main goals of log analysis is identifying abnormal behavior.

Common suspicious patterns include:

* Multiple failed login attempts
* Logins from unusual locations
* Activity outside normal working hours
* Large numbers of requests from a single IP

These patterns may indicate attacks such as:

* Brute force attacks
* Credential stuffing
* Account compromise
* Automated scanning

---

## 🔗 Event Correlation

Single log entries rarely provide enough context to understand an incident.

SOC analysts correlate events from multiple logs to reconstruct attacker activity.

Example investigation flow:

1. Detect multiple failed login attempts
2. Identify the source IP address
3. Check whether the attacker eventually succeeded
4. Investigate actions performed after login

This process helps determine whether a system has been compromised.

---

## 🕒 Timeline Reconstruction

Another important investigation technique is building a **timeline of events**.

Logs are arranged chronologically to understand the sequence of attacker actions.

Example timeline:

1. Multiple failed login attempts
2. Successful login
3. Privileged commands executed
4. Access to sensitive data

Creating a timeline helps investigators clearly understand **how the attack unfolded**.

---

## 🛡️ Log Analysis in SOC Environments

In real organizations, logs are analyzed using **SIEM platforms** that centralize and process large volumes of log data.

Common SIEM platforms include:

* Splunk
* Elastic Stack (ELK)
* IBM QRadar
* ArcSight

These platforms allow analysts to:

* Search large datasets quickly
* Correlate events across systems
* Detect suspicious activity
* Investigate incidents efficiently

---

## 🏁 Progress Status

* ✅ Tasks 7–10 completed

---

## 🚀 Key Takeaways

* Log filtering helps analysts manage large datasets
* Suspicious patterns can indicate malicious activity
* Event correlation is critical for investigations
* Timeline reconstruction reveals how an attack occurred

---

🚀 *This part of the room focuses on practical investigation techniques used by SOC analysts when analyzing logs during security incidents.*
