---
title: Computer Security and Privacy
date: 2019-03-12 11:28:04
tags:
---

# Computer Security and Privacy


### Module 1

- **Confidentiality** : Access to systems or data is limited to authorized parties
- **Integrity** : When you receive data, you get the “right data
- **Availability** : The system or data is there when you want it
- **Assets** : things we want to protect (Hardware, software, data)
- **vulnerabilities** : Weaknesses in a system that may be able to be exploited in
    order to cause loss or harm
- **Threats** : A loss or harm that might befall a system
    - Interception Interruption Modification Fabrication
    - When designing a system, we need to state the threat model
- **Attack** : An action which exploits a vulnerability to execute a threat
- **Control/Defence** : Removing or reducing a vulnerability
    - You control a vulnerability to prevent an attack and defend against a threat.
    - Prevent it: prevent the attack
    - Deter it: make the attack harder or more expensive 
    - Deflect it: make yourself less attractive to attacker 
    - Detect it: notice that attack is occurring (or has occurred)
    - Recover from it: mitigate the effects of the attack 
- **Principle of Easiest Penetration** : “A system is only as strong as its weakest link
- **Principle of Adequate Protection** : Don’t spend 100,000 to protect a system that
    can only cause 1,000 in damage
- **Ways to protect any of our assets** (Hardware, software, data):
    - **Cryptography** : signatures, transactions with cryptographic protocols,
       Ensuring the integrity of stored data
    - **Software Controls** : password, OS separate usr’s actions, Virus scanners,
       Development controls, personal firewalls
    - **Hardware Controls** : using separate hardware to protect the system as a whole e.g.
       Fingerprint readers,Smart tokens,Firewall, Intrusion detection systems


- **Physical Controls** : Protection of the hardware itself, as well as physical access to
    the console, storage media. e.g. locks, off-site backups, guards
- **Policies and Procedures** : Non-technical means can be used to protect against
- some classes of attack, e.g. Rules for passwords, Training in best security practices

### Module 2

Why is it so hard to write secure programs
Ans: Axiom (Murphy): Programs have bugs / Corollary: Security-relevant programs
have security bugs

#### 1. Flaws, faults, and failures

A flaw is a problem with a program, Flaws come in two types: faults and failures

- A **fault** is a potential problem is for programmer
- A **failure** is when something actually goes wrong is for user
How to find a fault, and how to fix them
- find: when experiences a failure, try to work backwards to uncover the fault
- try to cause failures (think like an attacker)
- fix: making small edits ( **patches** ) to the program(“penetrate and patch)


#### 2. Unintentional security flaws

Some flaws are intentional / inherent

- Malicious flaws
- Non-malicious
- Most security flaws are caused by unintentional program errors
- **TLS Heartbeat mechanism** : is designed to keep SSL/TLS connections alive even
when no data is being transmitted.letters


- there was a missing bounds check in the code
- **Apple’s SSL/TLS Bug** (February 2014)
    - An active attacker (a “man-in-the-middle) could potentially exploit this flaw to get
       a user to accept a counterfeit key that was chosen by the attacker.
    - 

###### Types of unintentional flaws

**- Buffer overflows**
    - most commonly exploited type of security flaw
    - strcpy(buffer, argv1) buffer
    - Upshot: overwrite things like the saved return address.
    - Targets: programs on a local machine that run with setuid (superuser) privileges
    - Defences: Programmer: use a language with bounds checking
       Compiler: place padding between data and return address
       Memory: Non-executable stack (memory page is either writable or executable)
       OS: Stack at random virtual addresses for each process
**- Integer overflows**
    - Attacker can pass values to program that will trigger overflow
**- Format string vulnerabilities**
    - printf(), fprintf(), sprintf()
**- Incomplete mediation**
    - ensure that what the user has entered constitutes a meaningful request
    - Client-side mediation: submit Javascript
    - client-side state: Webs will put hidden fields in the form which are passed back to
       the server when the user submits the form.
    - Defences against incomplete mediation: 1.do server-side mediation 2.Make sure
       client has not modified the data in any way.


**- TOCTTOU erros**
    - Time-Of-Check To Time-Of-Use
    - Keep a private copy of the request itself so that the request can’t be altered during
       the race
    - Where possible, act on the object itself, and not on some level of indirection
       - Make access control decisions based on filehandles
    - If that’s not possible, use locks to ensure the object is not changed during the race

##### 3. Malicious code: Malware

**- Virus:** Malicious code that adds itself to benign programs/files
    - Code for spreading  code for actual attack, Usually activated by users
    - host: program/document/system: copy to the beginning of programs/ add it as a
       macro to other files(documents with macros)/ computer boosted and active
    - Spreading: by send infected files
    - payload: erase hard drive/ Install a keystroke logger/ attacking target website
    - Spotting viruses: when files add to pc/ always scab entire state of pc
       - Signature-based protection: keep a list of known viruses with signature
          - infection code and payload code
          - the place they try to hide/how to propagates to others
       - Behaviour-based protection: look for suspicious patterns of behaviour
          - False negatives: fail to identify a threat that is present
          - False positives: claim a threat is present when it is not
- **Worms** : Malicious code spreading with no or little user involvement
    - self-contained piece of code that can replicate with little or no user involvement
    - Worms often use security flaws in widely deployed software as a path to infection
    - The Morris worm: fist buffer overflow exploit first internet worm.
    - The Code Red worm: exploited for Microsofts IIS web server
    - The Slammer worm: denial-of-service attack, first Warhol worm can
       infected with a single UDP packet


- Stuxnet: Very promiscuous/Very stealthy()/Very targeted(807-1210HZ)
- WannaCry: 2017
- **Trojans** : Malicious code hidden in seemingly innocent program that you download
- Ransomware: ( CryptoLocker in 2013)
- **Logic Bombs** : Malicious code hidden in programs already on your machine, wait
for a certain trigger to go off
- usually written by “insiders, and are meant to be triggered sometime in the future
- Spotting Trojan horses and logic bombs: User is intentionally running the code...
- don’t run code from entrusted sources
- prevent the payload from doing bad things

##### 4. Other malicious code

**- Web bugs (beacon):** object (usually a 1x1 pixel transparent image) embedded in a
    web page, which is fetched from a different server from the one that served the web
    page itself. then your knowledge or consent would be sent.
**- Back doors/trapdoor:** a set of instructions designed to bypass the normal
    authentication mechanism and allow access to the system to anyone who knows the
    back door exists.
**- Salami attacks:** an attack that is made up of many smaller, often considered
    inconsequential, attacks.
**- Privilege escalation:** an attack which raises the privilege level of the attacker
**- Rootkits:** a tool often used by “script kiddies, two parts:
    - A method for gaining unauthorized root / administrator privileges on a machine
    - A way to hide its own existence, Sometimes just this stealth part is called the
       rootkit.
    - stealth capability: clean up log messages-> modify commands-> modify kernel

```
Breeds Hosted Stealthy
Virus Y Y N
Worm Y N N
Trojan N Y Y
```

- e.g: Sony XCP
**- Keystroke logging
-** Application-specific loggers **:** Record only those keystrokes associated with a
particular application, such as an IM client
**-** System keyboard loggers **:** Record all keystrokes that are pressed (maybe only for
one particular target user)
**-** Hardware keyboard loggers **:** A small piece of hardware that sits between the
keyboard and the computer.
**- Interface illusions**
- Fake user interface
- Phishing: Fake website
- Phishing Detection: Unusual email/ Attachments with uncommon names/ unusual
wording/ No Https.
- Man-in-the-middle attacks
- e.g: Keyboard logging, interface illusions, and phishing

##### 5. Non malicious flaws

**- Covert channels:** An attacker creates a capability to transfer sensitive/unauthorized
    information through a channel that is not supposed to transmit that information. 
**- Side channels** : It turns out there are some very powerful attacks called side
    channel attacks
**-** Potential Attack Vectors

##### 6. Controls against security flaws in programs

**Software lifecycle:**

**1. Specification
2. Design**


- Modularity: should have low coupling(need encapsulation)
- Encapsulation: each modules should self-contained
- information hiding: The internals of one module cannot be visible to other modules
    - stronger statement than encapsulation: the implementation and internal state of
       one module should be hidden from developers of other modules
- Mutual suspicion: check their inputs are sensible before acting on them
- confinement:if Module A needs to call a potentially untrustworthy Module B, it
    can confine it (also known as sandboxing)
**3. Implementation**
- Don’t use C
- Static code analysis: use tools to find
- Formal methods: formal methods try to prove that the code does exactly what it’s
supposed to do.
- Genetic diversity: try to be different
**4. Change management**
- Source code and configuration control: Track all changes to either the source
code or the configuration information (what features to enable, what version to build,
etc.) in some kind of management system
**5. Code review**
- Guided code reviews: author explain why and how is done.(useful for changes to
code), Important for safety-critical systems!
- Easter egg code review
**6. Testing**
- Black-box testing: A test where you just have access to a completed object is a
black-box test fuzz testing
- White-box/clear-box testing: If you’re testing conformance to a specification by
taking into account knowledge of the design and implementation, that’s white-box
testing
- White-box testing is useful for regression testing


**7. Documentation**
    - write down things you tried that didn’t work
    - Write down the choices you made
    - Make checklists of things to be careful of
**8. Maintenance**

### Module 3

##### 1 Protection in general-purpose operating systems

- **Operating systems** allows different users to access different resources in a shared
    way. Identification and authentication are required for this access control
- Sequentially (based on executives)  Interleaving (based on monitors)
- **Separation** : Keep one user’s objects separate from other users
    - Physical separation
       - Use different physical resources for different users
       - Easy to implement, but expensive and inefficient
    - Temporal separation
       - Execute different users’ programs at different times
    - Logical separation
       - User is given the impression that no other users exist
       - As done by an operating system
    - Cryptographic separation
       - Encrypt data and make it unintelligible to outsiders/ Complex
**- Memory and address protection**
    - the OS can exploit hardware support for this protection, so it’s cheap
    - Memory protection is part of translation from virtual to physical addresses(MMU)
- Protection techniques
    - Fence register
    - Base/bounds register pair:
       - 


- different values for each user program
- Maintained by OS during context switch
- Limited flexibility
- Segmentation
- Advantages:
- Each address reference is checked for protection by hardware
- Many different classes of data items can be assigned different levels of
protection
- Users can share access to a segment, with potentially different access rights
- Users cannot access an un-permitted segment
- Disadvantages: 
- External fragmentation 
- Dynamic length of segments requires costly out-of-bounds check for generated
physical addresses
- Segment names are difficult to implement efficiently
- Paging
- Advantages:
- Each address reference is checked for protection by hardware
- Users can share access to a page, with potentially different access rights
- Users cannot access an un-permitted page
- Unpopular pages can be moved to disk to free memory
- Disadvantages:
- Internal fragmentation 
- Assigning different levels of protection to different classes of data items not
feasible
- x86 architecture
- x86 architecture has both segmentation and paging
- Memory protection bits indicate no access, read/write access or read-only access
- Most processors also include NX (No eXecute) bit


##### 2 Access control

- **Three goals** :
    1. Check every access: Else OS might fail to notice that access has been revoked
    2. Enforce least privilege: Grant program access only to smallest number of objects
       required to perform a task
    3. Verify acceptable use: Limit types of activity that can be performed on an
       object(for integrity reasons)
**- Access control matrix**
    - access control matrix is typically implemented as:
       - a set of a **ccess control lists** ACLs(column-wise) 
          - e.g: File 1: Alice:orw, Bob:r, File 2: Alice:rx, Bob:orx, Carol:rx
       - a set of **capabilities** (row-wise) 
          - A capability is an unforgeable() token
          - e.g Alice: File 1:orw, File 2:rx, File 3:o
          - Token can be transferable
       - or a combination
          - open() -> check ACL -> check capability for read or write
          - read()/write() -> check capability whether type of access is allowed
**- Role-based access control (RBAC)**
    - objects that a user can access depend on the user’s job function (role)
    - administrator assigns users to roles and grants access rights to roles
    - a user takes new tole, update only her role assignment, not access rights
    - Available in many commercial databases 
    - Hierarchical roles: reduce number of role/access tights assignments
    - Users can have multiple roles
    - Separation of Duty: a task need A and B role, these 2 cannot be same person

##### 3 User authentication

- Computer systems often have to identify (who r u) and authenticate(prove it) users
    before authorizing them


- Four classes of authentication factors: knows(Password), has(cookie), is(Biometrics:
    fingerprint) ,context(Location, time)
- **Passwords** : Security problems with passwords
    - Password guessing attacks: Brute-force: try all possible
       - Offline attack: Attack requires that attacker has encrypted password file or
          encrypted document
       - Online attack: guess your banking password by trying to log in to your bank’s
          website
       - Store only a digital fingerprint of the password (using a cryptographic hash, see
          later) in the password file
**- Password hygiene**
- Use a password manager to create and store passwords
- Use a pass phrase: randomly chosen words, avoid common phrases
- Have site-specific passwords
- Don’t reveal passwords to others
- Password files must be end up on backup tapes
**- Defending against guessing attacks**
- UNIX use user-specific salt in the password fingerprint
- Don’t use a standard cryptographic hash (like SHA-1 or SHA-512) to compute the
stored fingerprint
- An additional defence is to use a MAC(a secret key to compute the password
fingerprint)
- Password Recovery
- need to store an encrypted version of the password (keep safe)
**- Interception attacks**
- Attacker intercepts password while it is in transmission from client to server
- Challenge-response protocols 1. server send random challenge to a client ->
2. Client uses challenge and password to computer a one-time password and
send back to server-> 3.server check


- There are cryptographic protocols (e.g., SRP) that make intercepted information
    useless to an attacker
**- Server authentication**
- user should also authenticate system (server)else password might end up with
attacker!
- Biometrics(): Authenticate user based on physical characteristics
- Local vs. remote authentication
- Biometrics work well for local authentication
- in local authentication, 
- Authentication vs. identification
- Authentication: 
- Identification: (close not equality)
- False positives: AB
- Fale negative: A

##### 4 Security policies and models

**- Trusted operating systems**
    - Typically a trusted operating system builds on four factors:
       - ->->->
       - **Policy** : A set of rules outlining what is secured and why
       - **Model** : A model that implements the policy and that can be used for reasoning
          about the policy
       - **Design** : A specification of how the OS implements the model
       - **Trust** : Assurance that the OS is implemented according to design
**- Trusted software**
    - Functional correctness :Software works correctly
    - Enforcement of integrity(): Wrong inputs don’t impact correctness
       of data
    - Limited privilege: Access rights are minimized and not passed to others


- Appropriate confidence level(): Software has been rated as required by
    environment
**- Security policies**
- Each object/subject has a sensitivity/clearance level
- Subject s can access object o iff level(s)  level(o) and compartments(s) 
compartments(o)
- Commercial security policies
- Rooted in military security policies()
- Chinese Wall security policy
- 
- ss-property: s osoo
- *-propertysoo()
**- Security models**
- Lattices(): for every a and b, there is a unique lowest upper bound u for which
u dom a and u dom b and a unique greatest lower bound l for which a dom l
and b dom l ()
- **Bell-La Padula
confidentiality model:** Regulates information flow in MLS policies
clearance(o) > C(o)


- Underlying principle: Information can only flow up
- ss-property (“no read up): 
- *-property (“no write down): 
- **Biba integrity model** (): Prevent inappropriate modification of data
- Dual of Bell-La Padula model integrity(o)> I(o)
- Write access: s can modify o only if I(s) dom I(o) 
- Read access: s can read o only if I(o) dom I(s) 
- Can use dynamic integrity levels instead
- Subject Low Watermark Property: If subject s reads object o, then I(s) 
glb(I(s), I(o)), where glb()  greatest lower bound sos
- Object Low Watermark Property: If subject s modifies object o, then I(o) 
glb(I(s), I(o)) soo
- Integrity of subject/object can only go down, information flows down

##### 5 Trusted operating system design

- Security must be part of design early on
- Eight design principles for security:
    - **Least privilege** : Operate using fewest privileges possible
    - **Economy of mechanism** : Protection mechanism should be simple and
       straightforward
    - **Open design:** Avoid security by obscurity and Secret keys or passwords, but not
       secret algorithms
    - **Complete mediation** : Every access attempt must be checked
    - **Permission based / Fail-safe defaults** : Default should be denial of access
    - **Separation of privileges:** Two or more conditions must be met to get access
    - **Least common mechanism** : Every shared mechanism could potentiallybe
       used as a covert channel


- **Easy of use:** If protection mechanism is difficult to use, nobody will use it or it will
    be used in the wrong way
- **Access control**
- Mandatory access control (MAC): Chinese Wall, Bell-La Padula
- Discretionary access control (DAC): UNIX and windows
**- Object reuse protection**
-  stack
- OS should erase returned memory before handing it out to other users
- Hidden data: 
**- Complete mediation**
- all accesses must be checked
- Preventing access to OS
**- Trusted path**
- give feed back to the keystrokes and mouse
**- Accountability and audit**
- keep an audit log of all security-related events
- provides accountability if something goes bad
- At what granularity should events be logged
- For fine-grained logs, we might run into space/efficiency problems or finding
actual attack can be difficult 
- For coarse-grained logs, we might miss attack entirely or don’t have enough
details about it
**- Intrusion detection
- Trusted computing base (TCB)**
- TCB consists of the part of a trusted OS that is necessary to enforce OS security
policy
- Separate security kernel makes it easier to validate and maintain security
functionality


- Reference monitor: most important part of TCB, Must be amperproof 
    Unbypassable  Analyzable 
- **Application Insulation**
- Trusted code segment is encrypted in memory using a key living in secure hardware
(close to CPU)
- Untrusted code talks with trusted code via compact API
- Least privilege in popular OSs
- Windows Vista: 
- Traditional UNIX: a root and a user
- SELinux and AppArmor: use MAC for Linux, no more root user
- Chroot:
- Sandbox/jail a command by changing its root directory
- cannot access file outside its jail
- Compartmentalization: Split application into parts and apply least privilege to
each part
- setuid/suid bitU: If suid bit is set for an executable, the executable will execute under
the identity of its owner, not under the identity of the caller
**- Assurance**
- How can we convince others to trust our OS: Testing, Formal
verification,Validation(Requirements checking, design and code reviews,
system testing)
- **Evaluation** : Have trusted entity evaluate OS and certify that OS satisfies some
criteria,Two well-known sets of criteria are the **“Orange Book** of the U.S.
Department of Defence and the **Common Criteria**
- **Orange book:** D to A
- **Common criteria:** more international effort, Have Protection Profiles, which list
security threats and objectives, EAL1 to EAL7, Windows XP is EAL4  C


## Module 4

###### 1. Network concepts

```
TCP/IP protocol suite
```
- Participants knew and trusted each other
- Design addressed non-malicious errors (e.g., packet drops), but not
    malicious errors

###### 2. Threats in networks

- Port scan
    - port: different app running on the same server with each port
    - Attackers send queries to ports on target machine and try to identify the kind of
       app is running on a port
    - identify based on loose-lipped app or how the app implements a protocol
    - Loose-lipped system can show (non-confidential) info to attacker
       - Login app can show info about OS or whether ID is valid
       - Goal of attacker is to find app with remotely exploitable flaw
       - (Loose-lippedportflow)
- Intelligence
    - Social engineering
    - Dumpster diving
    - Eavesdropping() on oral communication


- Eavesdropping and wiretapping
    - Owner of node can monitor communication flowing though node
       - Active wiretapping involves modification or fabrication of communication
    - can eavesdrop across a link
    - Or when communication is accidentally sent to attacker’s node
    - 
- communication media
    - Copper cable: Inductance
    - Optical fiber: no Inductance
    - Microwave/satellite communication
    - WIFI: Can be easily intercepted by anyone with a WiFi-capable (mobile) device
- Misdelivered info
- Local Area Network (LAN)
- An attacker can change this and use a packet sniffer to capture these packets
- Impersonation
- Impersonate a person by stealing his/her password
- Exploit trust relationships between machines/accounts
- Spoofing
- Object (node, person, URL, Web page, email, WiFi access point,... )
masquerades as another one
- Web page spoofing and URL spoofing are used in Phishing attacks
- “Evil Twin attack for WiFi access points
- Session hijacking
- TCP protocol sets up state at sender and receiver end nodes and uses this state
while exchanging packets
- Attacker can sniff or steal cookie and masquerade as client\
- Man-in-the-middle attacks are similar attacker becomes stealth intermediate node,
not end node
- Traffic analysis


- TCP/IP has each packet include unique addresses for the packet’s sender and
    receiver end nodes, which makes traffic analysis easy
- Integrity attacks
- Attacker can modify packets while they are being transmitted
- Line noise, network congestion, or software errors could also cause these
problems
- DNS cache poisoning
- create wrong mapping to host name and address
- Protocol failures
- TCP includes a mechanism that asks a sender node to slow down if the network is
congested but An attacker could just ignore these requests
- Some implementations do not check whether a packet is well formatted
- Some protocols include broken security mechanisms
- Web site vulnerabilities
- Web site defacements
- Accessing a URL has a web server return HTML code
- Attacker sends malicious URL to web server
- Cross-site scripting (XSS)/request forgery (CSRF) attacks (code injection)
- XSS: Code steals sensitive information (e.g., cookie) contained in the web
page and sends it to attacker
- CSRF: Code performs malicious action at some web site
- **Denial of service (DoS)**
- 1. Cutting a wire or jamming a wireless signal
- 2. Flooding a node by overloading its Internet connection or its processing
capacity
- 3. ping of death
- send a large ping packet
- 4. ping flood
- ping victim
- 5. Surf attack


- spoof address of sender end node in ping packet to victims address
- broadcast ping packet
- 6.SYN flood
- attacker send many SYNs, but no ACKs
- 7. Exploit knowledge of implementation details about a node to make node
perform poorly
- 8. Send packet fragments that cannot be reassembled properly
- 9. Craft packets such that they are all hashed into the same bucket in a hash
table
- 10. Black hole attack (packet drop attack)
- Malicious router announces low cost for victim destination and discards any
traffic destined for victim router
- Has also happened because of router misconfiguration
- 11. DNS attacks
- DNS cache poisoning can lead to packets being routed to the wrong host
**- Reflection  Amplification DDoS Attack**
- **Amplification** : A vulnerable network node (e.g., a home wifi router) runs a
service (e.g., SNMP) that responds to queries with much more data than the
query itself
- **Reflection** : The attacker spoofs the source address of the queries to that of the
victim so that the vulnerable network nodes send (reflect) responses to the victim
- Hard to defend:
- The response traffic is coming from innocent nodes 
- It is hard to identify the real source (perhaps bots) of the queries due to spoofing
- Distributed denial of service (DDoS)
- Most attacking machines participate without knowledge of their owners
- Attacker use Trojan, buffer overflow to install malicious software
- Machine becomes zombie/bot, a network of bots called a bonnet
- New Generation Botnets
- Today’s botnets are very sophisticated


- Botnets’ Distributed, dynamic  redundant control infrastructure
    - “ **Fast Flux** 
       - A single host name maps to hundreds of addresses of infected machines
       - Machines proxy to malicious websites or to “mothership
       - Machines are constantly swapped in/out of DNS to make racking difficult
    - **Domain Generation Algorithm**
       - Infected machine generates a large set of domain names that changes
          every day
       - It contacts a random subset of these names for updates
       - To control the botnet, authorities would have to take control of 50,000
          different domain names each day
- Sample botnet: Storm
    - September 2017 send junk emails, rented for pharmacy/ investment spam
       self-defence
- Sample botnet: Mirai
    - fall 2016, attack 600000 loT devices due to unchanged default passwords
- Active code
- Java 1.2 can break out of sandbox if approved by user
- Java 7 runs signed applets out of sandbox by default
- **Privileged:** The application will run with unrestricted access which may put your
computer and personal information at risk.
- **Sandboxed** : The application will run with restricted  access that is
intended to protect your computer and personal information.
- Script kiddies
- Script kiddies can download scripts and raise an attack with minimum effort
3. Network security controls
- Design and implementation
- Always check inputs!!!! use white list, not black lis
- Segmentation and separation
- don’t put all server on a single machine


- Redundancy
    - Avoid single points of failure
    - servers should be deployed in a redundant way on multiple machines, ideally with
       different software to get genetic diversity and at different locations
    - Redundant servers should be kept in (close) sync so that backup servers can take
       over easily
- Access controls
    - ACLs on routers
       - all traffic to company goes though a single router
       - can use ACL drops packets in case of flooding attack
       - ACLs are expensive for high-traffic routers
       - Difficult to gather logs for forensics analysis
       - Source addresses of packets in flood are typically spoofed and dynamic

##### 4. Firewalls

- All traffic into/out of a company has to go through a small number of gates
- **Choke points** carefully examine traffic, especially incoming, and might refuse it
    access
- company need multiple layers of defence / defence in depth
- Type if firewalls
    **- Packet filtering gateways**
       - Simplest type
       - make decision based on header of a packet(address, port num)
       - ignore payload of packet
       - can drop spoofed traffic
    - **Stateful inspection firewalls**
       - More expensive than packet filtering
       - Keep state to identify packets that belong together
       - IP layer can fragment packets, so firewall might have to re-assemble packets for
          stateful inspection
    **- Personal firewalls**


- for user/s computer, forbid everything unless explicitly
- Protect against attacks on servers running on computer
**- Demilitarized Zone (DMZ)**
- Subnetwork that contains an organization’s external services, accessible to the
Internet
- Internal firewall protects internal network from attacks lodged in DMZ



###### 5. Honeypots / honey-nets

- Set up an (unprotected) computer or an entire network as a trap for an attacker
- System has no production value, so any activity is suspicious
- attackersattackerattacker
- Types of honeypots
    **- Low interaction**
       - 
    **- High interaction**
       -  

###### 6. Intrusion detection systems (IDSs)

- protect against inside attackers or insiders making mistakes and can be subverted
- Monitor activity to identify malicious or suspicious events
    - receive-> store and analyze-> Take action
- Host-based and network-based IDSs (Distributed IDSs combine them)
    - **Host-based** : protect host which run IDS, can exploit many info


- **Network-based IDSs** : run on node, protect all hosts attached to, hard to subvert,
    rely on info available in monitored packets
- Signature-based and heuristic/anomaly-based IDSs
- **Signature-based** : signature based, fail for new attacks or sign changes
- **heuristic/anomaly-based** : look for un-normal behaviour
- By modelling good behaviour and raising alert when system activity no longer
resembles this model
- Or by modelling bad behaviour and raising alert when system activity resembles
this model
- activity is good/suspicious/unknown
- Example: **Tripwire**
- Anomaly-based, host-based IDS, detects file modifications
- save fingerprints in a safe place, periodically re-compute FP

## Module 5

**1. Basics of cryptography**
    - Cryptography: plaintext -> cipher text
    - Cryptanalysis: Breaking secret messages
    - Alice, Bob, Carol, Dave, Eve, Mallory, Trent(trusted third party)
    - Cryptography three major types of components
       - Confidentiality components (reading)
       - Integrity components (modifying)
       - Authenticity components (impersonating)
    - Kerckhoffs’ Principle (19th c.): The security of a crypto-system should not rely on a
       secret that’s hard (or expensive) to change
    - Strong cryptosystems
       - Eve know the algorithm
       - Eve know some part of the plaintext
       - Eve know a number of corresponding plaintext/ciphertext pairs
       - Eve can access to an encryption and decryption oracle


**2. Secret-key encryption**
    - Secret-key encryption
    - Perfect secret-key encryption: one-time Pad
       - The key must be truly random, not pseudorandom
       - The key must never be used more than once!
    - 40-bit/56-bit crypto
       - it has 240/256 possible keys
       - 18hr for 1 pc, 11min for 1 lab, 5ms for BOINC
    - Types of secret-key cryptosystems
       - **Stream ciphers**
          - A stream cipher is what you get if you take the One-Time Pad, but use a
             pseudorandom keystream instead of a truly random one
          - very fast and useful when send a lot of data
       **- Block ciphers**
          - Block ciphers operate on the message one block at a time, Blocks are
             usually 64 or 128 bits long
          - **AES** is the block cipher everyone should use today
       - Modes of operation
          - This is called **Electronic Code Book (ECB)** mode
          - Common ones include Cipher Block Chaining ( **CBC** ), Counter ( **CTR** ), and
             Galois Counter ( **GCM** ) modes
          - an **IV** (Initial Value), which acts much like a salt
**3. Public-key encryption**
    - Also called asymmetric cryptography
       - A send a secret message to B without any prearranged shared secret
       - one key for encrypt, one key for decrypt
       - B gives everyone a copy of his public key, A encrypt by it, B use secret key
    - Public key sizes
       - Eve has shortcuts, 2128 RSA key need 233 tries


- Hybrid cryptography
    - public-key need longer keys, so need take long time
    - Pick a random 128-bit key K for a secret-key crypto-system
    - Encrypt large message with K (AES)
    - Encrypt the K using a public-key crypto-system
    - Send message an key to B
**4. Integrity**
- use Cryptographic checksum
- Cryptographic hash functions
- A hash function h takes an arbitrary length string x and computes a fixed length
string y  h(x) called a **message digest**
- (MD5, SHA-1, SHA-2, SHA-3)
- should have three properties
- **Preimage-resistance** : Given y, it’s hard to find x such that h(x)  y (i.e., a
“preimage of x)
- **Second preimage-resistance** : Given x, it’s hard to find x  x such that h(x)  
h(x) (i.e., a “second preimage of h(x))
- **Collision-resistance** : It’s hard to find any two distinct values x , x  such that
h(x)  h(x) (a “collision)
**5. Authentication**
- Message authentication codes ( **MAC** )
- Encrypt-then-MAC is the recommended strategy
- crypto library already provides an authenticated encryption mode
- Repudiation
- A sent B a message M and tag T with key K, so B can known A sent it by K
- Some interactions should be repudiable
- Private conversations
- Some interactions should be non-repudiable
- Electronic commerce


- Digital signatures
    - A sent a message with A’s digital signature
       - A(not an impersonator) sent the message
       - the message has not been changed
       - Bob can prove these facts to a third party
    - how to implement
       - A need to sign the message with her private signature key
       - B verify message by A’s public verification key
       - if it verifies correctly, the signature is valid
- Hybrid signatures
    - A send message and a signature on a hash of the message
    - the hash is smaller than message, so its faster to sign
- Combining public-key encryption and digital signatures
    - A,B has 2 pairs: (encryption, decryption) key pair,(signature, verification) pair
    - A use B’s encryption key to encrypt a message for B
    - A use A’s sign key to sign the message
    - B use A’s verify key to check signature
    - B use B’s decryption key to decrypt
- Relationship between key pairs
    - (sig, verify) is long-lived, (encrypt, decrypt) is short lived
    - new (E,D), A use sign key to sign new encrypt key, and B use A’s verify key
    - if A and B is interactive she can use secret-key not (E,D) pair
- The Key Management Problem
    - how B find A’s verification key
       - He can know it personally (manual keying) :SSH
       - He can trust a friend to tell him (web of trust): PGP
       - He can trust some third party to tell him (CA’s): TLS/SSL
       - A **CA** is a trusted third party who keeps a directory of people’s (and
          organizations’) verification keys( Certificate Authority)
- A create a (sig, verify) pair, send verification key and personal info to **CA** , both
signed with A’s signature key


- CA would generates a **certificate** consisting of A’s personal info and verification
    key, the entire certificate is signed with the CA’s signature key
- everyone is assumed to have a copy of the CA’s verification key
- There can be multiple levels of certificate authorities level n CA issues
    certificates for level n1 CA: Public-key infrastructure ( **PKI** )
- Need to have only verification key of root CA to verify certificate chain
- Put them together into **protocols**
**6. Security controls using cryptography**
- Encrypted code
- processors that will only execute encrypted code
- processor decrypt instructions, key is processor-dependent
- Malware can not speed without knowing a processor’s key
- Encrypted data
- **Hard-drive** encryption protects data when laptop gets lost/stolen
- cant against other users legitimately use laptop/malware/got key
- OS authentication
- Authentication mechanisms often use cryptography
- can use hardware token
**7. Link-layer security**
- intended to protect **local area networks**
- **WEP** : Wired Equivalent Privacy
- Confidentiality: Prevent an adversary() from learning the contents of your
wireless traffic
- Access Control: Prevent an adversary from using your wireless infrastructure
- Data Integrity
- sender and receiver share a secret k(40 or 104 bit)
- to transmit a message M: ( **integrity** )
- compute checksum(M) and pick an IV and generate a keystream RC4(IV,k)
- XORM, c(M)> with the keystream to get the ciphertext
- transmit v and the ciphertext over the wireless link


- when receive v and ciphertext:
    - use RC4(v,k) got M’,c>, check whether c’  checksum(M’)
- Problem1: WEPIV
     24 224IV
    IV1/224IV
    0.5
- Problem2: WEPCRCCRC
    C(xy)C(x) C(y)
    
- problem3: 5 RC4IVk
    
    
- WEP **access control**
- if adversary wants to inject a new message F onto a WEP-protected network
- he only need a plaintext and ciphertext pair, he can get v and RC4(v,k)
- then C’  F,c(F)> XOR RC4(v,k) and he transmits v, C’
- C’ is correct encryption of F, so the message can be accepted
- WEP **authentication protocol**
- access point send a challenge string to the client
- client sends back challenge, WEP-encrypted with the shared secret k
- the wireless access point checks of the challenge is correctly encrypted, and if
so, accepts the client
- Problem4: this is enough not only to inject packets (as in the previous attack),
but also to execute the authentication protocol himself!
- WEP **decryption**
- The access point knows k it turns out the adversary can trick it into decrypting
the packet for him and telling him the result.
- Recovering a WEP key


- Problem5: Problem number 5: it turns out that when RC4 is used with similar
    keys, the output keystream has a subtle weakness
- Replacing WEP ( **WPA** )
- Wi-fi Protected Access ( **WPA** ) was rolled out as a short-term patch to WEP while
formal standards for a replacement protocol (IEEE 802.11i, later called **WPA2** )
were being developed
- replace CRC-32 with a real MAC(MIC)
- IV is 48 bits, key is changed frequently (TKIP)
- Ability to use 802.1x authentication server and most older WEP hardware
- 802.11i standard in 2004, WPA2 > Wi-fi in 2006
- WPA2: change PC4 and MIC to CCM authenticated encryption mode (using AES)
- Dictionary attacks still possible
8. Network-layer security (need security across networks, end-to-end)
- Virtual Private Networks ( **VPN** )
- Function: connect two networks that are physically isolated, and make them
appear to be a single network, or connect a host to one network
- Goal: adversary between the networks should not be able to read or modify the
traffic flowing across the VPN
- Setting up a VPN
- **VPN gateway** : one host on each side
- The local VPN gateway uses cryptography (encryption and integrity techniques)
to send the traffic to the remote VPN gateway (use Tunnelling)
- **Tunnelling** : TCP-over-IP is not tunnelling, IP-over-TCP, IP-over-IP, PPP(a link
layer protocol bottom of the stack) - over-DNS(an application layer protocol
top of the stack)
- **IPSec** : One standard way to set up a VPN
- Transport mode: laptop the contents of the original IP
packet
- Tunnel mode: 2 The contents and the header of the original
IP packetVPN gatewayIP packet destined


- other styles of VPN:
    - Microsoft’s PPTP:
    - VPN based on ssh
       - Tunnel PPP over ssh: IP-over-PPP-over-ssh-over-TCP-over-IP
       - OpenSSH v4 supports IP-over-SSH tunnelling directly
**9. Transport-layer security and privacy**
- Transport-layer security mechanisms transform arbitrary TCP connections to add
security, and similarly for “privacy instead of “security
- The main transport-layer **security** mechanism: **TLS** (formerly known as **SSL** )
- Secure Socket Layer(SSL) to protect HTTP, also can protect any TCP connection
- HTTP  SSL  HTTPS
- SSL went though a few revisions, standardized into TLS(Transport Layer
Security)
- TLS at a high level
- client connects to server, and which cipher-suites it knows
- **Server** choose which cipher-suite and sends its certificate to client, contains:
- host name
- verification key
- other administrative information
- a signature from a Certificate Authority(CA)
- **Client** validates server’s certificate
- check signature from a CA whose public key is embedded in client
- check whether host name in certificate match the client wanna access
- **Client and server** run a key agreement protocol to establish keys for
symmetric encryption and MAC algorithms from the chosen cipher-suite
- Security properties provided by TLS
- Server authentication
- Message integrity
- Message confidentiality
- Client authentication (optional)


- The success of TLS
    - TLS (including SSL) has become the most successful **Privacy Enhancing**
       **Technology (PET)** ever, reasons:
- It comes with browser
- just work, without any configure
- it can protects the privacy of ur communications most time(WiFi)
- we wanna protect metadata/ existence/ contents
- The main transport-layer **privacy** mechanism: **Tor**
- Tor allows you to make TCP connections without revealing your IP address
- Scattered the Internet are about 7,000 Tor nodes, also called Onion Routers
- **How** it works:
- A pick one Tor nodes(n1) and use public-key cryptography to establish an
encrypted communication to it
- A tells n1 to contact n2, and make new encrypted communication channel
- many times, A tells the last node to connect to the website
- A share k1k2k3 with n1n2n3, sends EK1(EK2(EK3(M))), n1 decrypt and send
result EK2(EK3(M)) to n2...
- website replies message to n3, n3 encrypt it with k3 and send Ek3(R) to n2
- **Who** knows what
- n1 knows A is using Tor and next node is n2, but dont know A website wanna
- n3 knows some Tor user is using a particular website but doesn’t known who
- The website itself only knows that it got a connection from Tor node n3
- n3 and website is not encrypted!!!
- Anonymity vs. pseudonymity (vs)
- Tor provides for **anonymity** in TCP connections over the Internet, both unlink-ably
(long-term) and linkable (short-term)
- The Nymity Slider
- Verinymity: Government ID, SIN, credit card #, address
- Persistent pseudonymity: Noms de plume, many blogs
- Linkable anonymity: Prepaid phone cards, loyalty cards


- Unlinkable anonymity: Cash payments, Tor
- it’s easy to modify it to have a higher level of nymity, but hard to modify it to have
    a lower level 
**10. Application-layer security and privacy**
- Secure remote login (ssh)
- Usual usage (simplified):
- Client connects to server
- Server sends its verification key(client verify)
- Client and server run a key agreement protocol to establish session keys,server
signs its messages (all communication is encrypted and MACd with keys)
- Client authenticated to server
- Server accepts authentication, login proceeds
- **Authentication** with ssh
- Send a password over the encrypted channel: server need hash ur pwd
- Sign a random challenge with ur private signature key: server needs ur public
verification key
- Anonymity for email: **remailers**
- Type 0 remailers1990s)
- how it worked:
- send email to anon.penot.fi and forwarded to receiver
- From address is changed to ......
- replies to anon address would mapped back to real address
- list
- Type I remailers / Cypherpunk remailers
- Cypherpunk (type I) remailers removed the central point of trust
- Messages sent through a chain of several remailers
- Each step is encrypted, remailers also delay and reorder messages
- NO Replies!!!!!
- Easier recipient anonymity: alt.anonymous.messages


- Type II remailers / Mixmaster remailers
    - Mixmaster (type II) remailers appeared in the late 1990s
    - Constant-length messages to avoid an observer watching “that big file travel
       through the network
    - against replay attacks/ improved message reordering
    - requires a special email client to construct : pre-mail(a drop-in wrapper for
       sendmail)
- Type III remailers / Mixminion remailer
    - Native (and much improved) support for pseudonymity
    - Improved protection against replay and key compromise attacks
    - But it’s not very well deployed or mature /
- **Pretty Good Privacy(PGP)** : primary use is to protect the contents of email
messages
- Uses public-key cryptography to provide: encryption. digital signatures
- **Fingerprint** is a cryptographic hash of a key
    - A downloads B’s key from web
    - A’s software calculates the fingerprint
    - A call B and ask B read actual fingerprint to her
    - if match, A got an authentic copy of B’s key
    - (if C doesn’t know B, it will not work)
- Signing keys
    - when A verified B, A will use her signature key to sign B’s key
    - B can attack A’s signature to the key on his web
    - Now A can acts as an introducer for B
    - If C have checked A, she can use B’s key without check
- **Plot twist**
- if A and B’s communications are recorded by the bad guys
- Bs computer is stolon by this bad guy or broken
- Casual conversations
- off-the-record: No one else can hear/knows what they say/prove what they say


**- Perfect forward secrecy**
    - Future key compromises should not reveal past communication
    - Use secret-key encryption with a short-lived key (a session key)
    - The session key is created by a modified Diffie-Hellman protocol
    - Use long-term keys only to authenticate the Diffie-Hellman protocol messages
    - plot twist
**- Deniable authentication**
    - Do not want digital signatures (Non-repudiation is great for signing contracts)
    - do want authentication
    - use MAC (Message Authentication Codes)
- Using these techniques, we can make our online conversations more like face-to-face
“off-the-record conversations
- **Off-the-Record Messaging (OTR)** is software that allows you to have private
conversations over instant messaging, providing:
    - Confidentiality: only B can read the messages A sends him
    - Authentication: B is assured the message came from A
    - Perfect Forward Secrecy: 
    - Deniability: C
**- Signal Protocol**
- signal is an app for iOS, Android and Chrome(based on OTR used for encrypted
SMS), used by WhatsApp, Google Allo, and Facebook Messenger
- Perfect Forward Secrecy: uses a “ratchet to constantly rotate session keys
- Deniability: use “triple Diffie-Hellman deniable authenticated key
exchange( **DAKE** ), anyone can forge by their public keys
-


## Module 6

**1.Introduction to databases**

- database: a collection data ( **records)**
- each record consists of fields( **elements** )
- structure( **schema** ) set by database administrator
- Database management system ( **DBMS** ) provides support for queries and
    management
- Most popular DBMAS is based on **relational model**
- columns ( **attributes** ) and rows( **tuples** )
- result of a query is a **subschema
2.Security requirements**
- database integrity
- Protect against database corruption authorized
- Recover from physical problems: , log of transactions
- Element integrity
- Access control to limit who can update element
- Element checks to validate correctness
- typically enforced by triggers
- Change log or shadow fields to undo erroneous changes
- Error detection codes to protect against OS or hard disk problems
**- two-phase update**
- for a set of operations, either all or none of them should be performed
- First phase: 
- Second phase: 
- concurrency control
- Need to perform A and B as atomic operations
- Referential integrity
- Each table has a primary key and some foreign keys
- Referential integrityforeign key


- Auditability
    - Keep an audit log of all database accesses (read and write)
    - Must decide about granularity() of logging
- Access control
    - Might have to control access at the relation, record or even element level
    - Access control might consider past queries or type of query
- User authentication  Availability
    - Database might do its own authentication
    - Additional checks possible
    - availability can suffer if multiple users wanna access same record
**3.Data disclosure and inference (/)**
- Types of data disclosure
- Exact data, Bounds, Negative result()Existence, Probable value
    - Security vs. precision()
       - Security: 
       - Precision: 
- Data inference
- Derivation of sensitive data from (supposedly) non-sensitive data
- Direct attack: issues query directly produce sensitive data
- Indirect attack
- Infer sensitive data from statical results
- Sum, Count, Mean, Median
- Tracker attack
- T is a query whose result matches between 2k and N-2k
- q(C)q(C or T)q(C or not T)q(S) if q(C)  k
- q(C)  2q(S)q(not C or T)q(not C or not T) if q(C) > N-k
- Controls for statistical inference attacks
-
4.Multilevel security databases


5.Designs of secure databases
6.Data mining and data release



