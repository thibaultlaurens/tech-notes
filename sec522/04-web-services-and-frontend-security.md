---
description: SEC522 - SANS
---

## 4. Web Services and Frontend Security

### Web Services Intro

- Web Services: programmatic interface that can be accessed over the network using open protocols and standards.
- SOAP (Simple Object Access Protocol): Communication protocol for exchanging XML based messages (an envelope around XML messages). Used to call remote procedures.
- WSDL (Web Services Description Language): XML-formatted language to describe web services: functions, location, how to invoke etc.
- WSDL enumeration: WSDL tells the attackers where and how to attack the web service.
- WSDL enumeration prevention: Avoid WSDL publishing, limit to IP range.

### Web Services Attacks and Defense

- XML Schema validation with DTD (Document Type Declaration) and XSD (XML Schema Definition)
- XLM Schema Poisoning: compromised schema can lead to DoS attacks and unexpected data into the XML processing component.
- Entities (DTD): user-defined names and replacement text can be created.
- External Entity Attack: entities can refer to external content: files on the internet or any network the XML parser has access to.
- DTD related attacks mitigation: disable the use of DTD.

### Web Services Security Features and Options

- Web services unique vulnerabilities: network traffic, XML parser, XML processor.
- XML parameter tampering: feed malicious data into each XML parameter (SQL injection, XSS etc.)
- Oversized Payload: many parsers load the entire document into memory space.
- SOAP error reporting can reveal a lot of information.
- SAML (Security Assertion Markup Language): XML-based standard for exchanging security information between entities (authentication and authorization). Works by trust assertions.
- DOM based XML parsing: parse the file into a tree structure
- SAX (Simple API for XML) based XML parsing: parse a document as a stream (low memory requirement), tag by tag and element by element. Vulnerable to overwrting by injection.
- Web Services Firewall: perform schame validation and XML parameter validation, understand common web services attacks.
- WS-Security: effort to standardize authentication, authorization, encryption and digital signature.
- XML Signature: can sign for elements within the XML documents, can have different elements signed by different parties.
- XML Encryption: Designed from the ground up to protect XML documents: encrypt full XML files or single elements or only contents on an element.
- Vulnerability: SAML with XML parsing (via comments) `<NameID>user<!- comment -->@example.com</NameID>`

### AJAX Intro

- AJAX: Asynchronous JavaScript and XML.
- XHR (XMLHttpRequest): an API that JavaScript can use to transfer data between server and client.
- Fetch API: improved XHR, based on Promises instead of callbacks. Credential (cookie) and Cross-Origin requests are disabled by default.
- Same Origin Policy: prevents scripts from one website getting or setting properties (XHR, DOM, cookies) of a different site (doesnt prevent to send a request but to read the response).
- AJAX security: same as before, but with bigger attack surface (on the server and the client). Attacker knowledge increases substantially.
- AJAX XSS worms: a persistent XSS exploit code can now upload more XSS in the background.
- AJAX CSRF: in strict HTML/HTTP environments, only the GET method can be triggered, AJAX allows POST method to be triggered to a remote site (e.g via XSS).
- AJAX + XSS + CSRF renders anti-CSRF tokens useless (XHR requests, token parsing and token submits). MySpace SAMY worm example.

### Cross-Domain AJAX

- Proxy: a proxy can be used to get around Same Origin Policy (attacker can exploit the trust between the 2 bridging parties)
- JSONP (JSON with Padding): SOP doent not allo cross-domain use of resources, executing scripts on different domain is allowed -> put parentheses around javascript, let the client execute the code. Very poor in security.
- XHR Version 2: now able to make cross-domain HTTP requests (SOP was too limiting), new W3C access control syntax
- W3C Access Control (Cross-Origin Resource Sharing): standard that describes how a resource should be used for cross-domain access. Usage of HTTP headers to communicate access control decisions.
- Pre-Flight requests: required for requests other than GET/POST/HEAD or with custom headers. Use of an OPTIONS requests with special headers to consult the third-party site for permission to send request.
- New request headers: `Origin`, `Access-Control-Request-Method` (PUT, DELETE etc.) and `Access-Control-Request-Headers` (headers used by the intended request)
- New response headers: `Access-Control-Allow-Origin`, `Access-Control-Max-Age`, `Access-Control-Allow-Credentials`, `Access-Control-Allow-Methods`, `Access-Control-Allow-Headers`

### REST Security

- REST: Representational State Transfer, use standard HTTP request methods to map general actions to resource.
- REST Auth: Cookie + Session for browser based client and query based authentication (put extra signature or token in the request to validate identity of the requestor).
- REST and CSRF: custom header (e.g. `X-CSRF`) to trigger cross-origin pre-flight request or establish state and leverage anti CSRF token (break the stateless nature of REST).
- REST API Access Restriction: restrict methods for particular resources, validate content type, rate limit.

### Browser Defense Mechanism

**Content Security Policy (CSP)**:

- Firefox answer to multiple security problems (XSS, clickjacking, CSRF).
- Allows the site owner to specify security options so that the browser can reduce the capability on the client browser, reducing the attach surface.
- Use response header `X-Content-Security-Policy`. (`X-Content-Security-Policy-Report-Only` to reports the violation without performing any enforcement).
- CSP default restrictions: no inline javascript will execute, code will not be created from strings, no `data: URI` (inline content) etc.
- CSP directives: `default-src` (default source list for all policies), `script-src` (valid sources for javascript), `img-src`, `font-src` etc. `report-uri` (localtion to log information such as violations).

CSP pitfalls:

- `default-src` should be `self` or `none`, not `*`
- `default-src` doesn't cover all the resources (`base-uri`, `form-action`, etc.), for these, an explicit configuration is needed.
- `object-src` might leak, set it to `none`.
- CSP can be bypassed if the policy is not crafted properly.

Other browser defense mechanisms:

- MIME Sniffing: IE detects MIME type automatically and ignore MIME header. Problem: IE could potentially detect MIME type differently and execute some of the content. `X-Content-Type-Options: nosniff` to disable MIME sniffing in IE.
- XSS: browser protection against XSS helps to increase security but is no replacement for input filtering + output encoding.
