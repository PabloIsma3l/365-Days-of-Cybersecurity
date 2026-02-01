## Day 31 – Metasploit: Meterpreter

## Overview

This room focuses on **Meterpreter**, Metasploit’s advanced post-exploitation payload. Meterpreter operates primarily **in memory**, which makes it stealthier than traditional shells and extremely powerful for post-exploitation activities.

The objective of this day is to understand how to interact with compromised systems using Meterpreter and to become familiar with its most important commands from a Red Team perspective.

---

## Learning Objectives

* Understand what Meterpreter is and how it works
* Navigate and interact with compromised systems
* Perform system, network, and file enumeration
* Execute post-exploitation actions
* Learn common Meterpreter commands used in real engagements

---

## What is Meterpreter?

Meterpreter is an advanced payload included in the Metasploit Framework. Unlike standard shells, it:

* Runs entirely in memory
* Avoids writing binaries to disk by default
* Communicates over encrypted channels
* Supports modular extensions

Meterpreter is mainly used during the **post-exploitation phase** of a penetration test.

---

## Meterpreter Command Categories

Once a Meterpreter session is established, commands are grouped into several functional categories.

---

## Basic Commands

These commands are used to manage and interact with the current Meterpreter session.

* `background` – Backgrounds the current session
* `exit` – Terminates the Meterpreter session
* `guid` – Displays the session GUID (Globally Unique Identifier)
* `help` – Displays the help menu
* `info` – Shows information about a post module
* `irb` – Opens an interactive Ruby shell
* `load` – Loads one or more Meterpreter extensions
* `migrate` – Migrates Meterpreter to another process
* `run` – Executes a Meterpreter script or post module
* `sessions` – Switches between active sessions

---

## File System Commands

These commands allow interaction with the target file system.

* `cd` – Changes directory
* `ls` / `dir` – Lists files in the current directory
* `pwd` – Prints the current working directory
* `edit` – Edits a file on the target system
* `cat` – Displays the contents of a file
* `rm` – Deletes a specified file
* `search` – Searches for files
* `upload` – Uploads a file or directory
* `download` – Downloads a file or directory

---

## Network Commands

Used to enumerate and interact with the target network configuration.

* `arp` – Displays the ARP cache of the target host
* `ifconfig` – Shows available network interfaces
* `netstat` – Displays network connections
* `portfwd` – Forwards a local port to a remote service
* `route` – Views or modifies the routing table

---

## System Commands

These commands interact directly with the operating system.

* `clearev` – Clears event logs
* `execute` – Executes a command on the target system
* `getpid` – Displays the current process ID
* `getuid` – Shows the user Meterpreter is running as
* `kill` – Terminates a process by PID
* `pkill` – Terminates processes by name
* `ps` – Lists running processes
* `reboot` – Reboots the remote system
* `shell` – Drops into a system command shell
* `shutdown` – Shuts down the remote system
* `sysinfo` – Displays system information (OS, architecture, etc.)

---

## Other Useful Commands

These commands provide advanced post-exploitation capabilities.

* `idletime` – Returns how long the user has been idle
* `keyscan_start` – Starts keystroke capture
* `keyscan_dump` – Dumps captured keystrokes
* `keyscan_stop` – Stops keystroke capture
* `screenshare` – Views the remote desktop in real time
* `screenshot` – Takes a screenshot of the desktop
* `record_mic` – Records audio from the default microphone
* `webcam_list` – Lists available webcams
* `webcam_snap` – Takes a snapshot from a webcam
* `webcam_stream` – Streams video from a webcam
* `webcam_chat` – Starts a webcam chat session
* `getsystem` – Attempts to elevate privileges to SYSTEM
* `hashdump` – Dumps the SAM database (Windows credentials)

---

## Red Team Notes

* Meterpreter is extremely powerful but **noisy** in real environments
* Many commands trigger security alerts
* Always consider operational security (OpSec)
* Use Meterpreter primarily for enumeration and proof-of-concept actions

---

## Summary

* Meterpreter is a key post-exploitation tool in Metasploit
* Provides extensive control over compromised systems
* Command familiarity is essential for real-world pentesting
* Proper usage requires understanding both capabilities and limitations

---

