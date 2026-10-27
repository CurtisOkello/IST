# Cybersecurity Fundamentals: Information, Information Systems and Their Value

**Level:** Diploma in Cybersecurity
**Duration:** 90-minute instructional block
**Topics covered:** (1) Introduction to Information and its Importance; (2) Information Systems and the Value of Information

---

## Session Overview

### Learning Outcomes

By the end of this session, you will be able to:

1. **Distinguish** between raw data and actionable information, and place both within the DIKW pyramid using SOC examples.
2. **Explain** the CIA Triad and justify why information is the ultimate target of threat actors.
3. **Describe** the information lifecycle and apply a four-tier classification model.
4. **Define** an information system and identify its five components, their vulnerabilities and defenses.
5. **Explain** how compromising an information system destroys the value of information.
6. **Apply** the People-Process-Technology (PPT) framework to a practical SOC environment.

### Suggested 90-Minute Timetable

| Time | Segment | Activity |
|------|---------|----------|
| 0:00 - 0:10 | Data vs Information | Lecture + quick quiz |
| 0:10 - 0:25 | DIKW Pyramid with SOC examples | Lecture + worked example |
| 0:25 - 0:40 | CIA Triad | Lecture + scenario matching |
| 0:40 - 0:55 | Lifecycle and Classification | Lecture + classification exercise |
| 0:55 - 1:10 | Information Systems and 5 components | Lecture + component mapping |
| 1:10 - 1:20 | Value destruction + PPT framework | Discussion |
| 1:20 - 1:30 | Case study, review and Q&A | Group activity |

---

# PART 1: Cybersecurity Fundamentals - Introduction to Information and its Importance

## 1.1 Why Start With Information?

Cybersecurity is often described in terms of firewalls, malware and hackers. These are **tools and threats**. The thing they act upon is **information**. Every security control, from a password policy to a Security Operations Center (SOC), exists for one purpose: **to protect the information an organization depends on.**

> **Core principle:** You cannot protect what you do not understand. Understanding information, its forms, its value and its lifecycle is the foundation of every security decision.

---

## 1.2 Data vs Information

### Definitions

- **Data** is raw, unprocessed facts, figures, symbols or signals with no context or meaning on their own.
- **Information** is data that has been **processed, organized, structured and given context**, making it meaningful and useful for decision-making.

### Comparison

| Aspect | **Data** | **Information** |
|--------|----------|-----------------|
| **Nature** | Raw, unprocessed facts | Processed, contextualized data |
| **Meaning** | Little or none on its own | Meaningful and relevant |
| **Purpose** | Input to be processed | Output used to make decisions |
| **Form** | Numbers, text, logs, bytes, signals | Reports, alerts, dashboards, summaries |
| **Usefulness** | Low until processed | High and actionable |
| **Security example** | `192.168.4.17`, `3389`, `03:12:44`, `FAILED` | "Host 192.168.4.17 had 480 failed RDP logins in 4 minutes from a foreign IP at 03:12, consistent with brute-force." |

### Worked Example

**Raw data (firewall log lines):**

```
03:12:44  203.0.113.50 -> 10.0.0.15:3389  DENY
03:12:45  203.0.113.50 -> 10.0.0.15:3389  DENY
03:12:45  203.0.113.50 -> 10.0.0.15:3389  DENY
... (hundreds more)
```

**Information (after analysis):**

> "External IP 203.0.113.50 attempted over 400 connections to the Remote Desktop port of server 10.0.0.15 within five minutes. This indicates an automated brute-force or scanning attempt against an exposed service."

The data was always there. Only after **processing and context** did it become something a defender can act on.

### Why This Matters for Security

- Attackers steal **data**, but what they monetize or weaponize is the **information** inside it.
- Defenders collect enormous volumes of **data** (logs); the SOC's job is to convert it into **information** fast enough to act.
- **Data without context creates alert fatigue; information with context creates action.**

---

## 1.3 The DIKW Pyramid

The **DIKW pyramid** (Data, Information, Knowledge, Wisdom) models how raw facts become sound decisions. Each level adds **context, meaning and judgment**.

```
          /\
         /  \        WISDOM       "What is the right thing to do?"
        /----\
       /      \      KNOWLEDGE    "How does this fit what we know? What does it mean?"
      /--------\
     /          \    INFORMATION  "Who, what, where, when?"
    /------------\
   /              \  DATA         "Raw facts and signals"
  /________________\
```

### DIKW Levels in a SOC Context

| Level | Definition | SOC Example | Typical Role/Tool |
|-------|------------|-------------|-------------------|
| **Data** | Raw, isolated facts and events | Millions of log lines: firewall events, authentication attempts, DNS queries, endpoint telemetry | Sensors, agents, log sources |
| **Information** | Data organized and contextualized | "User `jdoe` failed login 50 times from IP 198.51.100.9 between 02:00-02:05" | SIEM correlation, parsing, dashboards |
| **Knowledge** | Information combined with experience, patterns and threat intelligence | "This pattern matches **credential stuffing**, and that IP appears on a threat-intel feed linked to a known botnet" | Tier 1/2 analysts, threat intel, MITRE ATT&CK mapping |
| **Wisdom** | Knowledge applied with judgment to decide the best action | "Block the IP, force a password reset for `jdoe`, enable MFA for all accounts, and update the lockout policy" | Senior analysts, SOC manager, CISO |

### Walk-Through: One Incident Across the Pyramid

1. **Data:** An endpoint agent records `powershell.exe -enc JABz...` executed at 14:02.
2. **Information:** The SIEM shows PowerShell with an **encoded command** launched by a **Word process** on the finance workstation.
3. **Knowledge:** The analyst recognizes this as a **common macro-based malware technique** (ATT&CK T1059.001) used to download a second-stage payload.
4. **Wisdom:** The team **isolates the host**, preserves evidence, hunts for the same behavior org-wide, and **disables macros from the internet** by policy to prevent recurrence.

> **Key takeaway:** Security maturity is measured by how far up the pyramid an organization can move **quickly and reliably**.

---

## 1.4 The CIA Triad

The **CIA Triad** is the foundational model for information security. Every attack and every control can be mapped to one or more of its three properties.

### The Three Properties

| Property | Definition | Goal | Common Threats | Common Controls |
|----------|------------|------|----------------|-----------------|
| **Confidentiality** | Information is accessible **only to authorized** people/systems | Prevent unauthorized disclosure | Data breaches, eavesdropping, phishing, insider theft, shoulder surfing | **Encryption**, access control, MFA, classification, DLP |
| **Integrity** | Information is **accurate, complete and unaltered** except by authorized change | Prevent unauthorized modification | Tampering, SQL injection, malware, man-in-the-middle, insider fraud | **Hashing**, digital signatures, change control, input validation, audit logs |
| **Availability** | Information and systems are **accessible when needed** by authorized users | Prevent disruption of access | DDoS, ransomware, hardware failure, power loss, natural disaster | **Redundancy**, backups, DR/BCP, patching, DDoS mitigation |

### Real-World Illustrations

- **Confidentiality breach:** A database of customer records is exfiltrated and sold. The data is unchanged and the system still works, but **secrecy is lost**.
- **Integrity breach:** An attacker alters account balances or a patient's medication record. Everything looks normal, but the **information is now false**.
- **Availability breach:** Ransomware encrypts hospital files. Nothing is leaked, but **no one can access what they need**.

### Extended Concepts (Awareness Level)

- **Authentication:** verifying identity ("Are you who you claim to be?").
- **Authorization:** determining permitted actions ("What are you allowed to do?").
- **Non-repudiation:** preventing denial of an action (digital signatures, audit trails).
- **Accountability:** being able to trace actions to an individual.

### Why Information Is the Ultimate Target of Threat Actors

Attackers rarely attack hardware or software for its own sake. These are **means to an end**. The end is the **information**, because information can be:

| Attacker Goal | How Information Is Exploited |
|---------------|------------------------------|
| **Financial gain** | Sell card numbers and credentials; ransom data; commit fraud |
| **Espionage** | Steal trade secrets, intellectual property, government intelligence |
| **Identity theft** | Use personal data (ID numbers, dates of birth) to impersonate victims |
| **Extortion** | Threaten to leak sensitive data (double extortion ransomware) |
| **Disruption / sabotage** | Destroy or corrupt data to cripple operations |
| **Further attacks** | Use stolen credentials/config information to move deeper into the network |

> **Remember:** Information is valuable, portable, copyable and often poorly protected. That combination makes it the preferred target.

---

## 1.5 The Information Lifecycle

Information passes through stages from birth to disposal. **It must be protected at every stage**, because an attacker only needs to find the weakest one.

### The Six Stages

```
Creation -> Storage -> Use -> Transmission -> Archiving -> Destruction
```

| Stage | Description | Key Risks | Security Controls |
|-------|-------------|-----------|-------------------|
| **1. Creation** | Information is generated, collected or received (forms, sensors, emails, transactions) | Collecting unnecessary data; no classification at origin; insecure input channels | **Classify at creation**, data minimization, input validation, secure forms |
| **2. Storage** | Information is held on servers, databases, endpoints, cloud or removable media | Unauthorized access, misconfigured cloud buckets, lost devices, unencrypted storage | **Encryption at rest**, access control, secure configuration, backups |
| **3. Use** | Information is accessed, processed or modified by users and applications | Insider misuse, over-privileged accounts, shadow IT, shoulder surfing | **Least privilege**, role-based access, activity monitoring, DLP |
| **4. Transmission** | Information moves across networks, email, APIs or physical media | Interception, man-in-the-middle, misdirected emails, insecure protocols | **Encryption in transit** (TLS/VPN), secure protocols, email controls |
| **5. Archiving** | Information no longer actively used is retained for legal/business reasons | Weak protection of old data, forgotten archives, media degradation | Encrypted archives, retention schedules, access restrictions, integrity checks |
| **6. Destruction** | Information is permanently and securely disposed of | **Data remanence**, discarded drives, incomplete deletion, dumpster diving | **Secure wipe**, degaussing, physical destruction, certificates of destruction |

### Three Important Principles

- **Data in three states:** *At rest* (stored), *in transit* (moving), *in use* (being processed). Each needs different protection.
- **Retention is a security issue:** data you no longer hold cannot be breached. Keep it only as long as legally and operationally required.
- **Deletion is not destruction:** simply deleting a file does not remove it from the media. Secure sanitization is required.

---

## 1.6 Information Classification

**Information classification** assigns a sensitivity label to information so the correct level of protection is applied. Without classification, organizations either **over-protect everything** (costly) or **under-protect critical assets** (dangerous).

### Standard Four-Tier Model

| Level | Description | Impact if Disclosed | Examples | Typical Handling |
|-------|-------------|---------------------|----------|------------------|
| **Public** | Approved for unrestricted release | None or negligible | Marketing brochures, press releases, public website content | No special controls; integrity still protected |
| **Internal** | For employees/authorized partners only; not meant for public | Minor embarrassment or limited operational impact | Internal memos, org charts, policies, intranet content | Access limited to staff; not shared externally without approval |
| **Confidential** | Sensitive business or personal information | Significant financial, legal or reputational damage | Customer records, contracts, financial reports, HR files, source code | **Encryption**, need-to-know access, logged access, NDAs |
| **Restricted** | Most sensitive; highest harm if exposed | Severe, possibly irreversible damage; regulatory or legal penalties | Authentication secrets/keys, health records, payment card data, M&A plans, security architecture | **Strong encryption**, MFA, strict named-individual access, full audit trail, special disposal |

### Classification Rules of Thumb

- Information should be **classified by its owner**, based on the impact of a CIA breach.
- **Handling rules** (storage, transmission, destruction) follow from the label.
- Classification should be **reviewed periodically**; sensitivity can change (e.g., an unreleased financial result becomes public after announcement).
- Unlabeled information should default to a **protective** classification until assessed.

### Quick Classification Exercise

Classify each item, then justify your answer:

1. A company's published annual report.
2. The staff phone directory.
3. A customer database with national ID numbers.
4. Administrator password hashes and encryption keys.

*Suggested answers:* (1) Public, (2) Internal, (3) Confidential or Restricted depending on regulation, (4) Restricted.

---

# PART 2: Information Systems and the Value of Information

## 2.1 What Is an Information System?

An **Information System (IS)** is an **integrated set of components for collecting, storing, processing and distributing information** to support an organization's operations, decision-making and control.

An information system is **not just a computer**. It is the combination of **technology, data, and the people and procedures** that use it.

### Examples of Information Systems

- A hospital patient-management system
- A bank's core banking and mobile app platform
- A university student information portal
- An e-commerce platform with payment processing
- A SOC's SIEM and ticketing environment

### The IS as the Primary Attack Surface

The **attack surface** is the sum of all points where an unauthorized party could try to enter, extract data from, or disrupt a system.

Information is rarely attacked directly in the abstract. It is attacked **through the information system that holds, processes and transmits it**. Therefore:

- Every component of an IS is a **potential entry point**.
- Every interface (web application, API, VPN, email, USB port, employee) **expands the attack surface**.
- **Reducing and monitoring the attack surface** is a central goal of cybersecurity.

> **Key relationship:** Information is the **asset**; the information system is the **container and gateway**; threat actors attack the gateway to reach the asset.

---

## 2.2 The Five Components of an Information System

| # | Component | What It Is |
|---|-----------|-----------|
| 1 | **Hardware** | The physical devices that make up the system |
| 2 | **Software** | The programs and code that run on hardware |
| 3 | **Data** | The facts and information stored and processed |
| 4 | **Procedures** | The documented rules and processes for operating and using the system |
| 5 | **People** | The users, administrators and decision-makers who interact with the system |

A weakness in **any one** component can compromise the whole system. Security is **only as strong as the weakest component**.

### Component Detail: Vulnerabilities and Defenses

#### 1. Hardware

*Servers, workstations, laptops, mobile devices, routers, switches, firewalls, IoT devices, storage media, USB drives.*

| Common Vulnerabilities | Defenses |
|------------------------|----------|
| Physical theft or loss of devices | **Physical security** (locks, badges, CCTV, secured server rooms) |
| Unauthorized physical access to ports | Port blocking, **device control**, tamper-evident seals |
| Malicious USB devices / hardware implants | Removable-media policy, device whitelisting |
| Unpatched firmware, end-of-life equipment | **Firmware updates**, lifecycle management, asset inventory |
| Power failure, overheating, hardware failure | UPS, generators, cooling, **redundancy** |
| Unencrypted lost laptops/phones | **Full-disk encryption**, remote wipe (MDM) |
| Insecure IoT and unmanaged devices | Network segmentation, asset discovery, default-credential removal |

#### 2. Software

*Operating systems, applications, databases, web applications, firmware, security tools, cloud services.*

| Common Vulnerabilities | Defenses |
|------------------------|----------|
| Unpatched operating systems and applications | **Patch management**, vulnerability scanning |
| Software bugs (buffer overflow, injection flaws, XSS) | **Secure coding**, code review, SAST/DAST testing |
| Misconfiguration and default settings | **Hardening baselines**, configuration management |
| Malware (viruses, ransomware, trojans) | **Anti-malware/EDR**, application allow-listing |
| Vulnerable third-party libraries (supply chain) | Software composition analysis, trusted sources, SBOMs |
| Unauthorized or pirated software | Approved software list, licensing control |

#### 3. Data

*Databases, files, emails, logs, backups, cloud storage; data at rest, in transit and in use.*

| Common Vulnerabilities | Defenses |
|------------------------|----------|
| Unencrypted data at rest or in transit | **Encryption** (e.g., AES at rest, TLS in transit) |
| Excessive access permissions | **Least privilege**, role-based access control |
| Data leakage (email, USB, cloud uploads) | **Data Loss Prevention (DLP)**, monitoring |
| Corruption or unauthorized modification | **Hashing**, integrity monitoring, version control |
| Lost or unrecoverable data | **Backups** (3-2-1 rule), tested recovery |
| Unclassified or unmanaged data sprawl | **Classification**, data inventory, retention policy |
| Insecure disposal | Secure wiping and destruction procedures |

#### 4. Procedures

*Policies, standards, workflows, incident response plans, change management, onboarding/offboarding, backup procedures.*

| Common Vulnerabilities | Defenses |
|------------------------|----------|
| Missing or outdated security policies | Documented, approved, **regularly reviewed policies** |
| Unenforced or ignored procedures | Audits, compliance checks, management support |
| No incident response plan | **IR plan** with defined roles, playbooks, and exercises |
| Weak change management (untested changes break security) | Formal **change control** and approval |
| Slow account deprovisioning for leavers | Automated **offboarding** and access reviews |
| No tested backup/recovery process | **BCP/DR plans** with regular testing |
| Lack of segregation of duties | Split critical tasks between individuals, dual control |

#### 5. People

*Employees, administrators, contractors, executives, customers, third-party vendors.*

| Common Vulnerabilities | Defenses |
|------------------------|----------|
| **Phishing and social engineering** susceptibility | **Security awareness training**, phishing simulations |
| Weak, reused or shared passwords | Password policy, **password managers, MFA** |
| Insider threats (malicious or negligent) | Least privilege, monitoring, background checks, **UEBA** |
| Accidental data exposure (misdirected email, misconfiguration) | Training, DLP, clear handling rules |
| Poor security culture | Leadership commitment, reporting culture, accountability |
| Third-party/contractor risk | Vendor due diligence, contracts, restricted access |

> **Teaching point:** The **People** component is frequently the most exploited, because attackers find it easier to deceive a person than to defeat strong technical controls. This is why it is often called the "human firewall" or the "weakest link."

### Cross-Component Attack Example

A single incident often touches several components:

1. **People:** An employee clicks a phishing link (people vulnerability).
2. **Software:** A malicious macro executes on an unpatched application (software vulnerability).
3. **Hardware:** The infected workstation connects to the corporate network (unmanaged endpoint).
4. **Procedures:** No process flags the unusual behavior or enforces rapid isolation (procedural gap).
5. **Data:** Sensitive customer files are encrypted and exfiltrated (data compromised).

---

## 2.3 How Compromise of an Information System Destroys the Value of Information

Information has value only while it remains **trustworthy, protected and usable**. When an information system is compromised, the CIA properties fail, and the value of the information is **destroyed or severely reduced**.

### Impact Mapped to the CIA Triad

| Property Lost | What Is Destroyed | Business Consequence | Example |
|---------------|-------------------|----------------------|---------|
| **Confidentiality** | **Trust and competitive advantage** | Loss of customer and partner trust; legal penalties; regulatory fines; loss of intellectual property; reputational damage | A retailer's breach exposes millions of customers' details; customers leave and regulators investigate |
| **Integrity** | **Decision-making ability and reliability** | Decisions based on false data; fraud; safety risks; loss of audit credibility; legal disputes | Altered lab results or financial figures lead to wrong treatment or wrong investment |
| **Availability** | **Operational continuity and productivity** | Revenue loss; service outage; missed deadlines; contractual penalties; customer frustration | Ransomware halts a hospital's systems and delays patient care |

### Dimensions of Impact

| Dimension | Examples |
|-----------|----------|
| **Financial** | Incident response costs, ransom, lost revenue, fines, legal fees, insurance increases |
| **Operational** | Downtime, disrupted supply chains, manual workarounds, recovery effort |
| **Reputational** | Loss of customer confidence, negative media, brand damage |
| **Legal / Regulatory** | Data protection violations, breach notification duties, lawsuits |
| **Strategic** | Stolen intellectual property, lost competitive edge, compromised mergers |
| **Human / Safety** | Harm to individuals whose data is exposed; risk to life in healthcare or industrial systems |

### Key Insight

> **Loss of confidentiality destroys trust. Loss of integrity destroys decision-making. Loss of availability destroys operations.**

A particularly dangerous case is an **integrity compromise that goes undetected**. Unlike a visible outage, silently altered data can continue to drive wrong decisions for a long time.

### The Value Equation

Information value can be thought of as:

**Value of Information = Accuracy (Integrity) x Exclusivity (Confidentiality) x Accessibility (Availability) x Relevance (Timeliness)**

If any factor drops towards zero, the overall value collapses.

---

## 2.4 The PPT Framework (People, Process, Technology)

Effective information protection cannot rely on technology alone. The **PPT framework** states that security requires **three balanced, interdependent pillars**:

| Pillar | Focus | Question It Answers |
|--------|-------|---------------------|
| **People** | Skills, awareness, roles, culture, accountability | *Who* protects and uses the information? |
| **Process** | Policies, procedures, workflows, governance | *How* is protection carried out consistently? |
| **Technology** | Tools, systems, automation, infrastructure | *What* enables and enforces protection? |

> **Principle:** Technology without trained people is misused. People without process are inconsistent. Process without technology does not scale. **All three are needed.**

### Relationship to the Five IS Components

| IS Component | PPT Pillar |
|--------------|------------|
| Hardware, Software, Data (technical elements) | **Technology** |
| Procedures | **Process** |
| People | **People** |

### PPT Applied in a Practical SOC

| Pillar | SOC Application | Examples |
|--------|-----------------|----------|
| **People** | Staffed, trained and organized team | Tiered analysts (**Tier 1** triage, **Tier 2** investigation, **Tier 3** threat hunting/forensics), SOC manager, threat intelligence analysts, incident responders; ongoing training and certification; on-call rotations and shift handovers; user awareness programs |
| **Process** | Defined and repeatable operations | **Incident response lifecycle** (preparation, detection, containment, eradication, recovery, lessons learned); **playbooks/runbooks** for common alerts; escalation matrix; SLAs; change management; reporting; post-incident reviews; metrics such as MTTD and MTTR |
| **Technology** | Tools that collect, analyze and respond | **SIEM** (log aggregation and correlation); **EDR/XDR** (endpoint visibility); **IDS/IPS** and firewalls; **SOAR** (automated response); vulnerability scanners; threat intelligence platforms; ticketing and case management |

### PPT in Action: Phishing Incident Walk-Through

1. **Technology:** The email gateway and SIEM flag a suspicious message and an unusual login. An alert is generated.
2. **People:** A Tier 1 analyst triages the alert and recognizes a likely credential-phishing campaign.
3. **Process:** The analyst follows the **phishing playbook**: confirm, isolate affected accounts, escalate to Tier 2, notify the user, and document the case.
4. **Technology:** SOAR automatically **blocks the sender domain**, purges the email from other mailboxes and forces credential resets.
5. **People and Process:** After closure, the team holds a **lessons-learned review**, updates the playbook, and runs targeted awareness training.

This shows how a weakness in any pillar (no alert, untrained analyst, no playbook) would let the attack succeed.

### SOC Metrics Linked to PPT

| Metric | Meaning | Pillar Most Influenced |
|--------|---------|------------------------|
| **MTTD** (Mean Time to Detect) | How quickly threats are identified | Technology and People |
| **MTTR** (Mean Time to Respond/Recover) | How quickly threats are contained and resolved | Process and People |
| **False positive rate** | Proportion of alerts that are not real threats | Technology (tuning) and People (skill) |
| **Training/phishing-test results** | Staff awareness level | People |

---

# Putting It All Together

```
INFORMATION  (valuable asset; protected by CIA)
     |
     |  moves through the lifecycle and carries a classification
     v
INFORMATION SYSTEM  (Hardware, Software, Data, Procedures, People)
     |
     |  this is the attack surface that threat actors target
     v
PROTECTED BY  PPT  (People + Process + Technology, operationalized in the SOC)
     |
     v
RESULT: Information stays confidential, accurate and available, so its VALUE is preserved.
```

---

## Case Study for Group Discussion (10 minutes)

**Scenario:** A regional bank's SOC detects that a customer-service employee's account downloaded 40,000 customer records at 2:00 AM. The account was recently the target of a phishing email. The database was not encrypted, and the bank has no documented process for suspicious bulk downloads.

**Discuss:**

1. Which **CIA properties** are at risk? Which is most affected?
2. Where does this incident sit in the **DIKW pyramid** at each stage of detection and response?
3. Which of the **five IS components** failed? Identify at least one vulnerability in each affected component.
4. At which **lifecycle stages** were controls missing? What **classification** should the customer records carry?
5. Propose improvements across **People, Process and Technology**.
6. Describe how the **value of information** was damaged.

---

## Key Terms Glossary

| Term | Definition |
|------|-----------|
| **Data** | Raw, unprocessed facts without context |
| **Information** | Processed, contextualized data that supports decisions |
| **DIKW** | Data, Information, Knowledge, Wisdom hierarchy |
| **Confidentiality** | Only authorized parties can access information |
| **Integrity** | Information remains accurate and unaltered |
| **Availability** | Information is accessible when needed |
| **Information lifecycle** | Creation, storage, use, transmission, archiving, destruction |
| **Information classification** | Labeling information by sensitivity to drive protection |
| **Information System (IS)** | Integrated hardware, software, data, procedures and people that manage information |
| **Attack surface** | All points where an attacker could attempt to compromise a system |
| **Least privilege** | Granting only the minimum access needed to do a job |
| **Data remanence** | Residual data left after deletion |
| **SIEM** | Security Information and Event Management platform |
| **SOC** | Security Operations Center; team and facility that monitors and responds to threats |
| **PPT** | People, Process, Technology framework |
| **MTTD / MTTR** | Mean time to detect / respond (or recover) |

---

## Review Questions

1. Explain the difference between data and information, using a security log example.
2. Describe each level of the DIKW pyramid and give a SOC example for each.
3. Define the CIA Triad. Give one threat and one control for each property.
4. Why is information considered the ultimate target of threat actors?
5. List the six stages of the information lifecycle and one key control for each.
6. Describe the four classification levels and give an example of each.
7. What is an information system, and why is it considered the primary attack surface?
8. Name the five components of an IS and give one vulnerability and one defense for each.
9. Explain how loss of confidentiality, integrity and availability each destroy the value of information.
10. Describe the PPT framework and show how it is applied within a SOC.

---

## Summary: Key Takeaways

- **Data** becomes **information** through context, and climbs the **DIKW pyramid** toward wisdom through analysis and judgment.
- The **CIA Triad** defines what security must protect: confidentiality, integrity and availability.
- **Information is the ultimate target**, because it can be sold, ransomed, weaponized or used to enable further attacks.
- Information must be protected across its **entire lifecycle** and handled according to its **classification**.
- An **information system** has **five components**: hardware, software, data, procedures and people. Each is part of the **attack surface**.
- Compromise of the system **destroys value**: lost confidentiality destroys **trust**, lost integrity destroys **decision-making**, lost availability destroys **operations**.
- The **PPT framework** ensures protection is balanced across **People, Process and Technology**, and is operationalized daily in the **SOC**.

> **Final thought:** Security is not a product you buy. It is a continuous practice of protecting the value of information through well-trained people, disciplined processes and well-configured technology.

---

*End of study notes.*
