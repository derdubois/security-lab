Summary: ARP (Address Resolution Protocol)
ARP is the protocol that links IP addresses to MAC addresses on a network. It lets devices find each other's physical (MAC) address so they can actually communicate.

Detailed Explanation
Why ARP is Needed
Devices on a network have two identifiers:

IP address — logical address (used for routing)
MAC address — physical address (used for actual delivery on a LAN)

The problem is — when your device wants to send data to 192.168.1.50, it knows the IP, but it doesn't know the MAC address. Without the MAC address, it can't deliver the data on the local network. ARP solves this.

The ARP Cache
Every device keeps a local ARP cache — a small table that stores known IP → MAC mappings so it doesn't have to ask every time.
Example ARP cache:
IP Address       MAC Address
192.168.1.1      AA:BB:CC:DD:EE:01
192.168.1.50     AA:BB:CC:DD:EE:02

How ARP Works — Two Steps
Step 1 — ARP Request (Broadcast)

The device doesn't know the MAC address, so it shouts to everyone on the network:

"Hey everyone! Who has IP address 192.168.1.50? Tell me your MAC address!"

This message goes to all devices on the network (broadcast).
Step 2 — ARP Reply (Unicast)

Only the device that owns that IP responds — privately back to the requester:

"That's me! My MAC address is AA:BB:CC:DD:EE:02"

The requesting device then stores this in its ARP cache for future use, so it doesn't need to ask again.

Full Flow Example
Device A wants to talk to Device B (192.168.1.50)
        ↓
Checks ARP cache → not found
        ↓
Sends ARP Request (broadcast to all devices):
"Who has 192.168.1.50?"
        ↓
All devices receive it, only Device B responds:
"I have 192.168.1.50, my MAC is AA:BB:CC:DD:EE:02"
        ↓
Device A saves it in ARP cache
        ↓
Device A can now send data directly to Device B

Key Points to Remember
ConceptDetailARP RequestBroadcast — sent to all devices on the networkARP ReplyUnicast — sent only back to the requesterARP CacheLocal table storing IP → MAC mappingsScopeOnly works within the same local network (LAN)

Real World Analogy
ARP is like walking into a room full of people and shouting "Who is John?" — everyone hears it, but only John raises his hand and tells you where he's sitting. You then remember his seat for next time.
