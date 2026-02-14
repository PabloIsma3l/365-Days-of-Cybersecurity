# 🔎DAY-045 Digital Forensics Fundamentals — TryHackMe

## 📌 Overview

This repository documents the completion of the **Digital Forensics Fundamentals** room on TryHackMe.

This room introduces the principles of digital forensics, evidence handling, forensic analysis techniques, and how investigators collect and analyze digital artifacts during security incidents.

All tasks have been successfully completed.

---

## 🎯 Learning Objectives Achieved

✔ Understand what digital forensics is
✔ Learn the importance of evidence integrity
✔ Understand the chain of custody process
✔ Identify common digital artifacts
✔ Learn basic disk and memory analysis concepts
✔ Understand forensic investigation workflow

---

## 🧠 What is Digital Forensics?

Digital forensics is the process of identifying, preserving, analyzing, and presenting digital evidence in a legally sound manner.

It is used in:

* Incident response
* Cybercrime investigations
* Internal corporate investigations
* Legal proceedings

The goal is to reconstruct events and determine what happened, how it happened, and who was responsible.

---

## 🔐 Core Principles

### 1️⃣ Evidence Integrity

* Evidence must not be altered
* Use of hashing (MD5, SHA1, SHA256)
* Verify integrity before and after analysis

### 2️⃣ Chain of Custody

A documented process that tracks:

* Who collected the evidence
* When it was collected
* How it was handled
* Where it was stored

This ensures evidence is admissible in legal contexts.

---

## 💾 Types of Digital Evidence

* Disk images
* Memory dumps
* Log files
* Network traffic captures (PCAP)
* Email artifacts
* Browser history
* System registry data

---

## 🧩 Forensic Investigation Process

1. Identification
2. Preservation
3. Collection
4. Examination
5. Analysis
6. Reporting

Each phase must follow proper documentation standards.

---

## 🖥️ Disk & File System Concepts

Basic understanding of:

* File systems (NTFS, FAT)
* Deleted file recovery
* Metadata analysis
* Timestamps (MAC times)

File timestamps can help reconstruct attacker timelines.

---

## 🛠️ Metadata Analysis Tools Used

During the room, metadata extraction techniques were explored using tools such as:

### 📄 PDF Metadata Analysis (pdfinfo)

Used to extract hidden metadata from PDF documents.

```bash
pdfinfo file.pdf
```

This can reveal:

* Author name
* Creation date
* Modification date
* Software used to generate the file

---

### 🖼️ Image Metadata Analysis (ExifTool / exiftool)

Used to extract EXIF metadata from image files.

```bash
exiftool image.jpg
```

This can reveal:

* Camera model
* GPS coordinates
* Creation timestamps
* Embedded software information

Metadata analysis is crucial in forensic investigations because it can expose hidden details that help reconstruct events or identify threat actors.

---

---

## 🧠 Memory Forensics (Conceptual Overview)

Memory analysis can reveal:

* Running processes
* Active network connections
* Injected malware
* Encryption keys

Memory forensics is critical in advanced incident response scenarios.

---

## 📊 Timeline Analysis

Investigators reconstruct events using:

* File timestamps
* Log correlation
* System activity records

Timeline building helps determine:

* Initial access
* Persistence mechanisms
* Lateral movement
* Data exfiltration

---

## 🛡️ Security Relevance

Digital forensics strengthens:

* Blue Team investigations
* Incident response capability
* Threat hunting
* Legal compliance

It also enhances Red Team awareness of detection artifacts.

---

## 🏁 Room Completion Status

* ✅ All tasks completed
* 🧠 Foundational understanding of forensic investigation achieved

---

## 🛠️ Additional Forensic Tools & Use Cases

Below are important tools commonly used in digital forensic investigations and their specific purposes:

### 🔍 File & Data Recovery

* **foremost** → Recover deleted files based on file signatures

  ```bash
  foremost disk.img
  ```

* **binwalk** → Analyze and extract embedded files from firmware or binary files

  ```bash
  binwalk -e file.bin
  ```

---

### 🔎 String & Artifact Extraction

* **strings** → Extract readable ASCII/Unicode strings from binaries

  ```bash
  strings suspicious.exe
  ```

Useful for identifying:

* Hardcoded passwords
* URLs
* IP addresses
* Suspicious commands

---

### 🔐 Hashing & Integrity Verification

* **sha256sum** → Generate file hash for integrity verification

  ```bash
  sha256sum evidence.img
  ```

* **hashdeep** → Advanced hashing and recursive integrity verification

  ```bash
  hashdeep -r evidence_folder/
  ```

Used to ensure evidence integrity before and after analysis.

---

### 🌐 Network Forensics

* **Wireshark** → Analyze PCAP files and inspect network traffic
* **tcpdump** → Capture and analyze network packets from CLI

  ```bash
  tcpdump -r capture.pcap
  ```

Used for detecting:

* Suspicious connections
* Data exfiltration
* Command & Control traffic

---

### 🧠 Memory Forensics

* **Volatility** → Analyze memory dumps

  ```bash
  volatility -f memory.dump --profile=PROFILE pslist
  ```

Used to identify:

* Running processes
* Injected code
* Network connections
* Malware artifacts

---

