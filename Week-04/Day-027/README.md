# 📅 · Day 26

## 🔓 John the Ripper: The Basics (TryHackMe)

### Part 2 — Tasks 8 → 12

Room: **John the Ripper: The Basics**
Scope today: **Advanced usage and attack modes**
Objective: Deepen practical knowledge of John the Ripper by using advanced cracking modes, rules, and workflow techniques.

---

## 🎯 Day Objectives (Part 2)

* Understand **incremental (brute-force) mode**
* Use **custom wordlists and rules** effectively
* Learn how **pot files** work
* Improve cracking efficiency and strategy
* Build a real pentesting-oriented cracking workflow

---

## ⚙️ Task 8 – Incremental (Brute-Force) Mode

Incremental mode attempts **all possible character combinations** based on a defined charset.

Example:

```
john --incremental hashes.txt
```

Custom incremental mode:

```
john --incremental=Digits hashes.txt
```

Key notes:

* Very powerful but time-consuming
* Useful for short or simple passwords
* Last resort when wordlists fail

---

## 📚 Task 9 – Wordlists and Rules

John can modify words dynamically using **rules**.

Example using rules with a wordlist:

```
john --wordlist=rockyou.txt --rules hashes.txt
```

Common rule transformations:

* Capitalization
* Appending numbers or symbols
* Leetspeak substitutions

Rules massively increase cracking success without full brute-force.

---

## 🧠 Task 10 – The Pot File (`john.pot`)

The pot file stores **already cracked hashes**.

Location example:

```
~/.john/john.pot
```

Useful commands:

Show previously cracked passwords:

```
john --show hashes.txt
```

Clear pot file (use with caution):

```
rm ~/.john/john.pot
```

Why this matters:

* Avoids re-cracking
* Saves time during engagements

---

## 🧪 Task 11 – Cracking Strategy & Performance

Effective cracking strategy includes:

* Identifying hash types correctly
* Starting with **single mode**
* Moving to **wordlists + rules**
* Using **incremental mode** as fallback

Performance tips:

* Use smaller, targeted wordlists first
* Combine with user/context information
* Parallelize attacks when possible

---

## 🧩 Task 12 – Real-World Pentesting Workflow

Example cracking workflow:

1. Identify hash format
2. Run single crack mode
3. Run wordlist + rules
4. Try incremental if needed
5. Review cracked credentials

This mirrors real **internal pentest and audit** scenarios.

---

## 🧪 What I Learned Today

* John supports multiple attack strategies
* Rules are more efficient than pure brute force
* Incremental mode is powerful but costly
* Pot files are critical for workflow efficiency

---

## 📝 Personal Notes

* John excels in structured cracking scenarios
* Hashcat may be faster, but John is extremely flexible
* Understanding strategy matters more than raw speed

---

