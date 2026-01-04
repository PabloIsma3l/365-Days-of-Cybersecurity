# Day 4 – Extending Your Network

## 🎯 Objective
Understand how networks are extended beyond a local environment by learning routing, switching, NAT, and firewall fundamentals.

---

## 📘 Rooms Completed (TryHackMe)
- Extending Your Network

---

## 🧠 Topics Covered

### 🌐 Network Devices

| Device | Description |
|------|-------------|
| Switch | Connects devices within a LAN using MAC addresses |
| Router | Connects different networks using IP routing |
| Firewall | Filters traffic based on rules |
| Access Point | Extends wireless connectivity |

---

### 🧭 Routing
- Determines the best path for packets between networks
- Uses routing tables
- Works at **OSI Layer 3 (Network)**

📌 Routers forward packets based on **destination IP address**.

---

### 🔀 Switching
- Operates at **OSI Layer 2 (Data Link)**
- Uses **MAC addresses**
- Efficient internal LAN communication

---

### 🔁 NAT (Network Address Translation)

| Type | Description |
|-----|-------------|
| Static NAT | One-to-one IP mapping |
| Dynamic NAT | Maps private IPs to public IPs dynamically |
| PAT (NAT Overload) | Multiple devices share one public IP |

📌 NAT allows private networks to access the internet.

---

### 🔥 Firewalls

| Firewall Type | Description |
|--------------|-------------|
| Packet Filtering | Filters based on IP, port, protocol |
| Stateful Firewall | Tracks connection states |
| Application Firewall | Inspects application-level data |

📌 Firewalls enforce security policies between networks.

---

## 🛠 Tools Used
- TryHackMe interactive labs
- Network diagrams

---

## 🔑 Key Takeaways
- Routers connect networks, switches connect devices
- NAT hides internal IP addresses
- Firewalls control traffic flow
- Network segmentation improves security

---

## 🔗 Useful Resources

- Routing explained (Cisco):  
  https://www.cisco.com/c/en/us/support/docs/ip/routing-information-protocol-rip/13769-1.html

- What is NAT? (Cloudflare):  
  https://www.cloudflare.com/learning/network-layer/what-is-nat/

- Firewalls explained:  
  https://www.cloudflare.com/learning/security/what-is-a-firewall/

---

## 🧠 Red Team Notes
Understanding routing, NAT, and firewalls helps identify:
- Network boundaries
- Segmentation weaknesses
- Firewall misconfigurations
- Pivoting opportunities

---

## ✅ Day 4 Completed
👉 Day 4 completed – Extending Your Network
