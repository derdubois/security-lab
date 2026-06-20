**Networking Fundamentals — Complete Summary**

---

## 1. OSI Model vs TCP/IP Model

Two models describe how network communication works.

The **OSI Model** has 7 layers and is used as a conceptual and educational framework. It is the reference model used for troubleshooting, teaching, and describing where protocols and attacks operate (e.g. "Layer 3 switch", "Layer 7 firewall").

The **TCP/IP Model** has 4 layers and is the actual working model of the internet — the one implemented in every OS, router, and application. It is used in real network programming, protocol development, and operations.

The simple rule: OSI is the model you *reason with*; TCP/IP is the model you *build with*.

---

## 2. OSI Layers — How They Connect

Each layer communicates only with the layer directly above and below it. As data travels down the stack, each layer adds a header (encapsulation). As data travels up on the receiving end, each header is stripped (decapsulation).

| Layer | Name | Data Unit | Key Protocols |
|---|---|---|---|
| 7 | Application | Data | HTTP, HTTPS, FTP, DNS, SSH |
| 6 | Presentation | Data | SSL/TLS, JPEG, ASCII |
| 5 | Session | Data | NetBIOS, RPC |
| 4 | Transport | Segment / Datagram | TCP, UDP |
| 3 | Network | Packet | IPv4, IPv6, ICMP, OSPF |
| 2 | Data Link | Frame | Ethernet, ARP, Wi-Fi |
| 1 | Physical | Bits | Fibre, Copper, Radio |

**Example flow:** A browser request starts as data → receives a TCP header → receives an IP header → wrapped in an Ethernet frame → transmitted as raw bits over a cable.

---

## 3. Packets and Frames

- A **Frame** operates at Layer 2 (Data Link). It contains **MAC addresses** and is used for communication within a local network. Frames do not cross routers.
- A **Packet** operates at Layer 3 (Network). It contains **IP addresses** and is responsible for routing data between different networks.

A packet is carried *inside* a frame on each local network segment. At every router hop, the frame is stripped and a new one is created for the next segment.

---

## 4. TCP — The Three-Way Handshake

TCP is a connection-oriented protocol. Before any data is sent, a reliable connection is established through three steps:

1. **SYN** — Client sends a synchronisation request to the server
2. **SYN-ACK** — Server acknowledges and responds
3. **ACK** — Client confirms, connection is established

TCP guarantees delivery, correct ordering, and error checking. It is used where reliability matters: web browsing, email, SSH, file transfer.

---

## 5. UDP — Connectionless Protocol

UDP sends data immediately with no handshake and no guarantee of delivery. Packets may be lost, duplicated, or arrive out of order.

| | TCP | UDP |
|---|---|---|
| Connection | Required (handshake) | None |
| Reliability | Guaranteed | Not guaranteed |
| Speed | Slower | Faster |
| Use cases | Web, email, SSH | DNS, VoIP, gaming, video streaming |

UDP is chosen when speed matters more than perfect reliability.

---

## 6. Port Forwarding

By default, services running inside a private network (e.g. a web server at 192.168.1.10) are only accessible to devices on that same local network — this is called an **intranet**.

**Port forwarding** is a router configuration that maps an external public IP and port to an internal private IP and port, making the service accessible from the internet.

**Port forwarding vs Firewall:**
- Port forwarding answers: *where does this traffic go?*
- A firewall answers: *should this traffic be allowed through?*

A port can be open via port forwarding but still blocked by a firewall. Both work together.

---

## 7. VPN (Virtual Private Network)

A VPN creates an encrypted tunnel between devices over the public internet, allowing them to communicate securely as if on the same local network.

**How it works:** Two offices (separate networks) connect through a VPN gateway on each side. Together they form a third, virtual private network. Devices on both sides can reach each other's resources without exposing anything to the public internet.

**Benefits:**
- **Geographic connectivity** — remote offices and workers access internal resources as if local
- **Privacy** — all traffic is encrypted; unreadable even if intercepted
- **Anonymity** — ISPs see only traffic to the VPN, not the final destination. Caveat: trust shifts to the VPN provider — a logging VPN provides no real anonymity
- **Security isolation** — vulnerable systems stay off the public internet entirely

**VPN Technologies:**

| Protocol | Encryption | Notes |
|---|---|---|
| PPP | Basic | Handles auth and encryption but cannot route across networks alone |
| PPTP | Weak | Carries PPP over the internet; easy to set up but outdated |
| IPSec | Strong | Industry standard; encrypts at IP level; complex to configure |

---

## 8. Routers

A router is a dedicated device that connects multiple networks and passes data between them. It operates at **Layer 3** of the OSI model.

When multiple paths exist, the router selects the best one based on:
- Shortest path (fewest hops)
- Most reliable path (least packet loss)
- Fastest medium (fibre over copper)

Routers also support admin features like port forwarding and firewalling through a web or console interface.

---

## 9. Switches

A switch connects multiple devices within the same network, typically via Ethernet (supporting 3–63 devices).

**Layer 2 Switch**
- Operates at the Data Link layer
- Forwards frames to devices using MAC addresses
- No routing capability — local delivery only

**Layer 3 Switch**
- Combines switching and basic routing
- Forwards frames by MAC address and routes packets by IP address
- Cannot operate in both Layer 2 and Layer 3 modes simultaneously

**VLAN (Virtual Local Area Network)**
VLANs allow devices on the same physical switch to be logically separated into different virtual networks. Each group is isolated from the others — they can share internet access but cannot communicate directly with each other unless explicitly permitted. This provides network segmentation and security without requiring additional physical hardware.

---

## Quick Reference — Key Devices

| Device | OSI Layer | Connects | Uses |
|---|---|---|---|
| Hub | Layer 1 | Devices (broadcasts to all) | Physical signal only |
| Switch (L2) | Layer 2 | Devices within a network | MAC addresses |
| Switch (L3) | Layer 3 | Devices + networks | MAC + IP addresses |
| Router | Layer 3 | Different networks | IP addresses |
| VPN Gateway | Layer 3+ | Networks over the internet | Encrypted tunnels |
