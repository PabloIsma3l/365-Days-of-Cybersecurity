# Day 6 – Linux Fundamentals (Part 1 & Part 2)

## 🎯 Objective
Build a strong foundation in Linux by learning basic commands, filesystem navigation, permissions, users, and process management.

---

## 📘 Rooms Completed (TryHackMe)
- Linux Fundamentals Part 1
- Linux Fundamentals Part 2

---

## 🧠 Topics Covered

### 📂 Linux Filesystem Basics

| Directory | Purpose |
|----------|---------|
| / | Root directory |
| /home | User home directories |
| /etc | Configuration files |
| /var | Logs and variable data |
| /bin | Essential binaries |
| /usr | User programs |

---

### 🖥 Basic Linux Commands

| Command | Description |
|--------|-------------|
| ls | List directory contents |
| cd | Change directory |
| pwd | Show current path |
| cat | Display file content |
| cp | Copy files |
| mv | Move/rename files |
| rm | Remove files |
| mkdir | Create directories |

---

### 🔐 Users & Permissions

| Permission | Meaning |
|-----------|---------|
| r | Read |
| w | Write |
| x | Execute |

| Entity | Description |
|-------|-------------|
| User | File owner |
| Group | Group ownership |
| Others | Everyone else |

📌 Permission example:

-rwxr-xr--

👥 User & Group Management
Command	Description
whoami	Show current user
id	Display user info
sudo	Execute as superuser
su	Switch user
⚙️ Process Management
Command	Description
ps	Show running processes
top	Real-time process view
kill	Terminate process
systemctl	Manage services
🛠 Tools Used

Linux terminal

TryHackMe virtual machines

🔑 Key Takeaways

Linux filesystem is hierarchical

Permissions control access

Users and groups define ownership

Process management is essential for troubleshooting

🔗 Useful Resources

Linux filesystem hierarchy:
https://www.pathname.com/fhs/

Linux permissions explained:
https://www.linux.com/training-tutorials/understanding-linux-file-permissions/

Linux commands cheat sheet:
https://www.geeksforgeeks.org/linux-commands-cheat-sheet/

🧠 Red Team Notes

Most servers run Linux. Understanding permissions and processes is critical for privilege escalation and lateral movement.
