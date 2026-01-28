# 🧪 Lab 01 – Client-Side Trust Vulnerability (FakeBank)

## 🎯 Objective

Identify and exploit a **client-side trust vulnerability** in a web banking application where sensitive business logic is controlled entirely by the client.

---

## 🧭 Environment

* **Platform:** TryHackMe
* **Path:** Cyber Security 101
* **Category:** Networking / Web Fundamentals
* **Target IP:** `10.66.161.27`

---

## 🔍 Initial Enumeration

### Host Discovery

```bash
nmap -sn 10.66.161.27
```

Result: Host is alive.

---

### Port Scanning

```bash
nmap -p- 10.66.161.27
```

Open ports discovered:

| Port | Service             |
| ---: | ------------------- |
|   22 | SSH                 |
|   80 | HTTP                |
| 3000 | HTTP                |
| 7777 | Unknown (HTTP-like) |

---

### Service & Version Detection

```bash
nmap -sV 10.66.161.27
```

Key findings:

* Port 80: nginx 1.18.0
* Port 3000: Node.js (Express)
* Port 7777: HTTP service returning 403 Forbidden

---

## 🌐 Web Enumeration

### Accessing Web Services

* `http://10.66.161.27` → Banking dashboard (auto-logged)
* `http://10.66.161.27:3000` → Same dashboard
* `http://10.66.161.27:7777` → 403 Forbidden

⚠️ **No authentication required** to access account information.

---

### Directory Enumeration

```bash
gobuster dir -u http://10.66.161.27 -w /usr/share/wordlists/dirb/common.txt
```

Result:

* Only static directories (`/css`, `/js`, `/images`, `/fonts`)
* No admin or API endpoints exposed

---

## 🍪 Session & Client-Side Analysis

### Cookies Identified

* `bank_value = "-1232.32"`

No other cookies, no JWT, no localStorage or sessionStorage data.

---

## 💥 Vulnerability Discovery

### Vulnerability Type

**Client-Side Trust / Broken Authentication & Authorization**

The application trusts a client-controlled cookie (`bank_value`) to manage sensitive financial data.

---

## 🧪 Proof of Concept (PoC)

### Steps

1. Open Developer Tools → Application → Cookies
2. Modify the value of `bank_value`
3. Refresh the page

### Result

* Account balance updates instantly
* Transactions are applied without validation
* No authentication or integrity checks performed

---

## 🎯 Impact

* Unauthorized modification of financial data
* Potential financial fraud
* Complete loss of data integrity

This represents a **high-severity business logic flaw**.

---

## 🛡️ Mitigation Recommendations

* Perform all balance calculations server-side
* Never trust client-controlled values
* Use signed or encrypted cookies
* Implement proper authentication and authorization controls

---

## 📌 Key Takeaways

* Client-side validation is not security
* Business logic flaws can be more dangerous than technical exploits
* Understanding application logic is critical in Red Team operations

---
