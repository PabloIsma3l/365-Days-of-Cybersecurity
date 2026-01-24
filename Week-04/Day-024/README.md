# 📅 Week 04 · Day 24

## 🔐 Public Key Cryptography Basics (TryHackMe)

Room: **Public Key Cryptography Basics**
Objective: Understand how public key cryptography (especially **RSA**) works and its role in real-world applications such as **SSH**.

---

## 🎯 Day Objectives

* Understand the difference between **symmetric** and **asymmetric** cryptography
* Understand the concept of a **key pair (public / private)**
* Learn the basic operation of **RSA**
* Understand what **n**, **φ(n)**, **e**, and **d** are
* Identify real-world applications of public key cryptography

---

## 🔑 Symmetric vs Asymmetric Cryptography

### 🔁 Symmetric Cryptography

* Uses **a single key** to encrypt and decrypt data
* Both parties must know the same key
* It is **fast**, but secure key distribution is difficult

Examples:

* AES
* DES

### 🔐 Asymmetric Cryptography

* Uses **two different keys**:

  * 🔓 Public key (can be shared)
  * 🔒 Private key (must remain secret)
* Data encrypted with one key can only be decrypted with the other
* Slower than symmetric cryptography, but ideal for secure key exchange

Examples:

* RSA
* ECC

---

## 🧠 Key Concepts

### 🔑 Key Pair

* **Public key**: freely distributed
* **Private key**: known only by the owner

Common uses:

* Data encryption
* Authentication
* Digital signatures

---

## 🔢 RSA – Fundamentals

RSA is based on the **difficulty of factoring large numbers**.

### Basic RSA Steps

1. Choose two large prime numbers:

   * `p`
   * `q`

2. Compute:

   * `n = p × q`
   * `φ(n) = (p − 1)(q − 1)`

3. Choose a number `e` such that:

   * `1 < e < φ(n)`
   * `gcd(e, φ(n)) = 1`

4. Compute `d` such that:

   * `(d × e) mod φ(n) = 1`

### Resulting Keys

* 🔓 **Public key**: `(n, e)`
* 🔒 **Private key**: `(n, d)`

---

## 🔐 Encryption and Decryption

### 📤 Encryption

Encrypted message:

```
c = m^e mod n
```

### 📥 Decryption

Original message:

```
m = c^d mod n
```

---

## 🖥️ Practical Applications

### 🔑 SSH

* SSH uses public key cryptography to:

  * Authenticate users without passwords
  * Securely exchange session keys

Simplified workflow:

1. The client sends its **public key** to the server
2. The server stores it in `authorized_keys`
3. The client proves ownership of the **private key**

---

## 🧪 What I Learned in This Room

* Asymmetric cryptography enables secure communication without sharing secrets
* RSA relies on simple mathematical operations that are hard to reverse
* The private key must **never be shared**
* SSH is a real-world and widely used example of public key cryptography

---

## 📝 Personal Notes

* Understanding RSA is very useful for topics such as:

  * Pentesting
  * TLS/SSL
  * Basic cryptographic attacks
* Strongly related to networking and authentication concepts


---

## 🛠️ Hands-on Mini Lab

### 🔐 RSA – Simple Example (Conceptual)

Assume we choose small prime numbers for learning purposes:

* `p = 11`
* `q = 17`

Calculate:

* `n = p × q = 187`
* `φ(n) = (p − 1)(q − 1) = 160`

Choose:

* `e = 7` (coprime with 160)

Compute:

* `d = 23` such that `(d × e) mod φ(n) = 1`

Keys:

* Public key: `(187, 7)`
* Private key: `(187, 23)`

This example shows how RSA keys are mathematically related.

---

### 🔑 SSH – Key Generation and Usage

Generate an SSH key pair:

```
ssh-keygen -t rsa -b 2048
```

Files generated:

* `id_rsa` → private key (keep secret)
* `id_rsa.pub` → public key (can be shared)

Add the public key to the server:

```
cat id_rsa.pub >> ~/.ssh/authorized_keys
```

Test authentication:

```
ssh user@server_ip
```

This demonstrates a real-world use of public key cryptography.

---

### 🔐 GPG – Encrypting and Decrypting with Public Keys

Generate a GPG key pair:

```
gpg --full-generate-key
```

List generated keys:

```
gpg --list-keys
```

Export the public key (to share):

```
gpg --export -a your_email@example.com > publickey.asc
```

Encrypt a file using a recipient's public key:

```
gpg --encrypt --recipient your_email@example.com secret.txt
```

Decrypt the file using the private key:

```
gpg --decrypt secret.txt.gpg
```

This shows how public key cryptography is used for secure file exchange.

---

📌 *Next step*: continue with the next cryptography room / proceed to Week 04 Day 25
