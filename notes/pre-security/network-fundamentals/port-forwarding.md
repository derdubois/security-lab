## Summary — Port Forwarding

---

### What is Port Forwarding?

Port forwarding is a router configuration that allows external devices (on the internet) to reach a specific service running inside a private network by 
mapping a public IP + port to an internal IP + port.

---

### Without Port Forwarding (Intranet only)

```
[PC 1] ──┐
          ├── [Router] ── (Internet) ✗
[PC 2] ──┘
[Server 192.168.1.10:80]
```

- The web server is only reachable by devices **on the same local network**
- This is called an **intranet** — private, internal access only
- No outside machine can reach it

---

### With Port Forwarding (Public access)

```
(Internet) ── 82.62.51.70:80 ──► Router ──► 192.168.1.10:80
```

- The router is told: *"any traffic arriving on port 80 → forward it to 192.168.1.10:80"*
- Now **anyone on the internet** can reach the web server via the public IP
- The internal server's private IP stays hidden

---

### Port Forwarding vs Firewall

These are often confused — here's the distinction:

| | Port Forwarding | Firewall |
|---|---|---|
| **Role** | Routes traffic to the right internal host | Decides if traffic is *allowed* through |
| **Question it answers** | *Where* does this traffic go? | *Should* this traffic pass? |
| **Configured on** | Router | Router / dedicated firewall device |

> A port can be **open via port forwarding** but still **blocked by a firewall** — both work together.

---

### Key Takeaway

Port forwarding is what bridges a **private internal service** to the **public internet**. It's configured at the router level and is fundamental to understanding how services like web servers, game servers, and remote desktop become publicly accessible — and also why misconfigured port forwarding is a common attack surface in cybersecurity.
