# 🌍 Intro to Cyber Threat Intelligence — TryHackMe

## 📅 Day 119 - 365 Days of Cybersecurity

## ✅ Status: Completed

---

# 🧠 Overview

In this room, I learned the foundations of **Cyber Threat Intelligence (CTI)** and how intelligence supports security operations by turning raw indicators into actionable knowledge.

The room introduced:

* Threat Intelligence classifications
* CTI Lifecycle
* MITRE ATT&CK
* Cyber Kill Chain
* Diamond Model
* Pyramid of Pain
* Threat intel sharing standards

📌 Key Concept:

Threat Intelligence is not just collecting IOCs —

It is **context + analysis + action**.

---

# 🎯 Learning Objectives

* Understand what Cyber Threat Intelligence is
* Learn major CTI classifications
* Understand the intelligence lifecycle
* Use frameworks to analyze adversary behavior
* Understand intelligence sharing standards and platforms

---

# 🔍 What is Cyber Threat Intelligence (CTI)?

CTI is knowledge about:

* Adversaries
* Their capabilities
* Their motives
* Their infrastructure
* Their TTPs (Tactics, Techniques and Procedures)

Purpose:

* Improve detection
* Support investigations
* Anticipate threats
* Enable better defensive decisions

---

# 📊 Threat Intelligence Classifications

---

## 🔹 Strategic Intelligence

High-level intelligence for business and risk decisions.

Examples:

* Ransomware trends
* Industry targeting patterns
* Emerging threat landscape

Audience:

* Executives
* Leadership
* Risk teams

---

## 🔹 Tactical Intelligence

Focuses on:

Adversary TTPs

Often mapped to:

* MITRE ATT&CK techniques

Example:

* PowerShell abuse
* Credential dumping techniques

Useful for:

* Detection engineering
* Threat hunting
* Security control improvements

---

## 🔹 Operational Intelligence

Focuses on:

* Specific campaigns
* Threat actor operations
* Adversary objectives

Example:

* Active phishing campaign targeting finance

---

## 🔹 Technical Intelligence

IOC-focused intelligence:

* IP addresses
* Hashes
* Domains
* URLs
* Artifacts

Used heavily by SOC teams.

---

# 🔄 CTI Lifecycle

Core 6-stage intelligence lifecycle:

---

## 1. Direction

Define:

* What intelligence is needed?
* What questions need answering?

Example:

"Are we exposed to ransomware activity targeting healthcare?"

---

## 2. Collection

Gather raw data from sources:

* Internal telemetry
* Threat feeds
* OSINT
* Vendor reports

---

## 3. Processing

Convert raw data into usable formats.

Example:

* Sorting
* Parsing
* Correlation
* Normalization

📌 Raw data → usable intelligence inputs

---

## 4. Analysis

Transform information into intelligence.

Answer:

* So what?
* Why does it matter?

---

## 5. Dissemination

Share intelligence with stakeholders.

Examples:

* Reports
* Alerts
* Intelligence briefs

---

## 6. Feedback

Improve intelligence process.

* What worked?
* What was missing?

CTI is cyclical.

---

# 🗺️ MITRE ATT&CK

Knowledge base of adversary behavior.

Maps:

* Tactics
* Techniques
* Procedures

---

## Example Technique

```text id="m8ra2p"
T1059.001 - PowerShell
```

Helps analysts:

* Map attacker behavior
* Standardize investigations
* Improve detections

---

## Example Use

Alert shows suspicious PowerShell:

Map to:

* Execution tactic
* T1059.001

Now investigation has context.

---

# ⚔️ Cyber Kill Chain

Lockheed Martin framework describing attack stages.

---

## 7 Phases

1. Reconnaissance
2. Weaponization
3. Delivery
4. Exploitation
5. Installation
6. Command and Control
7. Actions on Objectives

---

## Example

Phishing email:

* Delivery

Malware beacon:

* Command & Control

Data theft:

* Actions on Objectives

📌 Helps map where detection happened in the intrusion lifecycle.

---

# 💎 Diamond Model

Intrusion analysis model built around four elements:

* Adversary
* Infrastructure
* Capability
* Victim

---

## Example Correlation

Adversary
uses

Infrastructure (C2 domain)

to deliver

Capability (malware)

against

Victim

---

Useful for campaign analysis and intrusion tracking.

---

# 🔺 Pyramid of Pain

One of the most valuable concepts in the room.

Lower-level indicators:

Easy for attackers to change:

* Hashes
* IPs
* Domains

Higher-level indicators:

Hard for attackers to change:

* Tools
* TTPs

---

## Key Lesson

Detecting:

❌ Hashes only

Better:

✅ Adversary behavior

The higher up the pyramid, the more pain for attackers.

---

# 🔄 STIX & TAXII

## STIX

Structured language for threat intel.

Describes:

* Indicators
* Threat actors
* Campaigns
* Relationships

---

## TAXII

Protocol for sharing threat intelligence.

Supports:

* Automated intelligence exchange
* Feed distribution
* Near real-time updates

---

# 🧠 Threat Intel Platforms

## MISP

Threat intelligence sharing platform.

Supports:

* IOC sharing
* Correlation
* Enrichment

---

## OpenCTI

Threat knowledge management platform.

Used for:

* Relationship mapping
* Intelligence management

---

# 🛡️ Intelligence Sources

Common sources:

* Internal telemetry
* OSINT
* Commercial feeds
* ISAC communities
* Threat research blogs

---

## Example Sources

* AbuseIPDB
* URLhaus
* VirusTotal
* MISP feeds

---

# 🚨 IOC vs TTP Thinking

Important distinction learned:

Indicators:

* IP
* Domain
* Hash

Behavior:

* ATT&CK techniques
* TTP patterns

📌 Mature detection focuses beyond IOCs.

---

# 🛠️ Concepts & Frameworks Covered

* CTI Lifecycle
* MITRE ATT&CK
* Cyber Kill Chain
* Diamond Model
* Pyramid of Pain
* STIX / TAXII
* MISP / OpenCTI

---

# 🧠 Key Takeaways

* CTI transforms raw data into actionable intelligence
* Intelligence has multiple classifications and purposes
* ATT&CK helps map adversary behavior
* Kill Chain helps understand attack stages
* Pyramid of Pain shows why TTP detection matters
* Threat intel sharing standards enable collaboration

