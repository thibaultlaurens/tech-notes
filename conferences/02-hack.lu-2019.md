# HACK.LU 2019

## Tiplines today

_Harlo Holmes - Director of Newsroom Digital Security @Freedom of the Press Foundation_

Nowadays, the majority of US-based newsrooms rely on primarily consumer-facing applications to facilitate secure communications with sources. Usage of tools like Signal, WhatsApp, Threema, and others, have spiked in usage as the most state-of-the-art way to ensure confidential conversations with at-risk leakers and whistleblowers. Documents flood newsrooms, sometimes in gigabytes at a time, and journalists need tools to interrogate that data in relative safety from device compromise, legal interception, all while getting the job at the accelerated speed of the news cycle. Let’s explore how these tools, from both a technical and behavioral usage standpoint, make the news. Sometimes in a good way, when a story comes out after months of clandestine collaboration with sources, and toiling over data that needs to be interrogated; sometimes in a bad way, when sources get burned, or organizations endanger themselves.

With this talk, I aim to explain a theoretical bridge between hackers and other technologists; and a special group of end-users (journalists and their sources) who are, often without their prior knowledge, at the complete mercy of tools they barely understand under-the-hood. This talk should be as satisfying for hackers as it will be for folks who love to hear spicy stories about the “sausage gets made” in contemporary newsrooms.

Takeaway:

- [Freedom of the press fondation](https://freedom.press/)
- [US Press Freedom Tracker](https://pressfreedomtracker.us/)
- [Guardian Project](https://guardianproject.info/)

## The Road to Hell is Paved with Bad Passwords

_Chris Kubecka - founder and CEO @HypaSec_

Ever wonder what incident management is like when an embassy gets hacked, by ISIS? Come on a journey of surprisingly weak security, insider threats, a 50 million dollar extortion attempt, diplomatic immunity, city wide security lock down, all while >400 dignitary’s lives dangle in the negotiation crossfire. Join Chris, the lead investigator and resolver on a super-secret squirrel adventure against ISIS & Turkish Intel in The Hague, The Netherlands. Discussing the 2014 Saudi Arabian embassy hack. Whoever said STEM was boring made it boring! Solve the crime and save lives with key takeaways from a real life cyber terrorism investigation. No classified information will be shared, some terrorists were harmed in the making of this talk.

Takeaway:

- Incident management of an embassy hacked by ISI
- [Inside the 2014 hack of a Saudi embassy](https://www.csoonline.com/article/3386381/inside-the-2014-hack-of-a-saudi-embassy.html)
- [Hackernoon article ](https://hackernoon.com/the-road-to-hell-is-paved-with-bad-passwords-ef54815873f9)
- [Cyberwarfare](https://en.wikipedia.org/wiki/Cyberwarfare)

## Say Cheese - How I Ransomwared your DSLR Camera

_Eyal Itkin - vulnerability researcher @Check Point Software Technologies_

It’s a nice sunny day on your vacation, the views are stunning, and like on any other day you take out your DSLR camera and start taking pictures. Sounds magical right? But when you get back to your hotel the real shock hits you: someone infected your camera with ransomware! All your images are encrypted, and the camera is locked. How could that happen?

In this talk, we show a live demo of this exact scenario. Join us as we take a deep dive into the world of the Picture Transfer Protocol (PTP). The same protocol that allows you to control your camera from your phone or computer, can also enable any attacker to do that and more. We will describe in detail how we found multiple vulnerabilities in the protocol and how we exploited them remotely(!) to take over this embedded device.

But it doesn’t end here. While digging into our camera, we found a reliable way to take over most of the DSLR cameras without exploiting any vulnerability at all. We simply had to ask our camera to do that for us, and it worked.

This is the first vulnerability research on the Picture Transfer Protocol, a vendor agnostic logical layer that is common to all modern-day cameras. As DSLR cameras are used by consumers and journalists alike, this opens up the door for future research on these sensitive embedded devices.

Takeaway:

- [Picture Transfer Protocol](https://en.wikipedia.org/wiki/Picture_Transfer_Protocol)
- [Checkpoint GitHub account](https://github.com/CheckPointSW)

## Leveraging KVM as a debugging platform

_Mathieu_

Virtual Machine Introspection keeps opening new possibilities to interact with Virtual Machines, from sandboxing (VMRay), to cloud monitoring solutions (BitDefender HVI).

Our debuggers needs to benefit from this approach too, and so far we have seen multiple open source projects trying to leverage the hypervisor as a new debugging platform. However, most of these solutions are tied to one hypervisor.

The VMI ecosystem can only grow if it can bring all developers under the same roof, and provide the core libraries that will be the foundation for all VMI applications.

Keeping this vision in mind, pyvmidbg is a GDB stub built on top of LibVMI, a hypervisor-agnostic VMI library. It can introspect Windows VMs and explore the execution context to target and debug a specific process running on the system.

One of the goals of pyvmidbg is to attract developers and users by writing the missing layers that prevent VMI from gaining a wider adoption as of today.

The lack of VMI APIs available on KVM has made of LibVMI a Xen centric library, despite its flexible architecture. However, the situation recently changed in 2017, thanks to BitDefender proposing a new set of APIs for introspection.

This talk will demonstrate the new KVM introspection subsystem proposed by BitDefender, its integration in LibVMI, and how pyvmidbg is running on top of KVM today.

## The Red Square - Mapping the connections inside Russia's APT Ecosystem

_Ari Eitan - VP research @Intezer Labs and Itay Cohen - Reverse Engineer @CheckPoint_

If the names Turla, Sofacy, and APT29 strike fear into your heart, you are not alone. These are known to be some of the most advanced, sophisticated and notorious APT groups out there – and not in vain. These Russian-attributed actors are part of a bigger picture in which Russia is one of the strongest powers in the cyberwarfare today. Their advanced tools, unique approaches, and solid infrastructures suggest an enormous and complicated operation that involves different military and government entities inside Russia.

That said, and with all the available information on these groups, there are still some questions to bear in mind: Are the different government entities working alone or are they sharing code and techniques with each other? What artifacts, libraries and code are more likely to be shared between different families and teams of the same actor?

The fog behind these complicated operations made us realize that while we know a lot about single actors, we are short of seeing the bigger picture - a whole ecosystem with actor interaction (or lack thereof) and particular TTPs that can be viewed in a larger scope. We decided to know more and to look at things from a broader perspective. This led us to gather, classify and analyze thousands of Russian APT malware samples in order to find connections - not only between samples, but also between different families and actors.

In this talk, we will describe the process of our research. Namely, we will show how the technologies at our disposal allowed us to take a deep dive into these malware’s binary DNA in order to spot the mutual Genes that are shared between Russia’s APT families and actors. We will show interesting connections that we found, and present the interactive map we created to visualize this complicated Russian APT ecosystem. We will also release a signature-based tool to detect old and new samples based on the popular mutual Genes we found.

Takeaway:

- Goal : detect connections between Russian malware, entities, actors. What are Russian entities sharing in terms of code, libraries ? Can we validate known entities between groups ?
- Gather samples : 2000 unique samples based on IoCs extracted rom reports, not too hard
- Classification : most complicated part !
  - Challenges : no naming convention, IoCs precision
  - Actor, Family \(60\), Module \(200\), Version
- Find similarities : Intezer analysis based on assembly genes \(shared between malware and not by legitimate software\).

Challenge to automatically unpack samples \(static or dynamic\)

- Analyze connections
  - Gephi to visualize : [https://gephi.org/](https://gephi.org/)
  - [https://apt-ecosystem.com](https://apt-ecosystem.com) → Open-source graph tool
  - No new cross-actor connections were found, only connections between families already attributed to the same actor ▪ Why ? Good OPSEC, Politics, Other ?
  - Tool : Russian APT detector based on YARA : [https://github.com/ITAYC0HEN/APT-Ecosystem](https://github.com/ITAYC0HEN/APT-Ecosystem)

## The Glitch In The Matrix

_Marion Marschalek - Malware Analyst and Reverse Engineer @Intel STORM team_

Compared to the hordes of code reviewers and review tools that skim through pristine source code with every release cycle, the attention binary output gets from security engineers is limited. And why would security folks bother, bugs are all human-made; or, are they? Honestly, in reality, most are. Modern compilers and build setups are rather unlikely to accidentally introduce flaws into binaries, let alone security relevant flaws. Except, well, if an attacker gets her hands onto the build chain… Now, it has been established, that compromised compilers can introduce bugs to output binaries; but really, how stealthy can this be? How small of a change can an attacker plant, and still create a security vulnerability? And which means of detection do we have for such glitches in the matrix? Shall we ask Neo?

Takeaway:

- Bugify binaries by compromising the compiler ?
  - no one is auditing build chains or final output when they have the source code
  - usually not a problem because a compiler rarely introduces bugs and even rarely introduces a critical security bug
  - but very interesting attack vector !
- GCC:
  - front-end to create a generic representation
  - middle-end produces GIMPLE \(language independent\), … \(language optimizations\), RTL
  - back-end produces machine code. High complexity, millions lines of code, long legacy
- RTL : generic representation, proc independent, abstract description of final machine code
- Hard to execute bug, but full control on final binary is easy.
- Delete instruction to override a crypto key in memory with 0s because memory is not used after (mitigated in recent compilers but an existing "bug" that could be forced)
  - configurable bugs
  - very small modifications difficult to find through fuzzing : type confusions, off by one, unsign a signed type, shorten a key, kill a canary, attack mitigations
- Target GCC built-ins made for machine optimization of standard lib C and are customizable

## Hacktivism as a defense technique in a cyberwar. \#FRD Lessons for Ukraine

_Kostiantyn Korsun - ex head of CERT-UA, ex iSIGHT @Berezhasecurity_

Since 2014 Ukraine is under cyberwar. Energy grid attack BlackEnergy switched off electricity for 230,000 people for 6 hours. NotPetya attack effected ~30% of Ukrainian economy. Airports, railways, banking system, media, critical infrastructure had been attacked by Russian cyber groups (Telebots, BadRabbit, GrayEnergy). But have those attacks strengthened national cybersecurity system of Ukraine? Ukrainian cyber activists (hacktivists) checked that and published some shocking results. This activity got the name #FuckResponsibleDisclosure (#FRD) My talk is a historical retrospective of #FRD: when and how it started, what emotions it caused in Ukraine, how officials and resources’ owner communicated with hacktivists and others. How #FRD influenced on national cyber security and what local Cybersec-community thinks on #FRD. The preso contains plenty of expressive screenshots.

I researched #FRD as a unique activity in modern cybersecurity world. The main goal of #FRD is to increase cybersecurity level in Ukraine. However Ukrainian cyber activists used controversial methods to get this goal publishing indicators of low level of cyber protection in Governmental institutions and critical infrastructure objects. What was right/wrong in #FRD and how it influenced on national cybersecurity? This is the matter of the research.

Takeaway:

- Ukraine targeting by a lot of high level attacks against critical infrastructure (Central election comity network in 2014, BlackEnergy in 2015, NotPetya in 2017, DanaBot...)
- #FRD : Fuck Responsible Disclosure
  - Expose non directly exploitable bugs to the public to have officials/critical companies fix the problems faster
  - Legal : yes
  - Started in October 2017
- Result: open network disk of water supply company, email password available online for CERT-UA, open network disk of Kyiv electric supply company, of a nuclear power plant, plane plant, outdated PHP on State Financial, XSS everywhere, open network of National Police where everyone can search in records, open GIT of National Health with passwords to database full of personal health data.
- Typical reactions are the 5 stages of grief : denial, anger, bargaining, depression, acceptance
- Consequences : media, discharges, more investments
- Now supported by gov/police

## DNS On Fire

_Warren Mercer and Rascagneres Paul - Security researchers @Cisco Talos_

Cisco Talos identified malicious actors targeting the DNS protocol successfully for the past several years. In the presentation, we will present 2 threat actors we have been tracking.

The first one developed a piece of malware, named DNSpionage, targeting several government agencies in the Middle East, as well as an airline. During the research process for DNSpionage, we also discovered an effort to redirect DNSs from the targets and discovered some registered SSL certificates for them. We identified multiple countries targeted by this redirection. On 22 January 2019, the US DHS published a directive concerning this attack vector. In this presentation, we will present the timeline for these events and their technical details.

The second actor is behind the campaign we named “Sea Turtle”. This actor is more advanced and more aggressive than the previous one. They do not hesitate to target directly registrars and one registry. The talk will present the 2 actors and the methodology used to target the victims.

This talk will include:

- DNS presentation because few ppl mix register, registrar, registrant
- the oilrig leak on the similarities between DNSpionage and the technical details in the leak.
- unpublished DNS hijack if the investigation is finished by the conference.

Takeaway:

- DNS hijacking : DNS administer, DNS system interface, DNS servers, Network infra, Requestor’s endpoint
- DNSpionage :
  - spearphishing email or social media message \(Linkedin\)
  - domains similar to official ones and redirecting to them to host malicious documents : hr-wipro.com, hr-suncor.com
  - Macros to drop DNSpionage : HTTP & DNS tunnel. One sample in debug mode.
  - HTTP mode : DNS request to register to …..0ffice36o.com. Fake wikipedia page with base64 encoded commands.
  - DNS mode : IP == ASCII encoded
  - Monitoring through Cisco OpenDNS
  - On IP used for exfilration, .gov. domains pointing to it in the past and Let’s Encrypt certificates found at the same time \(Police/Intel/Gov, emails/VPN gateways\)
  - Main activity in september-november 2018 but first activity seen in Q1 2017
  - Alleged Oilrig leak : nothing related to DNSpionage
- Panel of ScareCrow, /Th!swasP@NEl in URL, close to panel name revealed by Lastline \(SAS 2019\)
- Webmask : MiTM via DNS redirection with middle east gov addresses in config file
- Very possible it has been used for DNSpionage
- SeaTurtle :
  - Espionage targeting middle east & north african gov departments, intel, oil & gas, military
  - Responsible for a publicly confirmed case of a DNS registry compromise \(Netnod in Sweden : [https://www.netnod.se/news/statement-on-man-in-the-middle-attack-against-netnod\](https://www.netnod.se/news/statement-on-man-in-the-middle-attack-against-netnod\)\)
  - Steal credentials for DNS administration and update DNS servers
  - Use it for MitM attacks to steal credentials \(VPN access\)
  - No concern about reveal : they have intensified their activity after disclosure
  - Attack multiple registrars, very aggressive, certificate abuse, steal certificates from victims infrastructure,
  - July 2019 \(blog post\) : single use of name-servers \(per victim\), less &lt; 24h live, Middle East and North Africa, a non profit in Swiss
- Protection : monitor your own DNS, monitor Certificate Transparency for your own names, patch, revoke and reset
