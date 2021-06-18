---
description: SANS - SEC522
---

# Defending Web Applications

## 1. Web Fundamentals And Security Configurations

### Web Applications Attacks and Trends

#### Core Goals in Security (CIA)

- **Confidentiality**: only allow access to data for which the user is permitted.
- **Integrity**: ensure data is not tampered or altered by unauthorized users
- **Availability**: ensure systems and data are available to authorized users when they need it.

#### Recent attack trends

- **API Hacks**: Authentication and access control issues.
- **Cryptomining**: On the web server or in the browser (see [Coinhive](https://web.archive.org/web/20190429040938/https://coinhive.com/)).
- **Credential Stuffing**: Data breaches etc. (see [have i been pwned?](https://haveibeenpwned.com/))
- **Malicious Script Injection**

### HTTP Basics

#### Introduction

- Development of HTTP was initiated by **Tim Berners-Lee** at CERN in 1989.
- [HTTP/1.1](https://www.w3.org/Protocols/rfc2616/rfc2616.html): request–response protocol in the client–server computing model.
- Request message: request line (e.g. `GET /images/logo.png HTTP/1.1`) + header fields (e.g. `Accept-Language: en`) + blank line + optional body.
- Headers order is not specified in RFC and may **leak the web server used** (Apache, Nginx, IIS etc.).
- For sending sensible data, prefer POST over GET requests, as **URLs gets logged and cached** all the time.

#### HTTP Methods

- Basics: GET, POST, HEAD, DELETE, PUT, PATCH.
- **OPTIONS**: Returns the methods supported by the server. Commonly used for fingerprinting of web server.
- **TRACE**: For testing purposes, the server echoes back the request body. The client can examine whether intermediate servers altered the request. Can impact the security of the server and its hosted apps.
- **CONNECT**: Used to establish a tunnel (such as TLS).

#### HTTP Response Status Code

- **1xx**: Informational, protocol upgrades
- **2xx**: Success
- **3xx**: Redirection
- **4xx**: Client Error
- **5xx**: Server Error

#### Referer

- Typo of "Referrer" that was mispelledd during the RFC phase.
- Browser lets web server know the previous page from which a link was followed (optional).
- **Can be easily forged**.
- **Referrer Policy** as an HTML meta tag or response header to control referer behavior (`Referrer-Policy: origin`).

#### User-Agent

- Tell what browser, version and OS the user is using.
- **Can be easily spoofed**.
- To be replaced by **Client Hints** to protect client's privacy better.

#### HTTP Capabilities

- **Compression**: saves bandwidth (`Accept-Encoding: gzip, deflate`).
- **Chunked Encoding**: allow the server to send data as soon as possible, no `Content-Length` header sent.
- **Range request header**: Client ask for a specific portion of the document to be returned (`Range: bytes=0-499,500-1000`).

#### HTTP/2

- Backward compatible with HTTP 1.1, developed by google as **SPDY** (speedy).
- Single TCP connection to transport the HTTP data (one highway where many transmissions can happen).
- Only implemented with TLS.
- **HPACK**: Header compression in a safe way.
- **Server push**: server sends data to the client without the client requesting the specific resource.

#### HTTP/3

- **HTTP/2 over UDP**, developed by google as **QUIC** (Quick UDP Internet Connections).
- Replace the limitation on TCP to further speed up connections.
- Always encrypted as part of protocol negotiation.

### Web Foundations Overview

#### Authentication

- **Basic Auth**: a request contains a header field in the form of `Authorization: Basic <credentials>`, where `credentials` is the Base64 encoding of ID and password joined by a single colon `:`. No encryption unless used over TLS.
- **Digest Auth**: an improved version of Basic Auth as passwords are not sent over the wire. It is based on challenge-response authentication (MD5 hashing with usage of **nonce** values to prevent **replay attacks**).
- **Certificate Auth**: both client and server own certificates signed by a CA. Clients and server mutually verify one another identity.
- **Integrated Windows Auth**: Uses Kerberos (strong) or NTLM (weak) authentication in the OS. Does not work through most HTTP proxies.
- **Form-Based Auth**: Does not rely on HTTP headers, a password field in the HTML form component.

#### Sessions

- Stateless nature of HTTP: all HTTP requests are independent of one another.
- HTTP Session: use of a unique session ID set by the server to regulate access, identify users etc.
- Session attacks: **interception, prediction, brute force, surf jack etc.**.
- Cookie: Used between client and server to keep track of informations. `Set-Cookie` header sent by the server.

#### Cookie parameters

- Name and value
- **Expiration**: The cookie will be stored until this time expires.
- **Domain**: The cookie will be sent only to this particular domain.
- **Path**: The cookie will be sent only at this particular path (URL).
- **Secure**: The cookie will be sent only over TLS.
- **HttpOnly**: JavaScript may not access the cookie (stops XSS).
- **SameSite**: Determines whether the cookie is sent with cross-origin requests.

#### Session Best Practices

- Use cookie to store session token.
- Use proper timeout for inactivity.
- Store all session data on the server.
- Use TLS to protect session ID.
- Use built-in session toolkit.

#### Input to Web Apps

- URL
- Header fields
- Cookie
- URL query string (GET method)
- HTTP body (POST method)
- Other systems

### Architecture and Defense-in-Depth

#### Architecture

- Proxy servers: foward HTTP traffic from clients to servers (reverse proxy do the opposite). Features: filter based on policies, caching, auth, manipulation etc.
- Load balancers and CDN.
- DNS: often subject to network-based attack (DDOS, spoofing, hijacking).
- **Web Application Firewall** (WAF): by inspecting HTTP traffic, it can prevent attacks exploiting a web application's known vulnerabilities, such as SQL injection, cross-site scripting (XSS), file inclusion, and improper system configuration (e.g CloudFlare WAF, Akamai WAF, Fastly WAF etc.).
- **Runtime Application Self-Protection** (RASP): uses runtime instrumentation to detect and block computer attacks by taking advantage of information from inside the running software (e.g. [sqreen](https://www.sqreen.com), [openrasp](https://github.com/baidu/openrasp)).
- Web servers and API gateways.
- Backend Storage (Database and Storage).

#### Defense-In-Depth

- Contains **multiple layers of defense**.
- Increase the difficulty of compromising critical hosts.
- **Buys time to detect and respond to attacks**.
- Relevant in web applications.

### Web Infrastructure Security

- **Directory browsing**: gives the user a listing of files in a directory, potential leak of important information. Use tools such as Wikto, OWASP DirBuster, w3bfukkor and web spiders.
- **Data leakage**: .git or .svn folders, HTML code comments etc.
- **Isolation**: network level, service/app level, permission level.
- **Reduce attack surface**: public vs private APIs, allowed HTTP methods, network IPs and service ports etc.
- **Detect and patch vulnerabilities** in OS, libraries, components, containers etc.
- Patch often, patch regularly

### Managing Configurations for Web Apps

- Configuration management tools (e.g. Ansible)
- OS Instrumentation framework (e.g. [osquery](https://osquery.io/): SQL powered operating system instrumentation, monitoring and analytics.)
- Cloud service configuration (e.g. Cloud formation, Terraform etc.)
- Cloud configuration validation (e.g. AWS config, Cloud asset inventory etc.)
- Permission configuration (e.g. IAM role etc.)
- **Server Side Request Forgery** (SSRF) vulnerability: Attacker can instruct the server to fetch and return data from a URL accessible by the server.

## 2. Defense Against Input-Related Threats

### Input-Related Flaws

#### Buffer Overflow

- Difficult to exploit in web apps: most web scripting languages are immune, lack of error messages etc.
- Likely to cause only a denial-of-service
- Mitigation: validate length of input, limit size of arrays/buffers to specific length.

#### OS Command Injection

- Badly designed apps use user input as OS commands or command-line args.
- Mitigation: don't do it, **input validation** (block semicolon, backtick, pipe etc.), use WAF devices etc.

### HTTP Response Splitting

- Allows attacker to **inject information into HTTP response header**.
- Input that a web server would put directly into a header, but: `test\r\nSet-Cookie:session=AAA`.
- Very hard vulnerability to detect and test.
- Not that severe but enable other kind of attacks: session fixation, proxy cache poisoning, XSS etc.
- Mitigation: input validation (reject CR/LF sequence etc.), use **Network Intrusion Prevention System** (NIPS).

### SQL Injection

#### The attack

- User input gets passed, without checking, to the backend SQL database.
- `SELECT number FROM table WHERE name = '$var'` -> if $var is ` OR 1 = 1 --` it will return everything.
- Potential to extract data, alter data, control the host running the db and jumping to other hosts.
- Attackers can plan the injection based on common database error messages OR do "blind" injection

#### Mitigation

- Filter/Validate/Escape input.
- Use language built-in mitigation.
- Use parameterized queries (pre-construct the static part of the query) and stored procedures.
- Tighten database permission and harden the SQL server.
- Hide SQL error message to end user and log everything.

### Cross-Site Request Forgery (CSRF)

#### The attack

- Also known as **one-click attack** or **session riding**.
- The end user is tricked by an attacker into submitting a web request that they did not intend. The user may be already logged in / already have a session into that site.
- Attacker uses iframe, hidden inputs, images, script tag etc.

#### Mitigation

- Make all forms leading to action accept only POST requests (not full mitigation).
- Session timeout: reduce the window of opportunity (not full mitigation).
- Use HTTP Referer (not full mitigation, but can help detect an attack).
- CAPTCHA provides strong protection but not practical for every form.
- **Anti-CSRF Token**: generate a token for every form with the hash of the name of the form + secret + session ID (strong protection).
- **SameSite=strict Cookie** to only send cookie in same origin-based requests (strong protection).

### HTTP Parameter Pollution

- HTTP allows multiple parameters of the same name (`var=number1&var=number2`).
- Different servers and/or application platforms handle it differently.
- Possiblities: override hardcoded parameters, change app behavior, modify existing variables.
- Mitigation: block multiple parameter instances, validate on multiple parameters when needed, constraint input.

### Cross-Site Scripting (XSS)

#### The attack

- Trick client browser to execute malicious scripts and HTML code. The victim usually visit a website with already injected malicious code, or click a link and get malicious code from it.
- Cause of XSS: **user input to the web app is displayed back in its original form**.
- Possibilities: discosure of cookies, force redirection, modify content of the webpage, run custom script etc.
- **Reflection XSS**: nothing is stored, the attacker sends a crafted URL with malicious scripts embedded.
- **Persistent XSS**: malicious payload is stored on a server where victims visit pages.
- **Local XSS**: injected scripts does not traverse tp the server but is placed in the scripts in the HTML page.

#### Mitigation

- **Input Filtering**: filter HTML characters and watch for encoding.
- **Output Encoding**: escape or encode all HTML entites to be sent to the clients
- Input Filtering and Output Encoding is hard and have pitfalls, see [Cross Site Scripting Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)

### Input Validation Strategy

- Path of validation: **Client-side -> WAF -> Web server filter -> Dev framework validation -> Custom validation**
- Validate the source of data: Header, Cookie, POST or GET method etc.
- Canonicalization: convert the input into acceptable encoding, decode URL etc.
- Use regular expressions.
- Use allow list (length, range, format, type etc) and deny list (for sql injection, xss etc.).
- Dont: clean out the offending content and continue, at this stage (later on, sanitize).

#### Regex Basics

| Pattern | Description                          |
| ------- | ------------------------------------ |
| .       | Match any character except newline   |
| \w      | Match any alphanumeric character     |
| \s      | Match any whitespace character       |
| \d      | Match any digit                      |
| \b      | Match the beginning or end of a word |
| ^       | Match the beginning of the string    |
| $       | Match the end of the string          |
| \*      | Repeat any number of times           |
| +       | Repeat one or more times             |
| ?       | Repeat zero or one time              |
| {n}     | Repeat n times                       |

### Unicode

- **ASCII**: English character encoding (128 total chars, 94 printable chars, 33 control chars).
- **UTF-8** (unicode standard): compatible with ASCII, 1-4 bytes long (preferred way for web apps).
- Unicode has unique code point for every character.
- **International Domains Names** (IDN): allow non-english chars in domain names.
- Security issue: register look-alike domains with different encoding (unicode spoofing).
- **Punycode**: a way of representing Unicode domain names using ASCII chars.

### File Upload

- Risks: size, filename, extension, file type, executable content, virus or malware etc.
- Handling strategy: limit size in HTML, check size, mime type, filename and rename on the server, save outside of web directories (maybe in isolated environment), watch for path traversal, review file content, run a virus scan etc.
