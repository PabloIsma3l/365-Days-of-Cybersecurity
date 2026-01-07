# Day 7 – Linux Fundamentals (Part 3)

## 🎯 Objective
Deepen Linux knowledge by understanding networking, services, logs, and environment variables, preparing for real-world administration and security scenarios.

---

## 📘 Rooms Completed (TryHackMe)
- Linux Fundamentals Part 3

---

## 🧠 Topics Covered

### 🌐 Networking in Linux

| Command | Description |
|--------|-------------|
| ip a | Show network interfaces |
| ip route | Display routing table |
| ss | Show listening ports |
| netstat | Network statistics |
| ping | Test connectivity |

---

### 🔌 Services & Processes

| Command | Description |
|--------|-------------|
| systemctl status | Check service status |
| systemctl start/stop | Manage services |
| ps aux | List processes |
| top | Real-time monitoring |

📌 Services commonly run as background processes (daemons).

---

### 📜 Logs & Monitoring

| Log Path | Description |
|---------|-------------|
| /var/log/syslog | System logs |
| /var/log/auth.log | Authentication logs |
| /var/log/apache2/ | Web server logs |

📌 Logs are critical for troubleshooting and incident analysis.

---

### 🌱 Environment Variables

| Variable | Purpose |
|--------|---------|
| PATH | Command search paths |
| HOME | User home directory |
| USER | Current user |

| Command | Description |
|--------|-------------|
| env | List environment variables |
| export | Set variables |
| echo $VAR | Print variable |

---

## 🛠 Tools Used
- Linux terminal
- TryHackMe virtual machines

---

## 🔑 Key Takeaways
- Linux networking tools help enumerate services
- Services and logs reveal system behavior
- Environment variables can affect execution paths
- This knowledge is essential for privilege escalation

---

## 🔗 Useful Resources

- Linux networking commands:  
  https://www.cyberciti.biz/faq/linux-ip-command-examples/

- Systemd services:  
  https://www.freedesktop.org/wiki/Software/systemd/

- Linux logs explained:  
  https://www.loggly.com/ultimate-guide/linux-logging-basics/

---

## 🧠 Red Team Notes
Understanding services, logs, and environment variables enables:
- Service enumeration
- Misconfiguration discovery
- Privilege escalation paths

---

## ✅ Day 7 Completed
👉 Day 7 completed – Linux Fundamentals Part 3
