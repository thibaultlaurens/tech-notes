---
description: SEC522 - sans.org
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

## 3. Web Application Authentication And Authorization

### Authentication

#### Application credentials

- Store ouside of source code, put into app environment and make runtime reference from the app.
- Use a **secret manager** ([vault](https://www.vaultproject.io/) etc.) to allow access to secrets by a remote API call and manage secret rotation.
- Mitigate hardcoded secrets in code: static analysis / scan, use brute forcing tools (Brutus, J-Baah etc.) to check for default passwords.

#### Authentication Best Practices

- Auth mechanism should be based on risk level (add IP, device ID, location if needed).
- Authenticate the user AND the transaction.
- Notify user of any abnormal activity (new device, new location).
- Continuous authentication through the entire session.
- Re-authenticate where necessary.

#### Passwords Security

- **Focus on length rather than many different requirements**.
- No password hints.
- Expect users to leverage password managers.
- Block usage of leaked/common passwords.

### Multi-factor Authentication

- Makes authentifaction more difficult to break but not entirely resistant to attacks (e.g. **Man-In-The-Middle**).
- Provide emergency backup mechanism for account recovery or multi-factor password reset.
- Common auth solutions: time-based tokens, per-use tokens, out-of-band channels (sms, phone, etc.), challenge-response tokens.
- SMS/Voice: popular but pitfalls; **SIM jacking**, **SIM swapping**, **social engineering**.
- **OTP** (One Time Password): **TOTP** (Time based) and **HOTP** (HAMC based) are open standards (RFCs).
- **Password-Less** auth: smartphone prompt (many users actually approve fraudulent request), temporary email login link, webauthn etc.

#### FIDO2

- Standard established by the **FIDO** (Fast Identity Online) Alliance. Consist of two components: WebAuthn and CTAP.
- **WebAuthn**: W3C standard that defines browser to server communication for password-less authentication (based on asymmetric cryptographic authentication).
- **CTAP**: Client to Authenticator Protocol. Can be traditional software/hardware, can be user gesture or facial/fingerprint recognition.
- Authenticator is often used with a PIN to add extra security.

### Session Fixation

- Allow an attacker to **fix a victim's session ID before he/she logs into the application**. Eliminate the need to acquire a session ID.
- Attacker either presets the session token for the user or acquires a legitimate session token and entices the user to login with the token.
- Mitigation: never accept session ID from clients, assign new session ID after each successful login, **bind session ID to an immutable property of the client** (network address, TLC client certificate etc.).

### Access Control

- Authorization should be based on authentication data and **not based on user-supplied data**.
- **Vertical access control** flaws: from unanthenticated to authenticated, from normal user to priviledged user.
- **Horizontal access control** flaws: from one user to another, accessing potentially sensitive info.
- Defense: use session (server-side) data to check user's identity, take a centralized approach (easier to manage), draw an access control matrix.
- **Path traversal**: process a file path with insufficient checking, allow attacker to traverse the filesystem.

#### Best practices

- All access to a resource needs to be authorized before proceeding.
- Grant the minimum level of access (**Least Privilege Principle**), deny all by default and grant permission as needed.
- Authenticate first and then perform authorization.

#### Layering of Access Control

- **URL** based access control: make decisions based on user's identity, role and URL.
- **Filesystem and server** permission: block the web server from traversing the system.
- **Application (business logic)** access control: control what the user can and cannot do in the app.
- **Data layer** access control: requires full user authentication to the data layer instead of generic app account, use of database view to limit access.
- **Application (presentation layer)** access control: Limits what the user can view.

### Single Sign-On & Session Sharing

#### Sharing Authentication and Authorization

- Considerations on sharing user/data with third parties: **session** (cookies should never be shared), **authentication** (user should not have the same ID on multiple website), **authorization** (how the user control what is being shared ?).
- Possible solutions: be part of the subdomain and share cookies, use encrypted / signed token, use back-channel to share an auth token (not the session ID).

#### Single Sign-On

- The user logs in once to a **central authentication authority** and then has access to multiple apps.
- Federated Identity: SSO across organizations or departments.
- **Attribute-based access control**: special form of federated identity, exact identity may not be needed, only a particular attribute.
- SSO Components: **Identity provider** (manages user's identity, user only provide credentials to it) and **Service Provider** (validate users using the identity provider).
- SSO limitations: careful implementation / key management, all eggs in one basket, all systems have to support SSO, availability (SSO down -> everything down).

#### OAuth

- Authorization standard: **provide the user of one app access to information stored in another app** in a safe manner.
- Worflow:
  1. Thee App request a token to the resource (authorization) server and redirect the user to the resource app to login and consent.
  2. The user gets redirected back to the app with an authorization code.
  3. The app exchange the authorization code for a token with the resource server.
  4. With the token, tha app can then access the resource directly on behalf of the user.
- Issues: **password change does not revoke any of the tokens**, phishing (many users do not read the auth page carefully and do not understand the implication of the granting acess).
- **JWT** (JSON Web Token): a compact way for transmitting identity info between two parties. JWT is **digitally signed** with a secret or public/private key pair to guard against tampering and for validation. Format: `Header.Payload.Signature` (often base64 URL encoded).
- **OpenID Connect**: the authentication protocol on top of OAuth 2; allow one login for multiple sites. **ID Token**: identity card in JWT format.

### Encryption

#### Terminology

- Encryption protect the integrity and the confidentiality of the data (e.g. during transport and storage).
- **Ciphers**: algorithms used to encrypt data (protect privacy).
- **Hashes**: algorithms used to sign data (detect changes).
- **Symmetric** (one key) vs **Asymmetric** (public/private key pair).

#### TLS

- **TLS secures data in transit**: protects privacy and integrity of data, creates a tunnel for any type of traffic.
- Asymmetric encryption is expensive, TLS use both asymmetric encryption to establish a secure session (initial handshake) and symmetric encryption to exchange data.
- Certificate is based on **FQDN** (Fully Qualified Domain Name)
- **Certificate trust**: Users trust CA; CA trust server; Users trust CA's trust for server.
- Trustworthy CA: **2048 bit RSA key certificate / SHA-2 for hashing**.

#### TLS Config Flaws Defense

- TLS 1.2 and 1.3 should be supported.
- **AES** (128/256) with **GCM** mode is currently the preferred mechanism for encrypting data during the TLS session (resistant to "Padding Oracle" attack).
- **Perfect Forward Secrecy** (PFS): even if the TLS private key is stolen, the captured TLS traffic cannot be decrypted. Algorithms to support PFS: **DHE** (Diffie-Hellman cipher suites) and **ECDHE** (Elliptic curve cryptography).
- Testing: [Hardenize](https://www.hardenize.com/)(replace [SSL Labs](https://www.ssllabs.com/ssltest)) for internet facing sites or OpenSSL `s_client` for internal sites.
- HTTP **Strict-Transport-Security** header forces the browser to connect using TLS, cert error = denied access.

#### Multidomain TLS certificate/hosting

- A **Unified Communication Certificate** (UCC) has multiple names (FQDN) within a single certificate.
- One certificate can be applied to multiple servers and can be valid for multiple domains.
- The **Subject Alternative Name** (SAN) field in the cert can contain multiple domain names.
- **Server Name Indication** (SNI) allows one IP to host multiple SSL sites, the client has to specify the domain name before the TLS starts.

#### OSCP Stapling

- **Certificate Revocation List** (CRL) was one of the widely used TLS mechanisms to revoke certificates but is being phased out (many challenges with the standard).
- **Online Certification Status Protocol** (OSCP) is now the standard for revoking certificates: done by the CA to revoke a certificate, the browser queries the CA to see whether the certificated is still valid.
- **OSCP Stapling**: server fetches and caches the CA response and then presents it to browsers, responses are signed by the CA to prevent forgery of OSCP response.

#### DNS Certification Authority Authorization (CAA)

- Allow the domain owner to publish the CA allowed to issue certificates for the domain name.
- Allow the specification of whether the CA is allowed to issue wildcard certificates.
- Not possible to specify certificate level of details.

### Encryption at Rest

#### Database Encryption

- Database encryption guard against unauthorized access to the data hosted in the db. No silver bullet: the app must be able to read the data.
- Common gotchas: performance issues, exposed keys, untested recovery procedure of backups.
- Alternatives: rely on traditional grant and revoke access to db, hash the data, store the data somewhere else.

#### Password Storage

- Store **cryptographic hashes** of the passwords (increase the time taken to recover the original password).
- **Hash cracking**: **brute force cracking** (try every combination) and **rainbow table cracking** (use pre-computed hashes).
- **Salted hash**: hash the password with random characters (should be unique for each user, minimum 8 bytes).
- **Linux password storage format**: `username:$algorithm$salt$hash:state` is standard to store passwords in db.
- Use standard hashing algorithms: **Bcrypt**. **PBKDF2**, **Scrypt**, **Argon2**.
- For extra safety, use **pepper**, a system wide random string that is not unique to each user password and stored outside the db.

### Tokenization

- Make a token of the information to be protected and then only use the token in further processing.
- Original data is stored in a secure location, encrypted and fully protected.
- The token effectovely act as a reference or alias of the original data.
- Alternative to / different from encryption. The two technologies do not replace each other (encryption is still required before tokenization happens).

## 4. Web Services and Frontend Security

### Web Services Introduction

- Web Service: programmatic interface that can be accessed over the network using open protocols and standards.
- **SOAP** (Simple Object Access Protocol): communication protocol for exchanging XML based messages (an envelope around XML messages). Used to call remote procedures.
- **WSDL** (Web Services Description Language): XML-formatted language to describe web services: functions, location, how to invoke etc.
- **WSDL Enumeration**: WSDL tells the attackers where and how to attack the web service.
- WSDL enumeration prevention: **avoid WSDL publishing** or limit to an IP range.

### Web Services Attacks and Defense

- XML Schema validation with **DTD** (Document Type Declaration) and **XSD** (XML Schema Definition)
- **XLM Schema Poisoning**: compromised schema can lead to DoS attacks and unexpected data into the XML processing component.
- **Entities** (DTD): user-defined names and replacement text can be created.
- **External Entity Attack**: entities can refer to external content, files on the internet or any network the XML parser has access to.
- DTD related attacks mitigation: **disable the use of DTD**.

### Web Services Security Features and Options

- **XML Parameter Tampering**: feed malicious data into each XML parameter (SQL injection, XSS etc.)
- **Oversized Payload**: many parsers load the entire document into memory space.
- SOAP error reporting can reveal a lot of information.
- **SAML** (Security Assertion Markup Language): XML-based standard for exchanging security information between entities (authentication and authorization). Works by trust assertions.
- DOM based XML parsing: parse the file into a tree structure
- SAX (Simple API for XML) based XML parsing: parse a document as a stream (low memory requirement), tag by tag and element by element. **Vulnerable to overwriting by injection**.
- **Web Services Firewall**: perform schame validation and XML parameter validation, understand common web services attacks.
- **WS-Security**: effort to standardize authentication, authorization, encryption and digital signature.
- **XML Signature**: can sign for elements within the XML documents, can have different elements signed by different parties.
- **XML Encryption**: Designed from the ground up to protect XML documents: encrypt full XML files or single elements or only contents on an element.
- Vulnerability: SAML with XML parsing (via comments) `<NameID>user<!- comment -->@example.com</NameID>`

### AJAX Intro

- AJAX: Asynchronous JavaScript and XML.
- **XHR** (XMLHttpRequest): an API that JavaScript can use to transfer data between server and client.
- **Fetch API**: improved XHR, based on promises instead of callbacks. Credentials (cookies) and Cross-Origin requests are disabled by default.
- **Same Origin Policy**: prevents scripts from one website getting or setting properties (XHR, DOM, cookies) of a different site (doesnt prevent to send a request but to read the response).
- AJAX security: same as before, but with bigger attack surface (on the server and the client). Attacker knowledge increases substantially.
- **AJAX XSS Worms**: a persistent XSS exploit code can now upload more XSS in the background.
- **AJAX CSRF**: in strict HTML/HTTP environments, only the GET method can be triggered, AJAX allows POST method to be triggered to a remote site (e.g via XSS).
- **AJAX + XSS + CSRF make anti-CSRF tokens useless** (XHR requests, token parsing and token submits). MySpace SAMY worm example.

### Cross-Domain AJAX

- Proxy: a proxy can be used to get around Same Origin Policy (attacker can exploit the trust between the 2 bridging parties).
- **JSONP** (JSON with Padding): SOP does not allow cross-domain use of resources, executing scripts on different domain is allowed -> put parentheses around javascript, let the client execute the code. Very poor in security.
- XHR Version 2: now able to make cross-domain HTTP requests (SOP was too limiting), new W3C access control syntax.
- **W3C Access Control** aka **CORS** (Cross-Origin Resource Sharing): standard that describes how a resource should be used for cross-domain access. Usage of **HTTP headers to communicate access control decisions**.
- **Pre-Flight requests**: required for requests other than `GET`/`POST`/`HEAD` or with custom headers. Use an `OPTIONS` requests with special headers to consult the third-party site for permission to send request.
- New request headers: `Origin`, `Access-Control-Request-Method` (PUT, DELETE etc.) and `Access-Control-Request-Headers` (headers used by the intended request)
- New response headers: `Access-Control-Allow-Origin`, `Access-Control-Max-Age`, `Access-Control-Allow-Credentials`, `Access-Control-Allow-Methods`, `Access-Control-Allow-Headers`

### REST Security

- REST: Representational State Transfer, use standard HTTP request methods to map general actions to resource.
- **REST Auth**: Cookie + Session for browser based client and **query based authentication** (put extra signature or token in the request to validate identity of the requestor).
- **REST and CSRF**: **custom header (e.g. `X-CSRF`) to trigger cross-origin pre-flight request** or establish state and leverage anti CSRF token (break the stateless nature of REST).
- REST API Access Restriction: **restrict methods for particular resources, validate content type, rate limit**.

### Browser Defense Mechanism

#### Content Security Policy (CSP)

- Firefox answer to multiple security problems (XSS, Clickjacking, CSRF).
- Allows the site owner to specify security options so that the browser can **reduce the capability on the client browser**, reducing the attack surface.
- Use response header `X-Content-Security-Policy` (`X-Content-Security-Policy-Report-Only` to reports the violation without performing any enforcement).
- **CSP default restrictions**: no inline javascript will execute, code will not be created from strings, no `data: URI` (inline content) etc.
- **CSP directives**: `default-src` (default source list for all policies), `script-src` (valid sources for javascript), `img-src`, `font-src` etc. `report-uri` (localtion to log information such as violations).

#### CSP Pitfalls

- `default-src` should be `self` or `none`, not `*`.
- `default-src` doesn't cover all the resources (`base-uri`, `form-action`, etc.), for these, an explicit configuration is needed.
- `object-src` might leak, set it to `none`.
- CSP can be bypassed if the policy is not crafted properly.

#### Other browser defense mechanisms

- **MIME Sniffing**: IE detects MIME type automatically and ignore MIME header. Problem: IE could potentially detect MIME type differently and execute some of the content. `X-Content-Type-Options: nosniff` to disable MIME sniffing in IE.
- **XSS**: browser protection against XSS helps to increase security but is no replacement for input filtering + output encoding.

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
