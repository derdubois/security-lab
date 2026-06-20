**Routers & Switches — Summary**

---

**What is a Router?**

A router is a dedicated device that connects multiple networks and passes data between them. It operates at **Layer 3 (Network)** of the OSI model and uses a process called routing — creating the best path for data to travel across networks.

When multiple paths exist between two points, the router decides which one to use based on:

- **Shortest path** — fewest hops between source and destination
- **Most reliable path** — least chance of packet loss
- **Fastest medium** — fibre is preferred over copper where available

Routers typically include an admin interface (web or console) that allows configuration of rules like port forwarding and firewalling.

---

**What is a Switch?**

A switch is a dedicated device that connects multiple devices within the same network (typically via Ethernet cables, supporting 3 to 63 devices). Switches come in two types:

**Layer 2 Switch**
- Operates at the Data Link layer
- Forwards **frames** to devices using their **MAC address**
- Has no routing capability — purely responsible for delivering frames within a local network

**Layer 3 Switch**
- More sophisticated — combines switch and some router functionality
- Forwards frames by MAC address (like Layer 2) and also routes **packets** between networks using **IP addresses**
- Cannot do both Layer 2 and Layer 3 at the same time — they are mutually exclusive modes

---

**VLAN (Virtual Local Area Network)**

A VLAN allows devices connected to the same physical switch to be logically separated into different virtual networks. Each group is treated as if it were on a completely separate network, even though the hardware is shared.

Example: A company has Sales and Accounting departments both connected to the same switch. Using VLANs:

- Both departments can access the internet
- They cannot communicate directly with each other
- Rules control exactly what traffic is allowed between groups

This provides **network segmentation and security** without requiring separate physical hardware.

---

**Router vs Switch — Key Differences**

| | Router | Switch |
|---|---|---|
| OSI Layer | Layer 3 | Layer 2 or Layer 3 |
| Connects | Different networks | Devices within one network |
| Uses | IP addresses | MAC addresses (L2) / IP (L3) |
| Main job | Route packets between networks | Forward frames to correct device |
| Extra features | Firewalling, port forwarding | VLANs (L3 only) |

---

**Key point to remember**

Routers connect networks to each other. Switches connect devices within a network. A Layer 3 switch bridges the gap — it can do both, but cannot operate in both modes simultaneously.
