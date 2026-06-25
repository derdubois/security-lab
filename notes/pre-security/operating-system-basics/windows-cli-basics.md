## Summary: Windows Command Line Basics (TryHackMe Room)

---

### Context & Purpose

This is a TryHackMe room designed for beginner cybersecurity learners, framed as "Day 2 of an internship." It follows a previous Linux CLI Basics room and shifts focus to the **Windows Command Prompt (CMD)** — a text-based interface for interacting with the Windows OS without relying on a graphical interface (GUI).

The core argument is that security professionals prefer the CLI because it's faster, more precise, gives deeper control, and many security tools are terminal-only.

---

### Learning Objectives

By the end of the room, learners can:
- Navigate the Windows filesystem via CMD
- Find files without knowing their location
- Reveal hidden files and directories
- Read file contents in the terminal
- Gather basic system and network information

**Prerequisites:** Operating Systems intro room + Linux CLI Basics room.

---

### Task 1 — Navigating the Filesystem

The task uses a storyline: a boss left a file called `task_brief.txt` somewhere in the user folder, and you must find and read it using only the command line.

| Step | Goal | Command |
|---|---|---|
| 1 | Check current directory | `cd` |
| 2 | List visible files/folders | `dir` |
| 3 | List including hidden items | `dir /a` |
| 4 | Move into a subfolder | `cd folder_name` |
| 4 | Go back one level | `cd ..` |
| 5 | Search all subfolders for a file | `dir /s task_brief.txt` |
| 6 | Navigate to the found path | `cd <path>` |
| 7 | Read the file contents | `type task_brief.txt` |

Key insight: **hidden ≠ secret** — Windows just hides certain files from default view. The `/a` flag reveals them all.

---

### Task 2 — System & Network Reconnaissance

Once navigation is understood, the room shifts to gathering information about the machine itself — a standard first step for both IT troubleshooting and security investigations.

| Step | Goal | Command | Key Output to Note |
|---|---|---|---|
| 1 | Who is the current user? | `whoami` | Username + permissions context |
| 2 | What is this machine called? | `hostname` | Computer name (used for network identification) |
| 3 | What OS version is running? | `systeminfo` | OS Name, OS Version, System Type (32/64-bit) |
| 4 | How is it connected to the network? | `ipconfig` | IPv4 Address, Default Gateway |

---

### Why This Matters (Security Perspective)

- Windows is the dominant OS in enterprise environments, making it a primary target in real-world attacks and investigations
- Not all files and information are visible through the GUI — CLI access reveals more
- These exact commands (`whoami`, `ipconfig`, `systeminfo`) are among the first run during incident response or penetration testing
- CLI skills are easier to script and automate than GUI interactions

---

### Commands Reference Card

```
cd              → show current directory / change directory
cd ..           → go up one level
dir             → list files and folders
dir /a          → list all including hidden
dir /s <file>   → search recursively for a file
type <file>     → read/print file contents
whoami          → current logged-in user
hostname        → computer name
systeminfo      → full OS and hardware info
ipconfig        → network configuration
```
