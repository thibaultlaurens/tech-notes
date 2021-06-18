---
description: SEC522 - SANS
---

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
