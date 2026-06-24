Here are your detailed notes from the TryHackMe Linux Basics room.---

## Detailed notes — TryHackMe Linux Basics (Day 1)

---

### The terminal

The terminal is a text-based interface for controlling a Linux system. Cybersecurity professionals prefer it because it is faster than a GUI, offers more precise control, and most security tools are CLI-only.

---

### Section 1: Filesystem navigation

**`pwd`** — Print Working Directory. Answers "where am I right now?" Shows the full absolute path of your current location (e.g. `/home/ubuntu`).

**`ls`** — Lists files and directories in the current location. Three common variants:
- `ls` — basic list
- `ls -l` — long format; reveals permissions, owner, file size, and last-modified date
- `ls -al` — long format including hidden files (names starting with `.`)

**`cd <directory>`** — Change Directory. Moves you into a named folder. Use `cd ..` to go up one level to the parent directory.

**`find <start> -name <filename>`** — Recursively searches a directory tree for a file by name. The home directory shortcut `~` saves typing. Example: `find ~ -name mission_brief.txt`. Linux will scan every subfolder and print the full path if found.

**`cat <filename>`** — Reads and prints the contents of a file directly to the terminal. No editor, no menus — just the raw content.

---

### Section 2: System information

**`whoami`** — Prints the current username. Essential first step in any new environment to confirm what account and privilege level you are operating under.

**`uname -a`** — Full system information in one line. Fields (in order): kernel name → hostname → kernel version → build info → hardware architecture (three times) → OS type. Example output: `Linux tryhackme 6.x-aws #17-Ubuntu SMP … x86_64 GNU/Linux`.

**`df -h`** — Disk Free with human-readable sizes (G/M/K instead of raw bytes). Key fields per row: filesystem, total size, used, available, use%, and mount point.
- `/dev/root` = the actual physical disk (your main storage)
- `tmpfs` entries = virtual filesystems that live in RAM (shared memory, runtime state, per-user temp storage). They don't consume disk space.

**`cat /etc/os-release`** — Reads the distro identification file stored in `/etc`. Contains fields like `PRETTY_NAME`, `VERSION_ID`, `VERSION_CODENAME`, and support URLs. More readable than `uname` for identifying the Linux distribution. On this machine: Ubuntu 24.04.1 LTS "Noble Numbat".

---

### Key concepts

**Hidden files** — Any file or folder whose name starts with a dot (`.bashrc`, `.ssh/`, `.config/`) is hidden from plain `ls` by default. Not secret — just conventionally omitted. Reveal with `ls -al`.

**`/` vs `~`** — `/` is the filesystem root, the very top of the entire directory tree. `~` expands to your home directory (`/home/username`). Absolute paths always start from `/`; relative paths start from wherever you currently are.

**`/etc` directory** — Stores system-wide configuration and informational files. A standard target when gathering system info or doing initial recon. Important file: `/etc/os-release`.

---

### Mini-challenge workflow (self-directed practice)

The room ends with an unguided task — find and read `day1_report.txt`:

```bash
find ~ -name day1_report.txt   # locate the file
cd <path returned above>       # navigate to it
cat day1_report.txt            # read it
```

This tests whether you can chain the three core skills together without step-by-step prompts.

---

### What comes next (roadmap)

These commands are the foundation. Upcoming topics in the series build on them: file permissions, users and groups, running processes, package management, and eventually real security tooling (network scanning, exploitation frameworks, log analysis).
