# 🤖 Introduction to SOAR — Day 67
## 📌 Overview

This document summarizes the concepts learned in the **"Introduction to SOAR"** room on TryHackMe.

The room introduces **Security Orchestration, Automation and Response (SOAR)** and explains how Security Operations Centers (SOCs) use automation to improve incident response and reduce analyst workload.

---

## 🎯 Learning Objectives

* Understand what SOAR is
* Learn the difference between **Orchestration, Automation, and Response**
* Understand how SOAR integrates with security tools
* Learn how **automated response playbooks** work

---

## 🧠 What is SOAR?

**SOAR (Security Orchestration, Automation and Response)** is a platform that allows security teams to:

* Automate repetitive security tasks
* Integrate multiple security tools
* Improve incident response time
* Reduce investigation workload

SOAR platforms typically integrate with:

* SIEM platforms
* EDR solutions
* Threat intelligence platforms
* Ticketing systems
* Firewalls and network security tools

---

## 🏗️ SOAR Core Components

### 🔹 Orchestration

**Orchestration** connects different security tools so they can work together within a single workflow.

Example:

1. A SIEM detects suspicious activity
2. SOAR queries a threat intelligence database
3. Additional context is added to the alert

---

### 🔹 Automation

**Automation** allows tasks to be executed automatically without human intervention.

Examples:

* Blocking malicious IP addresses
* Enriching alerts with threat intelligence
* Collecting endpoint data
* Creating incident tickets automatically

---

### 🔹 Response

SOAR enables automated or semi‑automated responses to security incidents.

Examples:

* Isolating a compromised endpoint
* Disabling a compromised user account
* Blocking malicious traffic

---

## 📘 SOAR Playbooks

A **playbook** is a predefined workflow that describes how a system should respond to a specific type of alert.

Playbooks define:

1. The trigger event
2. Data enrichment steps
3. Tools that should be queried
4. Response actions that should be executed

Playbooks help SOC teams respond to incidents in a **consistent and efficient way**.

---

## 🚨 Example Automated Incident Workflow

Example response using SOAR:

1. SIEM detects a suspicious login
2. SOAR enriches the alert with threat intelligence
3. The system checks whether the IP is malicious
4. If confirmed, the IP is automatically blocked
5. An incident ticket is created
6. The SOC team is notified

---

## 🧰 Benefits of SOAR in a SOC

* Faster incident response
* Reduced alert fatigue
* Standardized incident workflows
* Improved operational efficiency
* Better coordination between security tools

---

## 🏁 Room Completion Status

* ✅ All tasks completed
* 🧠 Fundamental understanding of SOAR concepts and automated security operations
