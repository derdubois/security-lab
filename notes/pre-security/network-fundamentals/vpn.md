**Virtual Private Networks (VPN) — Summary**

---

**What is a VPN?**

A Virtual Private Network (VPN) is a technology that creates a secure, encrypted tunnel between devices over the public internet. 
Devices connected through this tunnel form their own private network, even if they are physically in different locations.

---

**How it works**

A VPN connects two or more networks through an encrypted tunnel. For example, two offices (Network #1 and Network #2) 
can be joined via VPN to form a virtual shared network (Network #3). Devices in both offices can access each other's resources — servers, printers, 
files — as if they were on the same local network, while remaining invisible to the public internet.

---

**Benefits**

- **Geographic connectivity** — Offices and remote workers in different locations can access shared internal resources without exposing them to the internet.
- **Privacy** — All traffic is encrypted. Even if intercepted, the data is unreadable. Especially useful on public Wi-Fi where no encryption exists by default.
- **Anonymity** — Your ISP only sees traffic going to the VPN, not your actual destination. Important caveat: if the VPN provider logs your activity, anonymity is lost — trust shifts from your ISP to the VPN provider.
- **Security isolation** — Sensitive systems can be kept off the public internet entirely, accessible only through the VPN.

---

**VPN Technologies**

| Protocol | Encryption | Notes |
|---|---|---|
| PPP | Basic | Handles authentication and encryption but cannot travel across networks alone |
| PPTP | Weak | Carries PPP traffic across the internet; easy to set up but outdated and insecure |
| IPSec | Strong | Encrypts at the IP level; industry standard for enterprise VPNs; harder to configure |

---

**Key point to remember**

A VPN does not make you truly anonymous on its own — it shifts your trust from your ISP to the VPN provider. 
A provider that logs your data offers no real privacy benefit.
