# Networking Fundamentals — How It Works & the Protocols Involved

A study reference covering the layered model, the core protocols at each layer, how a
packet actually travels, and the security relevance of each layer.

---

## 1. The layered model

Networking is built in **layers**. Each layer does one job and only talks to the layer
directly above and below it through a defined **protocol** (an agreed set of rules for
formatting and exchanging data). This separation means you can swap Wi-Fi for Ethernet
without touching HTTP, or swap HTTP for SSH without touching IP.

### OSI model (7 layers — the reference taxonomy)

| # | Layer | PDU (unit of data) | Examples | Device |
|---|-------|--------------------|----------|--------|
| 7 | Application | Data | HTTP, DNS, SSH, SMTP | — |
| 6 | Presentation | Data | TLS, encoding, compression | — |
| 5 | Session | Data | session setup/teardown | — |
| 4 | Transport | Segment (TCP) / Datagram (UDP) | TCP, UDP | — |
| 3 | Network | Packet | IP, ICMP | Router |
| 2 | Data link | Frame | Ethernet, 802.11, ARP | Switch |
| 1 | Physical | Bits | copper, fiber, radio | Cable / NIC |

### TCP/IP model (4 layers — what's actually implemented)

The OSI model is the teaching/vocabulary standard; real stacks follow the simpler TCP/IP
model, which collapses OSI's layers into four:

| TCP/IP layer | Maps to OSI | Job |
|--------------|-------------|-----|
| Application | 5–7 | Apps you interact with |
| Transport | 4 | Reliable/unreliable delivery + ports |
| Internet | 3 | Logical addressing + routing |
| Link | 1–2 | Local delivery over physical media |

> **Why layer numbers matter in practice:** people refer to gear and attacks by OSI
> layer. *"Layer 2 device"* = switch (forwards by MAC). *"Layer 3 device"* = router
> (forwards by IP). *"Layer 7 firewall"* = application-aware (can read HTTP). *"Layer 4
> load balancer"* only sees IP:port.

### Key terms

- **PDU (Protocol Data Unit):** the name for the chunk of data at each layer — *frame*
  (L2), *packet* (L3), *segment*/*datagram* (L4).
- **Encapsulation:** as data goes *down* the stack, each layer wraps the layer above in
  its own **header** (and sometimes trailer). Like nested envelopes.
- **Decapsulation:** the receiver unwraps in reverse, going *up* the stack.
- **Header / Payload:** the header is the layer's own control info; the payload is
  everything from the layer above.
- **MTU (Maximum Transmission Unit):** largest payload a link can carry in one frame —
  typically **1500 bytes** on Ethernet. Bigger data is **fragmented**.

This is exactly the tree you expand in **Wireshark**: `Frame → Ethernet II → IPv4 → TCP → HTTP`.

---

## 2. The layers, in detail

### Link / Physical layer (L1–L2)

Moves bits across a single local network segment.

- **Frame:** the L2 PDU. Carries source + destination **MAC address**.
- **MAC address:** 48-bit hardware address burned into the **NIC** (Network Interface
  Card), e.g. `00:1A:2B:3C:4D:5E`. Unique per interface, used only on the local segment.
- **Ethernet (IEEE 802.3):** wired LAN standard. **802.11** is the Wi-Fi equivalent.
- **Switch:** L2 device. Builds a **MAC address table** and forwards frames only out the
  port where the destination lives (unlike a dumb **hub**, which floods everything).
- **ARP (Address Resolution Protocol):** maps a known **IP → unknown MAC**. The host
  broadcasts *"who has 192.168.1.1?"* and the owner replies with its MAC. ARP is the glue
  between L3 (IP) and L2 (MAC). **No authentication → ARP spoofing/poisoning attacks.**
- **Broadcast domain:** set of devices that receive each other's broadcasts (one per
  **VLAN**). **Collision domain:** segment where frames can collide (each switch port is
  its own).
- **VLAN (Virtual LAN):** logically separates one physical switch into multiple isolated
  L2 networks.

### Internet / Network layer (L3)

Gets a packet across *different* networks, hop by hop.

- **Packet:** the L3 PDU. Carries source + destination **IP address**.
- **IP (Internet Protocol):** logical addressing. **IPv4** = 32-bit (`192.168.1.10`).
  **IPv6** = 128-bit (`2001:db8::1`). IP is **connectionless** and **best-effort** — no
  guarantee of delivery or order (that's TCP's job, above).
- **Subnet mask / CIDR:** splits an IP into **network** and **host** portions.
  `/24` = `255.255.255.0` → 256 addresses, ~254 usable hosts.
- **Default gateway:** the router IP a host sends packets to when the destination is
  *outside* its own subnet.
- **Routing table:** how a router decides the **next hop** for a destination network.
- **NAT (Network Address Translation) / PAT:** rewrites **private IPs**
  (`10.x`, `172.16–31.x`, `192.168.x`) to one **public IP** on the way out, tracking
  connections by port. This is why your whole LAN shares one public address.
- **ICMP (Internet Control Message Protocol):** diagnostics + errors, *not* user data.
  - `ping` = ICMP **Echo Request / Echo Reply**.
  - `traceroute` works by sending packets with increasing **TTL** and reading the
    **Time Exceeded** replies from each hop.
- **TTL (Time To Live):** hop counter decremented by each router; hits 0 → packet dropped.
  Prevents routing loops.

### Transport layer (L4)

Delivers data to the correct **application** on a host, identified by a **port**.

- **Port:** 16-bit number (0–65535) identifying a service/connection on a host.
- **Socket:** the pair `IP:port` — the unique endpoint of a connection.
- **TCP (Transmission Control Protocol):** **connection-oriented, reliable, ordered.**
  - **Three-way handshake** to open a connection: `SYN → SYN-ACK → ACK`.
  - **Sequence & acknowledgment numbers** track bytes so lost segments are
    **retransmitted** and reordered.
  - **Flags:** `SYN` (start), `ACK` (acknowledge), `FIN` (graceful close), `RST` (abrupt
    reset), `PSH`, `URG`.
  - **Flow control** (window size) + **congestion control** prevent overwhelming the
    receiver/network.
  - **MSS (Maximum Segment Size)** = MTU minus IP+TCP headers.
- **UDP (User Datagram Protocol):** **connectionless, unreliable, no handshake.** Lower
  overhead, lower latency. Used by DNS, DHCP, VoIP, video, games — speed over guarantees.

| | TCP | UDP |
|---|-----|-----|
| Connection | Handshake first | None |
| Reliability | Guaranteed, ordered | Best-effort |
| Overhead | Higher | Lower |
| Use cases | Web, SSH, email, file transfer | DNS, streaming, gaming, VoIP |

### Application layer (L7)

Protocols the user/software actually speaks. Each typically rides a **well-known port**.

| Protocol | Port | Transport | Purpose |
|----------|------|-----------|---------|
| HTTP | 80 | TCP | Web (plaintext) |
| HTTPS | 443 | TCP | Web over TLS (encrypted) |
| DNS | 53 | UDP/TCP | Name → IP resolution |
| DHCP | 67/68 | UDP | Auto IP assignment |
| SSH | 22 | TCP | Encrypted remote shell |
| FTP | 20/21 | TCP | File transfer (plaintext) |
| SMTP | 25 | TCP | Sending email |
| POP3 / IMAP | 110 / 143 | TCP | Retrieving email |
| Telnet | 23 | TCP | Remote shell (plaintext — avoid) |
| RDP | 3389 | TCP | Remote desktop |

- **DNS (Domain Name System):** hierarchical name resolution — your **resolver** queries
  up through **root → TLD (.com) → authoritative** servers. Records: `A` (IPv4),
  `AAAA` (IPv6), `MX` (mail), `CNAME` (alias), `NS`, `TXT`.
- **DHCP:** hands a client its **IP, subnet mask, default gateway, and DNS server** via
  the `DORA` exchange — **D**iscover → **O**ffer → **R**equest → **A**cknowledge.
- **TLS (Transport Layer Security):** sits between L4 and L7. Its handshake negotiates
  encryption keys and validates the server **certificate**, turning HTTP into HTTPS.

---

## 3. Full lifecycle — what happens when you open a website

```
1. DHCP   → host boots, gets IP + mask + gateway + DNS server (DORA)
2. DNS    → "example.com" resolved to an IP (UDP query to resolver)
3. ARP    → find the MAC of the default gateway (IP → MAC on the LAN)
4. IP     → packet routed hop-by-hop toward the destination network
            (NAT rewrites private IP → public IP on the way out)
5. TCP    → three-way handshake to port 443 (SYN → SYN-ACK → ACK)
6. TLS    → handshake negotiates keys + validates certificate
7. HTTP   → encrypted GET request sent; server returns the response
```

Each step adds its header on the way down (encapsulation) and is stripped on the way up
(decapsulation) at the other end.

---

## 4. Security relevance (per layer)

Every layer is its own attack surface — useful framing for TryHackMe rooms and Wireshark
analysis, since you're almost always reasoning at *one specific layer*.

| Layer | Example threat | Why |
|-------|----------------|-----|
| L2 (ARP/Ethernet) | **ARP spoofing / MITM** | ARP has no authentication |
| L3 (IP/ICMP) | IP spoofing, ICMP tunneling | IP source can be forged |
| L4 (TCP) | **SYN flood (DoS)** | half-open handshakes exhaust resources |
| L7 (DNS) | **DNS poisoning / hijacking** | spoofed responses redirect traffic |
| L7 (plaintext) | Credential sniffing | HTTP/FTP/Telnet send data in the clear |

Defenses map to the same layers: **TLS/SSH** encrypt L7, **VPNs** tunnel L3, **switch port
security / dynamic ARP inspection** protect L2, and **firewalls** filter at L3/L4 (or L7
if application-aware).

---

## 5. Glossary (quick reference)

- **Bandwidth** — max data rate of a link (bits/sec).
- **Latency** — time for a packet to travel end to end.
- **Broadcast** — one-to-all on a segment. **Unicast** — one-to-one. **Multicast** — one-to-group.
- **Gateway** — exit point from a local network to other networks.
- **NIC** — network interface card (holds the MAC).
- **Loopback** — `127.0.0.1` (`localhost`), the host talking to itself.
- **Ephemeral port** — temporary high-numbered client-side port (49152–65535).
- **Stateless** — protocol that keeps no memory between requests (e.g. HTTP, UDP).
