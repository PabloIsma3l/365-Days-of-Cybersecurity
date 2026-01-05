# Day 5 – How The Web Works

## 🎯 Objective
Understand how the web functions by learning DNS resolution, HTTP communication, website architecture, and the complete client-server workflow.

---

## 📘 Rooms Completed (TryHackMe)
- DNS in Detail
- HTTP in Detail
- How Websites Work
- Putting it all together

---

## 🧠 Topics Covered

### 🌍 DNS in Detail

| Concept | Description |
|-------|-------------|
| DNS | Translates domain names into IP addresses |
| A Record | Maps domain to IPv4 address |
| AAAA Record | Maps domain to IPv6 address |
| CNAME | Alias for another domain |
| MX | Mail server records |
| TXT | Stores arbitrary text data |

📌 DNS works mainly at **Application Layer**.

---

### 🔁 DNS Resolution Flow
1. User enters a domain name  
2. Recursive DNS resolver queries root servers  
3. TLD server is queried  
4. Authoritative DNS server responds  
5. IP address is returned to the client  

---

### 🌐 HTTP in Detail

| Feature | Description |
|--------|-------------|
| Protocol | Application-layer protocol |
| Port | TCP 80 (HTTP), TCP 443 (HTTPS) |
| Methods | GET, POST, PUT, DELETE |
| Status Codes | 200, 301, 403, 404, 500 |

---

### 🔐 HTTP vs HTTPS

| Feature | HTTP | HTTPS |
|-------|------|-------|
| Encryption | No | Yes (TLS) |
| Default Port | 80 | 443 |
| Security | Low | High |

---

### 🏗 How Websites Work

| Component | Role |
|---------|------|
| Browser | Sends HTTP requests |
| Web Server | Handles requests (Apache, Nginx) |
| Application | Processes logic |
| Database | Stores data |

📌 Most websites follow a **client-server architecture**.

---

### 🔄 Putting It All Together
1. User enters URL  
2. DNS resolves domain to IP  
3. TCP connection established  
4. HTTP request sent  
5. Server processes request  
6. HTTP response returned  
7. Browser renders content  

---

## 🛠 Tools Used
- TryHackMe interactive labs
- Browser developer tools

---

## 🔑 Key Takeaways
- DNS is critical for web access
- HTTP is stateless and request-based
- HTTPS protects data in transit
- Understanding web flow is essential for web attacks

---

## 🔗 Useful Resources

- DNS explained (Cloudflare):  
  https://www.cloudflare.com/learning/dns/what-is-dns/

- HTTP overview (MDN):  
  https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview

- HTTP status codes:  
  https://developer.mozilla.org/en-US/docs/Web/HTTP/Status

---

## 🧠 Red Team Notes
Understanding how the web works helps identify:
- Misconfigured DNS records
- Insecure HTTP methods
- Authentication flaws
- Entry points for web attacks

---

## ✅ Day 5 Completed
👉 Day 5 completed – How The Web Works
