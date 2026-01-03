# Day 3 – OSI Model, Packets & Frames

## 🎯 Objective
Understand how data travels across a network by learning the OSI model and how packets and frames are structured and transmitted.

---

## 📘 Rooms Completed (TryHackMe)
- OSI Model
- Packets & Frames

---

## 🧠 Topics Covered

### 🟦 OSI Model (7 Layers)

| Layer | Name         | Description |
|------:|--------------|-------------|
| 7 | Application | User-facing services (HTTP, FTP, DNS, SSH) |
| 6 | Presentation | Encoding, encryption, compression |
| 5 | Session | Session management |
| 4 | Transport | TCP, UDP, ports |
| 3 | Network | IP addressing, routing |
| 2 | Data Link | Frames, MAC addresses |
| 1 | Physical | Bits, signals, cables |

---

### 📦 Packets & Frames

| Concept | Description |
|--------|-------------|
| Packet | Data unit at Layer 3 (IP) |
| Frame | Data unit at Layer 2 (MAC) |
| Encapsulation | Wrapping data with headers |
| Decapsulation | Removing headers at destination |

---

## 🔁 TCP/IP Model vs OSI Model

| TCP/IP Layer   | OSI Equivalent | Description |
|----------------|----------------|-------------|
| Application    | Layers 7–5     | HTTP, HTTPS, FTP, SMTP, DNS |
| Transport      | Layer 4        | TCP, UDP |
| Internet       | Layer 3        | IP, ICMP |
| Network Access | Layers 2–1     | Ethernet, ARP |

---

## ⚔️ TCP vs UDP – Key Differences

| Feature | TCP | UDP |
|--------|-----|-----|
| Connection | Connection-oriented | Connectionless |
| Reliability | Guaranteed delivery | No guarantee |
| Ordering | Maintains order | No ordering |
| Speed | Slower | Faster |
| Error handling | Yes | No |
| Handshake | 3-way handshake | None |

---

### 🔐 TCP – 3-Way Handshake

| Step | Description |
|------|-------------|
| SYN | Client initiates connection |
| SYN-ACK | Server responds |
| ACK | Client confirms connection |

---

## 🛠 Tools Used
- TryHackMe interactive labs

---

## 🔑 Key Takeaways
- The OSI model explains network communication layer by layer
- Packets and frames operate at different OSI layers
- TCP provides reliability, UDP provides speed
- Understanding protocols is critical for enumeration

---

## 🔗 Useful Resources

- OSI Model (Cisco):  
  https://www.cisco.com/c/en/us/support/docs/osi-model/osi-model.html

- OSI Model (Cloudflare):  
  https://www.cloudflare.com/learning/ddos/glossary/open-systems-interconnection-model-osi/

- Common TCP/UDP Ports:  
  https://www.vmaxx.net/techinfo/ports.htm

- IANA Port Registry:  
  https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml

- Packet vs Frame:  
  https://www.geeksforgeeks.org/difference-between-packet-and-frame/

- Encapsulation explained:  
  https://www.cloudflare.com/learning/network-layer/what-is-encapsulation/

---

## 🧠 Red Team Notes
Knowing how data moves through layers helps identify where to enumerate, scan, and exploit services.

---

## ✅ Day 3 Completed
👉 Day 3 completed – OSI Model and Packets & Frames


