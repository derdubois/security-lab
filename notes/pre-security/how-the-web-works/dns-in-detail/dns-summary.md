**What DNS Does (the core idea)**

DNS is basically the internet's phone book. Instead of memorizing numeric IP addresses like `104.26.10.229`, you type a human-readable name like `tryhackme.com` and DNS translates it to the right address behind the scenes.

---

**Domain Name Structure**

A full domain name like `jupiter.servers.tryhackme.com` has layers, read right to left:

- **.com** → TLD (Top-Level Domain). Either generic (gTLD: `.com`, `.org`, `.edu`) or country-based (ccTLD: `.uk`, `.ca`)
- **tryhackme** → Second-Level Domain — the actual registered name, max 63 characters
- **servers / jupiter** → Subdomains — prefixes that point to specific parts of a service. You can stack multiple, as long as the full name stays under 253 characters

---

**DNS Record Types**

| Record | Purpose |
|--------|---------|
| A | Maps a domain → IPv4 address |
| AAAA | Maps a domain → IPv6 address |
| CNAME | Maps a domain → another domain name (an alias) |
| MX | Points to email servers; has priority ordering for failover |
| TXT | Free-text field — used for spam prevention (SPF, DMARC), domain ownership verification, etc. |

---

**How a DNS Lookup Actually Works (step by step)**

1. Your computer checks its **local cache** first
2. If not cached → asks your **Recursive DNS Server** (usually your ISP's)
3. That server checks its own cache — if found, returns it immediately
4. If not → goes to a **Root Server**, which says "for `.com`, go ask the `.com` TLD server"
5. The **TLD server** points to the **Authoritative Nameserver** for that specific domain
6. The **Authoritative Nameserver** holds the actual DNS records and sends the answer back
7. The result travels back through the chain, gets **cached** at each step with a **TTL** (Time To Live) — a timer in seconds saying how long to keep it before re-checking

---

**Key terms to remember:** Recursive DNS Server, Authoritative Nameserver, TTL, and the five record types (A, AAAA, CNAME, MX, TXT). These come up constantly in networking and security contexts.
