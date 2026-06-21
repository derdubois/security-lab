## Detailed Summary: How Websites Work & Basic Web Security

---

### 1. How a Website Works

When you visit a website, your browser sends a **request** to a **web server** — a dedicated computer somewhere in the world. The server processes that request and sends back **data** that your browser uses to render the page visually.

Every website has two core sides:

| Side | Also Called | Role |
|---|---|---|
| **Front End** | Client-Side | What the browser renders and the user sees |
| **Back End** | Server-Side | The server that processes requests and returns responses |

---

### 2. The Three Building Blocks of a Website

| Technology | Purpose |
|---|---|
| **HTML** | Defines the *structure* and content of the page |
| **CSS** | Controls *appearance* — colors, layout, fonts, styling |
| **JavaScript** | Adds *interactivity* and dynamic behavior |

---

### 3. HTML — Structure of a Web Page

HTML (HyperText Markup Language) uses **elements** (also called tags) to tell the browser how to display content.

**Core structure of every HTML document:**

```html
<!DOCTYPE html>        → Declares the document as HTML5
<html>                 → Root element; everything lives inside this
  <head>               → Page metadata (title, links, scripts)
  </head>
  <body>               → Visible content shown in the browser
    <h1>Heading</h1>   → Large heading
    <p>Paragraph</p>   → Text paragraph
  </body>
</html>
```

**Key concepts in HTML:**

- **Tags** — building blocks like `<button>`, `<img>`, `<h1>`, `<p>`
- **Attributes** — extra properties added inside a tag:
  - `class` — used for styling, multiple elements can share the same class
  - `id` — unique identifier per element, used for styling and JS targeting
  - `src` — specifies the source path of an image or script

```html
<p class="bold-text">Styled paragraph</p>
<img src="img/cat.jpg">
<p id="example" attribute1="value1" attribute2="value2">
```

> You can view any website's HTML by right-clicking → **"View Page Source"**

---

### 4. JavaScript — Interactivity & Dynamic Behavior

JavaScript (JS) makes pages **interactive and dynamic**. Without it, every page would be completely static — no animations, no real-time updates, no clickable logic.

**How JS is included in a page:**
```html
<!-- Inline -->
<script>
  // JS code here
</script>

<!-- External file -->
<script src="/location/of/file.js"></script>
```

**Key capabilities:**

- **DOM Manipulation** — JS can find and modify HTML elements in real time:
  ```javascript
  document.getElementById("demo").innerHTML = "Hack the Planet";
  ```
  This finds the element with `id="demo"` and changes its content.

- **Event Handling** — HTML elements can trigger JS when interacted with:
  ```html
  <button onclick='document.getElementById("demo").innerHTML = "Button Clicked";'>
    Click Me!
  </button>
  ```
  Events like `onclick` and `onhover` execute JS code when the user interacts with the element.

---

### 5. Security Vulnerability #1 — Sensitive Data Exposure

**What it is:** A vulnerability where a website accidentally leaves sensitive information visible in its **frontend source code** — plain text that any user can read.

**How it happens:**
- Developers forget to remove debug info, credentials, or hidden links before deploying
- Sensitive data is left inside HTML comments or JavaScript variables

**What attackers look for in page source:**
- Hardcoded login credentials
- Hidden links to private/admin pages
- API keys or tokens
- Internal file paths

**Impact:** An attacker can use exposed credentials to log in to other parts of the application or access backend systems.

> **First step in any web security assessment:** always review the page source code for exposed data.

---

### 6. Security Vulnerability #2 — HTML Injection

**What it is:** A vulnerability that occurs when **user input is displayed on the page without being sanitized** (filtered/cleaned). The browser treats the injected text as real HTML and renders it.

**How it works:**

1. A website takes user input (e.g. a name field) and displays it on the page
2. The site fails to strip or escape HTML tags from the input
3. An attacker submits raw HTML like `<h1>Hacked</h1>` instead of a name
4. The browser renders it as actual HTML — the attacker now controls part of the page

**Example flow:**
```
User types: <h1>You've been hacked</h1>
Page renders it as a real heading instead of plain text
```

**Why it's dangerous:**
- Attacker can alter the visual appearance of the page for other users
- Can be escalated to **JavaScript injection**, enabling more serious attacks
- Opens the door to **database injection** — where malicious input manipulates backend queries to bypass authentication

**The fix — Input Sanitization:**
- Never trust user input
- Strip or escape all HTML/JavaScript tags before using input in any page logic
- Validate input on both the front end AND back end

---

### Key Takeaways

| Concept | Summary |
|---|---|
| Front End / Back End | Every site has a client side (what you see) and server side (what processes requests) |
| HTML | Defines page structure using tags and attributes |
| CSS | Controls visual styling |
| JavaScript | Adds interactivity and real-time page updates |
| Sensitive Data Exposure | Credentials or private links left in source code — always check page source |
| HTML Injection | Unfiltered user input rendered as HTML — always sanitize input |

**Core security principle from this topic:**
> **Never trust user input** — always sanitize and validate everything before it touches your page or database.
