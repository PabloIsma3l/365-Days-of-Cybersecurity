# 🔍 Committed — TryHackMe Writeup

**📅 Day 138 — 365 Days of Cybersecurity**
**✅ Status: Completed**
**🏷️ Tags:** `Git Forensics` `Secret Detection` `DFIR` `Source Code Security` `Credential Exposure` `DevSecOps`
**⚙️ Difficulty:** Easy

---

## 🧠 Overview

A developer accidentally committed sensitive credentials into a Git repository — then tried to cover their tracks by deleting the file in a follow-up commit. In this room, I investigated the repository's full commit history to recover the exposed secret.

This room teaches one of the most critical and underappreciated lessons in application security: **Git never truly forgets.** Even after a file is deleted or a commit is amended, the data persists in the repository's object store and can be fully recovered by anyone with access to the `.git` directory.

> **Core principle:** A secret pushed to a Git repository — even for one second, even if immediately deleted — must be considered permanently compromised. Rotation is the only remediation.

---

## 🎯 Learning Objectives

- Understand the structure of a Git repository and its commit history
- Use `git log` to enumerate all commits across all branches
- Use `git show` and `git diff` to inspect commit contents
- Recover data that was "deleted" from a repository but persists in Git history
- Understand why secret deletion from Git history requires specialized tools, not just `git rm`

---

## 🗂️ Environment

| Detail | Value |
|---|---|
| Artifact | `commited.zip` — a Git repository archive |
| Location | `/home/ubuntu/commited/` |
| Objective | Recover a credential/flag committed and then "deleted" |

---

## 🔧 Step 1 — Extracting the Repository

```bash
cd /home/ubuntu/commited
unzip commited.zip
cd commited/
```

Verify this is a valid Git repository:

```bash
ls -la
# Should show a .git/ directory
```

The `.git/` directory is the entire history of the repository — every commit, every version of every file, every branch. Everything needed for the investigation lives here.

---

## 🔍 Step 2 — Mapping the Full Commit History

The first step in any Git forensic investigation is getting a complete map of all commits across all branches.

```bash
git log --oneline --graph --all
```

### Breaking Down the Flags

| Flag | Purpose |
|---|---|
| `--oneline` | Compact view — one commit per line (hash + message) |
| `--graph` | ASCII branch graph showing merge topology |
| `--all` | **Critical** — includes ALL branches and refs, not just the current branch |

> **Why `--all` matters:** Without `--all`, `git log` only shows the history of your current branch. Secrets hidden in other branches, orphaned commits, or stash refs would be invisible. Always use `--all` in forensic investigations.

### Example Output

```
* a1b2c3d (HEAD -> main) Removed sensitive file
* e4f5g6h Oops
* i7j8k9l Initial commit
```

The commit message **"Oops"** is an immediate red flag — it's a classic indicator that a developer realized they committed something they shouldn't have and quickly tried to undo it. In Git, though, "undoing" a commit by adding another commit doesn't erase anything — it only adds a new state on top of the old one.

---

## 🔍 Step 3 — Inspecting the Suspicious Commit

```bash
git show e4f5g6h
```

`git show` displays the full diff of a commit — what was added (`+` lines in green) and what was removed (`-` lines in red).

### Example Output

```diff
commit e4f5g6h
Author: dev <dev@company.com>
Date:   Mon Jan 10 14:23:01 2023

    Oops

diff --git a/dbconn.py b/dbconn.py
index a3f1b2c..d4e5f6g 100644
--- a/dbconn.py
+++ b/dbconn.py
@@ -1,5 +1,5 @@
 import sqlite3
-DB_USER = "admin"
-DB_PASS = "s3cr3tpassword!"
-DB_FLAG = "flag{a489a9dbf8eb9d37c6e0cc1a92cda17b}"
+DB_USER = ""
+DB_PASS = ""
+DB_FLAG = ""
```

The `-` lines show what existed in that commit — the credentials and the flag that the developer tried to remove in the next commit. They're perfectly preserved in the repository history.

---

## 🔍 Additional Git Forensic Commands

These commands go beyond what the room requires but are essential for real-world investigations:

### Search All Commits for a Keyword

```bash
# Search commit diffs for a specific string
git log --all -S "password" --oneline

# More powerful: regex search across all history
git log --all --oneline -G "pass(word)?|secret|key|token|credential"
```

> `-S` (pickaxe search) finds commits where the *number of occurrences* of the string changed — ideal for finding where a secret was added or removed.

### Inspect a Specific File Across All Its Versions

```bash
# See all commits that touched a specific file
git log --all --oneline -- dbconn.py

# See every version of a file across history
git log --all -p -- dbconn.py
```

### Recover a Deleted File from a Specific Commit

```bash
# Restore a file as it existed in a specific commit
git checkout e4f5g6h -- dbconn.py

# Or view its content without modifying working tree
git show e4f5g6h:dbconn.py
```

### Search Git Stash

```bash
# List stashed work (developers sometimes stash secrets accidentally)
git stash list

# Show content of each stash
git stash show -p stash@{0}
```

### Inspect Orphaned/Dangling Commits

```bash
# Find commits not reachable from any branch (after git reset --hard)
git fsck --lost-found --unreachable

# View a dangling commit
git show <dangling_commit_hash>
```

> **Dangling commits** are created when a developer uses `git reset --hard` or force-pushes to "erase" a commit. The commit object still exists in `.git/objects/` until garbage collection runs — and forensically, it's fully recoverable.

---

## 🧠 How Git Stores Data — The Forensic Explanation

Understanding *why* deleted data persists in Git requires understanding its storage model:

```
.git/
├── objects/          ← Every version of every file, ever. Never auto-deleted.
│   ├── commits       ← Commit objects (metadata + tree pointer)
│   ├── trees         ← Directory snapshots
│   └── blobs         ← File content (one per unique file version)
├── refs/             ← Branch and tag pointers (just commit hashes)
├── logs/             ← Reflog — history of where HEAD has pointed
└── COMMIT_EDITMSG    ← Last commit message
```

When a developer does:
```bash
git rm secrets.txt
git commit -m "Removed sensitive file"
```

What actually happens:
1. A **new commit** is created with `secrets.txt` absent from the tree
2. The **blob object** containing `secrets.txt`'s content still exists in `.git/objects/`
3. The **previous commit object** still exists and still points to the blob
4. Nothing is deleted — only the branch pointer moved forward

The only way to truly remove data from a Git repository is with history rewriting tools like `git filter-branch`, `git filter-repo`, or BFG Repo Cleaner — **followed by a force push to all remotes and notification to all cloners**.

---

## 🚨 Real-World Impact — Why This Matters

This scenario represents one of the most common security incidents in software development. High-profile examples include:

- Developers accidentally committing AWS access keys, database passwords, and API tokens to public GitHub repositories
- Automated scanners (like **truffleHog**, **GitLeaks**, **GitHub Secret Scanning**) that continuously monitor public repos for credential patterns
- Attackers who specifically target GitHub/GitLab for exposed credentials using tools that scan commit history, not just the current code state

### The "I deleted it" misconception

```
Developer commits secret → Developer deletes secret → Developer thinks it's safe
                                                              ↓
                                                   IT IS NOT SAFE.
                                                   Anyone who cloned before deletion has it.
                                                   The full git history preserves it.
                                                   GitHub keeps it cached.
                                                   CI/CD logs may have printed it.
```

---

## 🛡️ Prevention — Stopping Secrets from Entering Git History

### Pre-commit Hooks (First Line of Defense)

```bash
# Install pre-commit framework
pip install pre-commit

# .pre-commit-config.yaml
repos:
  - repo: https://github.com/gitleaks/gitleaks
    rev: v8.16.1
    hooks:
      - id: gitleaks
```

This blocks any commit containing detected secrets **before** they enter the repository.

### Secret Detection Tools

| Tool | Use Case |
|---|---|
| **GitLeaks** | Pre-commit hook + CI/CD scanning of full history |
| **truffleHog** | Deep entropy + regex scanning of git history |
| **GitHub Secret Scanning** | Automatic scanning of public/private GitHub repos |
| **detect-secrets** | Yelp's tool — baseline + diff scanning |
| **git-secrets** | AWS-focused, blocks AWS credential patterns |

### Scanning an Existing Repository for Secrets

```bash
# GitLeaks — scan full history
gitleaks detect --source . --verbose

# truffleHog — entropy + regex scan
trufflehog git file://. --since-commit HEAD~50

# Search manually for common patterns
git log --all -p | grep -E \
  "(password|passwd|secret|api_key|access_key|token|credential)\s*=\s*['\"][^'\"]{8,}"
```

### Using `.gitignore` Correctly

```gitignore
# .gitignore — keep these files out of git entirely
.env
.env.local
*.pem
*.key
config/secrets.yml
credentials.json
```

> **Important:** `.gitignore` only prevents *future* accidental commits. If a file was already committed, `.gitignore` won't remove it from history.

### Environment Variables Instead of Hardcoded Secrets

```python
# BAD — what the developer in this room did
DB_PASS = "s3cr3tpassword!"

# GOOD — read from environment at runtime
import os
DB_PASS = os.environ.get("DB_PASS")
```

Secrets should live in:
- Environment variables (local dev)
- `.env` files (never committed, listed in `.gitignore`)
- Secrets managers (AWS Secrets Manager, HashiCorp Vault, Azure Key Vault)
- CI/CD secret stores (GitHub Actions Secrets, GitLab CI Variables)

---

## 🔄 Remediation — If a Secret Was Already Committed

```
Step 1: ROTATE THE SECRET IMMEDIATELY
         Assume it's compromised. Change the password/key/token NOW.
         Don't wait for history cleanup.

Step 2: Remove from history using git filter-repo
         pip install git-filter-repo
         git filter-repo --path secrets.txt --invert-paths

Step 3: Force push to all remotes
         git push origin --force --all
         git push origin --force --tags

Step 4: Notify all collaborators
         Everyone who cloned must re-clone — their local copy still has the secret.

Step 5: Check CI/CD logs
         Pipeline logs may have printed the secret. Purge them too.

Step 6: Check for unauthorized use
         Review access logs for the compromised credential.
         AWS CloudTrail, GCP Audit Logs, etc.
```

---

## 🛠️ Git Forensics Command Reference

```bash
# Full history map — all branches
git log --oneline --graph --all

# Inspect a specific commit (full diff)
git show <commit_hash>

# Search history for a string (pickaxe)
git log --all -S "keyword" --oneline

# Search history with regex
git log --all -G "regex_pattern" --oneline

# Show all versions of a file
git log --all -p -- filename.py

# Restore a file from a specific commit
git show <hash>:filename.py > recovered_file.py

# Find dangling (orphaned) commits
git fsck --lost-found --unreachable

# Check stash for hidden content
git stash list && git stash show -p

# Show full diff between two commits
git diff <hash1> <hash2>

# Show what changed in a specific file between commits
git diff <hash1> <hash2> -- filename.py
```

---

## 🧪 Key Concepts Practiced

- Git repository structure and the `.git/` object store
- Full commit history enumeration with `git log --all`
- Commit diff inspection with `git show`
- Understanding why Git "deletion" doesn't erase data
- Identifying suspicious commits by message patterns ("Oops", "fix", "remove")
- Applying Git forensics in a DFIR/security investigation context

---

## 🧠 Key Takeaways

1. **`git log --all` is the foundation of Git forensics.** Without `--all`, you only see the current branch. Secrets hidden in other branches, stashes, or orphaned commits are invisible without it.

2. **"I deleted it from Git" means nothing without history rewriting.** A `git rm` followed by a commit creates a new state — it doesn't alter the old one. The original data remains in `.git/objects/` indefinitely until explicit history rewriting + garbage collection.

3. **Suspicious commit messages are forensic signals.** "Oops", "remove key", "fix credentials", "accidentally pushed" — these are flags that a developer noticed and tried to undo a sensitive commit. Always inspect what changed in these commits.

4. **The blast radius of an exposed secret extends beyond the repository.** CI/CD pipelines may have logged it, collaborators may have cloned it, and automated scanners may have already found it. Rotation is the only safe response.

5. **Pre-commit hooks are the most effective prevention.** Catching secrets before they enter the repository costs nothing (a fraction of a second per commit). Remediation after the fact costs hours of work and potential security incidents.

6. **`.gitignore` is not a security control.** It prevents future accidental commits of matched files — it does nothing for files already in history, and it won't prevent a developer from force-adding an ignored file.

7. **This is a DevSecOps skill, not just a CTF skill.** Secret scanning, Git history forensics, and pre-commit hooks are standard expectations in security engineering and AppSec roles. The workflow practiced in this room maps directly to real incident response for credential exposure events.

---

## 📌 Final Thoughts

Committed is a compact room with an outsized real-world lesson. Credential exposure via Git history is consistently one of the top findings in bug bounty programs and red team engagements — and one of the most preventable. Tools like GitLeaks and GitHub's native secret scanning exist precisely because this mistake is made constantly, even by experienced developers.

The investigation technique is also transferable: the same `git log --all -S` approach used here is how security researchers have discovered exposed AWS keys, database passwords, and private API tokens in public repositories — sometimes years after the original commit.

The takeaway isn't just "be careful what you commit" — it's that the **entire Git history of a repository is an attack surface**, and it deserves the same security scrutiny as the running application itself.

