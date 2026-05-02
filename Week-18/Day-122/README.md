# 🌐 IP and Domain Threat Intelligence — TryHackMe

## 📅 Day 122 - 365 Days of Cybersecurity

## ✅ Status: Completed

---

# 🧠 Overview

In this room, I learned how to perform **IP and domain-based threat intelligence analysis**, a key skill in SOC operations when investigating suspicious network activity.

The focus is on enriching and analyzing:

* IP addresses
* Domain names
* DNS data
* Network indicators

📌 Key Concept:

IP and domain intelligence transforms **network artifacts into attacker infrastructure visibility**.

---

# 🎯 Learning Objectives

* Investigate suspicious IP addresses
* Analyze domain reputation and behavior
* Perform DNS-based intelligence analysis
* Use threat intelligence platforms for enrichment
* Correlate indicators with malicious activity

---

# 🌐 IP Address Analysis

IP addresses are critical indicators in network-based investigations.

---

## 🔹 Key Questions

When analyzing an IP:

* Is it malicious or benign?
* What is its reputation?
* Is it part of known malicious infrastructure?
* What services are exposed?

---

## 🔍 Intelligence Sources

Used to enrich IPs:

* AbuseIPDB
* VirusTotal
* Shodan

---

## 🔹 Data Collected

* Geolocation
* ISP / ASN
* Open ports
* Associated domains
* Historical activity

---

📌 SOC Insight:

A single IP can be part of:

* Command & Control (C2)
* Malware hosting
* Phishing infrastructure

---

# 🌍 Domain Analysis

Domains provide more context than raw IPs.

---

## 🔹 Key Checks

* Domain reputation
* WHOIS data
* Registration details
* Associated IPs
* Subdomains

---

## 🔍 Important Indicators

* Newly registered domains
* Suspicious naming patterns
* Typosquatting
* Short domain lifespan

---

📌 Example:

* `micr0soft-login[.]com` → phishing indicator

---

# 🧬 DNS Intelligence

DNS analysis reveals how domains behave.

---

## 🔹 Key Records

* A record → IP mapping
* MX record → email servers
* NS record → name servers

---

## 🔍 Detection Use Cases

* Fast-flux domains
* Domain-IP rotation
* Suspicious infrastructure patterns

---

📌 SOC Insight:

DNS is one of the most valuable sources for **detecting attacker infrastructure**.

---

# 🔗 IP ↔ Domain Correlation

A key skill learned:

➡️ Linking infrastructure together

---

## Example Correlation

* Domain → resolves to IP
* IP → hosts multiple domains
* Domains → part of same campaign

---

📌 This enables:

* Campaign tracking
* Infrastructure mapping
* Threat hunting

---

# 🧪 Threat Intelligence Platforms

Tools used during the room:

---

## 🔹 VirusTotal

* Reputation scoring
* Associated files
* Domain-IP relationships

---

## 🔹 AbuseIPDB

* Abuse reports
* Malicious activity history

---

## 🔹 Shodan

* Open ports
* Services
* Banner information

---

## 🔹 WHOIS Lookup

* Domain registration data
* Creation date
* Registrar information

---

# 🚨 Indicators of Compromise (IoCs)

## Network-Based

* Malicious IP addresses
* Suspicious domains
* Known C2 infrastructure

---

## Behavioral Indicators

* Connections to rare IPs
* Communication with newly registered domains
* DNS anomalies
* Beaconing behavior

---

# 🛡️ SOC Investigation Workflow

---

## 🧠 Step-by-Step Process

1. Detect suspicious IP/domain
2. Enrich using threat intel platforms
3. Analyze reputation and history
4. Correlate with other indicators
5. Identify attacker infrastructure
6. Determine impact
7. Take action (block, alert, investigate)

---

📌 Core Principle:

➡️ **Enrich → Correlate → Understand → Act**

---

# 🧱 Infrastructure-Based Detection

Unlike file-based detection:

* IPs and domains represent attacker infrastructure
* Infrastructure can change rapidly

---

## 📌 Challenge

Attackers can:

* Rotate IPs
* Change domains
* Use cloud infrastructure

---

## 📌 Solution

Focus on:

* Patterns
* Behavior
* Relationships

---

# 🛠️ Tools & Concepts Covered

* VirusTotal
* AbuseIPDB
* Shodan
* WHOIS
* DNS analysis
* IP reputation
* Domain intelligence

---

# 🧠 Key Takeaways

* IP and domain analysis is critical in network investigations
* Threat intelligence platforms provide valuable context
* DNS analysis reveals attacker behavior
* Infrastructure correlation enables campaign tracking
* Detection should focus on patterns, not just single indicators

---

