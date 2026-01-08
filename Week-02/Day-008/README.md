# Day 8 – Windows Fundamentals 1

## 🎯 Objective
Understand the basics of the Windows operating system, including its architecture, file system, users, and permissions, to build a solid foundation for security analysis and exploitation.

---

## 📘 Rooms Completed (TryHackMe)
- Windows Fundamentals 1

---

## 🧠 Topics Covered

### 🪟 Windows Architecture
- User Mode vs Kernel Mode
- Role of the Windows Kernel
- System processes and services
- Importance of privileges

---

### 📂 Windows File System

| Path | Description |
|------|-------------|
| C:\ | Main system drive |
| C:\Windows | Core operating system files |
| C:\Program Files | Installed applications (64-bit) |
| C:\Program Files (x86) | Installed applications (32-bit) |
| C:\Users | User profiles |

📌 Windows primarily uses the **NTFS** file system.

---

### 👤 Users & Groups

| Group | Description |
|------|-------------|
| Administrators | Full system privileges |
| Users | Limited privileges |
| SYSTEM | Highest privilege level |

📌 User Account Control (UAC) restricts privilege escalation by default.

---

### 🔐 Permissions (NTFS)

| Permission | Description |
|-----------|-------------|
| Read | View file contents |
| Write | Modify files |
| Execute | Run files |
| Full Control | Complete access |

📌 NTFS permissions are more granular than Linux permissions.

---

### ⚙️ System Information & Basic Commands

| Command | Description |
|--------|-------------|
| whoami | Show current user |
| hostname | Show system name |
| systeminfo | Detailed system info |
| tasklist | List running processes |
| net user | List users |

---

## 🛠 Tools Used
- Windows Command Prompt
- PowerShell
- TryHackMe virtual machines

---

## 🔑 Key Takeaways
- Windows has a strict privilege model
- NTFS permissions control access
- SYSTEM is more powerful than Administrator
- Understanding Windows internals is critical for enumeration

---

## 🔗 Useful Resources

- Windows Internals overview:  
  https://learn.microsoft.com/en-us/windows/win32/sysinfo/about-windows

- NTFS permissions:  
  https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/file-system

---

## 🧠 Red Team Notes
Most enterprise environments run Windows. Knowing users, groups, and permissions is essential for privilege escalation and lateral movement.

---

## ✅ Day 8 Completed
👉 Day 8 completed – Windows Fundamentals 1
