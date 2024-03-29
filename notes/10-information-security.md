# Security & Cryptography

## Fundamentals of Security

### Core Pillars of Information Security

- **Confidentiality**: only allow access to data for which the user is permitted.
- **Integrity**: ensure data is not tampered or altered by unauthorized users.
- **Availability**: ensure systems and data are available to authorized users when they need it.

### Security Principles

- Minimize attack surface area
- Establish secure defaults
- Principle of Least privilege
- Principle of Defense in depth
- Fail securely
- Don’t trust services
- Separation of duties
- Avoid security by obscurity
- Keep security simple
- Fix security issues correctly
- Reliability & Security

### Authentication vs Authorization

- Authentication
- Autorization
- OpenID
- OAuth

### Cryptography

- Block ciphers
- Stream ciphers
- Key exchange
- Public-key encryption
- Hash functions
- Digital Certificates
- CA Enrollment process

### Login Security

- SSH
- Kerberos
- Certificate Chain
- TLS Handshake
- "Perfect" Forward Secrecy

## Network Security

### Introduction

#### TCP/IP

#### Public Key Infrastructure

#### IPSec

#### PGP and S/MIME

#### SSL/TLS

### Network Perimeter Security

#### General Firewall Framework

#### Packet Filters

#### Circuit Gateways

#### Application Gateways(ALG)

#### Trusted Systems & Bastion Hosts

### Scanning and Packet Capturing

#### Nmap

#### WireShark

#### IDS

### TCP/IP Security Issues

#### IP Spoofing

#### Covert Channel

#### IP Fragmentation Attack

#### Connection Hijacking

#### Buffer Overflow

#### ARP Spoofing

#### DNS Spoofing

## Attacks & Defense

### DNS

#### Cache Poisoning Attack

#### DNSSEC

### BGP

#### How BGP Works

#### BGP Vulnerabilities

#### BGP Security

### Web-Based Attacks

#### HTTP Response Splitting Attacks

#### Cross-Site Request Forgery (CSRF or XSRF)

#### Cross-Site Scripting (XSS)

#### DOM XSS Attacks

#### Clickjacking

#### SQL injection

### Security Breach

#### Denial of Service Attacks

#### Distributed Denial of Service Attacks

#### Wiretapping

#### Backdoors

### Malicious Attacks

#### Birthday Attack

#### Brute-Force Password Attacks

#### Dictionary Password Attacks

#### Replay Attacks

#### Man-in-the-Middle Attacks

#### Masquerading

#### Eavesdropping

#### Social Engineering

#### Phreaking

#### Phishing

#### Pharming

## Secure Programming

### [OWASP Top Ten](https://owasp.org/www-project-top-ten/) Web Application Security Risks:

- [**Injection**](https://owasp.org/www-project-top-ten/2017/A1_2017-Injection). Injection flaws, such as SQL, NoSQL, OS, and LDAP injection, occur when untrusted data is sent to an interpreter as part of a command or query. The attacker’s hostile data can trick the interpreter into executing unintended commands or accessing data without proper authorization.
- [**Broken Authentication**](https://owasp.org/www-project-top-ten/2017/A2_2017-Broken_Authentication). Application functions related to authentication and session management are often implemented incorrectly, allowing attackers to compromise passwords, keys, or session tokens, or to exploit other implementation flaws to assume other users’ identities temporarily or permanently.
- [**Sensitive Data Exposure**](https://owasp.org/www-project-top-ten/2017/A3_2017-Sensitive_Data_Exposure). Many web applications and APIs do not properly protect sensitive data, such as financial, healthcare, and PII. Attackers may steal or modify such weakly protected data to conduct credit card fraud, identity theft, or other crimes. Sensitive data may be compromised without extra protection, such as encryption at rest or in transit, and requires special precautions when exchanged with the browser.
- [**XML External Entities \(XXE\)**](https://owasp.org/www-project-top-ten/2017/A4_2017-XML_External_Entities_%28XXE%29). Many older or poorly configured XML processors evaluate external entity references within XML documents. External entities can be used to disclose internal files using the file URI handler, internal file shares, internal port scanning, remote code execution, and denial of service attacks.
- [**Broken Access Control**](https://owasp.org/www-project-top-ten/2017/A5_2017-Broken_Access_Control). Restrictions on what authenticated users are allowed to do are often not properly enforced. Attackers can exploit these flaws to access unauthorized functionality and/or data, such as access other users’ accounts, view sensitive files, modify other users’ data, change access rights, etc.
- [**Security Misconfiguration**](https://owasp.org/www-project-top-ten/2017/A6_2017-Security_Misconfiguration). Security misconfiguration is the most commonly seen issue. This is commonly a result of insecure default configurations, incomplete or ad hoc configurations, open cloud storage, misconfigured HTTP headers, and verbose error messages containing sensitive information. Not only must all operating systems, frameworks, libraries, and applications be securely configured, but they must be patched/upgraded in a timely fashion.
- [**Cross-Site Scripting XSS**](https://owasp.org/www-project-top-ten/2017/A7_2017-Cross-Site_Scripting_%28XSS%29). XSS flaws occur whenever an application includes untrusted data in a new web page without proper validation or escaping, or updates an existing web page with user-supplied data using a browser API that can create HTML or JavaScript. XSS allows attackers to execute scripts in the victim’s browser which can hijack user sessions, deface web sites, or redirect the user to malicious sites.
- [**Insecure Deserialization**](https://owasp.org/www-project-top-ten/2017/A8_2017-Insecure_Deserialization). Insecure deserialization often leads to remote code execution. Even if deserialization flaws do not result in remote code execution, they can be used to perform attacks, including replay attacks, injection attacks, and privilege escalation attacks.
- [**Using Components with Known Vulnerabilities**](https://owasp.org/www-project-top-ten/2017/A9_2017-Using_Components_with_Known_Vulnerabilities). Components, such as libraries, frameworks, and other software modules, run with the same privileges as the application. If a vulnerable component is exploited, such an attack can facilitate serious data loss or server takeover. Applications and APIs using components with known vulnerabilities may undermine application defenses and enable various attacks and impacts.
- [**Insufficient Logging & Monitoring**](https://owasp.org/www-project-top-ten/2017/A10_2017-Insufficient_Logging%2526Monitoring). Insufficient logging and monitoring, coupled with missing or ineffective integration with incident response, allows attackers to further attack systems, maintain persistence, pivot to more systems, and tamper, extract, or destroy data. Most breach studies show time to detect a breach is over 200 days, typically detected by external parties rather than internal processes or monitoring.

### [OWASP Secure Coding Practices](https://owasp.org/www-project-secure-coding-practices-quick-reference-guide/migrated_content) Quick Reference Guide //WIP

- Input Validation
- Output Encoding
- Authentication and Password Management
- Session Management
- Access Control
- Cryptographic Practices
- Error Handling and Logging
- Data Protection
- Communication Security
- System Configuration
- Database Security
- File Management
- Memory Management
- General Coding Practices

### [Mozilla Web Security](https://infosec.mozilla.org/guidelines/web_security.html) //WIP

- Transport Layer Security \(TLS/SSL\)
  - HTTPS
  - HTTP Strict Transport Security
  - HTTP Redirection
  - HTTP Public Key Pinnig
  - Resource Loading
- Content Security Policy
- contribute.json
- Cookies
- Cross-origin Resource Sharing
- CSRF Prevention
- Referrer Policy
- robots.txt
- Subresource Integrity
- X-Content-Type-Options
- X-Frame-Options
- X-XSS-Protection

## Cyber Threat Intelligence

### OSINT

#### Shadowserver

- The Shadowserver Foundation is a nonprofit security organization that **gathers and analyzes data on malicious internet activity** \(including malware, botnets, and computer fraud\), sends daily network reports to subscribers, and works with law enforcement organizations around the world in cybercrime investigations. Established in 2004 as a "volunteer watchdog group", it liaises with national governments, CSIRTs, network providers, academic institutions, financial institutions, Fortune 500 companies, and end users to improve Internet security, enhance product capability, advance research, and dismantle criminal infrastructure.

#### Microsoft

- **CTIP**\(\)
- **DCU** \(Digital Crimes Unit\)

#### VirusTotal

Analyze suspicious files and URLs to detect types of malware

#### Rapid7

#### Shodan

All of the useful information about the target domain or IP address you could want, like open ports, used technology stack and possible vulnerabilities etc.

#### Farsight

- **DNSDB**: A database that stores and indexes both the passive DNS data available via Farsight Security Information Exchange as well as the authoritative DNS data that various zone operators make available.
- **Passive DNS** is a technique where IP to hostname mappings are made by recording the answers of other people's queries.

#### Censys

#### WHOIS

- provides the registration details, also known as the WHOIS record data, of a domain name, an IP address, or an email address.
- **ccTLDs**: country code top-level domains
- **gTLD**: generic top-level domains

#### IANA

The **Internet Assigned Numbers Authority** is responsible for coordinating some of the key elements that keep the Internet running smoothly. IANA allocates and maintains unique codes and numbering systems that are used in the technical standards \("protocols"\) that drive the Internet:

- **Domain Names**: Management of the DNS Root, the .int and .arpa domains, and an IDN practices resource.
- **Number Resources**: Co-ordination of the global pool of IP and AS numbers, primarily providing them to Regional Internet Registries \(RIRs\).
- **Protocol Assignments**: Internet protocols’ numbering systems are managed in conjunction with standards bodies

Today the services are provided by **PTI** \(Public Technical Identifiers\), a purpose-built organization for providing the IANA functions to the community. PTI is an affiliate of **ICANN** \(Internet Corporation for Assigned Names and Numbers\), an internationally-organised non-profit organisation set up by the Internet community to coordinate our areas of responsibilities

#### RIR

**Regional Internet Registries**:

- **AFRINIC**: Africa
- **APNIC**: Asia and Pacific
- **ARIN**: North America
- **LACNIC**: Latin America
- **RIPE NCC**: Europe, Russia, Middle East

## Detection

- Architecure
- IPS and IDS \(Snort vs Bro vs zeek vs [more](https://github.com/sbilly/awesome-security#ids--ips--host-ids--host-ips)\)
- Fast Packet Processing

## Cybersecurity Glossary

- **APT**: Advanced Persistent Threat. Nation-state adversary (or sponsored by a nation). They are remarkable in their persistence, skills, and resources.
- **ASR**: Attack Surface Reduction.
- **ATT&CK** (MITRE): Adversarial Tactics, Techniques, and Common Knowledge. Document and track techniques attackers use throughout the different stages of a cyberattack to infiltrate networks and exfiltrate data.
- **AV**: Antivirus.
- **CASB**: Cloud Access Security Broker. Security policy enforcement gateway placed between users and cloud service providers to combine and interject enterprise security policies as cloud-based resources are accessed.
- **CIA**: Confidentiality, Integrity, and Availability.
- **CSIRT/CERT**: Computer Security Incident Response Team / Computer Emergency Response Team.
- **CSPM**: Cloud Security Posture Management. Assess secure and compliant configurations of the cloud platform’s control plane.
- **CVE**: Common Vulnerabilities and Exposures.
- **CVSS**: Common Vulnerability Scoring System.
- **CWE**: Common Weakness Enumeration.
- **CWPP**: Cloud Workload Protection Platform. Security protection solution for cloud workloads, including physical servers, virtual machines (VMs), containers, and serverless workloads.
- **DAST**: Dynamic Application Security Testing.
- **DoW**: Detect on Write.
- **EDR**: Endpoint Detection and Response. More advanced than EPP. Detect and investigate security incidents, ability to remediate endpoints to pre-infection state.
- **EPP**: Endpoint Protection Platform, covers traditional anti-malware scanning.
- **FIM**: File Integrity Monitoring.
- **IAM**: Identity and Access Management.
- **IDS/IPS**: Intrusion Detection Systems / Intrusion Protection Systems.
- **IOA**: Indicator of Attack. Focus on detecting the intent of what an attacker is trying to accomplish, regardless of the malware or exploit used in an attack. Used by next-gen AV for malware-free intrusions and zero-day exploits.
- **IOC**: Indicator of Compromise. Evidence on a computer that indicates that the security of the network has been breached. Traditional AV signatures.
- **IOM**: Indicator of Misconfiguration.
- **MDR**: Managed Detection and Response. Outsourced 24/7 cybersecurity services, Continuously monitors, prioritizes, and responds to cybersecurity threats with humans behind the wheel.
- **NDR**: Network Detection and Response. Continuously monitors an organization's network to detect cyber threats and anomalous behavior using non-signature-based tools or techniques.
- **NIST**: National Institute of Standards and Technology (USA).
- **NVD**: National Vulnerability Database (USA). Maintained by NIST.
- **OSINT**: Open-Source Intelligence. Data collected from publicly available sources to be used in an intelligence context.
- **PE**: Portable Executable, a windows file format for executables.
- **RASP**: Run-time Application Self Protection. Use runtime instrumentation to detect and block computer attacks by taking advantage of information from inside the running software.
- **RCE**: Remote Code Execution.
- **SAST**: Static Application Security Testing.
- **SIEM**: Security Information and Event Management. Collect, normalize, correlate, aggregate, and detect anomalies across a variety of data sources.
- **SOAR**: Security Orchestration, Automation, and Response. Describe three software capabilities: threat and vulnerability management, security incident response and security operations automation.
- **SOC**: Security Operation Center. Unit that handles the detection, analysis, and response to cybersecurity incidents in an organization.
- **SQLI**: SQL Injection.
- **TIP**: Threat Intelligence Platform/Provider.
- **TPP**: Tactics, Techniques and Procedures (MITRE ATT&CK). Refers to the methods, tools, and patterns that malicious parties use to carry out attacks.
- **WAF**: Web Application Firewall. Inspect HTTP requests to safeguard against attacks against web applications.
- **XDR**: Extended Detection and Response. Security threat detection and incident response tool that natively integrates multiple security products into a cohesive security operations system.
- **XSRF**: Cross-site Request Forgery.
- **XSS**: Cross-site Scripting.
- **XXE**: XML External Entities.

## Resources

- [Hacker101 Video Lessons](https://www.hacker101.com/videos)
- [The Open Web Application Security Project](https://owasp.org/)
- [OWASP Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [Bugcrowd University](https://github.com/bugcrowd/bugcrowd_university)
- [Top 125 Network Security Tools](https://sectools.org/)
- [A Quick Linux Server Hardening Checklist](https://securecompliance.co/linux-server-hardening-checklist/)
- [How To Secure A Linux Server](https://github.com/imthenachoman/How-To-Secure-A-Linux-Server)
- [PGP and You](https://thoughtbot.com/blog/pgp-and-you)
- [MITRE ATT&CK](https://attack.mitre.org/)
- [Secure Secure Shell](https://stribika.github.io/2015/01/04/secure-secure-shell.html)
- [Wikipedia OpenPGP](https://en.wikipedia.org/wiki/Pretty_Good_Privacy#OpenPGP)
- [Wikipedia X.509](https://en.wikipedia.org/wiki/X.509)
- [Scholl of SRE - Security](https://linkedin.github.io/school-of-sre/security/intro/)
- [Geeksforgeeks - Network Security and Cryptography](https://www.geeksforgeeks.org/computer-network-tutorials/#nsc)
- [Glossary of Cyber Security Terms, Abbreviations and Acronyms](https://www.infosecmatter.com/infosec-glossary/)
