## Summary: DHCP (Dynamic Host Configuration Protocol)

DHCP is the protocol that **automatically assigns IP addresses to devices** when they join a network, so you don't have to configure them manually.

---

## Detailed Explanation

### Two Ways to Get an IP Address

| Method | Description |
|---|---|
| **Manual (Static)** | Admin manually types in the IP address on the device — used for servers, printers, routers |
| **Automatic (DHCP)** | Device gets an IP assigned automatically from a DHCP server — used for most everyday devices |

---

### The 4-Step DHCP Process

**Step 1 — DHCP Discover**
A new device joins the network but has no IP yet. It broadcasts to everyone:
> *"Is there a DHCP server here? I need an IP address!"*

**Step 2 — DHCP Offer**
The DHCP server hears the request and replies:
> *"Yes I'm here! You can use IP address 192.168.1.50, here's your offer."*

**Step 3 — DHCP Request**
The device replies back confirming it wants that address:
> *"Great, I'll take 192.168.1.50 please!"*

**Step 4 — DHCP ACK (Acknowledgement)**
The DHCP server confirms and finalizes the assignment:
> *"Done! 192.168.1.50 is yours. You're good to go."*

---

### Full Flow Diagram

```
Device joins network (no IP yet)
        ↓
DHCP Discover → broadcast to entire network
        ↓
DHCP Offer ← server replies with available IP
        ↓
DHCP Request → device confirms it wants that IP
        ↓
DHCP ACK ← server confirms, IP is now assigned
        ↓
Device is now on the network with a working IP
```

---

### What DHCP Also Assigns
It's not just an IP address — a DHCP server typically also gives the device:

| Setting | Purpose |
|---|---|
| **IP Address** | Device's identity on the network |
| **Subnet Mask** | Defines the size of the network |
| **Default Gateway** | The router's address for reaching other networks |
| **DNS Server** | For resolving domain names like google.com |

---

### Real World Analogy
DHCP is like arriving at a hotel:
- You walk in with no room *(no IP)*
- You ask reception "any rooms available?" *(Discover)*
- Reception says "room 205 is free" *(Offer)*
- You say "I'll take it" *(Request)*
- Reception hands you the key *(ACK)*

The hotel manages all room assignments so guests don't have to figure it out themselves.

---

### Key Point — Lease Time
DHCP addresses are not permanent — they have a **lease time** (e.g. 24 hours). When it expires, the device must renew its IP. This is why your IP can sometimes change between sessions, unless a **static** or **reserved** IP is set.
