---
description: SEC522 - SANS
---

## 5. Cutting Edge Web Security

### Serialization Security

- Serialization: programming technique to convert an object into a stream of bytes (or a string) so it can be transmitted or stored. JSON and XML are common serialization formats.
- **Serialization attacks involves sending a chain of serialized objects to the entry point to trigger actions of harmful nature to the system**.
- Defense: **protect and isolate the endpoints, sign data stream, validate the type of data etc**.

### DNS Rebinding

- Break the hostname based security model (Same Origin Policy).
- **Use DNS TTL to force user to go through another round of DNS resolution**, also works with multiple A records.
- Can be used to breach a private network by causing the victim's web browser to access computers at private IP addresses and return the results to the attacker.

#### How It Works

- Attacker registers a domain and delegates it to a DNS server that is under it's control.
- The server is configured to respond with a very short time to live (TTL) record, preventing the DNS response from being cached.
- When the victim browses to the malicious domain, the attacker's DNS server first responds with the IP address of a server hosting a malicious client-side code.
- The malicious client-side code makes additional accesses to the original domain name (allowed by the Same Origin Policy). When the victims browser runs the script, it makes a new DNS request for the domain, and the attacker replies with a new IP address.
- **The attacker DNS could reply with an internal IP address or the IP address of a target somewhere else on the Internet**.

#### Mitigation

- **DNS server filtering**: filter out private IP addresses and loopback IP addresses.
- **Firewall filtering** (e.g [DNSWall](https://www.dnswall.net/)) in the gateway or in the local computer can filter local addresses.
- Web servers can reject HTTP requests with an unrecognized Host header or **use TLS to check for FQDN**.
- Web browsers can resist DNS rebinding with **DNS pinning**: IP address is locked to the value received in the first DNS response (issue: block legitimate use of Dynamic DNS).

### Clickjacking (UI redressing)

- **Trick a user into clicking on something different from what the user perceives**.
- Example: On a clickjacked page, the attackers load another page over the original page in a transparent layer to trick the user into taking actions.
- Multiple categories: Classic (uses hidden layers on web pages), **Cursorjacking** (change the cursor from the location the user perceives), **CookieJacking** (user drag an object that seems harmless, but select the entire content of the cookie), **FileJacking** (select a different file from the user computer) etc.

#### Mitigation

- Browser add-on: [NoScript](https://noscript.net/) (prevents users from clicking on invisible or "redressed" page elements), [NoClickJack](https://www.dnswall.net/) etc.
- `X-Frame-Options` HTTP header to prevent (only) against framing (is superseded by Content Security Policy, if exist)
- `Content Security Policy` (frame-ancestors) to disallow embedding of content
- `Framekiller` include javascript snippet that prevent a page from being within a frame (can be disabled if the page that loads the iframe disallow javascript from running in the frame).

### HTML 5

- Video: browser now has codecs built in -> more attack surface, **codec compromised = browser compromised**
- Web Storage: similar to cookies but stores more information, is accesible via javascript and is not sent back to the server unless the js code does so.
- 2 types of Web Storage: **SessionStorage** (scope: same window or tab, guard against accidental refresh) and **LocalStorage** (persistent accross browser sessions unless the js code deletes the content, Same Origin Access via JavaScript).
- **IndexedDB**: key-value pair storage for structured data with limited queries and searches (allow offline web apps).
- Offline Applications: cached pages serve as offline applications, **cache manifest** files define the content to be cached.
- FileAPI: browser can acccess the local filesystem through JavaScript, can create and access a temporary area of the fs on the client side. Uploads are sent over XHR.
- WebSockets: full duplex, bi-directional communication (ws: and wss:). Uses HTTP header (`Upgrade: websocket` and `Connection: Upgrade`) to establish the socket connection.
- IFrame Sandbox: **Cannot access the DOM of parent, execute scripts or have input forms by default**. `sandbox` attribute.
- Cross Document Messaging: allows IFrames to message each other accross different origins with XSS prevention in mind. Receiver needs to check the origin of the message (domain) and to validate the input message.
- New elements: tel, url, email and search with **built in validation attributes**.
- Geolocation: JavaScript and browser addons can access the users location information: after explicit user approval, only over TLS connection. **Can be easily spoofed**: through proxy tools, browser add-on, browser debugging tools etc.
