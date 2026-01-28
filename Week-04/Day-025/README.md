# 📅Day 25

## 🔐 Hashing Basics (TryHackMe)

Room: **Hashing Basics**
Objective: Learn how hashing functions work and how they are used for **password verification** and **file integrity checking**.

---

## 🎯 Day Objectives

* Understand what a **hash function** is
* Learn the main properties of cryptographic hash functions
* Understand the difference between **hashing** and **encryption**
* Explore common hashing algorithms
* Learn real-world use cases such as password storage and file integrity verification

---

## 🔑 What Is Hashing?

Hashing is a **one-way mathematical function** that takes input data of any size and produces a fixed-length output called a **hash** or **digest**.

Key characteristics:

* Deterministic (same input → same output)
* One-way (cannot be reversed)
* Fast to compute
* Small changes in input produce completely different hashes

---

## 🔄 Hashing vs Encryption

| Feature      | Hashing                  | Encryption      |
| ------------ | ------------------------ | --------------- |
| Reversible   | ❌ No                     | ✅ Yes           |
| Key required | ❌ No                     | ✅ Yes           |
| Purpose      | Integrity / verification | Confidentiality |

Hashing is used for **verification**, not for hiding data.

---

## 🧠 Properties of Cryptographic Hash Functions

A secure cryptographic hash function should provide:

* **Pre-image resistance**: cannot recover the original input from the hash
* **Second pre-image resistance**: difficult to find another input with the same hash
* **Collision resistance**: hard to find two different inputs with the same hash

---

## 🔢 Common Hashing Algorithms

| Algorithm | Status   | Notes                         |
| --------- | -------- | ----------------------------- |
| MD5       | ❌ Broken | Vulnerable to collisions      |
| SHA-1     | ❌ Broken | Deprecated                    |
| SHA-256   | ✅ Secure | Widely used                   |
| SHA-512   | ✅ Secure | Stronger variant              |
| bcrypt    | ✅ Secure | Designed for password hashing |
| scrypt    | ✅ Secure | Memory-hard                   |

---

## 🔐 Password Hashing

Passwords should **never be stored in plain text**.

Secure password storage includes:

* Hashing the password
* Adding a **salt**
* Using slow hashing algorithms

Example workflow:

1. User enters password
2. Password is salted and hashed
3. Hash is stored in the database
4. During login, hashes are compared

---

## 🧂 Salting

A **salt** is a random value added to a password before hashing.

Benefits:

* Prevents rainbow table attacks
* Ensures identical passwords produce different hashes

---

## 🖥️ File Integrity Checking

Hashing can be used to verify file integrity.

Use cases:

* Verifying downloaded files
* Detecting file tampering

If the hash changes, the file has been modified.

---

## 🛠️ Hands-on Mini Lab

### 🔐 Hashing a File

Generate a SHA-256 hash:

```
sha256sum file.txt
```

Generate an MD5 hash:

```
md5sum file.txt
```

Compare hashes before and after modifying the file to observe changes.

---

### 🔑 Password Hashing Example

Hash a password using OpenSSL:

```
echo -n "password123" | sha256sum
```

Note: Fast hashes like SHA-256 are **not ideal** for password storage.

Better alternatives:

* bcrypt
* scrypt
* Argon2

---

### 🧨 Hashcat – Password Cracking Basics (Mini)

Hashcat is a powerful tool used to **crack password hashes** by comparing hashes of guessed passwords against a target hash.

Example: cracking an MD5 hash using a wordlist:

```
hashcat -m 0 -a 0 hashes.txt wordlist.txt
```

Where:

* `-m 0` → MD5 hash mode
* `-a 0` → straight attack (wordlist-based)
* `hashes.txt` → file containing target hashes
* `wordlist.txt` → password list

Example for SHA-256:

```
hashcat -m 1400 -a 0 hashes.txt wordlist.txt
```

Notes:

* Weak hashing algorithms are easier to crack
* Salting significantly increases cracking difficulty
* Hashcat is commonly used in **pentesting and audits**

---

## 🧪 What I Learned in This Room

* Hashing is a one-way function used for verification, not encryption
* Secure systems never store passwords in plain text
* Salts are essential for password security
* Hashing plays a critical role in integrity and authentication

---

## 📝 Personal Notes

* Hashing is fundamental for:

  * Authentication systems
  * Malware detection
  * Digital forensics
* Weak hash algorithms are still common in legacy systems

---


📌 *Next step*: continue with the next cryptography room / proceed to Week 04 Day 26
