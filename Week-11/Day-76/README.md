# 👻 Eviction — TryHackMe DAY 76

## 📌 Overview

This document summarizes the completion of the **"Eviction"** room on TryHackMe.

The Eviction room is a **Blue Team investigation challenge** where the objective is to identify and remove a malicious presence within a compromised system. It simulates a real-world incident where an attacker has gained access and must be detected, analyzed, and evicted from the environment.

This lab reinforces skills related to:

* Threat detection
* Log analysis
* Incident response
* Identifying persistence mechanisms

---

## 🎯 Learning Objectives

* Identify indicators of compromise (IOCs)
* Detect malicious activity on a system
* Understand attacker persistence techniques
* Apply incident response methodologies
* Remove (evict) the threat from the system

---

## 🧠 Investigation Approach

A structured approach is critical during incident response:

1. **Detection** – Identify suspicious activity
2. **Analysis** – Investigate logs and system behavior
3. **Containment** – Limit attacker access
4. **Eradication** – Remove malicious components
5. **Recovery** – Restore normal operations

---

## 🔎 Key Concepts Practiced

### Indicators of Compromise (IOCs)

During the investigation, analysts search for signs of compromise such as:

* Suspicious processes
* Unknown files or binaries
* Unusual network connections
* Unauthorized user activity

---

### Persistence Mechanisms

Attackers often maintain access using persistence techniques such as:

* Scheduled tasks
* Startup scripts
* Modified system services
* Backdoors

Identifying and removing persistence is essential to fully evict the attacker.

---

### Log Analysis

Logs provide visibility into attacker actions. Analysts review logs to:

* Identify when the compromise occurred
* Track attacker behavior
* Detect lateral movement or privilege escalation

---

### Threat Eviction

Once the threat is understood, the analyst removes:

* Malicious files
* Unauthorized accounts
* Persistence mechanisms

This ensures the attacker no longer has access.

---

## 🛡️ Skills Reinforced

* Incident response workflow
* Threat detection and analysis
* Log investigation
* System hardening after compromise

---

## 🏁 Room Completion Status

* ✅ All tasks completed

---

## 🚀 Key Takeaways

* Effective incident response requires a structured approach
* Persistence mechanisms are critical to identify and remove
* Logs are essential for understanding attacker behavior
* Full eviction ensures attackers cannot regain access

---

🚀 *This room simulates a real-world Blue Team scenario where analysts must detect, investigate, and remove a threat from a compromised system.*
