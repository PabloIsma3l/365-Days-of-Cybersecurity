# 🔺 Pyramid of Pain — Day 68
## 📌 Overview

This document summarizes the knowledge gained from completing the **"Pyramid of Pain"** room on TryHackMe.

The Pyramid of Pain is a threat intelligence model that helps security analysts understand how difficult it is for attackers to change different types of indicators. The higher you go in the pyramid, the more difficult it becomes for adversaries to adapt.

This model is widely used in **threat hunting, detection engineering, and SOC operations** to prioritize detection strategies.

---

## 🎯 Learning Objectives

* Understand the concept of the Pyramid of Pain
* Learn the different levels of indicators
* Identify which indicators are easiest or hardest for attackers to change
* Understand how defenders can increase operational cost for adversaries

---

## 🧠 What is the Pyramid of Pain?

The **Pyramid of Pain**, created by security researcher David Bianco, represents the difficulty attackers experience when defenders detect and block indicators associated with their operations.

Lower-level indicators are easy for attackers to change, while higher-level indicators force them to modify tools, infrastructure, or entire attack methodologies.

---

## 🔺 Pyramid Levels

### 🔹 Hash Values

Examples:

* MD5
* SHA1
* SHA256

These represent file fingerprints used to identify specific malware samples.

❗ **Pain Level for Attacker:** Very Low

Attackers can easily modify malware to generate a new hash.

---

### 🔹 IP Addresses

These represent infrastructure used by attackers for command and control or hosting malicious services.

Examples:

* C2 servers
* Malicious hosting infrastructure

❗ **Pain Level for Attacker:** Low

Attackers can change IP addresses relatively quickly using new servers.

---

### 🔹 Domain Names

Attackers often register domains for phishing campaigns or command-and-control communication.

Examples:

* phishing domains
* malware download sites

❗ **Pain Level for Attacker:** Low to Moderate

Domains require more effort than IP changes but are still relatively easy to replace.

---

### 🔹 Network / Host Artifacts

Artifacts are traces left by attacker activity on systems or networks.

Examples:

* registry modifications
* suspicious file paths
* unusual network traffic patterns

❗ **Pain Level for Attacker:** Moderate

Changing artifacts may require modifying malware behavior.

---

### 🔹 Tools

These represent the software or frameworks used by attackers.

Examples:

* Mimikatz
* Metasploit
* Custom malware frameworks

❗ **Pain Level for Attacker:** High

Attackers must significantly modify their tools or develop new ones.

---

### 🔹 Tactics, Techniques, and Procedures (TTPs)

TTPs describe how attackers operate at a strategic level.

Examples:

* credential dumping
* lateral movement techniques
* privilege escalation strategies

❗ **Pain Level for Attacker:** Very High

Changing TTPs requires attackers to redesign their entire attack methodology.

These are often mapped using the **MITRE ATT&CK framework**.

---

## 🛡️ Why the Pyramid of Pain Matters

For defenders, focusing only on low-level indicators such as hashes or IPs provides limited long-term protection.

Security teams should aim to detect **tools and attacker behavior (TTPs)** because these are much harder for adversaries to change.

---

## 📊 Practical Use in SOC Operations

SOC analysts use the Pyramid of Pain to:

* Improve detection strategies
* Prioritize threat hunting efforts
* Focus on behavioral detection
* Increase the operational cost for attackers

---

