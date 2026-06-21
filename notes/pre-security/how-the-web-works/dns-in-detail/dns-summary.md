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


### CLIENT SIDE

**1. User types a URL**
You enter `https://tryhackme.com/learn` into the browser.

**2. Browser checks its own cache**
Before doing anything, the browser checks if it already has a saved (cached) copy of the page from a previous visit. If yes, it may skip the network entirely.

**3. Browser parses the URL**
Breaks the URL into scheme, host, port, path, query string, fragment.

---

### DNS RESOLUTION

**4. DNS lookup — multi-step process**
The browser doesn't go straight to a DNS server. It checks in order:
- Browser's own DNS cache
- Operating system DNS cache
- Your router's cache
- Your ISP's DNS server
- If still not found → Root nameserver → TLD nameserver (`.com`) → Authoritative nameserver for `tryhackme.com`
- Finally returns the IP address

---

### NETWORK & SECURITY LAYERS

**5. TCP handshake**
Before any data is sent, your machine and the server establish a connection using a 3-step handshake:
- Client sends **SYN** (I want to connect)
- Server replies **SYN-ACK** (acknowledged, go ahead)
- Client sends **ACK** (confirmed, connection open)

**6. TLS/SSL handshake (HTTPS only)**
Since the site uses HTTPS, an additional security handshake happens right after TCP. The server sends its SSL certificate, the browser verifies it's legitimate, and both sides agree on an encryption method. All data from this point is encrypted.

**7. Client-side firewall**
Your own machine or router may have a firewall that checks outgoing requests and blocks suspicious destinations.

---

### REQUEST TRAVELS THROUGH THE INTERNET

**8. ISP network routing**
Your request hops across multiple routers across the internet, each one forwarding the packet closer to the destination server. This can involve dozens of hops across different networks globally.

**9. CDN (Content Delivery Network) check**
Many large websites use a CDN (like Cloudflare or Akamai). Your request may hit a CDN edge server that is geographically closer to you rather than the origin server. If the CDN has a cached copy of what you need, it serves it directly — much faster. If not, it forwards the request to the origin server.

---

### SERVER-SIDE SECURITY & PROCESSING

**10. Server-side firewall**
The request hits the server's firewall first. It checks whether your IP is allowed, whether the request looks legitimate, and whether it matches any block rules.

**11. WAF (Web Application Firewall)**
A more intelligent layer than a regular firewall. The WAF inspects the actual HTTP request content — looking for signs of attacks like SQL injection, XSS, or HTML injection. If it looks malicious, it's blocked here.

**12. Load balancer**
Large websites don't run on a single server. A load balancer sits in front of many servers and decides which one should handle your request, distributing traffic evenly to prevent any one server from being overwhelmed.

**13. Web server receives the request**
The actual web server software (like Nginx or Apache) receives the HTTP request and hands it off to the application.

**14. Back-end processing**
The application runs its logic — checking your session/cookies, querying the database, applying business rules, generating the HTML response.

**15. Database query (if needed)**
The back end may talk to a database (like MySQL or MongoDB) to fetch or write data.

---

### RESPONSE TRAVELS BACK

**16. HTTP response built and sent**
The server builds the HTTP response — status code, headers, and the body (HTML/CSS/JS) — and sends it back.

**17. Response passes back through WAF, load balancer, CDN**
On the way back, the CDN may cache the response for future users. The WAF may also inspect outgoing responses.

**18. Data travels back across the internet**
Packets travel back through routers, through your ISP, to your machine.

**19. Client-side firewall checks incoming data**
Your machine's firewall checks the incoming response.

---

### BROWSER RENDERING

**20. Browser receives the response**
The browser reads the status code — if 200 OK, it proceeds to render.

**21. Browser parses HTML**
Builds the DOM (Document Object Model) — the structure of the page.

**22. Browser fetches additional resources**
For every image, CSS file, JavaScript file, and font referenced in the HTML, the browser repeats a mini version of the whole process above to fetch each one.

**23. CSS applied**
Styling is applied to the DOM elements.

**24. JavaScript executed**
JS runs, adding interactivity, making additional API calls if needed, and dynamically updating the page.

**25. Page is displayed to the user**

---

### Quick Overview

```
You → Browser Cache → URL Parsing → DNS (multi-step)
→ TCP Handshake → TLS Handshake → Client Firewall
→ ISP Routing → CDN → Server Firewall → WAF
→ Load Balancer → Web Server → Back End → Database
→ Response → CDN Cache → Back to Browser
→ Parse HTML → Fetch Assets → Apply CSS → Run JS → Page rendered
```

All of this typically happens in **under 1 second**. The 7-step version is a good mental model for beginners, but in real-world cybersecurity and networking, every one of these extra layers matters — especially the firewall, WAF, CDN, and TLS steps.

