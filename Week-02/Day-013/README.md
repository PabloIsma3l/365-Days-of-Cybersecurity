# Day 13 – Windows Command Line (CMD) Fundamentals 🪟💻

## 🎯 Objective
Learn and practice the Windows Command Line (CMD) to navigate the operating system, enumerate system information, and understand its relevance in cybersecurity contexts.

---

## 🧠 Why Windows CMD Matters in Cyber Security
The Windows Command Line is still widely used for:
- System administration
- Incident response
- Forensic triage
- Enumeration during penetration tests
- Living-off-the-land techniques (LOLBins)

Understanding CMD commands helps recognize attacker behavior and perform quick system analysis.

---

## 🪟 Windows Command Line Basics

### 📂 Navigation & File System
- `dir` – List directory contents
- `cd` – Change directory
- `cd ..` – Move up one directory
- `cls` – Clear screen
- `tree` – Display directory structure
- `type <file>` – Display file contents

---

### 👤 User & System Information
- `whoami` – Show current logged-in user
- `hostname` – Display computer name
- `systeminfo` – Detailed system information
- `echo %USERNAME%` – Show username
- `set` – List environment variables

---

### 👥 Users & Groups
- `net user` – List local users
- `net user <username>` – User details
- `net localgroup` – List local groups
- `net localgroup administrators` – List administrators

🔐 *These commands are commonly used during local enumeration.*

---

### 🌐 Networking Commands
- `ipconfig` – Show IP configuration
- `ipconfig /all` – Detailed network info
- `ping <ip/domain>` – Test connectivity
- `arp -a` – View ARP table
- `netstat -ano` – Active connections with PIDs
- `route print` – View routing table

---

### ⚙️ Processes & Services
- `tasklist` – List running processes
- `taskkill /PID <pid> /F` – Terminate a process
- `sc query` – List services
- `sc query state= all` – List all services

---

## 🧪 Practical Security Focus
- Identify valuable system data from command output
- Understand how attackers enumerate systems without external tools
- Recognize which commands generate logs
- Differentiate CMD from PowerShell use cases

---

## 🧠 Key Takeaways
- CMD is still relevant in modern Windows systems
- Native tools can provide deep system visibility
- Enumeration often requires no malware or third-party tools
- Mastery of basics strengthens blue and red team skills

---

## 📌 Progress
- ✔ Windows Command Line (CMD) Fundamentals
- ✔ Cyber Security 101 – Ongoing

---

## 🚀 Next Steps
➡️ Day 14 – Windows PowerShell Fundamentals  
➡️ Advanced enumeration and automation

> “Know the basics before automating the complex.”
