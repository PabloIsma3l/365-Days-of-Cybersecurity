# 📅  · Day 26

## 🔓 PART1 - John the Ripper: The Basics (TryHackMe)

Room: **John the Ripper: The Basics**
Scope today: **Tasks 1 → 7**
Objective: Learn how to use **John the Ripper** to crack different types of password hashes and understand its core attack modes.

---

## 🎯 Day Objectives

* Understand what **John the Ripper (JtR)** is and when it is used
* Learn essential terminology related to password cracking
* Set up the environment for using John
* Crack basic hashes
* Crack Windows authentication hashes
* Crack Linux `/etc/shadow` hashes
* Understand and use **Single Crack Mode**

---

## 🧠 Task 1 – Introduction

John the Ripper is a **password cracking tool** used to identify weak passwords by performing offline attacks against password hashes.

Key points:

* Open-source and widely used
* Supports many hash formats
* Commonly used in **pentesting**, **red team**, and **forensics**

---

## 📘 Task 2 – Basic Terms

Important terminology:

* **Hash**: Fixed-length representation of data
* **Plaintext**: Original password before hashing
* **Wordlist**: File containing candidate passwords
* **Cracking**: Attempting to recover plaintext passwords from hashes
* **Brute force**: Trying all possible combinations
* **Dictionary attack**: Using wordlists to guess passwords

---

## 🛠️ Task 3 – Setting Up Your System

Check John installation:

```
john --help
```

Check supported hash formats:

```
john --list=formats
```

John usually works with:

* `/usr/share/wordlists/`
* Common wordlists like `rockyou.txt`

---

## 🔐 Task 4 – Cracking Basic Hashes

Prepare a file with hashes:

```
cat hashes.txt
```

Run John with a wordlist:

```
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
```

Show cracked passwords:

```
john --show hashes.txt
```

This demonstrates basic dictionary-based cracking.

---

## 🪟 Task 5 – Cracking Windows Authentication Hashes

Windows commonly uses **NTLM** hashes.

Example command:

```
john --format=nt hashes.txt
```

Key notes:

* NTLM is fast and vulnerable to cracking
* Weak passwords are cracked quickly

---

## 🐧 Task 6 – Cracking `/etc/shadow` Hashes

Linux password hashes are stored in `/etc/shadow`.

Steps:

Combine `/etc/passwd` and `/etc/shadow`:

```
unshadow passwd.txt shadow.txt > unshadowed.txt
```

Run John:

```
john unshadowed.txt
```

Show results:

```
john --show unshadowed.txt
```

---

## 🎯 Task 7 – Single Crack Mode

Single Crack Mode uses **username-based rules** and information to generate password guesses.

Example:

```
john --single hashes.txt
```

Characteristics:

* Very fast
* Effective against poor password hygiene
* Uses usernames, GECOS fields, and rules

---

## 🧪 What I Learned Today

* John the Ripper is a core tool for password auditing
* Many systems still rely on weak hashing and passwords
* Dictionary and single crack modes are highly effective
* Offline cracking avoids account lockouts

---

## 📝 Personal Notes

* John pairs well with Hashcat for different scenarios
* Understanding hash formats is critical
* Very relevant for:

  * Internal pentests
  * Active Directory attacks
  * Linux privilege escalation

---

