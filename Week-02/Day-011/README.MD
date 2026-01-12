# Day 11 – Linux Fundamentals (Security Refresher) 🐧

## 🎯 Objective
Reinforce Linux fundamentals with a cybersecurity-focused mindset, understanding how attackers and defenders interact with Linux systems during the reconnaissance and enumeration phases.

---

## 🐧 Why Linux Matters in Cybersecurity
Linux is the backbone of:
- Servers and cloud infrastructure
- Security tools and frameworks
- Red Team and Blue Team operations

Understanding Linux fundamentals is essential for identifying misconfigurations, privilege boundaries, and exposed services.

---

## 🧪 Activities Performed
- Reviewed Linux Fundamentals (Parts 1, 2, and 3)
- Re-executed core system and network commands
- Focused on understanding outputs rather than memorizing syntax
- Maintained daily consistency to preserve TryHackMe streak

---

## 🔍 Commands Reviewed & Security Relevance

### 👤 User & Privilege Enumeration
- `whoami` – Identify current user context
- `id` – Check user and group memberships
- `groups` – Identify privilege scope

🔎 **Security Insight:**  
Improper group membership can lead to privilege escalation.

---

### 📂 File System & Permissions
- `ls -la` – List files and permissions
- `pwd` – Identify current directory
- `stat` – View file metadata

🔎 **Security Insight:**  
World-writable files and misconfigured permissions are common attack vectors.

---

### ⚙️ Processes & Services
- `ps aux` – List running processes
- `top` / `htop` – Monitor system activity

🔎 **Security Insight:**  
Running services reveal potential attack surfaces and privilege boundaries.

---

### 🌐 Networking & Interfaces
- `ip a` – Network interfaces and IP addresses
- `ss -tuln` / `netstat -tuln` – Listening services

🔎 **Security Insight:**  
Open ports and listening services indicate entry points for attackers.

---

## 🧠 Key Takeaways
- Linux enumeration is the foundation of most attacks
- Understanding permissions is more important than exploiting vulnerabilities
- Many compromises happen due to misconfigurations, not exploits
- Security begins with visibility and context

---

## 📌 Progress
- ✔ Linux Fundamentals (PreSecurity) — Completed
- ✔ Linux refresher completed with security focus
- ✔ Daily practice maintained

---

## 🚀 Next Steps
Move forward with **Command Line (PowerShell & Bash)** to improve efficiency, automation, and speed during security operations.

> Consistency builds expertise. One day at a time.
