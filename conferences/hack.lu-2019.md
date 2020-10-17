# HACK.LU 2019

### Tiplines today

Explain a theoretical bridge between hackers and other technologists; and a special group of end-users \(journalists and their sources\) who are, often without their prior knowledge, at the complete mercy of tools they barely understand under-the-hood.

* [Freedom of the press fondation](https://freedom.press/) 
* [US Press Freedom Tracker](https://pressfreedomtracker.us/)

### The Road to Hell is Paved with Bad Passwords

* Incident management of an embassy hacked by ISI
* [Inside the 2014 hack of a Saudi embassy](https://www.csoonline.com/article/3386381/inside-the-2014-hack-of-a-saudi-embassy.html)
* [Hackernoon article ](https://hackernoon.com/the-road-to-hell-is-paved-with-bad-passwords-ef54815873f9)
* [Cyberwarfare](https://en.wikipedia.org/wiki/Cyberwarfare)

### Say Cheese - How I Ransomwared your DSLR Camera

* [Precision Time Protocol](https://en.wikipedia.org/wiki/Precision_Time_Protocol) 
* [Checkpoint GitHub account](https://github.com/CheckPointSW)

#### Leveraging KVM as a debugging platform

* KVM vs Xen vs Virtualbox vs VMware 
* Bitdefender KVM VMi 
* QEMU vs VMI 
* Libvmi 
* Fuzzing 
* OS hardening

#### The Red Square - Mapping the connections inside Russia's APT Ecosystem

Genetic malware analysis Big DB of "genes" of assembly code Visualize with graph tool gephy [apt-ecosystem.com](http://apt-ecosystem.com/)

Ari Eitan \(VP research Intezer\), Itay Cohen \(reverse @ CheckPoint\) • Goal : detect connections between Russian malware, entities, actors ◦ What are Russian entities sharing in terms of code, libraries ? Can we validate known entities between groups ? • Gather samples : 2000 unique samples based on IoCs extracted rom reports, not too hard • Classification : most complicated part ! ◦ Challenges : no naming convention, IoCs precision ◦ Actor, Family \(60\), Module \(200\), Version • Find similarities : Intezer analysis based on assembly genes \(shared between malware and not by legitimate software\).

Challenge to automatically unpack samples \(static or dynamic\) • Analyze connections ◦ Gephi to visualize : [https://gephi.org/](https://gephi.org/) ◦ [https://apt-ecosystem.com](https://apt-ecosystem.com) → Open-source graph tool ◦ No new cross-actor connections were found, only connections between families already attributed to the same actor ▪ Why ? Good OPSEC, Politics, Other ? ◦ Tool : Russian APT detector based on YARA : [https://github.com/ITAYC0HEN/APT-Ecosystem](https://github.com/ITAYC0HEN/APT-Ecosystem)

Pas plus de détails qu’en source ouverte, outils de visualisation intéressants, la méthodo serait difficile sur des APT chinoise partageant largement des outils, la méthodo rate l’utilisation de versions rares de librairies légitimes par différents acteurs

#### Fileless Malware Infection and Linux Process Injection in Linux OS

Bleu vs red team Merlin tool on github Advanced threat tactics Reddit r/malware must die ? Shellcode

Fileless Malware Infection and Linux Process Injection in Linux OS アドリアン ヘンドリック - Hendrik Adrian - @MalwareMustDie, LACERT / LAC Reverse + Linux internals peu compréhensible

The Glitch In The Matrix

Marion Marschalek, Intel STORM team

```text
•    Bugify binaries by compromising the compiler ?
◦    no one is auditing build chains or final output when they have the source code
◦    usually not a problem because a compiler rarely introduces bugs and even rarely introduces a critical security bug
◦    but very interesting attack vector !
•    GCC : front-end to create a generic representation, middle-end produces GIMPLE (language independent), … (language optimizations), RTL, back-end produces machine code. High complexity, millions lines of code, long legacy
•    RTL : generic representation, proc independent, abstract description of final machine code
•    Hard to execute bug full control on final binary is easy. Stealth :
◦    mimicking optimizations fails,
▪    delete instruction to override a crypto key in memory with 0s because memory not used after [mitigated in recent compilers but an existing « bug » that could be forced]
◦    configurable bugs
◦    very small modifications difficult to find through fuzzing : type confusions, off by one, unsign a signed type, shorten a key, kill a canary, attack mitigations
•    Target GCC built-ins made for machine optimization of standard lib C and are customizable
```

Présentation très accessible abordant GCC internals, POC et réflexion sur la faisabilité d’attaques du compilateur

Hacktivism as a defense technique in a cyberwar. \#FRD Lessons for Ukraine

Kostiantyn Korsun, ex head of CERT-UA, ex iSIGHT, Berezhasecurity

```text
•    Ukraine targeting by a lot of high level attacks against critical infrastructure (Central election comity network in 2014, BlackEnergy in 2015, NotPetya in 2017, DanaBot…)
•    #FRD : Fuck Responsible Disclosure
◦    Expose non directly exploitable bugs to the public to have officials/critical companies fix the problems faster
◦    Legal : yes
◦    Started in October 2017 : open network disk of water supply company, email password available online for CERT-UA, open network disk of Kyiv electric supply company, of a nuclear power plant, plane plant, outdated PHP on State Financial, XSS everywhere, open network of National Police where everyone can search in records, open GIT of National Health with passwords to database full of personal health data.
•    Typical reactions are the 5 stages of grief : denial, anger, bargaining, depression, acceptance
•    Consequences : media, discharges, more investments
•    Now supported by gov/police
```

Equivalent de l’article 47 de la LPM 2013 en France. La légalité effective a été interrogée à plusieurs reprises dans les questions.

#### What the log?! So many events, so little time…

EventList MITTR Attack sigma

#### The Glitch In The Matrix

Gcc graphic overview Gimple -&gt; RTL Gcc vs llvm

DNS On Fire

Warren Mercer and Rascagneres Paul, Cisco Talos

```text
•    DNS hijacking : DNS administer, DNS system interface, DNS servers, Network infra, Requestor’s endpoint
•    DNSpionage :
◦    spearphishing email or social media message (Linkedin)
◦    domains similar to official ones and redirecting to them to host malicious documents : hr-wipro.com, hr-suncor.com
◦    Macros to drop DNSpionage : HTTP & DNS tunnel. One sample in debug mode.
◦    HTTP mode : DNS request to register to …..0ffice36o.com. Fake wikipedia page with base64 encoded commands.
◦    DNS mode : IP == ASCII encoded
◦    Monitoring through Cisco OpenDNS
◦    On IP used for exfilration, .gov. domains pointing to it in the past and Let’s Encrypt certificates found at the same time (Police/Intel/Gov, emails/VPN gateways)
◦    Main activity in september-november 2018 but first activity seen in Q1 2017
◦    Alleged Oilrig leak : nothing related to DNSpionage
▪    Panel of ScareCrow, /Th!swasP@NEl in URL, close to panel name revealed by Lastline (SAS 2019)
▪    webmask : MiTM via DNS redirection with middle east gov addresses in config file
•    very possible it has been used for DNSpionage
•    SeaTurtle :
◦    Espionage targeting middle east & north african gov departments, intel, oil & gas, military
◦    Responsible for a publicly confirmed case of a DNS registry compromise (Netnod in Sweden : https://www.netnod.se/news/statement-on-man-in-the-middle-attack-against-netnod)
◦    Steal credentials for DNS administration and update DNS servers
◦    Use it for MitM attacks to steal credentials (VPN access)
◦    No concern about reveal : they have intensified their activity after disclosure
◦    Attack multiple registrars, very aggressive, certificate abuse, steal certificates from victims infrastructure, 
◦    July 2019 (blog post) : single use of name-servers (per victim), less < 24h live, Middle East and North Africa, a non profit in Swiss
•    Protection : monitor your own DNS, monitor Certificate Transparency for your own names, patch, revoke and reset
```

