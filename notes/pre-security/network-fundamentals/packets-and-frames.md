## Summary: Packets and Frames

**Packets** (Layer 3) and **Frames** (Layer 2) are both small pieces of data but serve different purposes:

- A **packet** contains an IP header and data payload — used for routing between networks
- A **frame** wraps the packet and adds MAC addresses — used for delivery within a local network

**The envelope analogy:**
- Packet = the letter inside
- Frame = the envelope carrying it

---

**Why packets exist:**
Instead of sending one large chunk of data, it gets broken into small packets so that:
- Network doesn't get clogged
- If one packet is lost, only that one needs to be resent
- Multiple devices can share the network simultaneously

---

**Key IP Packet Headers:**

| Header | Purpose |
|---|---|
| **Source Address** | IP of the sender |
| **Destination Address** | IP of the receiver |
| **TTL** | Kills the packet after too many hops to prevent it looping forever |
| **Checksum** | Verifies data wasn't corrupted in transit |

---
**Key point:** The packet stays the same the entire journey across the internet, but the frame is **replaced at every router hop** since MAC addresses only work locally.

TCP/IP (The Three-Way Handshake)
TCP is connection-oriented — before sending data, a reliable connection is established via three steps:
StepDirectionFlagMeaning1Client → ServerSYN"I want to connect"2Server → ClientSYN-ACK"Okay, I acknowledge"3Client → ServerACK"Connection confirmed"
After this, data transfer begins. TCP guarantees delivery, ordering, and error checking.

Practical Handshake
This is the hands-on application of Task 2 — typically done using tools like:

Wireshark — capture and inspect SYN / SYN-ACK / ACK packets live
Telnet / Netcat — manually initiate TCP connections
tcpdump — command-line packet capture

You observe the three-way handshake in real traffic to confirm how it looks at the byte level.

UDP/IP
UDP is the connectionless alternative to TCP:

No handshake — data is sent immediately without establishing a connection
No guarantee — packets may be lost, arrive out of order, or be duplicated
Much faster — low overhead makes it ideal for speed-sensitive applications

TCPUDPConnectionRequired (handshake)NoneReliabilityGuaranteedNot guaranteedSpeedSlowerFasterUse caseWeb, email, SSHDNS, VoIP, gaming, video streaming
