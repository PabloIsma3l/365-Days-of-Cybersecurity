# 📅 Day 23 – Cryptography Basics

## 🎯 Daily Objective

Understand the fundamentals of **cryptography**, its purpose in cybersecurity, and how **symmetric encryption** is used to protect data confidentiality.

---

## 🔐 What is Cryptography?

Cryptography is the practice of securing information by transforming it into a format that is unreadable without the proper key.

Its main goals are:

* **Confidentiality** – only authorized parties can read the data
* **Integrity** – data is not altered in transit
* **Authentication** – verify the identity of parties
* **Non-repudiation** – actions cannot be denied

---

## 🧱 Key Cryptographic Concepts

### Plaintext & Ciphertext

* **Plaintext**: original readable data
* **Ciphertext**: encrypted, unreadable data

### Encryption & Decryption

* **Encryption**: converting plaintext into ciphertext using an algorithm and a key
* **Decryption**: reversing the process using the correct key

---

## 🔑 Symmetric Encryption

Symmetric encryption uses **the same key** for both encryption and decryption.

### Characteristics

* Fast and efficient
* Suitable for large amounts of data
* Key distribution is a challenge

### Common Algorithms

| Algorithm | Description                                    |
| --------- | ---------------------------------------------- |
| AES       | Advanced Encryption Standard (most used today) |
| DES       | Deprecated, insecure                           |
| 3DES      | Legacy, slower                                 |
| ChaCha20  | Modern stream cipher                           |

---

## 🧪 Basic CLI Examples

### Encrypting a file with AES (OpenSSL)

```bash
openssl enc -aes-256-cbc -salt -in secret.txt -out secret.enc
```

### Decrypting the file

```bash
openssl enc -aes-256-cbc -d -in secret.enc -out secret.txt
```

### Generating a random key

```bash
openssl rand -hex 32
```

---

## 🧠 Hashing vs Encryption (Important Distinction)

| Feature    | Encryption   | Hashing          |
| ---------- | ------------ | ---------------- |
| Reversible | Yes          | No               |
| Uses key   | Yes          | No               |
| Purpose    | Protect data | Verify integrity |

Example hash generation:

```bash
sha256sum file.txt
```

---

## 🔴 Red Team Perspective

From an offensive security standpoint, cryptography knowledge helps to:

* Identify weak or deprecated algorithms
* Detect improper key management
* Recognize insecure implementations
* Crack or bypass protections when misconfigured

---

## 🛠️ Key Takeaways

* Cryptography is fundamental to cybersecurity
* Symmetric encryption is fast but requires secure key handling
* Not all data protection mechanisms are encryption

---
