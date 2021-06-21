---
description: SEC522 - SANS
---

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
