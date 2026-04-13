# 🪟 Windows Logging for SOC — TryHackMe day 103

## 📅 Day X - 365 Days of Cybersecurity

## ✅ Status: Completed

---

## 🧠 Overview

In this room, I learned how to **analyze and interpret Windows logs** for security monitoring and incident detection, including both **native Windows Event Logs** and **Sysmon logs**.

Windows logging is a fundamental component of any **SOC environment**, as it provides visibility into system activity, user behavior, and potential security incidents.

---

## 🎯 Learning Objectives

* Understand Windows Event Logs structure
* Identify key log sources for security monitoring
* Analyze Event IDs and their meaning
* Understand the role of **Sysmon** in advanced logging
* Detect suspicious activity using logs
* Recognize Indicators of Compromise (IoCs)

---

## 📂 Windows Event Logs

Managed through **Event Viewer**, divided into:

### 🔹 Main Categories:

* **Security Log**
* **System Log**
* **Application Log**

---

### 🔐 Security Log (Most Important)

Tracks:

* Logon/logoff activity
* Authentication attempts
* Account changes
* Privilege usage

📌 Primary source for detecting attacks

---

## 🔢 Important Windows Event IDs

### 🔐 Authentication Events

* **4624** → Successful logon
* **4625** → Failed logon
* **4634** → Logoff

---

### 👤 Account Management

* **4720** → User created
* **4726** → User deleted
* **4732** → User added to group

---

### ⚠️ Privilege & Process Events

* **4672** → Special privileges assigned
* **4688** → Process creation

---

## 🔎 Sysmon (System Monitor)

**Sysmon** is a Windows system service that provides **enhanced logging capabilities** far beyond default Windows logs.

📌 Key Advantage:
Gives **deep visibility into system activity**, essential for detecting advanced threats.

---

## 🔢 Important Sysmon Event IDs

### ⚙️ Process Activity

* **Event ID 1 → Process Creation**

  * Logs detailed process execution
  * Includes:

    * Command line
    * Parent process
    * Hashes

📌 Detection:

* Suspicious processes
* Living-off-the-land attacks (LOLBins)

---

### 🌐 Network Activity

* **Event ID 3 → Network Connection**

  * Logs outbound connections

📌 Detection:

* Malware beaconing
* Connections to malicious IPs

---

### 📁 File Activity

* **Event ID 11 → File Creation**

📌 Detection:

* Dropped malware
* Suspicious file creation

---

### 🔁 Persistence & Changes

* **Event ID 13 → Registry Value Set**

📌 Detection:

* Persistence mechanisms
* Registry modifications

---

### 🧬 Process Injection

* **Event ID 8 → CreateRemoteThread**

📌 Detection:

* Code injection techniques
* Advanced malware behavior

---

## 📊 Log Analysis Techniques

### 🔍 What to Look For:

* Multiple failed logins (4625)
* Suspicious process creation (4688 / Sysmon 1)
* Unusual network connections (Sysmon 3)
* Registry persistence (Sysmon 13)
* Unexpected file creation (Sysmon 11)

---

## 🚨 Indicators of Compromise (IoCs)

* High volume of failed logins
* Suspicious command-line executions
* Unknown processes spawning from legitimate ones
* Connections to external or unknown IPs
* Unauthorized registry modifications

---

## 🛡️ Detection Scenarios

### 🔹 Brute Force Attack

* Many **4625**
* Followed by **4624**

---

### 🔹 Suspicious Process Execution

* **4688** or **Sysmon Event 1**
* Unusual parent-child process relationships

---

### 🔹 Malware Beaconing

* **Sysmon Event 3**
* Repeated outbound connections

---

### 🔹 Persistence Mechanism

* **Sysmon Event 13**
* Registry autorun keys modified

---

## 🔎 Log Correlation (SOC Perspective)

In a SOC:

* Logs are centralized in a **SIEM**
* Events are correlated across sources

📌 Example:

* Sysmon Event 1 (process)
  → followed by Sysmon Event 3 (network connection)
  → indicates possible malware execution

---

## 🛠️ Tools & Technologies

* Windows Event Viewer
* **Sysmon**
* SIEM (Splunk / ELK)
* EDR solutions

---

## 🧠 Key Takeaways

* Windows logs provide essential visibility
* Sysmon significantly enhances detection capabilities
* Event correlation is critical for identifying attacks
* Process and network monitoring are key detection points
* Logs are the foundation of incident response

---

## 📌 Final Thoughts

This room helped me understand:

* The difference between default Windows logs and Sysmon logs
* How to detect advanced threats using detailed telemetry
* How attackers operate on Windows systems
* How to correlate multiple events for accurate detection

This knowledge is fundamental for real-world SOC operations and threat detection.
