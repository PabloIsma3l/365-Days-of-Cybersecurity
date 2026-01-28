# 📅 Day 22 – Nmap: The Basics

## 🎯 Daily Objective

Learn how to use **Nmap** to discover live hosts, identify **open ports**, detect **service versions**, and understand the most common scanning options used during network reconnaissance.

---

## ⏱️ Timing Templates (-T0 to -T5)

Control how fast and aggressive Nmap performs scans.

| Option | Name       | Description             |
| ------ | ---------- | ----------------------- |
| -T0    | Paranoid   | Very slow, IDS evasion  |
| -T1    | Sneaky     | Slow scan, low noise    |
| -T2    | Polite     | Reduced bandwidth usage |
| -T3    | Normal     | Default timing          |
| -T4    | Aggressive | Faster, common in labs  |
| -T5    | Insane     | Very fast, noisy        |

Example:

```bash
nmap -T4 192.168.1.10
```

---

## 🐞 Debugging Levels (-d0 to -d9)

Used to troubleshoot Nmap behavior and scan logic.

| Option     | Description             |
| ---------- | ----------------------- |
| -d         | Basic debugging         |
| -d2 to -d4 | Moderate debug output   |
| -d9        | Maximum debug verbosity |

Example:

```bash
nmap -d9 scanme.nmap.org
```

---

## 🔊 Verbosity Levels (-v)

Shows more information during scan execution.

| Option | Description       |
| ------ | ----------------- |
| -v     | Verbose output    |
| -vv    | Very verbose      |
| -v4    | Maximum verbosity |

Example:

```bash
nmap -vv -sS -p- 10.10.10.10
```

---

## 🔴 Red Team Tips

* Use **-T0/-T1** for stealth and evasion
* Use **-T4** for labs and CTFs
* Combine **-vv** with **-oA** for better reporting
* Avoid **-T5** in real environments (very noisy)

