# 📅 Day 22 – Nmap: The Basics

## 🎯 Daily Objective

Learn how to use **Nmap** to discover live hosts, identify **open ports**, detect **service versions**, and understand the most common scanning options used during network reconnaissance.

---

## 🛰️ What is Nmap?

Nmap (Network Mapper) is a powerful **network scanning and enumeration tool** widely used in cybersecurity to map attack surfaces.

It is commonly used for:

* Host discovery
* Port scanning
* Service and version detection
* OS fingerprinting

Nmap is a **core tool** for Red Team operations and defensive assessments.

---

## 📡 Host Discovery

Host discovery determines which systems are **alive** before deeper scanning.

Examples:

```bash
nmap 192.168.1.0/24
nmap -sn 192.168.1.0/24
```

---

## 🔌 Port Scanning

Ports represent exposed services and potential **entry points**.

Examples:

```bash
nmap <IP>
nmap -p 22,80,443 <IP>
nmap -p- <IP>
```

---

## 🧠 Service & OS Detection

Understanding what is running behind each port is critical for enumeration.

Examples:

```bash
nmap -sV <IP>
nmap -O <IP>
nmap -A <IP>
```

---

## 📊 Nmap Options Reference

### 🔍 Scan Types & Options

| Option | Explanation                               |
| ------ | ----------------------------------------- |
| `-sL`  | List scan – list targets without scanning |

### 🖥️ Host Discovery

| Option | Explanation                     |
| ------ | ------------------------------- |
| `-sn`  | Ping scan – host discovery only |

### 🔌 Port Scanning

| Option       | Explanation                                     |
| ------------ | ----------------------------------------------- |
| `-sT`        | TCP connect scan – complete three-way handshake |
| `-sS`        | TCP SYN scan – first step of the handshake      |
| `-sU`        | UDP scan                                        |
| `-F`         | Fast mode – scans the 100 most common ports     |
| `-p <range>` | Specify port range (`-p-` scans all ports)      |
| `-Pn`        | Treat all hosts as online                       |

### 🧠 Service Detection

| Option | Explanation                              |
| ------ | ---------------------------------------- |
| `-O`   | OS detection                             |
| `-sV`  | Service version detection                |
| `-A`   | OS detection, version detection, scripts |

### ⏱️ Timing & Performance

| Option              | Explanation                          |
| ------------------- | ------------------------------------ |
| `-T0`–`-T5`         | Timing templates (paranoid → insane) |
| `--min-parallelism` | Minimum parallel probes              |
| `--max-parallelism` | Maximum parallel probes              |
| `--min-rate`        | Minimum packet rate                  |
| `--max-rate`        | Maximum packet rate                  |
| `--host-timeout`    | Max time per host                    |

### 🖥️ Real-Time Output

| Option | Explanation              |
| ------ | ------------------------ |
| `-v`   | Verbosity (`-vv`, `-v4`) |
| `-d`   | Debugging (`-d`, `-d9`)  |

### 📄 Output & Reporting

| Option       | Explanation                 |
| ------------ | --------------------------- |
| `-oN <file>` | Normal output               |
| `-oX <file>` | XML output                  |
| `-oG <file>` | Grepable output             |
| `-oA <name>` | Output in all major formats |

---

## 🔍 Red Team Perspective

Nmap is the **starting point** of almost every offensive engagement:

* Defines the attack surface
* Identifies services and versions
* Guides further enumeration and exploitation

Good scanning saves time and avoids unnecessary noise.

---

## 🛠️ Key Takeaways

* Nmap is essential for reconnaissance
* Scan options dramatically affect results and stealth
* Understanding output is as important as running scans

---

