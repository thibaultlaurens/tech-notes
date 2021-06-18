---
description: SEC522 - SANS
---

## 3. Web Application Authentication And Authorization

### Authentication // TODO

Application credentials:

- Store ouside of source code and put into app environment and make runtime reference from the app.
- Use a secret manager (vault etc.) to allow access to secrets by a remote API call and manage secret rotation.
- Mitigate hardcoded secrets in code: static analysis / scan, use brute forcing tool (Brutus, J-Baah etc.) to check for default passwords

Weak authentication:

- Auth based on IP or Referrer: can be easily spoofed.
- Defense: username and passwor minimum, two-factor auth is much better

### Multifactor Authentication

### Session Fixation

### Access Control

- Authorization should be based on authentication data and **not based on user-supplied data**.
- **Vertical access control** flaws: from unanthenticated to authenticated, from normal user to priviledged user.
- **Horizontal access control** flaws: from one user to another, accessing potentially sensitive info.
- Defense: use session (server-side) data to check user's identity, take a centralized approach (easier to manage), draw an access control matrix.
- Path traversal: process a file path with insufficient checking, allow attacker to traverse the filesystem.

Best practices:

- All access to a resource needs to be authorized before proceeding.
- Grant the minimum level of access (**Least Privilege Principle**), deny all by default and grant permission as needed.
- Authenticate first and then perform authorization.

Layering of access control:

- URL based access control: make decisions based on user's identity, role and URL.
- Filesystem and server permission: block the web server from traversing the system.
- Application (business logic) access control: control what the user can and cannot do in the app.
- Data layer access control: requires full user authentication to the data layer instead of generic app account, use of database view to limit access.
- Application (presentation layer) access control: Limits what the user can view.

### Single Sign-On & Session Sharing

Sharing authentication and authorization:

- Considerations on sharing user/data with third parties: **session** (cookies should never be shared), **authentication** (user should not have the same ID on multiple website), **authorization** (how the user control what is being shared ?).
- Possible solutions: be part of the subdomain and share cookies, use encrypted / signed token, use back-channel to share an auth token (not the session ID).

Single Sign-On:

- The user logs in once to a central authentication authority and then has access to multiple apps.
- Federated Identity: SSO across organizations or departments.
- Attribute-based access control: special form of federated identity, exact identity may not be needed, only a particular attribute.
- SSO Components: **Identity provider** (manages user's identity, user only provide credentials to it) and **Service Provider** (validate users using the identity provider).
- SSO limitations: careful implementation / key management, all eggs in one basket, all systems have to support SSO, availability (SSO down -> everything down).

OAuth:

- Authorization standard: provide the user of one app access to information stored in another app in a safe manner.
- Worflow:
  1. Thee App request a token to the resource (authorization) server and redirect the user to the resource app to login and consent.
  2. The user gets redirected back to the app with an authorization code.
  3. The app exchange the authorization code for a token with the resource server.
  4. With the token, tha app can then access the resource directly on behalf of the user.
- Issues: password change does not revoke any of the tokens, phishing: many users does not read the auth page carefully and do not understand the implication of the granting acess.
- **JWT** (JSON Web Token): a compact way for transmitting identity info between two parties. JWT is digitally signed with a secret or public/private key pair to guard against tampering and for validation. Format: `Header.Payload.Signature` (often base64 URL encoded).
- **OpenID Connect**: the authentication protocol on top of OAuth 2; allow one login for multiple sites. **ID Token**: identity card in JWT format.

### Encryption //TODO

Terminology:

- Ciphers: algorithms used to encrypt data (protect privacy).
- Hashes: algorithms used to sign data (detect changes).
- Symmetric (one key) vs Asymmetric (public/private key pair).

TLS:

- TLS secure data in transit: protects privacy and integrity of data, creates a tunnel for any type of traffic.
- Asymmetric encryption is expensive, TLS use both asymmetric encryption to establish a secure session (initial handshake) and symmetric encryption to exchange data.
- Certificate trust: Users trust CA; CA trust server; Users trust CA's trust for server.
- Trustworthy CA: 2048 bit RSA key certificate / SHA-2 for hashing.

TLS Config Flaws Defense:

- TLS 1.2 and 1.3 should be supported.
- **AES** (128/256) with **GCM** mode is currently the preferred mechanism for encrypting data during the TLS session (resistant to "Padding Oracle" attack).
- **Perfect Forward Secrecy** (PFS): even if the TLS private key is stolen, the captured TLS traffic cannot be decrypted. Algorithms to support PFS: **DHE** (Diffie-Hellman cipher suites) and **ECDHE** (Elliptic curve cryptography).
- Testing: [Hardenize](https://www.hardenize.com/)(replace [SSL Labs](https://www.ssllabs.com/ssltest)) for internet facing sites or OpenSSL `s_client` for internal sites.
- HTTP **Strict-Transport-Security** header forces the browser to connect using TLS, cert error = denied access.

Multidomain TLS certificate/hosting:

- A **Unified Communication Certificate** (UCC) has multiple names (FQDN) within a single certificate.

**OSCP Stapling**:

- Certificate Revocation List (CRL) was one of the widely used TLS mechanisms to revoke certificates but is being phased out (many challenged with the standard).
- **Online Certification Status Protocol** (OSCP) is now the standard for revoking certificates: done by the CA to revoke a certificate, the browser queries the CA to see whether the certificated is still valid.
- OSCP Stapling: server fetches and caches the CA response and then presents it to browsers, responses are signed by the CA to prevent forgery of OSCP response.

- **DNS Certification Authority Authorization (CAA)**:

- Allows the domain owner to publish the CA allowed to issue certificates for the domain name.
- Allows the specification of whether the CA is allowed to issue wildcard certificates.
- Not possible to specify certificate level of details.

### Encryption at Rest

### Tokenization
