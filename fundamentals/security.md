# Security & Cryptography

{% embed url="https://www.geeksforgeeks.org/computer-network-tutorials/\#nsc" %}

- - tools \([https://sectools.org/](https://sectools.org/)\)
  - cryptography
  - reverse engineering
  - bleu vs red teams
  - web app sec \(owasp top 10\)

## Secure Programming

### [OWASP Top Ten](https://owasp.org/www-project-top-ten/) Web Application Security Risks:

- [I**njection**](https://owasp.org/www-project-top-ten/2017/A1_2017-Injection). Injection flaws, such as SQL, NoSQL, OS, and LDAP injection, occur when untrusted data is sent to an interpreter as part of a command or query. The attacker’s hostile data can trick the interpreter into executing unintended commands or accessing data without proper authorization.
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

## OSINT

- VirusTotal: Analyze suspicious files and URLs to detect types of malware
- Shodan: All of the useful information about the target domain or IP address you could want, like open ports, used technology stack and possible vulnerabilities etc.
- Farsight DNSDB: A database that stores and indexes both the passive DNS data available via Farsight Security Information Exchange as well as the authoritative DNS data that various zone operators make available.
- WHOIS: Provides the registration details, also known as the WHOIS record data, of a domain name, an IP address, or an email address
- Censys:
- Shasowserver

- **IANA** (Internet Assigned Numbers Authority) is responsible for coordinating some of the key elements that keep the Internet running smoothly. IANA allocates and maintains unique codes and numbering systems that are used in the technical standards ("protocols") that drive the Internet:

  - Domain Names: Management of the DNS Root, the .int and .arpa domains, and an IDN practices resource.
  - Number Resources: Co-ordination of the global pool of IP and AS numbers, primarily providing them to Regional Internet Registries (RIRs).
  - Protocol Assignments: Internet protocols’ numbering systems are managed in conjunction with standards bodies

Today the services are provided by **PTI** (Public Technical Identifiers), a purpose-built organization for providing the IANA functions to the community. PTI is an affiliate of **ICANN** (Internet Corporation for Assigned Names and Numbers), an internationally-organised non-profit organisation set up by the Internet community to coordinate our areas of responsibilities

- **RIR** (Regional Internet Registries):

  - **AFRINIC**: Africa
  - **APNIC**: Asia and Pacific
  - **ARIN**: North America
  - **LACNIC**: Latin America
  - **RIPE NCC**: Europe, Russia, Middle East

- **Passive DNS** is a technique where IP to hostname mappings are made by recording the answers of other people's queries.

- **ccTLDs**: country code top-level domains
- **gTLD**: generic top-level domains

## Resources

- Video Lessons: [Hacker101](https://www.hacker101.com/videos)
- The Open Web Application Security Project: [OWASP](https://owasp.org/)
- OWASP Web Security Testing Guide**:** [WSTG](https://owasp.org/www-project-web-security-testing-guide/)
- Master the art of bug hunting: [Bugcrowd University](https://github.com/bugcrowd/bugcrowd_university)
- Top 125 Network Security Tools: [SecTools.Org](https://sectools.org/)
- [A Quick Linux Server Hardening Checklist](https://securecompliance.co/linux-server-hardening-checklist/)
- [How To Secure A Linux Server](https://github.com/imthenachoman/How-To-Secure-A-Linux-Server)
- [PGP and You](https://thoughtbot.com/blog/pgp-and-you)
- [Exploiting Stack Overflows](http://repository.root-me.org/Exploitation%20-%20Syst%C3%A8me/Unix/EN%20-%20Exploiting%20Stack%20Buffer%20Overflows%20in%20the%20Linux%20x86%20Kernel.pdf)
- [https://attack.mitre.org/groups/](https://attack.mitre.org/groups/)
- [https://stribika.github.io/2015/01/04/secure-secure-shell.html](https://stribika.github.io/2015/01/04/secure-secure-shell.html)
- [https://en.wikipedia.org/wiki/Pretty_Good_Privacy\#OpenPGP](https://en.wikipedia.org/wiki/Pretty_Good_Privacy#OpenPGP)
- [https://en.wikipedia.org/wiki/X.509](https://en.wikipedia.org/wiki/X.509)
