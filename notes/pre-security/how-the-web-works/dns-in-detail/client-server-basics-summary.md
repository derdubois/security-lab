## Summary

This material introduces the **client-server model** — how one computer uses services provided by another — using a pizza takeaway analogy, then applies those concepts concretely to **HTTP(S)** and web browsing.

The big picture: computers used to work in isolation, but networks like ARPANET, CYCLADES, NPL, and NSFNET connected them so they could share information and resources. Once connected, systems specialized — some offer services, others consume them. That's the client-server relationship.

## The pizza analogy (Document 1)

Alice wants pizza, Bob fetches it from Luigi's. Each part of that errand maps onto a networking concept:

**Client / Server / Service** — Alice is the *client* (she wants something), Luigi's is the *server* (it provides the service). Bob carries the request between them. In real terms: your browser is the client, the website's machine is the server. The key rule is that **the client always initiates the request** — the server never reaches out first.

**Request / Response** — Alice's order is the *request*; the pizza (or an error like "no pepperoni left") is the *response*. Importantly, the request is really aimed at Luigi's, not at Bob — Bob just delivers it. If the request is malformed or the resource doesn't exist, you get an error response instead of what you wanted.

**Protocol** — Bob represents the *protocol*: the agreed rules for communication. Alice speaks a language Luigi's understands and orders from a known menu. A protocol defines five things: which commands exist (e.g. `get`), how a request is structured, what syntax/language is used, what response a valid request gets, and what response a faulty request gets.

**Port** — Luigi's makes everyone enter through a specific door. A *port* is that door — it identifies a specific service on a machine. One server can run many services at once (takeaway, dine-in, delivery = different doors), each on its own port, so the client must connect to the right one.

**DNS** — Bob only knew the *name* "Luigi's," which isn't enough to drive there, so his GPS converted the name into coordinates. **DNS (Domain Name Service)** does the same: it resolves a name like `tryhackme.com` into an **IP address** — the machine's actual "street address" on the network.

## HTTP(S) and the GET request (Document 2)

**HTTP(S)** is the protocol of the World Wide Web, and it's **stateless** — each request is handled on its own, with no memory of previous requests. That's why websites add statefulness *on top* of the protocol: when you log in, the server issues a **session identifier** (stored in a cookie or token) that rides along with every later request. Without it, you'd have to log in again on every single page load.

HTTP defines **9 core methods** (HTTP's word for commands): GET, POST, PUT, DELETE, PATCH, HEAD, OPTIONS, CONNECT, TRACE. The text focuses on **GET**, the method used to *retrieve* a resource. When you type `https://tryhackme.com` into a browser, the browser silently builds a proper GET request using your input plus fields defined by the HTTP spec, sends it, and the server replies with a **status code** plus the requested content.

The lab walks through inspecting a real GET request in Firefox Dev Tools (F12 → Network tab → reload). The fields it highlights:

- **Scheme** — which protocol was used (HTTP or HTTPS)
- **Host** — the name of the machine you're requesting from
- **Filename** — which file was requested; `/` resolves to `index.html`
- **Address** — the IP serving the site (here `127.0.0.1`, meaning it's hosted locally on the same machine — the "loopback" address)
- **Status** — whether it worked; `200 OK` means success

Finally, every response has two parts: the **response header** (metadata about the response) and the **response body** (the actual content — in this case the page's HTML).

---

A couple of things worth filing away for your notes since they tend to come up later in TryHackMe and in interviews: `127.0.0.1` is the *loopback* address (a machine referring to itself), and the GET-vs-POST distinction (GET retrieves, POST submits/creates) is one of the most common practical follow-ups. Want me to expand the HTTP methods section or the DNS resolution flow into something more detailed for your Obsidian notes?
