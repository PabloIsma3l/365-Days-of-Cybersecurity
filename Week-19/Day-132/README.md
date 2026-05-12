# 👻 Boogeyman 2 — TryHackMe Writeup

**📅 Day 132 — 365 Days of Cybersecurity**
**✅ Status: Completed**
**🏷️ Tags:** `Phishing Analysis` `Memory Forensics` `Volatility` `Macro Analysis` `olevba` `DFIR` `C2` `Persistence` `SOC`
**⚙️ Difficulty:** Medium

---

## 🧠 Overview

The Boogeyman threat group is back — this time targeting **Human Resources** instead of Finance. In Boogeyman 2, a malicious Word document disguised as a job application resume was delivered to an HR specialist, kicking off a multi-stage attack chain that ended with an established C2 connection and persistence via a scheduled task.

This room introduces **memory forensics with Volatility** as the primary investigation tool alongside macro analysis with `olevba`, making it a significant step up in technical depth from Boogeyman 1.

> **Core principle:** The memory dump doesn't lie. Even if malware cleans up its tracks on disk, RAM captures the execution state at a point in time — processes, network connections, command-line arguments, and more.

---

## 🎯 Learning Objectives

- Analyze a malicious Word document macro using `olevba`
- Understand multi-stage payload delivery (doc → JS → exe)
- Use the **Volatility 3** framework for memory forensics
- Extract process trees, network connections, and command-line arguments from a memory dump
- Identify C2 infrastructure and persistence mechanisms from memory artifacts
- Reconstruct the full attack chain from initial phishing to established foothold

---

## 🗂️ Artifacts Provided

| File | Description |
|---|---|
| Phishing email | Email received by Maxine containing the malicious attachment |
| `Resume_WesleyTaylor.doc` | Malicious Word document with embedded VBA macro |
| `WKSTN-2961.raw` | Full memory dump from the compromised workstation |

---

## 📧 Task 2 — Spear-Phishing Human Resources

### Scenario

**Maxine Beck**, an HR Specialist at *Quick Logistics LLC*, received what appeared to be a job application from a candidate named Wesley Taylor. The attached Word document — a fake resume — contained a malicious VBA macro that executed automatically when opened. The security team flagged suspicious commands on her workstation, triggering this investigation.

> **Why HR?** HR staff regularly open unsolicited attachments (resumes, portfolios, applications) as part of their job — making them a high-value social engineering target. Attackers exploit this professional habit rather than relying on a generic phishing lure.

### Email Header Findings

```
Sender:   westaylor23@outlook.com      ← Free webmail — no corporate domain
Victim:   maxine.beck@quicklogisticsorg.onmicrosoft.com
Subject:  Job Application — Wesley Taylor
Attachment: Resume_WesleyTaylor.doc
```

> The attacker used a free Outlook account to impersonate a job applicant. Unlike Boogeyman 1 (which used a typosquatted domain + ElasticEmail relay), this approach is simpler — just a free webmail account. Harder to proactively block, but easier to spot post-incident.

### Hashing the Attachment

Before any analysis, always hash the file — it's the fingerprint used for threat intel correlation and chain of custody:

```bash
md5sum Resume_WesleyTaylor.doc
# Output: 52c4384a0b9e248b95804352ebec6c5b
```

This hash can be submitted to **VirusTotal** or cross-referenced against threat intel feeds to check if this exact sample has been seen in prior campaigns.

### Macro Analysis with `olevba`

`olevba` (part of the **oletools** suite) is the standard tool for extracting and analyzing VBA macros from Office documents without executing them. It's safe, fast, and reveals the macro logic in plaintext.

```bash
olevba Resume_WesleyTaylor.doc
```

**What the macro revealed:**

```vba
' Macro executes on document open (AutoOpen)
' Stage 1: Downloads a disguised payload (update.png — actually a JS script)
' Stage 2 payload URL:
https://files.boogeymanisback.lol/aa2a9c53cbb80416d3b47d85538d9971/update.png

' The downloaded file is saved as:
C:\ProgramData\update.js

' Execution triggered by:
wscript.exe C:\ProgramData\update.js
```

**Key observations from the macro:**
- The payload is disguised as a `.png` image to evade content-type filtering on proxies and email gateways
- `wscript.exe` (Windows Script Host) executes the JS file — a classic LOLBin abuse
- The domain `boogeymanisback.lol` is the attacker's infrastructure (same group as Boogeyman 1, new domain)

### Stage 2 — JavaScript Payload (`update.js`)

The JS script executed by `wscript.exe` acts as a dropper for the final payload:

```
Stage 2 download URL:
https://files.boogeymanisback.lol/aa2a9c53cbb80416d3b47d85538d9971/update.exe

Saved to: C:\Windows\Tasks\updater.exe
```

The final binary (`updater.exe`) establishes the C2 connection.

### MITRE ATT&CK Mapping — Initial Access & Execution

| Technique | ID | Description |
|---|---|---|
| Spearphishing Attachment | T1566.001 | HR-targeted phishing with fake resume |
| Malicious File (Macro) | T1204.002 | VBA AutoOpen macro in Word document |
| Windows Script Host (wscript) | T1059.005 | JS payload executed via wscript.exe |
| Masquerading | T1036 | Payload disguised as `.png` image |
| Ingress Tool Transfer | T1105 | Multi-stage payload download (png → exe) |

---

## 🧠 Task 3 — Memory Forensics with Volatility 3

### Why Memory Forensics?

When malware executes, it leaves traces in RAM that may not exist on disk — especially with fileless techniques, process injection, or when malware deletes itself post-execution. A memory dump captures:

- Running processes (including hidden/injected ones)
- Open network connections
- Command-line arguments used to launch processes
- Loaded DLLs and modules
- Registry handles, file handles, and more

### Volatility 3 — Core Commands Reference

```bash
# Base syntax
vol -f WKSTN-2961.raw <plugin>

# List running processes as a tree (shows parent-child relationships)
vol -f WKSTN-2961.raw windows.pstree

# List processes (flat list with PID, PPID, timestamps)
vol -f WKSTN-2961.raw windows.pslist

# Show command-line arguments for each process
vol -f WKSTN-2961.raw windows.cmdline.CmdLine

# Scan for network connections (active + recently closed)
vol -f WKSTN-2961.raw windows.netscan

# Dump memory of a specific process (for further analysis)
vol -f WKSTN-2961.raw windows.memmap --dump --pid <PID>

# Search raw strings in the memory dump
strings WKSTN-2961.raw | grep -i "schtasks\|powershell\|http"
```

---

### Investigation Findings from Memory

#### Process Tree Analysis

```bash
vol -f WKSTN-2961.raw windows.pstree
```

```
WINWORD.EXE (PID: 1124)        ← Victim opened the malicious resume
└── wscript.exe (PID: 4260)    ← Macro launched wscript to run update.js
    └── updater.exe (PID: 6216) ← Stage 2 binary — C2 implant
```

> **Analyst note:** `WINWORD.EXE` spawning `wscript.exe` is the same red flag pattern as Office spawning `powershell.exe` in Boogeyman 1. Office applications should never directly launch scripting engines — this is almost always macro abuse.

#### Key Process Details

| Process | PID | Parent PID | Role |
|---|---|---|---|
| `WINWORD.EXE` | 1124 | — | Opened the malicious `.doc` |
| `wscript.exe` | 4260 | 1124 | Executed `update.js` (stage 2 dropper) |
| `updater.exe` | 6216 | 4260 | C2 implant — established callback |

#### Full File Path of the Attachment (from memory)

```bash
vol -f WKSTN-2961.raw windows.cmdline.CmdLine
```

The `cmdline` plugin reveals that Word opened the document from Outlook's temp cache — confirming it arrived via email:

```
C:\Users\maxine.beck\AppData\Local\Microsoft\Windows\INetCache\Content.Outlook\WQHGZCFI\Resume_WesleyTaylor (002).doc
```

> This path is a forensic goldmine — `INetCache\Content.Outlook` is where Outlook temporarily stores email attachments when a user opens them directly from the email without saving first. This confirms the delivery vector was email, and the specific subfolder (`WQHGZCFI`) is unique to this Outlook profile/session.

#### C2 Network Connection

```bash
vol -f WKSTN-2961.raw windows.netscan | grep updater.exe
```

```
Process:   updater.exe (PID: 6216)
Local:     WKSTN-2961:<ephemeral port>
Remote:    128.199.95.189:8080
State:     ESTABLISHED
```

- **IP:** `128.199.95.189` — DigitalOcean VPS (common for budget C2 infrastructure)
- **Port:** `8080` — HTTP alternate port, often used to blend in with legitimate web traffic

#### Persistence — Scheduled Task

```bash
# Dump strings from the C2 process memory
vol -f WKSTN-2961.raw windows.memmap --dump --pid 6216

# Search for scheduled task commands
strings WKSTN-2961.raw | grep -i schtasks
```

The attacker created a scheduled task immediately after establishing C2 — a standard "land and persist" pattern:

```powershell
schtasks /Create /F /SC DAILY /ST 09:00 /TN Updater /TR \
'C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe \
-NonI -W hidden -c "IEX ([Text.Encoding]::UNICODE.GetString(\
[Convert]::FromBase64String((gp HKCU:\Software\Microsoft\Windows\CurrentVersion debug).debug)))"'
```

**Breaking down this persistence command:**

| Component | Meaning |
|---|---|
| `/SC DAILY /ST 09:00` | Runs every day at 9:00 AM |
| `/TN Updater` | Task name disguised as a legitimate updater |
| `-NonI` | Non-interactive — no window |
| `-W hidden` | Hidden window — invisible to the user |
| `-c "IEX ..."` | Executes a Base64-decoded payload via `Invoke-Expression` |
| `gp HKCU:\Software\Microsoft\Windows\CurrentVersion debug` | Reads a registry key named `debug` under HKCU — the actual payload is **stored in the registry** |

> **This is a Registry-based fileless persistence technique (T1547.001 + T1027).** The PowerShell payload is stored in the registry, not on disk — meaning standard file scanning won't find it. The scheduled task just triggers the in-memory execution daily.

### MITRE ATT&CK Mapping — Post-Exploitation

| Technique | ID | Description |
|---|---|---|
| Process Injection / Spawning | T1055 | Malicious process chain from WINWORD |
| Command and Control: Non-Standard Port | T1571 | C2 over port 8080 |
| Scheduled Task | T1053.005 | Daily persistence via schtasks |
| Registry Run / Storage | T1547.001 | Payload stored in HKCU registry key |
| Obfuscated Files: Encoding | T1027 | Base64-encoded payload in registry |
| PowerShell | T1059.001 | Fileless execution via IEX + registry read |
| Masquerading | T1036.004 | Task named "Updater", binary in `C:\Windows\Tasks\` |

---

## 🔄 Full Attack Chain Reconstruction

```
[T+0:00] Maxine opens Resume_WesleyTaylor.doc from Outlook
         └── Saved to: C:\...\INetCache\Content.Outlook\WQHGZCFI\

[T+0:01] VBA AutoOpen macro fires
         └── Downloads update.png (actually JS) from:
             https://files.boogeymanisback.lol/.../update.png
         └── Saves as: C:\ProgramData\update.js

[T+0:02] Macro executes: wscript.exe C:\ProgramData\update.js (PID: 4260)
         └── Parent: WINWORD.EXE (PID: 1124)

[T+0:03] update.js downloads final payload:
         https://files.boogeymanisback.lol/.../update.exe
         └── Saved as: C:\Windows\Tasks\updater.exe

[T+0:04] updater.exe executes (PID: 6216)
         └── Establishes C2 callback to 128.199.95.189:8080

[T+0:05] Attacker issues persistence command over C2:
         └── schtasks creates "Updater" task (daily @ 09:00)
         └── Payload stored in HKCU registry — fileless execution
```

---

## 🚨 Indicators of Compromise (IoCs)

### Network-Based

| IoC | Type | Description |
|---|---|---|
| `files.boogeymanisback.lol` | Domain | Payload hosting server |
| `128.199.95.189` | IP | C2 server (DigitalOcean VPS) |
| Port `8080` | Port | C2 communication channel |
| `/aa2a9c53cbb80416d3b47d85538d9971/` | URL path | Unique staging directory |

### Host-Based

| IoC | Type | Description |
|---|---|---|
| `Resume_WesleyTaylor.doc` | File | Malicious Word document with macro |
| `52c4384a0b9e248b95804352ebec6c5b` | MD5 Hash | Hash of the malicious document |
| `C:\ProgramData\update.js` | Path | Stage 2 dropper script |
| `C:\Windows\Tasks\updater.exe` | Path | C2 implant binary |
| `HKCU:\Software\Microsoft\Windows\CurrentVersion debug` | Registry | Fileless payload storage key |
| Scheduled Task: `Updater` | Task | Daily persistence at 09:00 |

### Behavioral

- `WINWORD.EXE` spawning `wscript.exe`
- `wscript.exe` making outbound HTTP connections
- Binary written to `C:\Windows\Tasks\` (unusual path for executables)
- Outbound `ESTABLISHED` connection to non-standard port 8080
- Scheduled task with PowerShell IEX + registry read in the command

---

## 🛡️ Detection Opportunities

```sql
-- Office application spawning script interpreter
EventID = 4688 AND
ParentProcessName IN ("WINWORD.EXE", "EXCEL.EXE", "POWERPNT.EXE") AND
NewProcessName IN ("wscript.exe", "cscript.exe", "powershell.exe", "cmd.exe")

-- wscript executing JS files (common dropper pattern)
EventID = 4688 AND
NewProcessName LIKE "%wscript.exe%" AND
CommandLine LIKE "%.js%"

-- Executable written to Windows\Tasks (abnormal binary location)
EventID = 11 (Sysmon File Created) AND
TargetFilename LIKE "C:\Windows\Tasks\%.exe"

-- Scheduled task with obfuscated PowerShell payload
EventID = 4698 AND
TaskContent CONTAINS ("IEX" OR "FromBase64String" OR "hidden")

-- Registry used as payload storage
EventID = 13 (Sysmon Registry Value Set) AND
TargetObject LIKE "HKCU\Software\Microsoft\Windows\CurrentVersion\%" AND
Details CONTAINS ("<base64_pattern>")

-- C2 beaconing on port 8080
NetworkConnection AND
DestinationPort = 8080 AND
InitiatingProcess NOT IN (known_browser_list)
```

---

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| **olevba** (oletools) | VBA macro extraction and static analysis from `.doc` |
| **Volatility 3** | Memory forensics — processes, network, cmdline |
| **md5sum** | File hashing for threat intel correlation |
| **strings** | Extracting readable text from raw memory dump |
| **grep** | Filtering strings output for specific keywords |
| **VirusTotal** | Hash and IOC correlation against threat intel |

---

## 🧪 Key Concepts Practiced

- Macro-based initial access via social engineering (HR targeting)
- Static analysis of Office macros with `olevba` — no sandbox required
- Multi-stage payload delivery: `.doc` → `.js` → `.exe`
- LOLBin abuse: `wscript.exe` as a script executor
- Memory forensics workflow with Volatility 3: `pstree`, `cmdline`, `netscan`, `memmap`
- Identifying C2 connections from memory network scan
- Uncovering fileless persistence: scheduled task + registry-stored payload
- Chaining `strings` + `grep` for targeted memory string extraction

---

## 🧠 Key Takeaways

1. **HR is a high-value social engineering target.** Opening unsolicited attachments is part of the job for HR professionals. Security awareness training must specifically address this — with guidance on opening submissions in sandboxed or read-only environments.

2. **`olevba` before execution, always.** Never open a suspicious document to "see what it does." `olevba` extracts the macro logic statically, letting you analyze it safely without any risk of execution.

3. **Disguising payloads as images (`update.png`) bypasses naive content filtering.** File extension ≠ file type. Robust defenses inspect file magic bytes, not just extensions, and sandbox all downloads from Office macros.

4. **`C:\Windows\Tasks\` is not just for tasks.** Placing an executable in this directory is a masquerading technique — it blends in with legitimate Windows infrastructure. Monitor for `.exe` files written to this path.

5. **Memory forensics fills the gaps disk forensics misses.** The C2 binary, its network connection, and the persistence command were all recoverable from RAM — even if the attacker later cleaned disk artifacts, the memory snapshot would preserve the evidence.

6. **Registry-based payload storage is a mature evasion technique.** Storing the actual malicious code in a registry value and reading it at runtime via PowerShell means there's no malicious file on disk for AV to scan. Detection requires behavioral monitoring (registry write + PowerShell IEX correlation).

7. **Process trees tell the story instantly.** `WINWORD → wscript → updater.exe` is an immediately suspicious chain. Building alerting around anomalous Office parent-child relationships catches a huge range of macro-based attacks.

---

## 📊 Boogeyman 1 vs Boogeyman 2 — Comparison

| Aspect | Boogeyman 1 | Boogeyman 2 |
|---|---|---|
| Target | Finance (Julianne) | HR (Maxine) |
| Lure | Fake invoice (BEC) | Fake job application |
| Delivery | LNK inside encrypted ZIP | Macro-enabled Word document |
| Stage 1 execution | PowerShell download cradle | VBA AutoOpen macro + wscript.exe |
| Stage 2 format | PS1 script | JS dropper → EXE |
| C2 method | HTTP POST | HTTP on port 8080 |
| Exfiltration | DNS (kdbx file) | Not observed (focus on persistence) |
| Persistence | Scheduled task (basic) | Scheduled task + registry fileless payload |
| Primary investigation tool | jq (JSON logs) + Wireshark | Volatility 3 (memory forensics) |

---

## 📌 Final Thoughts

Boogeyman 2 builds directly on the first room but shifts the investigation lens significantly — from log and PCAP analysis to **memory forensics**, which is a core skill gap for many SOC analysts. The Volatility workflow (`pstree → cmdline → netscan → memmap → strings`) is transferable to real-world IR engagements and is worth practicing until it becomes second nature.

The persistence mechanism here — daily scheduled task executing a Base64 payload read from the registry — is a technique used in real campaigns by groups like **Emotet**, **TrickBot**, and various APT actors. It's specifically designed to survive reboots, evade file-based AV, and look legitimate at a glance (`Updater` running `powershell.exe` at 9:00 AM sounds perfectly normal).

The evolution from Boogeyman 1 to 2 reflects how threat actors layer techniques — each campaign is slightly more sophisticated, using more evasion and more stages to complicate detection and response.

