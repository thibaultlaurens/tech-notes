# DFRWS EU 2020

## Presentation

- DFRWS: Community around Forensic research papers
- First virtual DFRWS: 140 participants / 30 countries
- 1 keynote / 5 papers presentations / 2 workshops sessions / virtual social events

## Paper Presentations I - Memory Forensics

### BMCLeech: Introducing Stealthy Memory Forensics to BMC

**Tobias Latzo, Julian Brost and Felix Freiling**
_Department of Computer Science, Friedrich-Alexander-Universit€at Erlangen-Nürnberg (FAU), Erlangen, Germany_
[link to paper](https://dfrws.org/wp-content/uploads/2020/05/BMCLeech-Introducing-Stealthy-Memor_2020_Forensic-Science-International-Di.pdf)

**BMC**: Baseboard Management Controller

- asynchronously access and control the host's computing resources
- allows an administrator to monitor and administer a server remotely (temperature, fans, kvm, IPMI, Redfish)
- used by big companies like FB, MS etc.

**Memory access hierarchy**:

- ring 1: user level
- ring 0: kernel level
- ring -1: hypervisor level
- ring -2: sync management level
- ring -3: async device level

**OpenBMC**:

- Linux distribution for embedded devices that have a BMC
- examples: servers, top of rack switches, RAID appliance etc.

**BMCLeech**:

- introduced in this paper and based on OpenBMC
- brings forensic memory acquisition onto the BMC, useful for incident response teams
- internally leverages the power of **PCILeech**, a framework for memory acquisition via **DMA** (Direct Memory Access) attack.

Conclusion with the 3 criteria of memory acquisition techniques:

- atomicity (not applicable here)
- integrity (yes)
- correctness (yes)

### Tampering Digital Evidence is Hard: The Case of Main Memory Images

**Janine Schneider, Julian Wolf, Felix Freiling**
_Department of Computer Science, Friedrich-Alexander-Universit€at Erlangen-Nürnberg (FAU), Erlangen, Germany_
[link to paper](https://dfrws.org/wp-content/uploads/2020/05/Tampering-with-Digital-Evidence-is-Hard-_2020_Forensic-Science-Internationa.pdf)

Tampered digital evidence may jeopardize its correct interpretation.
HDD tampering is "hard" and the effort to create forgeries is "high", what about memory ?
Experiment to quantify the necessary effort to perform a convincing manipulation of digital evidence.

Controlled experiments:

- Main memory is tampered by graduate students -> memory is easier to tamper than HDD
- Main memory is analyzed by graduate students -> the analysis effort is higher than the manipulation effort
- Main memory is analyzed by professionals -> most forgeries were successfully detected

Conclusion:

- tampering with main memory dumps is harder than tampering with hard disc images
- the probability to fool an analyst is higher too

### On Challenges in Verifying Trusted Executables Files in Memory Forensics

**Daniel Uroz, Ricardo J. Rodríguez**
_Dept. of Computer Science and Systems Engineering, University of Zaragoza, Spain_
[link to paper](https://dfrws.org/wp-content/uploads/2020/05/On-Challenges-in-Verifying-Trusted-Execut_2020_Forensic-Science-Internationa.pdf)

Security **incident response process**:

- memory, disk and network dump (especially if malware may be present)
- looking for facts about the security incident

**Memory dump**:

- collection of memory artifacts
- snapshot of running processes, logged users, open files, open network connections, recent system resources freed

**Code signing**:

- help establish trust in computer software (integrity + authenticity)
- commonly used in modern OSes
- can it be a preliminary step to prioritize the list of processes to analyze ?

Problems:

- malware are abusing the code signing technology to remain stealthy and undetected
- a memory dump does not contain an exact copy of an executable file (the file as stored on disk)

Windows PE memory dump:

- embedded signature (WIN_CERTIFICATE structure\*\* or catalog based
- verification of a signature is done by WINTRUST and CRYPT32 DLLs

Limitations of the digital signature verification process of Windows PE signed files:

- data incompleteness due to memory swapping
- data changes caused by relocation
- catalog-signed files
- executable file and process inconsistencies

**sigcheck**:

- Volatility plugin introduced in this paper
- recovers executable files from a memory dump
- computes its digital signature (if feasible\*\*

Conclusion:

- sigcheck tested on Windows 7 x86 and x64 memory dumps
- success rate is low, especially when the memory is acquired from a system that has been running for a long time

## Paper Presentation II: Digital Forensic Science

### Towards Sound Forensic Arguments: Structured Argumentation Applied to Digital Forensics Practice

**Virginia N. L. Franqueira and Graeme Horsman**
_School of Computing, University of Kent, Canterbury, CT2 7NF, UK_
_School of Health&Life Sciences, Teesside University, Middlesbrough, TS1 3BA, UK_
[link to paper](https://dfrws.org/wp-content/uploads/2020/05/Towards-Sound-Forensic-Arguments-Structured-A_2020_Forensic-Science-Interna.pdf)

Digital forensic practitioners are increasingly facing examinations which are both complex in nature and structure.
Throughout this process, during the examination and analysis phases, the practitioner is constantly drawing logical inferences which will be reflected in the reporting of results.
Therefore, it is important to expose how all the elements of an investigation fit together to allow review and scrutiny,and to support associated parties to understand the components within it.
This paper proposes the use of‘Structured Argumentation’as a valuable and flexible ingredient of the practitioners' thinking toolbox.
It explores this approach using three case examples which allow discussion of the benefits and application of structured argumentation to real world contexts.
We argue that, despite requiring a short learning curve, structured argumentation is a practical method which promotes accessibility of findings facilitating communication between technical and legal parties, peer review, logical reconstruction, jury interpretation, and error detection.

Practice vs Science (push for science in recent years)

### An Argumentation-Based Reasoner to Assist Digital Investigation and Attribution of Cyber-Attacks

**Erisa Karafili, Linna Wang and Emil Lupu**
_Electronics and Computer Science, University of Southampton, Southampton, UK_
_Department of Computing, Imperial College London, London, UK_
[link to paper](https://dfrws.org/wp-content/uploads/2020/05/An-Argumentation-Based-Reasoner-to-Assist-Digi_2020_Forensic-Science-Interna.pdf)

We expect an increase in the frequency and severity of cyber-attacks that comes along with the need for efficient security counter measures.
The process of attributing a cyber-attack helps to construct efficient and targeted mitigating and preventive security measures.
In this work, we propose an argumentation-based reasoner (ABR) as a proof-of-concept tool that can help a forensics analyst during the analysis of forensic evidence and the attribution process.
Given the evidence collected from a cyber-attack, our reasoner can assist the analyst during the investigation process, by helping him/her to analyze the evidence and identify who performed the attack.
Furthermore, it suggests to the analyst where to focus further analyses by giving hints of the missing evidence or new investigation paths to follow.
ABR is the first automatic reasoner that can combine both technical and social evidence in the analysis of a cyber-attack, and that can also cope with incomplete and conflicting information.
To illustrate how ABR can assist in the analysis and attribution of cyber-attacks we have used examples of cyber-attacks and their analyses as reported in publicly available reports and online literature.
We do not mean to either agree ordisagree with the analyses presented therein or reach attribution conclusions.

### Structuring the Evaluation of Location-Related Mobile Device Evidence

**Eoghan Casey, David-Olivier Jaquet-Chiffelle, Hannes Spichiger, Elénore Ryser and Thomas Souvignet**
\*Ecole des Sciences Criminelles, University of Lausanne, 1015, Switzerland\*\*
[link to paper](https://dfrws.org/wp-content/uploads/2020/05/Structuring-the-Evaluation-of-Location-R_2020_Forensic-Science-International.pdf)

Location-related mobile device evidence is increasingly used to address forensic questions in criminal investigations.
Evaluating this form of evidence, and expressing evaluative conclusions in this forensic discipline, are challenging because of the broad range of technological subtleties that can interact with circumstantial features of cases in complex ways.
These challenges make this type of digital evidence prone to misinterpretations by both forensic practitioners and legal decision-makers.
To mitigate the risk of misleading digital forensic findings, it is crucial to follow a structured approach to evaluation of location-related mobile device evidence.
This work presents an evaluation framework widely used inforensic science that employs scientific reasoning within a logical Bayesian framework to clearly distinguish between, on the one hand, what has been observed (i.e., what data are available\*\* and, on the other hand, how those data shed light on uncertain target propositions.
This paper provides case examples to illustrate the advantages and difficulties of applying this approach to location-based mobile device evidence.
This work helps digital forensic practitioners follow the principles of balanced evaluation and convey location-related mobile device evidence in a way that allows decision-makers to properly understand the relative strength of, and limitations in, digital forensic results.

## Practitioner Presentations I

### Digital Forensic Techniques for Preservation and Archiving

**Neil Jefferies**

### Automated Normalisation and correlation of mobile device extractions using CASE

**Eoghan Casey, Quentin Rossy and Martina Reif**

### Relevance scoring and clustering of digital traces

**Ameya Puranik**

## Paper Presentations III - Artificial Intelligence Aided Investigation

### DeepUAge: Improving Underage Age Estimation Accuracy to Aid CSEM Investigation

**Felix Anda, Nhien An Le Khac and Mark Scanlon**
_Forensics and Security Research Group, University College Dublin, Ireland_
[link to paper](https://dfrws.org/wp-content/uploads/2020/05/DeepUAge-Improving-Underage-Age-Estimatio_2020_Forensic-Science-Internation.pdf)

Age is a soft biometric trait that can aid law enforcement in the identification of victims of Child SexualExploitation Material (CSEM) creation/distribution. Accurate age estimation of subjects can classifyexplicit content possession as illegal during an investigation. Automation of this age classification has thepotential to expedite content discovery and focus the investigation of digital evidence through theprioritisation of evidence containing CSEM. In recent years, artificial intelligence based approaches forautomated age estimation have been created, and many public cloud service providers offer this serviceon their platforms. The accuracy of these algorithms have been improving over recent years. Theseexisting approaches perform satisfactorily for adult subjects, but perform wholly inadequately for un-derage subjects.To this end, the largest underage facial age dataset, VisAGe, has been used in this work to train aResNet50 based deep learning model, DeepUAge, that achieved state-of-the-art beating performance forage estimation of minors. This paper describes the design and implementation of this model. An eval-uation, validation and comparison of the proposed model is performed against existing facial age clas-sifiers resulting in the best overall performance for underage subjects.

### Cutting through the Emissions: Feature Selection from Electromagnetic Side-Channel Data for Activity Detection

**Asanka Sayakkara, Luis Miralles, Nhien An Le Khac and Mark Scanlon**
_Forensics and Security Research Group, University College Dublin, Ireland_
_Centre for Applied Data Analytics Research (CeADAR), University College Dublin, Dublin, Ireland_
[link to paper](https://dfrws.org/wp-content/uploads/2020/05/Cutting-Through-the-Emissions-Feature-Selection_2020_Forensic-Science-Inter.pdf)

Electromagnetic side-channel analysis (EM-SCA) has been used as a window to eavesdrop on computingdevices for information security purposes. It has recently been proposed to use as a digital evidenceacquisition method in forensic investigation scenarios as well. The massive amount of data produced byEM signal acquisition devices makes it difficult to process in real-time making on-site EM-SCA infeasible.Uncertainty surrounds the precise information leaking frequency channel demanding the acquisition ofsignals over a wide bandwidth. As a consequence, investigators are left with a large number of potentialfrequency channels to be inspected; with many not containing any useful information leakages. Theidentification of a small subset of frequency channels that leak a sufficient amount of information cansignificantly boost the performance enabling real-time analysis. This work presents a systematicmethodology to identify information leaking frequency channels from high dimensional EM data withthe help of multiplefiltering techniques and machine learning algorithms. The evaluations show that it ispossible to narrow down the number of frequency channels from over 20;000 to less than a hundred (81channels). The experiments presented show an accuracy of 0.9315 when all the 20;000 channels areused, an accuracy of 0.9395 with the highest 500 channels after calculating the variance between theaverage value of each class, and an accuracy of 0.9047 when the best 81 channels according to RecursiveFeature Elimination are considered.

### Towards Open-Set Forensic Source Grouping on JPEG Header Information

**Patrick Mullan, Christian Riess and Felix Freiling**
_IT Security Infrastructures Lab, Friedrich-Alexander University Erlangen-Nürnberg, Germany_
[link to paper](https://dfrws.org/wp-content/uploads/2020/05/Towards-Open-Set-Forensic-Source-Groupin_2020_Forensic-Science-International.pdf**

Image provenance, i.e., information on the model and make of the device that was used to produce animage, is a helpful cue in many digital investigations. Such information can, for example, help refute thehypothesis that an illegal photograph found on the Internet was produced using the personal device of asuspect. Grouping images by provenance can be done in different ways. Based on the encouraging in-sights from previous works, we consider the grouping of JPEG images by theirfile headers where pre-vious work performed image classification on a closed-set of devices. However, due to the ongoingdevelopment of new camera models and the practical difficulty to keep a model database up-to-date, wepropose to treat image provenance as an open-set classification problem with the goal to predict themake of a previously unseen camera model. We show that such a prediction can performe remarkablywell, with median accuracies beyond 90% for each make. In a more challenging experiment with imagesthat were postprocessed, we achieve a median accuracy of about 55% and 75% for desktop software andfor smartphone apps, respectively.

## Practitioner Presentations II

### Forensics analysis of Apple Homepod

**Mattia Epifani**

- Homepod: apple smart speaker, hub of the Homekit system (framework for home automation)
- Get data from the homepod:
  - use apple sysdiagnose protocol (bug report)
  - use the hidden 4 pin port (exploit not available yet)
  - synced iphone (sqlite db of the homepod)

Homepod data to extract from the homepod:

- router mac address
- id of all the connected ios devices
- geolocation
- info about the home (bedrooms etc.)
- Siri vocal commands
- List of songs played with timestamps + id of the device used to play the song
- logs: 24 hours of everything that happened

### Expressing evaluative conclusions in cases involving tampering of digital evidence

**Timothy Bolle and Eoghan Casey**

Tampering:

- Destruction: mass deletion and File wiping
  - traces of program execution
  - wipe patterns: metadata zeroed / name overwritten
- Hiding: missing device
  - Shellbags and LNK traces of devices
- Staging: backdating / file alteration

Paper about "Standardization of forming and expressing preliminary evaluative opinions on digital evidence\*\*.

## Paper Presentations IV - Network Forensics

### A Scalable Platform for Enabling the Forensic Investigation of Exploited IoT Devices and their Generated Unsolicited Activities

**Sadegh Torabi, Elias Bou-Harb, Chadi Assi and Mourad Debbabi**
_Security Research Centre, Concordia Institute for Information Systems Engineering, Concordia University, Montreal, Canada_
_The Cyber Center for Security and Analytics, University of Texas at San Antonio, San Antonio, United States_
[link to paper](https://dfrws.org/wp-content/uploads/2020/05/A-Scalable-Platform-for-Enabling-the-Forensic-Inve_2020_Forensic-Science-Int.pdf)

Introduction

- IoT devices have been used as effective attack enabler
- The Mirai botnet
- Mitigation

System architecture

- IoT data collection and filtering
  - data driven methodologies
  - collect iot data from Shodan
  - iOT generated traffic from the darknet
- IoT threat repository
  - collect IoT malware ...
  - ...
- IoT traffic Analysis (Apache spark)
  - fast and scalable operations
  - ..

Experimental results:

- collected 400k devices from shodan
- 4TB of darknet data over 5 days
- 28000 compromised devices

Network forensic capabilities and applications:

- Macroscopic views of exploited devices and their activities
- Compromised IoT device detection and traffic analysis
- Adaptive and dynamic device profiling (botnet detection, scanning campaigns detection, infer targeted DoS victims)

Conclusion: proposed and evaluated an effective and scalable system prototype for IoT centric cyber forensic ...

The analysis of large-scale cyber attacks, which utilized millions of exploited Internet of Things (IoT)devices to perform malicious activities, highlights the significant role of compromised IoT devices ini enabling evasive and effective attacks at scale.

Motivated by the shortage of empirical data related to thedeployment of IoT devices, and the lack of understanding about compromised devices and their unso-licited activities, in this paper, we leverage a big data analytics framework (Apache Spark) to design anddevelop a scalable system for automated detection of compromised IoT devices and characterization oftheir unsolicited activities.

The system utilizes IoT device information and passive network measure-ments obtained from a large network telescope, while implementing an array of data-driven method-ologies rooted in data mining and machine learning techniques, to provide a macroscopic view of IoT-generated malicious activities. We evaluate the system with more than 4TB of passive network mea-surements and demonstrate its effectiveness in the network forensic investigation of compromiseddevices and their activities, in near real-time. In addition, we empirically analyze and elaborate on thecapabilities of the developed system as a scalable infrastructure, which can support a number of ap-plications that enable IoT-centric forensics.

### IoT Botnet Forensics: A Comprehensive Digital Forensic Case Study onMirai Botnet Servers

**Xiaolu Zhang, Oren Upton, Nicole Lang Beebe**, Kim-Kwang Raymond Choo\*\*
_Department of Information Systems&Cyber Security, University of Texas at San Antonio, San Antonio, TX, 78249, USA_
[link to paper](https://dfrws.org/wp-content/uploads/2020/05/IoT-Botnet-Forensics-A-Comprehensive-Digita_2020_Forensic-Science-Internati.pdf)

Mirai:

- malware for centralized IoT botnet
- open source
- caused the worst Dos attacks

Mirai botnet structure

- attacker terminal
- scan receiver / loading servers / CNC server / DNS server / Database
- infected IoT devices / vulnerable IoT devices
- victims of DDoS attack

Research questions:

- what evidence can be retrievable from mirai servers
- where are the evidence located ?
- ...
- ...

Internet of Things (IoT) bot malware is relatively new and not yet well understood forensically, despite itspotential role in a broad range of malicious cyber activities.
For example, it was abused to facilitate the distributed denial of service (DDoS) attack that took down a significant portion of the Internet on October 21, 2016, keeping millions of people from accessing over 1200 websites, including Twitter and NetFlix for nearly an entire day.
The widespread adoption of an estimated 50 billion IoT devices, as well as the increasing interconnectivity of those devices to traditional networks, not to mention to one another withthe advent offifth generation (5G) networks, underscore the need for IoT botnet forensics.
This study is the first published, comprehensive digital forensic case study on one of the most well known families of IoT bot malware - Mirai.
Past research has largely studied the botnet architecture and analyzed the Mirai source code (and that of its variants) through traditional static and dynamic malware analysis means, but has not fully and forensically analyzed infected devices or Mirai network devices.
In this paper, we set upa fully functioning Mirai botnet network architecture and conduct a comprehensive forensic analysis on the Mirai botnet server.
We discuss forensic artifacts left on the attacker's terminal, command and control (CNC) server, database server, scan receiver and loader, as well as the network packets therefrom.
We discuss how a forensic investigator might acquire some of these artifacts remotely, without direct physical access to the botnet server itself.
This research provides findings tactically useful to forensic investigators, not only from the perspective of what data can be obtained (e.g., IP addresses of bot member, but also important information about which device they should target for acquisition and investigation to obtain the most investigatively useful information.

### IP addresses in the context of digital evidence in the criminal and civil case law of the Slovak Republic

**Pavol Sokol, Laura Rózenfeldová, Katarína Lučivjanská and Jakub Harašta**
_Pavol Jozef Safarik University in Kosice, Faculty of Science, Jesenn5,Koice, Slovakia_
[link to paper](https://dfrws.org/wp-content/uploads/2020/05/IP-Addresses-in-the-Context-of-Digital-Evidence_2020_Forensic-Science-Intern.pdf)

Use of IP addresses by courts in their decisions is one of the issues with growing importance.
This applies especially at the time of the increased use of the internet as a mean to violate legal provisions of bothcivil and criminal law.
This paper focuses predominantly on two issues: (1) the use of IP addresses asdigital evidence in criminal and civil proceedings and possible mistakes in courts' approach to thisspecific evidence, and (2) the anonymisation of IP addresses in cases when IP addresses are to beconsidered as personal data.
This paper analyses the relevant judicial decisions of the Slovak Republicspanning the time period from 2008 to 2019, in which the relevant courts used the IP address as evidence.
On this basis, the authors formulate their conclusions on the current state and developing trendsin the use of digital evidence in judicial proceedings.
The authors demonstrate the common errors thatoccur in the courts’decisions as regards the use of IP addresses as evidence in the cases of the IP ad-dresses anonymisation, usage of the in dubio pro reo principle in criminal proceedings, and the rela-tionship between IP addresses and devices and persons.

## Keynote presentation by Dr Gillian Tully: Risk, Quality Assurance and Innovation in Digital Forensics

Abstract: The massive demand for extraction and analysis of data from digital devices has led, in England and Wales, to evolution of a cottage industry of small units, each using a selection of software tools, extracting data and passing it, often largely uninterpreted, to investigators.

Some of these digital forensic units have in place the quality assurance measures needed to ensure that the limitations of their work are known and that the provenance, continuity and validity of the data they have extracted can be demonstrated; others do not. Increasingly, front-line police officers are carrying out data extraction using self-service “kiosk” technology.

Those analysing the data are often, in this jurisdiction, intelligence analysts or investigators, with access to few advanced tools. A lack of methodological robustness in the analysis and interpretation of evidence has, in some cases, resulted in failures to find exculpatory evidence, which was present within the extracted data.

In this presentation, risks and failures in the extraction, analysis and interpretation of digital evidence will be considered alongside the need for process and technology innovation, with a view to achieving sustainable improvement.

## Paper Presentations V - File System Forensics

### Forensic Analysis of the Resilient File System (ReFS\*\* Version 3.4

**Paul Prade, Tobias Groß and Andreas Dewald**
_Friedrich-Alexander University Erlangen-Nürnberg, Germany_
_ERNW Research GmbH, Heidelberg, Germany_
[link to paper](https://dfrws.org/wp-content/uploads/2020/05/Forensic-Analysis-of-the-Resilient-File_2020_Forensic-Science-International-.pdf)

ReFS is a modern file system that is developed by Microsoft and its internal structures and behavior is not officially documented.
Even so there exist some analysis efforts in deciphering its data structures, some of these findings have yet become deprecated and cannot be applied to current ReFS versions anymore.
In this work, general concepts and internal structures found in ReFS are examined and documented.
Based on the structures and the processes by which they are modified, approaches to recover (deleted)files from ReFS formattedfile systems are shown.
We also evaluated our implementation and the allo-cation strategy of ReFS with respect to accuracy, runtime and the ability to recover olderfile states.

### Artifacts for detecting timestamp manipulation in NTFS and their reliability

**David Palmbach and Frank Breitinger**
_Cyber Forensics Research and Education Group (UNHcFREG), Tagliatela College of Engineering, ECECS, University of New Haven, 300 Boston Post Rd., WestHaven, CT, 06516, USA_
_Hilti Chair for Data and Application Security, Institute of Information Systems, University of Liechtenstein, Fürst-Franz-Josef-Strasse, 9490,Vaduz,Liechtenstei_
[link to paper](https://dfrws.org/wp-content/uploads/2020/05/Artifacts-for-Detecting-Timestamp-Manipulati_2020_Forensic-Science-Internati.pdf)

Timestamps have proven to be an expedient source of evidence for examiners in the reconstruction of computer crimes.
Consequently, active adversaries and malware have implemented timestomping techniques (i.e., mechanisms to alter timestamps\*\* to hide their traces.
Previous research on detecting timestamp manipulation primarily focused on two artifacts: the $MFT as well as the records in the $LogFile.
In this paper, we present a new use of four existing windows artifacts - the \$USNjrnl, linkfiles, prefetchfiles, and Windows event logsethat can provide valuable information during investigations and diversify the artifacts available to examiners.
These artifacts contain either information about executed programs or additional timestamps which, when inconsistencies occur, can be used to prove timestamp forgery.
Furthermore, we examine the reliability of artifacts being used to detect timestamp manipulation, i.e., testing their ability to retain information against users actively trying to alter or delete them.
Based on our findings we conclude that none of the artifacts analyzed can withstandactive exploitation.

## Workshop: Dynamic Instrumentation for forensic research using Frida

**Or Begam**

- Intro

  - Decoding: turning unstructured data into structured data
  - File format decoding example: raw stream of bits -> database (reverse) -> a chat application (forensic)
  - Automatic (with a tool) vs Manual decoding (need to write our own tool)

- Mobile application decoding

  - Generate data -> perform extraction / pull the data -> dig in
  - Trying to find messages attachments owner in instagram app
  - problem: the image is cached, the key is an md5 hash but we can't find any reference of this hash anywhere in the app db / binary / anywhere
  - let's look at the code if we cant find it in the data: decompile the code to reverse engineer OR use dynamic analysis (debugger) OR use dynamic instrumentation (Frida)

- Dynamic instrumentation

  - Instrumentation: The ability to monitor or measure the level of a product performance, to diagnose errors, and to write trace information
  - Source vs Binary instrumentation

- Frida:

  - inject frida-agent into a process, create a new thread that is used for establishing a communication channel between the process and us
  - channel can be local, network or usb cable
  - frida can be used to create hooks, trace processes, inspect and modify memory, call functions, modify function arguments

- Hooking
  - altering or augmenting the software behaviour of software components by intercepting function calls and ..... (wiki) (hook = man in the middle for function call)
  - hook trampoline: save registers -> call frida_on_enter / our own code -> restore registers
  - hook in real life: replace a called function by some code to call our frida trampoline + add the code of the original function to the trampoline after restoring the register

Using frida

- frida CLI - js shell for prototyping and debugging
- frida tools - cli that wrap frida API
- frida API - with bindings for python, C, Node, .NET etc.

Dynamic instrumentation is a method for monitoring specific components of a program, that can greatly simplify forensic research tasks involving reverse engineering.

When dealing with problems related to encryption or hashing, using instrumentation can reveal the "bottom line" a researcher is looking for without the need for complex analysis of an application’s code.

In this workshop, we will give an overview of how to use Frida, an easy-to-use yet very powerful open source instrumentation framework, in a mobile environment;
We will demonstrate how to quickly solve mobile forensics problems like identifying the connection between attachments with hashed filenames and the database records that describe the instant messages that contains them, using a generic method of hooking hash functions in different mobile environments;
And we will present a generic method for finding the passphrases to SQLCipher encrypted databases without any knowledge of the key generation process.
