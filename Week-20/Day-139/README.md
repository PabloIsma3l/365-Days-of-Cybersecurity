# ⚙️ Compiled — TryHackMe Writeup

**📅 Day 139 — 365 Days of Cybersecurity**
**✅ Status: Completed**
**🏷️ Tags:** `Reverse Engineering` `Ghidra` `Binary Analysis` `Decompilation` `Crackme` `CTF` `Static Analysis`
**⚙️ Difficulty:** Easy

---

## 🧠 Overview

In this room I performed **static reverse engineering** on a compiled Linux binary to recover a hidden password. The program prompts for a password at runtime — but without the source code, the only way to find it is to analyze the binary itself using a decompiler.

This is a classic **crackme** challenge — the entry point for anyone learning reverse engineering. The goal is to understand what the program is *doing* at the machine level by working backwards from compiled code to readable logic.

> **Core principle:** Compiled code is not unreadable — it's just transformed. A decompiler converts machine instructions back into human-readable pseudocode, revealing the logic the developer wrote, including any hardcoded values like passwords or flags.

---

## 🎯 Learning Objectives

- Understand the difference between static and dynamic binary analysis
- Use **Ghidra** to decompile a binary and navigate its functions
- Read and interpret decompiled C pseudocode from the `main()` function
- Understand how `scanf`, `strcmp`, and format strings work at the binary level
- Identify hardcoded passwords and logic embedded in compiled programs

---

## 🗂️ Environment

| Detail | Value |
|---|---|
| Binary | `Compiled` (Linux ELF x86-64) |
| Location | `/root/Rooms/Compiled/` (AttackBox) or downloaded task file |
| Tool | Ghidra (static decompiler) |
| Note | Binary won't execute on AttackBox — analysis only |

---

## 🔍 Step 1 — Initial Reconnaissance

Before opening any binary in a decompiler, always run basic recon commands to understand what you're working with:

```bash
# Identify the file type
file Compiled
# Output: ELF 64-bit LSB executable, x86-64, dynamically linked

# Check for readable strings embedded in the binary
strings Compiled
```

### Why `strings` First?

`strings` extracts any sequence of printable characters from the binary — this sometimes reveals hardcoded passwords, URLs, error messages, or other useful artifacts without any complex analysis.

```bash
strings Compiled | grep -i "pass\|flag\|correct\|wrong\|init\|CTF"
```

Even if `strings` doesn't hand you the password directly, it gives you vocabulary to recognize important values when you see them in the decompiler.

### Running the Binary

```bash
./Compiled
# Password: test
# Try again!
```

The binary takes user input and compares it against an expected value. Our job is to find that expected value.

---

## 🔍 Step 2 — Loading into Ghidra

**Ghidra** is NSA's open-source reverse engineering framework — one of the most powerful free decompilers available.

### Basic Ghidra Workflow

```
1. Create a new project (File → New Project)
2. Import the binary (File → Import File → select Compiled)
3. Double-click the file → Ghidra auto-analyzes it
4. Accept default analysis options → click Analyze
5. Open the Symbol Tree panel → Functions → main
6. Double-click main → decompiled code appears in the Decompiler window
```

> **Tip:** After import, Ghidra's auto-analysis identifies functions, data types, cross-references, and calling conventions. For a small binary like this, it takes seconds and produces clean results.

### Navigating to `main()`

Every C program starts execution at `main()`. In the Symbol Tree (left panel):

```
Functions
└── main     ← double-click this
```

The decompiler window on the right will show the pseudocode reconstruction of the function.

---

## 🔍 Step 3 — Analyzing the Decompiled `main()` Function

### Ghidra's Decompiled Output

```c
undefined8 main(void)
{
  int iVar1;
  char local_28 [32];

  fwrite("Password: ", 1, 10, stdout);
  __isoc99_scanf("DoYouEven%sCTF", local_28);

  iVar1 = strcmp(local_28, "__dso_handle");
  if ((-1 < iVar1) && (iVar1 = strcmp(local_28, "__dso_handle"), iVar1 < 1)) {
    printf("Try again!");
    return 0;
  }

  iVar1 = strcmp(local_28, "_init");
  if (iVar1 == 0) {
    printf("Correct!");
  } else {
    printf("Try again!");
  }
  return 0;
}
```

---

## 🔬 Step 4 — Reading the Logic Line by Line

### Variable Declarations

```c
char local_28 [32];   // Buffer — 32-byte array to store the user's input
int iVar1;            // Return value holder for strcmp comparisons
```

### The `scanf` Format String — Hidden Clue

```c
__isoc99_scanf("DoYouEven%sCTF", local_28);
```

This is the most interesting line. `scanf` reads user input using a format string — normally something like `"%s"` for a plain string. Here, the format string is `"DoYouEven%sCTF"`.

What this means:
- The user types something like `_init`
- `scanf` with `"DoYouEven%sCTF"` reads the input and stores it in `local_28`
- The `%s` is the variable part — the rest is literal text in the format specifier

> The format string `"DoYouEven%sCTF"` is itself a hint from the developer — the full password phrase is `DoYouEven_initCTF`, which can be read by combining the format string prefix, the expected `strcmp` value, and the suffix.

### The Double `strcmp` Logic — Password Gate

```c
// First check: REJECT if input equals "__dso_handle"
iVar1 = strcmp(local_28, "__dso_handle");
if ((-1 < iVar1) && (iVar1 = strcmp(local_28, "__dso_handle"), iVar1 < 1)) {
    printf("Try again!");
    return 0;
}
```

`strcmp` returns:
- `0` if strings are **equal**
- `< 0` if first string is lexicographically **less**
- `> 0` if first string is lexicographically **greater**

The condition `(-1 < iVar1) && (iVar1 < 1)` means `iVar1 == 0` — so this block executes when input **equals** `"__dso_handle"`. In other words: if you type `__dso_handle`, you get rejected.

```c
// Second check: ACCEPT if input equals "_init"
iVar1 = strcmp(local_28, "_init");
if (iVar1 == 0) {
    printf("Correct!");
}
```

The winning condition: input must equal `"_init"`.

### Reconstructing the Full Password

Combining what we found:

| Component | Value |
|---|---|
| `scanf` format prefix | `DoYouEven` |
| Accepted `strcmp` value | `_init` |
| `scanf` format suffix | `CTF` |
| **Full password** | **`DoYouEven_init`** |

```bash
./Compiled
# Password: DoYouEven_init
# Correct! Enjoy Decompiling! (--;)
```

---

## 🧠 Understanding the Binary Logic — Deeper Dive

### Why Are Two `strcmp` Calls Used?

The double `strcmp` structure creates an **exclusion + inclusion** gate:

```
Input == "__dso_handle"  →  REJECT  (first check)
Input == "_init"         →  ACCEPT  (second check)
Anything else            →  REJECT  (falls through to else)
```

`__dso_handle` is a real symbol in the ELF binary's own symbol table — it's the address used by the C runtime for DSO (Dynamic Shared Object) destructors. Its presence in the check is a deliberate red herring: if you ran `strings` on the binary and found `__dso_handle`, you might try it as the password — but the logic explicitly rejects it.

`_init` is also a real ELF symbol — it's the address of the binary's initialization function, called before `main()`. The password is literally the name of a standard ELF section.

> This is a clever design: both decoy and real password are valid symbol names found in any ELF binary, testing whether the reverse engineer understands ELF structure or just guesses from `strings` output.

### The `scanf` Format String as Obfuscation

Using `"DoYouEven%sCTF"` instead of plain `"%s"` has two purposes:
1. **Obfuscation** — `strings` will show `DoYouEven%sCTF` but it's not the password, it's the format string
2. **Misdirection** — a beginner might think the full string including prefix/suffix is the password

Only by reading the `scanf` documentation and correlating with the `strcmp` value can you reconstruct `DoYouEven_init`.

---

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| **Ghidra** | Primary decompiler — converts binary to C pseudocode |
| `file` | Identify binary type and architecture |
| `strings` | Extract readable text from the binary |
| `chmod +x` | Make binary executable |
| **Ghidra Symbol Tree** | Navigate functions within the binary |
| **Ghidra Decompiler** | View pseudocode reconstruction of `main()` |

---

## 📚 Ghidra Quick Reference for Beginners

```
Shortcut       Action
──────────────────────────────────────────
G              Go to address
L              Rename a variable or function
T              Retype a variable
Ctrl+F         Search in decompiler view
Alt+←          Go back (navigation history)
Double-click   Follow a function call or variable
Right-click    Decompiler context menu (re-type, rename, etc.)
```

### Improving Decompiler Readability

When Ghidra uses generic names like `iVar1`, `local_28`, you can rename them to improve readability:

```
Right-click iVar1 → Rename Variable → cmp_result
Right-click local_28 → Rename Variable → user_input
```

After renaming:
```c
int cmp_result;
char user_input[32];

fwrite("Password: ", 1, 10, stdout);
scanf("DoYouEven%sCTF", user_input);

cmp_result = strcmp(user_input, "__dso_handle");
if ((-1 < cmp_result) && (cmp_result < 1)) {
    printf("Try again!");
    return 0;
}
cmp_result = strcmp(user_input, "_init");
if (cmp_result == 0) {
    printf("Correct!");
}
```

Much clearer — renaming variables is one of the most important habits to build in reverse engineering.

---

## 🔄 Static vs Dynamic Analysis

This room uses **static analysis** — examining the binary without executing it. It's worth understanding when to use each approach:

| | Static Analysis | Dynamic Analysis |
|---|---|---|
| **Definition** | Analyze binary without running it | Run the binary and observe behavior |
| **Tools** | Ghidra, IDA Pro, radare2, Binary Ninja | GDB, ltrace, strace, x64dbg |
| **When to use** | Malware on live systems, no-exec environments | Understanding runtime behavior, anti-analysis bypass |
| **Risk** | None — binary never runs | Risk of executing malicious code |
| **What you see** | All code paths | Only executed code paths |
| **Anti-analysis** | Obfuscation, packing | Anti-debugging, timing checks |

> For this room specifically, the AttackBox note says "binary will not execute" — making static analysis the only option, and Ghidra the ideal tool.

---

## 🛡️ Real-World Security Relevance

Reverse engineering skills like those practiced here are directly applicable to:

**Malware Analysis:**
- Analyzing suspicious binaries without executing them
- Identifying C2 addresses, encryption keys, or payload logic hardcoded in malware
- Understanding what a binary does before deciding whether to run it in a sandbox

**Vulnerability Research:**
- Finding hardcoded credentials in compiled applications
- Identifying buffer overflow conditions by analyzing `scanf`/`strcpy` usage
- Locating authentication bypass conditions in binary logic

**CTF & Bug Bounty:**
- Crackme challenges are a standard category in CTF competitions
- Some bug bounty programs include compiled binaries (mobile apps, desktop clients) where hardcoded secrets may be present

**Incident Response:**
- When source code isn't available for a suspicious binary found during an investigation
- Confirming what a tool does before attributing it to an attacker

---

## 🧪 Key Concepts Practiced

- Static binary analysis workflow (file → strings → decompiler)
- Loading and navigating a binary in Ghidra
- Reading decompiled C pseudocode from `main()`
- Interpreting `strcmp` return values and conditional logic
- Understanding `scanf` format strings and their role in input parsing
- Recognizing ELF binary symbols (`_init`, `__dso_handle`) and their significance
- Variable renaming as a core reverse engineering discipline

---

## 🧠 Key Takeaways

1. **Start every RE challenge with `strings`.** It takes two seconds and occasionally hands you the answer. Even when it doesn't, it populates your mental dictionary of what's in the binary.

2. **`main()` is almost always your starting point.** Every C program's logic flows from `main()`. Finding it in the Symbol Tree and reading the decompiled output gives you the program's complete decision tree.

3. **`strcmp` returning 0 means equal.** This trips up beginners constantly. The winning condition `if (iVar1 == 0)` means the strings *matched* — not that the comparison failed.

4. **Format strings in `scanf` are not always `"%s"`.** Non-standard format strings like `"DoYouEven%sCTF"` are used as obfuscation. Always read the full format string, not just the `%` specifier.

5. **Renaming variables transforms unreadable code into readable code.** `iVar1` means nothing; `strcmp_result` means everything. Make renaming a reflex — it costs 5 seconds and makes the remaining analysis 10x faster.

6. **Decoys are common in crackmes.** `__dso_handle` was placed in the binary specifically to mislead. Real malware uses similar techniques — embedding fake C2 addresses, dummy keys, and misleading strings to slow down analysts.

7. **Static RE is a fundamental defensive skill.** Every piece of malware is a compiled binary. The ability to open it in Ghidra, find `main()`, and read what it does is one of the most transferable skills in the entire security discipline.

---

## 📌 Final Thoughts

Compiled is an excellent first step into reverse engineering — compact enough to complete quickly but rich enough to introduce the full static analysis workflow. The use of real ELF symbols (`_init`, `__dso_handle`) as the password/decoy shows thoughtful room design: it rewards analysts who understand binary structure over those who just run `strings` and guess.

The Ghidra workflow practiced here — import → analyze → navigate to `main()` → read decompiler → rename variables → follow logic — is the same workflow used by professional malware analysts on real-world samples. The binary might be a simple crackme today, but the methodology scales directly to analyzing ransomware, RATs, and APT implants.

Reverse engineering is one of the highest-value skills in offensive and defensive security. Rooms like this are where it starts.

