## Summary: The OSI Model

The OSI model is a **7-layer framework** that standardizes how devices send, receive, and interpret data across a network. It ensures that devices from different manufacturers and designs can all communicate with each other by following the same rules at each layer.

---

## The 7 Layers — Detailed

### Layer 7 — Application
The layer **closest to the user**. This is where the actual software and user interaction happens.
- Provides network services directly to applications (browsers, email clients, etc.)
- Protocols: **HTTP, HTTPS, FTP, SMTP, DNS**
- Example: when you type `google.com` in your browser, that request starts here

---

### Layer 6 — Presentation
Responsible for **translating, formatting, and encrypting** data so both sides can understand it.
- Converts data into a format the application layer can accept
- Handles **encryption/decryption** (SSL/TLS)
- Handles **compression**
- Example: converting a JPEG image into binary data that can be sent over the network, or encrypting your HTTPS traffic

---

### Layer 5 — Session
Manages **sessions** — opening, maintaining, and closing communication between two devices.
- Keeps track of which data belongs to which conversation
- Handles **authentication and reconnection**
- Example: when you log into a website, the session layer maintains that connection so you don't have to log in on every click

---

### Layer 4 — Transport
Responsible for **end-to-end communication**, error checking, and how much data is sent at once.
- Breaks data into **segments**
- Two main protocols:
  - **TCP** (Transmission Control Protocol) — reliable, confirms delivery, slower
  - **UDP** (User Datagram Protocol) — fast, no confirmation, used for video/gaming
- Handles **flow control** and **error correction**
- Example: making sure all pieces of a file download arrive correctly and in order

---

### Layer 3 — Network
Handles **logical addressing and routing** — deciding the best path for data to travel across networks.
- Uses **IP addresses**
- Breaks data into **packets**
- Routers operate at this layer
- Protocols: **IP, ICMP, OSPF, BGP**
- Example: your router deciding to send your packet through a specific path to reach Google's servers

---

### Layer 2 — Data Link
Handles **physical addressing** and delivery within the same local network.
- Uses **MAC addresses**
- Breaks data into **frames**
- Switches operate at this layer
- Detects and corrects errors from the physical layer
- Two sublayers:
  - **MAC** (Media Access Control) — controls how devices access the network
  - **LLC** (Logical Link Control) — error checking
- Example: your switch reading the MAC address on a frame and forwarding it to the correct port

---

### Layer 1 — Physical
The actual **hardware layer** — raw bits (0s and 1s) traveling over physical media.
- Cables, fiber optics, radio waves, electrical signals
- Defines voltage levels, cable types, pin layouts, speeds
- Protocols/standards: **Ethernet, USB, fiber optic, Wi-Fi (radio)**
- Example: the CommScope/SYSTIMAX cables you run in your structured cabling work — that's all Layer 1

---

## All 7 Layers Together

```
Layer 7 - Application   → What the user sees (HTTP, FTP, DNS)
Layer 6 - Presentation  → Encryption, formatting, compression
Layer 5 - Session       → Opens/maintains/closes connections
Layer 4 - Transport     → TCP/UDP, segments, error checking
Layer 3 - Network       → IP addresses, packets, routing
Layer 2 - Data Link     → MAC addresses, frames, switches
Layer 1 - Physical      → Cables, signals, raw bits
```

---

## Encapsulation

As data travels **down** the layers (sending), each layer **adds its own header** of information:

```
Application data
        ↓ Layer 4 adds → [TCP Header]     = Segment
        ↓ Layer 3 adds → [IP Header]      = Packet
        ↓ Layer 2 adds → [MAC Header]     = Frame
        ↓ Layer 1      → raw binary bits sent over cable
```

On the **receiving end**, each layer **strips off** its header and passes the data up — this is called **decapsulation**.

---

## Easy Way to Remember the Layers

**Top to bottom (7→1):**
> **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing

| Letter | Layer |
|---|---|
| A | Application |
| P | Presentation |
| S | Session |
| T | Transport |
| N | Network |
| D | Data Link |
| P | Physical |

---
