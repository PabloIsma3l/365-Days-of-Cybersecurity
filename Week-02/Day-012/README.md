# Day 12 – Windows Fundamentals Review & Active Directory Basics 🪟🧩

## 🎯 Objective
Reinforce core Windows security fundamentals while introducing the foundational concepts of Active Directory, a critical component in modern enterprise environments and a primary target in real-world attacks.

---

## 🪟 Windows Fundamentals (Part 1, 2 & 3) – Security Review

### 🔐 Windows Desktop & NTFS
- Windows desktop environment overview
- NTFS file system structure
- File and folder permissions
- Access Control Lists (ACLs)

🔎 **Security Insight:**  
Misconfigured NTFS permissions are a common privilege escalation vector.

---

### ⚠️ User Account Control (UAC)
- Purpose of UAC
- Elevation of privileges
- UAC settings and behavior

🔎 **Security Insight:**  
Weak UAC configurations increase the risk of privilege abuse.

---

### 🛠️ System Configuration & Resource Monitoring
- Startup programs and services
- System Configuration (`msconfig`)
- Resource Monitor

🔎 **Security Insight:**  
Persistence mechanisms often rely on startup entries and scheduled tasks.

---

### 🧩 Windows Registry
- Registry structure and hives
- Common persistence locations
- Role of the registry in system behavior

🔎 **Security Insight:**  
The registry is frequently abused for persistence and configuration manipulation.

---

### 🛡️ Built-in Windows Security Tools
- Windows Update
- Windows Security
- BitLocker
- Firewall basics

🔎 **Security Insight:**  
Outdated systems and disabled protections are frequent entry points for attackers.

---

## 🧠 Active Directory Basics (Introduction)

### 🧩 What is Active Directory?
- Centralized identity and access management
- Used in enterprise environments
- Backbone of authentication and authorization

---

### 🏗️ Core Components
- Domains
- Domain Controllers
- Users & Groups
- Organizational Units (OUs)
- Group Policy Objects (GPOs)

---

### 🔐 Why Active Directory Matters in Security
- Centralized control means centralized risk
- Most enterprise attacks target AD
- Misconfigurations lead to lateral movement and privilege escalation

---

## 🧠 Key Takeaways
- Windows security relies heavily on correct configuration
- Active Directory is a high-value target in enterprise networks
- Understanding Windows fundamentals is essential before attacking or defending AD
- Enumeration is more important than exploitation

---

## 📌 Progress
- ✔ Windows Fundamentals (Parts 1–3) — Reviewed
- ✔ Active Directory Basics — Completed
- ✔ Cyber Security 101 — Ongoing (27%)

---

## 🚀 Next Steps
Continue with **Command Line (PowerShell & Bash)** to gain hands-on skills for enumeration and automation in both Windows and Linux environments.

> Strong foundations build effective attackers and defenders.
