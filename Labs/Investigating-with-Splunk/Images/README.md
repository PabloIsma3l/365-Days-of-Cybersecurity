# TryHackMe — Investigating with Splunk

**Platform:** TryHackMe
**Category:** SIEM / Log Analysis
**Difficulty:** Easy

---

# Overview

This lab focuses on investigating suspicious activity using **Splunk SIEM**.
The objective is to analyze Windows event logs and identify malicious activity occurring on a workstation.

During the investigation we identify:

* Suspicious command execution
* Creation of a new user account
* Registry modifications
* The external URL accessed by the compromised system

---

# Dataset

The dataset analyzed in this lab is:

```
splunk_challenge1.json
```

All logs are ingested into Splunk and queried using **SPL (Search Processing Language)**.

---

# Initial Exploration

The investigation begins by exploring all events in the dataset.

Search used:

```
source="splunk_challenge1.json" index=main
```

This query allows us to observe the structure of the logs and identify relevant fields such as:

* EventID
* Hostname
* EventTime
* AccountName
* Message
* CommandLine

This step helps determine which logs may contain suspicious activity.

---

# Detecting Suspicious Command Execution

During log analysis we identify a suspicious command execution involving **wmic.exe**.

Command observed:

```
net user /add Alberto password
```

This command is used to create a new user account in Windows.

The execution through **WMIC** may indicate suspicious activity or post-exploitation behavior.

---

# Investigating User Creation

To confirm the account creation we search for the Windows event that logs new user accounts.

Relevant Windows Event ID:

```
4720
```

Search used:

```
source="splunk_challenge1.json" EventID=4720
```

This event confirms that a new user account was created.

Important details identified:

* **Creator User:** James
* **New Account:** Alberto
* **Host:** WORKSTATION6
* **Event Type:** User Account Management

This indicates that the user **James created the account Alberto**.

---

# Registry Activity

Further investigation shows registry activity related to the new user.

Relevant Event ID:

```
13
```

Search used:

```
source="splunk_challenge1.json" EventID=13 "Alberto"
```

This reveals a registry modification linked to the account creation.

Registry path observed:

```
HKLM\SAM\SAM\Domains\Account\Users\Names\Alberto
```

This confirms that the account was successfully written to the Windows registry.

---

# Network Investigation

After confirming the system compromise, the next step is to analyze **network-related events** in the logs.

The objective is to determine whether the compromised system connected to any suspicious external resources.

Relevant logs show outbound activity that includes a URL accessed by the workstation.

---

# Identifying the Suspicious URL

By filtering the logs and analyzing the network activity, we identify the malicious or suspicious URL that the compromised system accessed.

Example search strategy:

```
source="splunk_challenge1.json" http
```

or

```
source="splunk_challenge1.json" url
```

Through log inspection we identify the **external URL accessed by the host**, which is the final indicator of compromise required for the lab.

---

# Timeline of the Incident

Based on the investigation we reconstruct the sequence of events:

1. A suspicious command is executed using **wmic.exe**.
2. The command `net user /add` creates a new user account.
3. Windows logs record the event with **EventID 4720**.
4. Registry modifications confirm the creation of the account.
5. The compromised system accesses an external suspicious URL.

---

# Key Findings

The investigation reveals:

* A user account named **Alberto** was created.
* The action was performed by **James**.
* The command used was `net user /add`.
* Registry activity confirms the account creation.
* The system accessed a **suspicious external URL**.

---

# Skills Practiced

* SIEM Investigation
* Log Analysis
* Splunk SPL Queries
* Windows Event Log Analysis
* Threat Investigation
* Identifying Indicators of Compromise (IOCs)

---

# Tools Used

* Splunk
* Windows Security Logs
* SPL (Search Processing Language)
