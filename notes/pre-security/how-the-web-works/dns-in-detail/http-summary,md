## Detailed Summary: HTTP, HTTPS, URLs, and Web Communication

---

### 1. HTTP & HTTPS

**HTTP (HyperText Transfer Protocol)** is the foundational set of rules for communication between a client (your browser) and a web server. Created by Tim Berners-Lee between 1989–1991, it governs the transfer of web content — HTML pages, images, videos, etc.

**HTTPS (HyperText Transfer Protocol Secure)** is the encrypted version of HTTP. It serves two purposes:
- **Confidentiality** — encrypts data so third parties can't read what's being sent or received
- **Authentication** — verifies you're talking to the real server, not an impersonator

---

### 2. URL Structure (Uniform Resource Locator)

A URL is an instruction that tells the browser *how* and *where* to retrieve a resource. It has up to 7 components:

| Part | Purpose | Example |
|---|---|---|
| **Scheme** | Protocol to use | `http://`, `https://`, `ftp://` |
| **User** | Optional login credentials | `user:password@` |
| **Host** | Domain name or IP of the server | `tryhackme.com` |
| **Port** | Connection port (80=HTTP, 443=HTTPS) | `:8080` |
| **Path** | File/resource location on the server | `/blog/article` |
| **Query String** | Extra parameters passed to the path | `?id=1` |
| **Fragment** | Anchor to a specific section on the page | `#section2` |

---

### 3. HTTP Requests & Responses

**A request** is sent by the client to ask the server for a resource. At minimum it's one line, but in practice it includes headers.

Example request breakdown:
```
GET / HTTP/1.1          → Method, path, protocol version
Host: tryhackme.com     → Which website is being requested
User-Agent: Firefox/87  → Browser identity
Referer: ...            → Where the user came from
[blank line]            → Signals end of request
```

**A response** is what the server sends back:
```
HTTP/1.1 200 OK         → Protocol version + status code
Server: nginx/1.15.8    → Server software
Date: ...               → Server date/time
Content-Type: text/html → Type of content being returned
Content-Length: 98      → Size of the response body
[blank line]            → End of headers
<html>...</html>        → The actual content
```

---

### 4. HTTP Methods

These define the *intent* of a request:

| Method | Purpose |
|---|---|
| **GET** | Retrieve/read data from the server |
| **POST** | Submit new data, potentially creating a record |
| **PUT** | Submit data to *update* an existing record |
| **DELETE** | Remove a record from the server |

---

### 5. HTTP Status Codes

Status codes in the response tell the client what happened with their request. They're grouped into 5 ranges:

| Range | Category | Meaning |
|---|---|---|
| 100–199 | Informational | Request received, keep going |
| 200–299 | Success | Request completed successfully |
| 300–399 | Redirection | Resource has moved elsewhere |
| 400–499 | Client Error | Problem with the request itself |
| 500–599 | Server Error | Server failed to handle the request |

**Key codes to memorize:**

- `200 OK` — Success
- `201 Created` — New resource created
- `301 Moved Permanently` — Permanent redirect
- `302 Found` — Temporary redirect
- `400 Bad Request` — Malformed or incomplete request
- `401 Unauthorized` — Login required
- `403 Forbidden` — Access denied even if logged in
- `404 Not Found` — Resource doesn't exist
- `405 Method Not Allowed` — Wrong HTTP method used
- `500 Internal Server Error` — Server-side crash
- `503 Service Unavailable` — Server overloaded or in maintenance

---

### 6. HTTP Headers

Headers are key-value metadata attached to requests and responses to provide extra context.

**Request headers** (client → server):

| Header | Purpose |
|---|---|
| `Host` | Specifies which website on the server to access |
| `User-Agent` | Identifies the browser/software making the request |
| `Content-Length` | Tells the server how much data is being sent |
| `Accept-Encoding` | Lists compression methods the client supports |
| `Cookie` | Sends stored cookie data back to the server |

**Response headers** (server → client):

| Header | Purpose |
|---|---|
| `Set-Cookie` | Instructs the browser to store a cookie |
| `Cache-Control` | Defines how long the browser should cache the response |
| `Content-Type` | Tells the browser what kind of data is being returned |
| `Content-Encoding` | Indicates the compression method used on the response |

---

### 7. Cookies

Cookies are small data files stored in the browser, used to work around a core limitation of HTTP: **HTTP is stateless** — it has no memory of previous requests.

**How they work:**
1. Server sends a `Set-Cookie` header in a response
2. Browser saves the cookie
3. Browser automatically includes that cookie in every future request to the same server

**Primary use case:** Authentication — instead of storing your plain password, a cookie holds a **token** (a unique, non-guessable secret string) that identifies your session securely.

**How to inspect cookies:** Open browser DevTools → Network tab → click any request → Cookies tab.

---

### Key Takeaways

- HTTP is the language of the web; HTTPS is its secure version
- URLs tell the browser exactly where and how to reach a resource
- Every web interaction is a **request–response cycle**
- Methods (GET/POST/PUT/DELETE) define what action is intended
- Status codes tell you what happened to the request
- Headers carry metadata that enriches both requests and responses
- Cookies give stateless HTTP a memory of who you are
