# 👻 Boogeyman 3 — TryHackMe Writeup

**📅 Day 133 — 365 Days of Cybersecurity**
**✅ Status: Completed**
**🏷️ Tags:** `Elastic SIEM` `DFIR` `Lateral Movement` `UAC Bypass` `Mimikatz` `DCSync` `Ransomware` `Threat Hunting` `SOC` `Active Directory`
**⚙️ Difficulty:** Hard

---

## 🧠 Overview

Boogeyman 3 — *"The Chaos Inside"* — is the most advanced entry in the trilogy and the capstone of the **TryHackMe SOC Level 1** path. The Boogeyman threat actor has evolved significantly: this campaign moves beyond a single-host compromise into a **full Active Directory attack chain**, culminating in a domain-wide ransomware deployment.

The entire investigation takes place inside **Elastic SIEM**, making this room a practical exercise in real-world SOC tooling — writing KQL queries, pivoting between log sources, and following the attacker's trail across multiple machines and accounts.

> **Core principle:** In an Active Directory environment, compromising one endpoint is just the beginning. The real threat is lateral movement — and the attacker's goal is always the Domain Controller.

---

## 🎯 Learning Objectives

- Investigate a multi-stage attack using **Elastic SIEM** (KQL queries, log pivoting)
- Understand HTA-based initial access and DLL side-loading execution
- Identify **UAC bypass** via `fodhelper.exe` and registry manipulation
- Trace **credential dumping** with Mimikatz across multiple machines
- Follow **lateral movement** through credential reuse and PowerShell remoting
- Understand **DCSync attacks** and their impact on the entire domain
- Identify ransomware staging and delivery from attacker infrastructure

---

## 🗂️ Investigation Platform

| Tool | Role |
|---|---|
| **Elastic SIEM** | Primary investigation platform — all log sources ingested here |
| **KQL (Kibana Query Language)** | Query language for filtering and correlating events |
| **Sysmon** | Endpoint telemetry provider (process, network, registry, file events) |
| **Windows Event Logs** | Authentication, process creation, scheduled tasks |

---

## 📧 Scenario — The Chaos Inside

A new campaign by the Boogeyman group was detected targeting *Quick Logistics LLC*. This time the victim received a phishing email with what appeared to be a **PDF review document**. In reality, the attachment was an **HTA (HTML Application)** file — a disguised executable that kicked off a sophisticated multi-stage attack chain reaching all the way to the Domain Controller.

The security team flagged suspicious commands and initiated the investigation. Your task: **trace every step of the attacker's actions across the environment using Elastic SIEM.**

---

## 🔍 Elastic SIEM — Investigation Methodology

### Essential KQL Filters Used

```kql
// Filter by date range first — always scope to the incident window
@timestamp >= "2023-..." AND @timestamp <= "2023-..."

// Find process creation events (Sysmon Event ID 1)
event.code: 1

// Filter by specific file extension
file.extension: html

// Follow surrounding events for a specific process
process.pid: 6392

// Search for specific tool names
process.name: "fodhelper.exe"
process.name: "mimikatz.exe"

// Search across all fields for a keyword
*mimikatz*

// Filter by hostname for lateral movement investigation
host.hostname: "WKSTN-1327"

// Combine filters
host.hostname: "WKSTN-1327" AND event.code: 1

// Search for download activity
*download* OR *DownloadFile* OR *WebClient*

// Search for ransomware staging
host.hostname: "DC" AND *ransom*
```

> **SOC Insight:** Always start with a time filter. In a real incident, the alert timestamp gives you the pivot point — scope your search to a reasonable window around it to reduce noise before drilling down.

---

## 📥 Task 2 — Initial Access: Stage 1 Payload

### The Phishing Lure

The victim received what appeared to be a PDF document for review. However, the attachment was disguised — its true extension was `.hta` (HTML Application). This is a well-known **initial access technique** that abuses the Windows `mshta.exe` binary to execute arbitrary code.

```
Filename:     review.pdf  ← displayed name
True type:    HTML Application (.hta)
Executor:     mshta.exe (PID: 6392)
```

**Why HTA files are dangerous:**
- They execute with the privileges of the current user
- They can run VBScript and JScript natively via `mshta.exe`
- Many users (and email gateways) don't flag `.hta` as dangerous
- They bypass PowerShell execution policy restrictions entirely

### KQL Query to Find Stage 1

```kql
file.extension: html
```

This surfaces the log of the HTA file being written/executed, revealing the PID of `mshta.exe`: **6392**.

---

## 🔄 Task 3 — Stage 1 Execution Chain

### Step 1 — File Copy via xcopy

Following the surrounding log documents around PID 6392, the first malicious action was copying a DLL payload from removable/external media to the user's temp directory:

```cmd
"C:\Windows\System32\xcopy.exe" /s /i /e /h D:\review.dat C:\Users\EVAN~1.HUT\AppData\Local\Temp\review.dat
```

**Breaking down this command:**

| Flag | Meaning |
|---|---|
| `/s` | Copy subdirectories (except empty ones) |
| `/i` | Treat destination as a directory |
| `/e` | Copy all subdirectories including empty |
| `/h` | Copy hidden and system files |
| `D:\review.dat` | Source — a drive (likely USB or mounted image) |
| `C:\Users\EVAN~1.HUT\AppData\Local\Temp\` | Destination — user temp folder |

> **Analyst note:** The source path `D:\` indicates the payload arrived on removable media or a mounted drive — not just downloaded from the internet. This suggests either physical access or a virtual drive mount as part of the delivery chain.

### Step 2 — DLL Execution via rundll32

The copied `.dat` file is actually a **DLL** (disguised with a `.dat` extension to evade detection). The stage 1 HTA script then executes it using `rundll32.exe`:

```cmd
"C:\Windows\System32\rundll32.exe" D:\review.dat,DllRegisterServer
```

- `rundll32.exe` is a LOLBin used to execute exported functions from DLL files
- `DllRegisterServer` is a standard COM registration export — abused here to trigger malicious code
- The file is executed from the original `D:\` path, not the copied location

> This is **DLL side-loading / masquerading** (T1574.002 + T1036). Using a `.dat` extension hides the true nature of the file from casual inspection and many endpoint tools that filter by extension.

### Step 3 — Persistence via Scheduled Task

Immediately after execution, the stage 1 payload creates a scheduled task to survive reboots:

```cmd
schtasks /Create /TN "Review" /TR "rundll32.exe D:\review.dat,DllRegisterServer" /SC ONLOGON
```

- Task name: **`Review`** — innocuous-sounding, mimics a legitimate review process
- Trigger: `ONLOGON` — runs every time any user logs in
- Action: Re-executes the DLL payload via `rundll32.exe`

### Step 4 — C2 Connection

Following the log for the `rundll32.exe` execution and viewing surrounding documents reveals an outbound network connection established by the DLL:

```
C2 IP:    165.232.170.151
Port:     80
Protocol: HTTP
Process:  rundll32.exe
```

Port 80 (plain HTTP) is used deliberately — it blends in with normal web traffic and is rarely blocked outright.

### MITRE ATT&CK Mapping — Stage 1

| Technique | ID | Description |
|---|---|---|
| Phishing: Spearphishing Attachment | T1566.001 | HTA disguised as PDF document |
| Mshta | T1218.005 | HTA execution via mshta.exe |
| Masquerading | T1036 | DLL disguised as `.dat` file |
| Rundll32 | T1218.011 | DLL execution via rundll32 LOLBin |
| Scheduled Task | T1053.005 | `Review` task for ONLOGON persistence |
| Command and Control: HTTP | T1071.001 | C2 over port 80 |

---

## 🔐 Task 4 — Privilege Escalation: UAC Bypass

### Discovery of Admin Access

The attacker's implant determined the current user (`evan.hutchins`) is a **local administrator** — but with **UAC (User Account Control)** restricting full elevated privileges. To escalate to a high-integrity process, the attacker used a UAC bypass.

### fodhelper.exe UAC Bypass (T1548.002)

`fodhelper.exe` is a legitimate Windows binary (`C:\Windows\System32\fodhelper.exe`) that:
- Is marked as **auto-elevate** in its manifest
- Checks a specific registry key before launching
- Does NOT prompt the user with a UAC dialog

The bypass works by writing a malicious command into the registry key that `fodhelper.exe` reads, then launching `fodhelper.exe` — which auto-elevates and executes the attacker's command with high integrity:

```
Registry key written:
HKCU\Software\Classes\ms-settings\shell\open\command

Value: <attacker's command>

fodhelper.exe launched → reads key → executes command at HIGH integrity
(no UAC prompt shown to user)
```

Evidence in Elastic: searching for `fodhelper.exe` in the logs shows it modifying the registry — a known behavioral indicator of this specific bypass technique.

> **Why this matters:** UAC bypass converts a medium-integrity process (standard user session) into a high-integrity one (administrator) without triggering any visible security prompt. The user sees nothing.

---

## 🔑 Task 5 — Credential Dumping with Mimikatz

### Downloading Mimikatz

With elevated privileges, the attacker downloaded Mimikatz directly from the official GitHub repository:

```
URL: github.com/gentilkiwi/mimikatz/releases/download/2.2.0-20220919/mimikatz_trunk.zip
```

> Downloading from the **official** GitHub repo (rather than a private server) is a deliberate choice — it reduces suspicion from URL reputation tools, since `github.com` is trusted. This is a common technique seen in real-world campaigns.

KQL query to find this:
```kql
*download* AND *github*
```

### Credentials Dumped — Machine 1 (WKSTN-2961)

Searching for Mimikatz execution in the logs reveals the credential dumped from the first workstation:

```
Username: itadmin
NTLM Hash: F84769D250EB95EB2D7D8B4A1C5613F2
```

> **NTLM hashes** can be used directly for **Pass-the-Hash** attacks — the attacker doesn't need to crack the password, just present the hash to authenticate to other systems. This is what enables lateral movement.

---

## 🌐 Task 6 — Lateral Movement

### File Share Enumeration with PowerView

The attacker also downloaded **PowerView** (a PowerShell reconnaissance framework from PowerSploit) to enumerate network shares accessible with the stolen `itadmin` credentials:

```
File accessed from remote share: IT_Automation.ps1
```

This PowerShell script contained **plaintext credentials** — a common finding in IT automation scripts that are left poorly secured on file shares:

```
Credentials found inside IT_Automation.ps1:
Username: QUICKLOGISTICS\allan.smith
Password: Tr!ckyP@ssw0rd987
```

> **This is Credentials in Files (T1552.001).** Automation scripts, config files, and batch files frequently contain hardcoded credentials. Attackers specifically target accessible file shares for this reason.

### Moving to the Second Machine

With `allan.smith`'s credentials, the attacker moved laterally to:

```
Target hostname: WKSTN-1327
Method: PowerShell Remoting (WinRM)
```

KQL query for the second machine:
```kql
host.hostname: "WKSTN-1327" AND event.code: 1
```

**Parent process on the second machine:** `wsmprovhost.exe`

> `wsmprovhost.exe` is the **Windows Remote Management** provider host — it's the process that spawns commands executed via PowerShell Remoting (`Enter-PSSession`, `Invoke-Command`). Seeing it as a parent process for malicious commands is a strong indicator of lateral movement via WinRM.

### Credential Dump — Machine 2 (WKSTN-1327)

Mimikatz was re-executed on the second machine, dumping another set of credentials:

```
Username: administrator
NTLM Hash: 00f80f2538dcb54e7adc715c0e7091ec
```

With a local administrator hash, the attacker now had the keys to reach the Domain Controller.

### MITRE ATT&CK Mapping — Lateral Movement

| Technique | ID | Description |
|---|---|---|
| UAC Bypass: Fodhelper | T1548.002 | Registry manipulation + auto-elevate binary |
| OS Credential Dumping | T1003.001 | Mimikatz LSASS credential extraction |
| Pass the Hash | T1550.002 | Using NTLM hash without cracking |
| Credentials in Files | T1552.001 | Plaintext creds in IT_Automation.ps1 |
| Remote Services: WinRM | T1021.006 | Lateral movement via PowerShell Remoting |
| Ingress Tool Transfer | T1105 | Downloading Mimikatz and PowerView |

---

## 👑 Task 7 — Domain Compromise: DCSync Attack

### Reaching the Domain Controller

Using the `administrator` NTLM hash from WKSTN-1327, the attacker pivoted to the **Domain Controller** — the most critical asset in any Active Directory environment.

### DCSync Attack (T1003.006)

A **DCSync attack** abuses the legitimate **Directory Replication Service (DRS)** protocol. Instead of running code on the DC itself, the attacker's tool impersonates another Domain Controller and requests credential replication — extracting password hashes for any account in the domain.

```
Tool used: Mimikatz (lsadump::dcsync)
Accounts targeted:
  - administrator
  - backupda        ← secondary account dumped
```

> **Why DCSync is devastating:** It extracts hashes for **every account** in the domain — including the `krbtgt` account, which enables **Golden Ticket** attacks, and service accounts with domain-wide access. A successful DCSync means total domain compromise.

The `backupda` account is particularly interesting — backup/service accounts often have elevated privileges across multiple systems and are frequently overlooked in password rotation policies.

### Ransomware Staging

With full domain access established, the attacker's final step was downloading ransomware to the Domain Controller:

```
Download URL: http://ff.sillytechninja.io/ransomboogey.exe
```

KQL query used to find this:
```kql
host.hostname: "DC" AND *ransom*
```

> Deploying ransomware **from the Domain Controller** is the endgame of many financially-motivated threat actors. From the DC, Group Policy can push executables to every machine in the domain simultaneously — enabling a network-wide ransomware deployment in minutes.

### MITRE ATT&CK Mapping — Domain Compromise

| Technique | ID | Description |
|---|---|---|
| DCSync | T1003.006 | Domain credential replication via DRS protocol |
| Golden Ticket (potential) | T1558.001 | krbtgt hash enables forged Kerberos tickets |
| Data Encrypted for Impact | T1486 | Ransomware deployment targeting the domain |
| Ingress Tool Transfer | T1105 | Ransomware binary downloaded to DC |

---

## 🔄 Full Attack Chain Reconstruction

```
[INITIAL ACCESS]
  Phishing email → HTA file disguised as PDF (mshta.exe, PID: 6392)
  T1566.001 + T1218.005

       ↓
[EXECUTION — STAGE 1]
  xcopy.exe copies review.dat (DLL) from D:\ to Temp\
  rundll32.exe executes review.dat,DllRegisterServer
  T1218.011 + T1036

       ↓
[PERSISTENCE]
  Scheduled Task "Review" created → ONLOGON trigger
  T1053.005

       ↓
[C2 ESTABLISHED]
  rundll32.exe → outbound HTTP → 165.232.170.151:80
  T1071.001

       ↓
[PRIVILEGE ESCALATION]
  fodhelper.exe UAC bypass → high-integrity shell
  T1548.002

       ↓
[CREDENTIAL ACCESS — MACHINE 1]
  Mimikatz downloaded from GitHub
  LSASS dumped → itadmin:F84769D250EB95EB2D7D8B4A1C5613F2
  T1003.001 + T1105

       ↓
[DISCOVERY]
  PowerView enumerates file shares
  IT_Automation.ps1 accessed → QUICKLOGISTICS\allan.smith:Tr!ckyP@ssw0rd987
  T1021.002 + T1552.001

       ↓
[LATERAL MOVEMENT → WKSTN-1327]
  WinRM with allan.smith credentials
  Parent: wsmprovhost.exe
  T1021.006

       ↓
[CREDENTIAL ACCESS — MACHINE 2]
  Mimikatz re-run → administrator:00f80f2538dcb54e7adc715c0e7091ec
  T1003.001

       ↓
[DOMAIN COMPROMISE — DC]
  DCSync attack → dumps administrator + backupda hashes
  T1003.006

       ↓
[IMPACT — RANSOMWARE]
  ransomboogey.exe downloaded to DC
  http://ff.sillytechninja.io/ransomboogey.exe
  T1486
```

---

## 🚨 Indicators of Compromise (IoCs)

### Network-Based

| IoC | Type | Description |
|---|---|---|
| `165.232.170.151` | IP | Stage 1 C2 server |
| Port `80` | Port | C2 communication (plain HTTP) |
| `ff.sillytechninja.io` | Domain | Ransomware delivery server |
| `github.com/gentilkiwi/mimikatz/...` | URL | Mimikatz download source |

### Host-Based

| IoC | Type | Description |
|---|---|---|
| `review.dat` | File | Malicious DLL (disguised as data file) |
| `C:\Users\EVAN~1.HUT\AppData\Local\Temp\review.dat` | Path | Dropped DLL location |
| `ransomboogey.exe` | File | Ransomware binary |
| Scheduled Task: `Review` | Task | ONLOGON persistence mechanism |
| `HKCU\Software\Classes\ms-settings\shell\open\command` | Registry | fodhelper UAC bypass key |

### Behavioral

- `mshta.exe` executing user-downloaded files
- `rundll32.exe` loading `.dat` files with `DllRegisterServer` export
- `fodhelper.exe` modifying `ms-settings` registry key
- Mimikatz process execution (any path)
- `wsmprovhost.exe` spawning cmd/powershell on non-DC machines
- Domain Controller initiating outbound HTTP downloads

---

## 🛡️ Detection Opportunities

```kql
// HTA execution (mshta.exe launching user content)
event.code: 1 AND process.name: "mshta.exe" AND
process.command_line: *AppData* OR process.command_line: *Temp*

// Rundll32 executing .dat files (DLL masquerading)
event.code: 1 AND process.name: "rundll32.exe" AND
process.command_line: *.dat*

// fodhelper UAC bypass — registry key write
event.code: 13 AND
registry.path: *ms-settings\\shell\\open\\command*

// Mimikatz execution (by name or common arguments)
event.code: 1 AND (
  process.name: "mimikatz.exe" OR
  process.command_line: *sekurlsa* OR
  process.command_line: *lsadump*
)

// WinRM lateral movement (wsmprovhost spawning shells)
event.code: 1 AND
process.parent.name: "wsmprovhost.exe" AND
process.name: ("powershell.exe" OR "cmd.exe")

// DCSync detection (requires AD audit logs)
event.code: 4662 AND
object.properties: (*1131f6aa* OR *1131f6ad* OR *89e95b76*)
// These GUIDs = DS-Replication-Get-Changes permissions

// Ransomware download from DC
host.hostname: "DC" AND
event.code: 3 AND
network.direction: "egress" AND
destination.port: 80
```

---

## 🛠️ Tools Used in This Investigation

| Tool | Purpose |
|---|---|
| **Elastic SIEM** | Full investigation platform — log ingestion, KQL querying, timeline |
| **Kibana** | Elastic's UI — Discover tab for log search and pivoting |
| **Sysmon (via logs)** | Endpoint telemetry source (Event IDs 1, 3, 11, 13) |
| **KQL** | Kibana Query Language for filtering and correlating events |
| **Mimikatz** *(attacker tool, analyzed)* | Credential dumping — LSASS + DCSync |
| **PowerView** *(attacker tool, analyzed)* | AD enumeration — share discovery |

---

## 🧪 Key Concepts Practiced

- SIEM-based investigation workflow using Elastic/Kibana
- KQL query construction and log pivoting techniques
- HTA-based initial access and DLL execution via rundll32
- UAC bypass detection and understanding `fodhelper.exe` abuse
- Credential dumping via Mimikatz (LSASS + DCSync)
- Pass-the-Hash lateral movement across Active Directory
- Recognizing `wsmprovhost.exe` as an indicator of WinRM-based movement
- DCSync attack mechanics and domain-wide credential exposure
- Ransomware staging and final-stage attacker objectives

---

## 🧠 Key Takeaways

1. **HTA files are a significant blind spot.** Most users associate `.exe` and `.js` with danger — but `.hta` files are equally capable of executing arbitrary code and are far less scrutinized. Email gateways should block or sandbox `.hta` attachments.

2. **UAC is not a security boundary.** Microsoft explicitly states that UAC is a convenience feature, not a security control. The `fodhelper.exe` bypass has been publicly known for years and remains effective. Privileged users should operate with the minimum necessary rights — ideally separated accounts for admin tasks.

3. **Automation scripts are a credential treasure chest.** `IT_Automation.ps1` containing plaintext credentials on a network share is an extremely common finding in real engagements. Any script with embedded credentials should be replaced with a secrets management solution (e.g., Azure Key Vault, HashiCorp Vault, CyberArk).

4. **`wsmprovhost.exe` is a lateral movement fingerprint.** Legitimate use of PowerShell Remoting exists in most environments, but `wsmprovhost.exe` spawning shells on endpoints (not servers) is a high-fidelity indicator of compromise worth alerting on.

5. **DCSync is silent on the network.** The attack uses a legitimate protocol (DRS) and blends in with normal AD replication traffic. Detection requires auditing `Event ID 4662` with specific replication GUIDs — not available by default; requires explicit AD auditing configuration.

6. **The Domain Controller is always the final target.** Every step of this attack — from the HTA lure to UAC bypass to lateral movement — was working toward DC access. Once the DC is compromised, the entire domain is compromised. Protecting the DC (tiered access model, Privileged Access Workstations) is the most impactful defensive investment in an AD environment.

7. **SIEM pivoting speed matters.** In Elastic, the `surrounding documents` feature (viewing logs ±N minutes around a specific event) is one of the fastest ways to follow an attacker's trail. Master your SIEM's pivot capabilities — they're the difference between a 2-hour investigation and an 8-hour one.

---

## 📊 The Boogeyman Trilogy — Full Comparison

| Aspect | Boogeyman 1 | Boogeyman 2 | Boogeyman 3 |
|---|---|---|---|
| **Target** | Finance (Julianne) | HR (Maxine) | Unknown employee (Evan) |
| **Lure** | Fake invoice (BEC) | Fake resume | Fake PDF review |
| **Attachment type** | LNK inside ZIP | Macro-enabled .doc | HTA disguised as PDF |
| **Stage 1 executor** | PowerShell (download cradle) | wscript.exe (JS) | mshta.exe (HTA) |
| **Payload type** | PS1 (fileless) | JS → EXE | DLL (.dat) via rundll32 |
| **Persistence** | Schtasks + registry fileless | Schtasks + registry fileless | Schtasks (ONLOGON) |
| **Privilege escalation** | None observed | None observed | fodhelper UAC bypass |
| **Credential access** | Sticky Notes + KeePass | — | Mimikatz (LSASS + DCSync) |
| **Lateral movement** | None | None | WinRM (Pass-the-Hash) |
| **Final impact** | Data exfiltration (DNS) | C2 foothold | Domain compromise + ransomware |
| **Primary investigation tool** | jq + Wireshark | Volatility 3 | Elastic SIEM |
| **Scope** | Single host | Single host | Multi-host + Domain |

---

## 📌 Final Thoughts

Boogeyman 3 is the most complete simulation of a real APT-style intrusion in the trilogy — and a fitting capstone for the SOC Level 1 path. The attack chain mirrors documented campaigns from financially-motivated groups like **Conti**, **BlackCat/ALPHV**, and **Hive**, all of which follow a similar playbook: initial access → privilege escalation → credential theft → lateral movement → domain compromise → ransomware deployment.

What sets this room apart is the pivot from single-artifact analysis (one log file, one PCAP) to **chasing an attacker across a live SIEM** — which is exactly what Tier 2/3 SOC analysts and IR responders do in real incidents. The ability to construct targeted KQL queries, follow surrounding events, and connect activity across machines is a skill that directly transfers to defensive roles.

Completing the full Boogeyman trilogy provides hands-on experience with:
- Email forensics → Endpoint forensics → Memory forensics → SIEM investigation
- Single-host compromise → Domain-wide compromise
- Static artifact analysis → Live threat hunting

That's a complete picture of the modern SOC analyst's toolkit.

