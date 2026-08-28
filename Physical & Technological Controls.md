# Annex A Domains Part 2 — Physical & Technological Controls
**Module:** Module 9 — Information Security Management System (ISMS) | **Unit:** Unit 3 — ISO/IEC 27001 Lead Auditor

---

## Session Objectives & Real-World Context

**What You Will Learn:**
- A detailed working knowledge of the **Physical Controls** theme (14 controls) — covering perimeter security, environmental protection, secure work areas, equipment handling, and the full physical asset lifecycle from installation to disposal.
- A detailed working knowledge of the **Technological Controls** theme (34 controls) — the largest single theme in Annex A — covering endpoint and access management, operational resilience, monitoring and logging, network security, cryptography, and the full secure development lifecycle.
- How today's controls connect directly to concepts you already know cold from Module 8 — malware protection, Sysmon/SIEM logging, network segmentation, and secure coding — now reframed as specific, numbered, auditable Annex A requirements rather than general technical best practice.
- Why several Technological controls were **newly added in the 2022 revision** specifically to address modern risks (data masking, data leakage prevention, web filtering, monitoring activities) that either didn't exist or weren't yet significant when the 2013 version was published.
- How a genuinely thorough gap assessment treats Physical and Technological controls as **interdependent**, not separate silos — because, as today's case studies demonstrate, a purely technological control can be completely undermined by a physical failure, and vice versa.

**Why It Matters to a Security Professional:** With today's session, you complete your first full pass through all four Annex A themes — Organizational and People from your previous session, Physical and Technological today. This is the single densest technical session in this entire unit, and deliberately so: the Technological theme alone contains more individual controls (34) than the Organizational and People themes combined (45), reflecting just how much of a modern ISMS's actual, day-to-day risk surface lives in technical systems. Everything you learned about malware, SIEM hunting, and network architecture in Module 8 has a specific, numbered home in today's content — by the end of this session you should be able to look at almost any technical control you've studied so far in this diploma and immediately say which Annex A control number it satisfies.

---

## Core Theory & Technical Mechanics

### Physical Controls — Protecting the Tangible Layer

Recall from Day 6's four-layer model (People, Process, Systems, Information) that "systems" explicitly includes manual and physical systems, not just digital ones. The Physical Controls theme exists because no amount of technological sophistication protects information that walks out the front door on a stolen laptop or an unshredded printout — a lesson today's secondary case study will demonstrate with striking clarity.

**Cluster: Perimeter and Entry Control (7.1–7.4)**
- **7.1 Physical security perimeters** — requires security perimeters to be defined and used to protect areas containing information and other associated assets, establishing the physical equivalent of the network segmentation concept you'll encounter again in the Technological theme below.
- **7.2 Physical entry** — requires secure areas to be protected by appropriate entry controls and access points, ensuring that only authorized individuals can physically enter areas housing sensitive assets — the physical-world counterpart to the Access Rights control (5.18) from your previous session.
- **7.3 Securing offices, rooms, and facilities** — requires physical security for offices, rooms, and facilities to be designed and implemented, extending perimeter thinking down to individual rooms within an otherwise-secured building (a server room within a general office, for instance, warranting its own additional layer of entry control).
- **7.4 Physical security monitoring** — requires premises to be continuously monitored for unauthorized physical access, typically through CCTV, security guards, or intrusion detection systems — the physical equivalent of the continuous SIEM monitoring concept from Module 8, now applied to the physical environment rather than the network.

**Cluster: Environmental and Operational Protection (7.5–7.8)**
- **7.5 Protecting against physical and environmental threats** — requires protection against physical and environmental threats such as natural disasters, malicious attack, or accidents to be designed and implemented, directly connecting to the Natural and Environmental threat categories from Unit 2's Day 3 taxonomy.
- **7.6 Working in secure areas** — requires procedures and controls for working in secure areas to be designed and implemented, governing how personnel (and visitors) behave once inside a secure zone, not just how they get in.
- **7.7 Clear desk and clear screen** — requires clear desk rules for papers and removable storage media, and clear screen rules for information processing facilities, to be defined and appropriately enforced — a deceptively simple control that directly addresses the risk of sensitive information being casually visible to anyone walking past an unattended desk.
- **7.8 Equipment siting and protection** — requires equipment to be sited securely and protected, considering factors like reducing the risk of environmental threats and hazards, and opportunities for unauthorized access.

**Cluster: Media, Off-Site Assets, and Supporting Infrastructure (7.9–7.12)**
- **7.9 Security of assets off-premises** — requires off-site assets to be protected, directly relevant to laptops, mobile devices, and portable media taken outside the organization's physical premises — the exact control category central to today's Veterans Affairs case study below.
- **7.10 Storage media** — requires storage media to be managed through their lifecycle of acquisition, use, transportation, and disposal in accordance with the organization's classification scheme and handling requirements, directly connecting Day 2's classification content to the physical handling of the media that information is actually stored on.
- **7.11 Supporting utilities** — requires information processing facilities to be protected from power failures and other disruptions caused by failures in supporting utilities, connecting to the Availability leg of the CIA Triad and to the Colonial Pipeline-adjacent operational resilience themes covered earlier in this unit.
- **7.12 Cabling security** — requires cabling carrying power, data, or supporting information services to be protected from interception, interference, or damage — an easily overlooked control addressing the physical network layer that everything else in the Technological theme ultimately depends on.

**Cluster: Equipment Lifecycle (7.13–7.14)**
- **7.13 Equipment maintenance** — requires equipment to be maintained correctly to ensure the availability, integrity, and confidentiality of information, ensuring maintenance activities themselves (which often require third-party access or equipment being taken off-site for repair) don't become their own control gap.
- **7.14 Secure disposal or re-use of equipment** — requires items of equipment containing storage media to be verified to ensure that any sensitive data and licensed software has been removed or securely overwritten prior to disposal or re-use — directly connecting to the Information Deletion control (8.10) you'll encounter in the Technological theme below, and to the Disposal stage of the Information Lifecycle from Day 1.

### Technological Controls — The Largest Theme in Annex A

With 34 controls, the Technological theme requires careful clustering to remain manageable. Notice throughout how many of these controls formalize concepts you already studied in depth during Module 8 — today largely provides the official Annex A vocabulary for technical practices you've already built hands-on skill in.

**Cluster: Endpoint and Access Management (8.1–8.5)**
- **8.1 User endpoint devices** — requires information stored on, processed by, or accessible via user endpoint devices to be protected, covering laptops, desktops, and mobile devices as a specific, named control category.
- **8.2 Privileged access rights** — requires the allocation and use of privileged access rights to be restricted and managed, a control of particular significance given how many real-world incidents (including today's primary case study) trace back to over-broad or poorly monitored privileged access specifically, as distinct from ordinary user access covered under 5.18.
- **8.3 Information access restriction** — requires access to information and other associated assets to be restricted in accordance with the established access control policy, reinforcing 5.15 at the technical implementation level.
- **8.4 Access to source code** — requires read and write access to source code, development tools, and software libraries to be appropriately managed, protecting against unauthorized modification of the code that ultimately becomes an organization's production systems — directly relevant to the SolarWinds case study from Unit 2.
- **8.5 Secure authentication** — requires secure authentication technologies and procedures to be implemented based on information access restrictions and the access control policy — the formal Annex A anchor for the Multi-Factor Authentication concepts central to the Colonial Pipeline case study from earlier in this unit.

**Cluster: Operational Resilience and Malware (8.6–8.14)**
- **8.6 Capacity management** — requires the use of resources to be monitored and adjusted in line with current and expected capacity requirements, connecting to the Availability leg of the CIA Triad by ensuring systems don't fail simply from being overwhelmed by legitimate (or illegitimate, in a DDoS scenario) demand.
- **8.7 Protection against malware** — requires protection against malware to be implemented and supported by appropriate user awareness, the direct formal Annex A home for the entire malware taxonomy — viruses, worms, trojans, ransomware, fileless/LotL malware — you studied in exhaustive detail in Module 8.
- **8.8 Management of technical vulnerabilities** — requires information about technical vulnerabilities to be obtained, the organization's exposure evaluated, and appropriate measures taken, formalizing the vulnerability management and patching discipline central to the Colonial Pipeline and TalkTalk case studies covered earlier in this unit.
- **8.9 Configuration management** — requires configurations, including security configurations, of hardware, software, services, and networks to be established, documented, implemented, monitored, and reviewed — a control of central importance to today's primary case study.
- **8.10 Information deletion** (new in 2022) — requires information stored in information systems, devices, or in any other storage media to be deleted when no longer required, formalizing the Disposal stage of the Information Lifecycle from Day 1 into an explicit technical requirement.
- **8.11 Data masking** (new in 2022) — requires data masking to be used in accordance with the organization's access control policy and other related topic-specific policies, and business requirements — a technique for obscuring sensitive data (e.g., showing only the last four digits of an account number) while still allowing systems and staff to use the data for legitimate purposes without full exposure.
- **8.12 Data leakage prevention** (new in 2022) — requires data leakage prevention measures to be applied to systems, networks, and any other devices that process, store, or transmit sensitive information, directly connecting to the exfiltration/beaconing detection content from Module 8.
- **8.13 Information backup** — requires backup copies of information, software, and systems to be maintained and regularly tested, formalizing disaster recovery practice as an explicit, testable control (recall: an untested backup is not a genuine control at all, merely an assumption).
- **8.14 Redundancy of information processing facilities** — requires information processing facilities to be implemented with redundancy sufficient to meet availability requirements.

**Cluster: Monitoring and Logging (8.15–8.19)**
- **8.15 Logging** — requires logs that record activities, exceptions, faults, and other relevant events to be produced, stored, protected, and analyzed — the formal Annex A home for the entire Sysmon and Windows Event Log discipline you built extensive hands-on skill in throughout Module 8.
- **8.16 Monitoring activities** (new in 2022) — requires networks, systems, and applications to be monitored for anomalous behavior and appropriate action taken to evaluate potential information security incidents, the formal Annex A home for the SIEM correlation and threat-hunting workflows (Wazuh, beacon-hunting, EID correlation) that formed the practical backbone of Module 8's labs.
- **8.17 Clock synchronization** — requires the clocks of information processing systems to be synchronized to approved time sources, a deceptively small-sounding but critically important control: without synchronized clocks, correlating events across multiple systems during an incident investigation — exactly the kind of multi-source timeline reconstruction practiced in Module 8's labs — becomes far harder or outright unreliable.
- **8.18 Use of privileged utility programs** — requires the use of utility programs that can override system and application controls to be restricted and tightly controlled, addressing tools that, while sometimes legitimately necessary for administration, carry significant risk if misused or accessed by unauthorized personnel.
- **8.19 Installation of software on operational systems** — requires procedures and measures to be implemented to securely manage software installation on operational systems, preventing unauthorized or unvetted software from being introduced into production environments.

**Cluster: Network Security (8.20–8.23)**
- **8.20 Networks security** — requires networks and network devices to be secured, managed, and controlled to protect information in systems and applications, the overarching Annex A anchor for network-layer defense.
- **8.21 Security of network services** — requires security mechanisms, service levels, and service requirements of network services to be identified, implemented, and monitored.
- **8.22 Segregation of networks** — requires groups of information services, users, and information systems to be segregated in the organization's networks, the formal Annex A requirement behind the network segmentation failures identified in both the Equifax case study (Module 8) and, as you'll see below, today's primary Capital One case study.
- **8.23 Web filtering** (new in 2022) — requires access to external websites to be managed to reduce exposure to malicious content, a control formalizing what many organizations previously treated as a purely operational IT decision into an explicit, auditable security requirement.

**Cluster: Cryptography (8.24)**
- **8.24 Use of cryptography** — requires rules for the effective use of cryptography, including cryptographic key management, to be defined and implemented, covering encryption at rest, encryption in transit, and the often-overlooked but equally critical discipline of key management itself.

**Cluster: Secure Development Lifecycle (8.25–8.34)**
- **8.25 Secure development life cycle** — requires rules for the secure development of software and systems to be established and applied, the overarching umbrella control for this entire cluster.
- **8.26 Application security requirements** — requires information security requirements to be identified, specified, and approved when developing or acquiring applications.
- **8.27 Secure system architecture and engineering principles** — requires principles for engineering secure systems to be established, documented, maintained, and applied to any information system development activity.
- **8.28 Secure coding** — requires secure coding principles to be applied to software development, formalizing defensive programming practices as an explicit control rather than an informal developer skill.
- **8.29 Security testing in development and acceptance** — requires security testing processes to be defined and implemented in the development life cycle, directly connecting to the vulnerability scanning and sandbox-testing skills built in Module 8.
- **8.30 Outsourced development** — requires the organization to direct, monitor, and review the activities related to outsourced system development, extending the Supplier Relationship controls from your previous session specifically into the software development context.
- **8.31 Separation of development, test, and production environments** — requires development, testing, and production environments to be separated and secured, preventing exactly the kind of build-pipeline compromise central to the SolarWinds case study from Unit 2.
- **8.32 Change management** — requires changes to information processing facilities and information systems to be subject to change management procedures, ensuring modifications to production systems follow a controlled, reviewed, and auditable process rather than ad-hoc, unreviewed changes.
- **8.33 Test information** — requires test information to be appropriately selected, protected, and managed, specifically addressing the common, risky practice of using real, sensitive production data in lower-security test environments.
- **8.34 Protection of information systems during audit testing** — requires audit tests and other assurance activities involving assessment of operational systems to be planned and agreed between the tester and appropriate management, a control that closes the loop directly back to Unit 2's audit planning content, ensuring that the very act of auditing a live system doesn't itself introduce unacceptable risk or disruption.

### Non-Technical Analogies

> 🏰 **Physical Controls as a Medieval Castle's Full Defense-in-Depth.** The outer curtain wall and moat are the security perimeter (7.1); the guarded gatehouse checking everyone who enters is entry control (7.2); the inner keep, a further-secured building within the already-secured walls, represents securing specific offices and rooms (7.3); watchtowers with sentries scanning constantly are physical monitoring (7.4); reinforced construction against siege weapons and fire represents protection against physical and environmental threats (7.5); rules forbidding servants from leaving the treasury's ledgers open on a table represent clear desk and clear screen (7.7); a trusted courier escorting the kingdom's gold to a neighboring ally represents security of assets off-premises (7.9); the castle's own well and food stores represent supporting utilities (7.11); and finally, when an old, worn set of armor or a retired document is disposed of, ensuring no readable royal seal or sensitive marking remains represents secure disposal (7.14). A castle that has a magnificent wall but no rule against leaving the treasury ledger open on an unattended table has not actually protected its treasury at all.

> 🏭 **Technological Controls as a Modern Factory's Full Production and Security Stack.** Endpoint devices are the individual workstations on the factory floor (8.1); privileged access is the master key that only the floor supervisor holds (8.2); malware protection is the factory's pest-control and contamination-prevention program (8.7); logging and monitoring are the factory's continuous production-line sensors and the control room watching them in real time (8.15, 8.16); network segmentation is separating the hazardous chemical storage area from the general assembly floor with its own controlled access (8.22); cryptography is the tamper-evident sealed packaging on the factory's finished, high-value products (8.24); and the secure development lifecycle cluster (8.25–8.34) is the factory's full quality-engineering discipline — engineering review before a new production line is built, rigorous testing before a new process goes live, a strictly separated pilot/test production line kept apart from the real assembly line, and a formal change-control process before anyone is allowed to modify how the main line actually runs. A factory with excellent pest control but no separation between its test line and its live production line is one bad experimental batch away from a genuinely serious incident.

---

## Multi-Perspective Breakdown

**Attacker's POV:** Attackers specifically exploit the seams between Physical and Technological controls, precisely because organizations very often invest heavily in one theme while under-investing in the other. An organization with excellent network segmentation (8.22) and strong cryptography (8.24) can still be trivially compromised if a decommissioned laptop with an unencrypted hard drive is improperly disposed of (7.14/8.10) — the technological sophistication of the rest of the environment becomes irrelevant if a single physical control gap hands an attacker the data directly. Similarly, sophisticated attackers specifically target configuration management gaps (8.9) — as in today's primary case study — because a misconfigured cloud permission or firewall rule can bypass an enormous amount of otherwise well-implemented technical control, precisely because misconfiguration doesn't require defeating any control at all; it simply exploits a control that was never actually set correctly in the first place.

**Defender's / SOC Analyst's POV:** A huge proportion of the technical, hands-on work covered throughout Module 8 — Sysmon deployment, SIEM correlation, network segmentation review, vulnerability scanning — maps directly onto specific Technological controls covered today (8.15, 8.16, 8.20–8.22, 8.8). Recognizing this mapping is professionally valuable in a very concrete way: when a SOC Analyst implements or improves a piece of technical monitoring capability, they are not merely doing good technical work in the abstract — they are directly satisfying, and potentially generating audit evidence for, a specific, numbered Annex A requirement. A mature SOC function keeps this mapping explicit, so that ongoing operational work naturally produces the audit trail a certification or surveillance audit will later require, rather than operational security work and compliance evidence being treated as two entirely separate, duplicated efforts.

**Auditor's / Forensic Investigator's POV:** Auditing the Technological theme specifically requires the CAAT-based techniques and re-performance testing introduced in Unit 2's Day 4 session far more than document review alone — a policy stating that "networks are appropriately segmented" (8.22) means very little without actually testing whether traffic can, in practice, cross between segments that should be isolated. Forensic investigators reconstructing an incident timeline depend enormously on 8.15 (Logging) and 8.17 (Clock Synchronization) specifically — an investigation attempting to correlate events across multiple systems with unsynchronized clocks, or with insufficient logging in the first place, faces a dramatically harder evidentiary task, directly connecting today's content to the forensic methodology you will study formally in Module 11.

---

## Real-World Case Study

**Primary Case Study: The 2019 Capital One Data Breach — A Technological Configuration Failure**

**Incident Summary:** In 2019, Capital One, a major U.S. financial institution, suffered a breach exposing the personal information of approximately 100 million individuals in the United States and 6 million in Canada, including names, addresses, credit scores, and, for a subset of victims, Social Security numbers and linked bank account numbers. The data was hosted on Amazon Web Services (AWS) cloud infrastructure. The attacker, a former AWS employee, was identified and arrested relatively quickly after publicly discussing the intrusion online.

**Root Cause & Vulnerability Exploited:** The attacker exploited a **Server-Side Request Forgery (SSRF)** vulnerability in a misconfigured Web Application Firewall (WAF) that Capital One had deployed in its AWS environment. Through this vulnerability, the attacker was able to trick the WAF server into making requests to AWS's internal metadata service — a legitimate AWS feature designed to let cloud instances retrieve their own configuration information — and retrieve **temporary security credentials** associated with an IAM (Identity and Access Management) role assigned to that WAF instance. Critically, that IAM role had been granted **far broader permissions than the WAF instance actually needed** to perform its function — including permissions to list and read the contents of numerous Amazon S3 storage buckets containing sensitive customer data entirely unrelated to the WAF's own operational purpose. The attacker used these overly-broad, stolen temporary credentials to access and exfiltrate the data directly.

**Business & Legal Impact:** Capital One agreed to pay a $80 million civil penalty to U.S. federal banking regulators (the Office of the Comptroller of the Currency) and reached an approximately $190 million class-action settlement with affected customers. The company also faced significant reputational damage and was required to make substantial commitments to remediate its cloud security posture under regulatory oversight.

**Key Lessons for Defenders & Auditors — connecting directly to today's Technological theme:** This case is a textbook illustration of a **Configuration Management (8.9)** and **Privileged Access Rights (8.2)** failure occurring together. The WAF software itself was not exploited through some entirely novel, unpatchable flaw — SSRF is a well-understood, well-documented vulnerability class. The catastrophic scale of the breach resulted specifically from the IAM role attached to that WAF instance having permissions vastly exceeding what its actual function required — a direct, severe violation of the Principle of Least Privilege as applied to a *technical service identity*, not just a human user account. This is a crucial, often-underappreciated point: least-privilege thinking (which you first encountered in Module 8 applied to human accounts) applies with equal, arguably greater, force to the *service roles and permissions granted to applications and infrastructure components themselves* — a misconfigured service role can be exploited without any human credential ever being phished at all. An auditor applying today's framework, reviewing Capital One's cloud environment beforehand, should have specifically tested (not merely documented) whether the actual permissions granted to each service role were proportionate to that specific service's genuine operational need — exactly the kind of re-performance/CAAT-style technical testing from Unit 2's Day 4 session that a document-review-only audit would have completely missed, since the IAM policy documentation may well have existed and looked reasonable on paper while the actual configured permissions told a very different story.

**Secondary Case Study — The 2006 U.S. Department of Veterans Affairs Laptop Theft: A Physical Controls Failure**

**Incident Summary:** In 2006, an unencrypted laptop and external hard drive containing the personal information — including names, Social Security numbers, and dates of birth — of approximately 26.5 million U.S. military veterans and active-duty personnel was stolen from the home of a Department of Veterans Affairs data analyst, who had taken the equipment home as part of his routine work without proper authorization or adequate physical and technical safeguards.

**Root Cause & Vulnerability Exploited:** The core failure was overwhelmingly a **Physical Controls** gap, specifically **Security of Assets Off-Premises (7.9)**: an employee was permitted to remove highly sensitive data on portable equipment to an unsecured personal residence, with **no encryption** applied to the storage media (a gap that, viewed through today's Technological lens, also implicates 8.24, Use of Cryptography, as a compensating control that was never applied). The laptop was later recovered by the FBI, and investigators concluded the thieves did not appear to have specifically targeted the sensitive data or understood what they had stolen — but this was discovered only after significant public alarm and cost, not because any control had actually prevented or limited the exposure.

**Business & Legal Impact:** The incident led to a formal U.S. congressional investigation, the resignation of the department's Assistant Secretary for Policy and Planning, and directly prompted the passage of the Veterans Benefits, Health Care, and Information Technology Act of 2006, which imposed new, more stringent data security and breach-notification requirements specifically on the VA. Total costs associated with credit monitoring, notification, and remediation ran into the tens of millions of dollars.

**Key Lessons for Defenders & Auditors:** This case makes a point that a purely technology-focused security program can easily overlook: an organization can have reasonably strong network security, logging, and access control (Technological theme controls) protecting its central systems, and still suffer a catastrophic breach entirely through a Physical Controls gap the moment sensitive data physically leaves the building on an unencrypted device. The lesson connects directly to 7.9 and 8.1 (User Endpoint Devices) together — a genuinely mature ISMS treats "data on a laptop that might leave the premises" as requiring *both* a physical policy governing whether and how equipment may be taken off-site, *and* a technological control (full-disk encryption) that ensures the data remains protected even if the physical control is bypassed or fails, exactly the kind of layered, defense-in-depth thinking that neither theme alone can fully provide.

---

## Interactive 35-Minute Lab

**Lab Title:** Complete the Bidii SACCO Annex A Mapping — Physical and Technological Controls

**Objective:** Extend the Annex A mapping exercise from your previous session to cover Physical and Technological controls, completing a full four-theme gap assessment of the Bidii SACCO scenario used throughout this unit, and apply today's two case studies to identify one new, previously-unidentified risk in the scenario.

**Required Environment / Tools:** Your accumulated Bidii SACCO materials and your Day 7 Organizational/People Annex A mapping table, a text editor or notebook.

**Note on class format:** Two pairs, continuing the same split as your previous session. Pair A now maps relevant findings to **Physical Controls**; Pair B maps relevant findings to **Technological Controls**.

**Step-by-Step Execution Guide:**

1. **(5 min, individually)** Recall the Bidii SACCO scenario elements not yet fully explored through a physical or technological lens: the physical filing room holding paper loan application forms, the core banking application, the decommissioned pilot reporting server, and the third-party SMS gateway.

2. **(10 min, in your assigned pair)** For each relevant scenario element, identify the specific Annex A control number and title (within your assigned theme, from today's session) it relates to, exactly as practiced in your previous session's lab.

3. **(10 min, same pair)** Using today's Capital One and Veterans Affairs case studies as direct inspiration, identify **one entirely new risk** in the Bidii SACCO scenario that hasn't been explicitly named in any previous session this unit — Pair A (Physical) should think specifically about the filing room and any staff laptops/portable devices; Pair B (Technological) should think specifically about the pilot server's configuration state and any cloud or third-party service permissions the SMS gateway integration might require. State the risk, the control it relates to, and briefly justify why it's a genuine, plausible risk for this specific organization.

4. **(5 min) Class debrief.** Both pairs present their newly identified risk. The instructor will specifically ask each pair to justify why this risk had not been surfaced in the six prior sessions' worth of analysis of the same scenario — reinforcing the lesson that a genuinely thorough gap assessment requires deliberately viewing the same environment through every Annex A theme, since no single theme's lens surfaces every risk on its own.

**Expected Artifacts & Evidence:**

```
ANNEX A MAPPING — BIDII SACCO (Physical & Technological Controls)

| Finding / Element                        | Control Number & Title                  | Justification for Applicability                          |
|----------------------------------------------|---------------------------------------------|------------------------------------------------------------------|
| Physical filing room holding national ID copies | 7.2 Physical Entry / 7.10 Storage Media   | No documented entry restriction or media handling procedure |
| Pilot reporting server, never decommissioned  | 8.9 Configuration Management / 8.10 Information Deletion | Configuration and data retention state unknown/unreviewed since project end |
| SMS gateway third-party integration           | 8.2 Privileged Access Rights / 8.24 Use of Cryptography | Unclear whether integration credentials follow least-privilege or whether data in transit is encrypted |

NEWLY IDENTIFIED RISK (inspired by today's case studies):
Risk:               ...
Control:            ...
Justification:      ...
```

---

## Mini-Project / Take-Home Challenge

**Challenge: The Off-Premises Data Audit**

Drawing directly on the Veterans Affairs case study, identify **one specific instance** in an organization you're familiar with (or your own personal practice) where sensitive information regularly leaves a secure, primary location — a work laptop taken home, files synced to a personal device, documents carried to an off-site meeting, or similar. Assess it against both 7.9 (Security of Assets Off-Premises) and 8.1/8.24 (User Endpoint Devices / Use of Cryptography):

- Is the device or media encrypted?
- Is there a documented policy governing whether this off-premises movement is even permitted, and under what conditions?
- What would the realistic consequence be if this specific device or media were lost or stolen tomorrow?

**Deliverable format:** A short written report (200–300 words), submitted before the next session. Be ready to present your findings — as with previous challenges in this unit, expect all four students to share.

---

## Discussion Questions & Knowledge Check

Run this as an open round-table — every student answers each question before moving to the next.

1. In the Capital One case, the vulnerability exploited (SSRF) is well-documented and well-understood in the security community. Why do you think a well-known vulnerability class combined with an overly-permissive IAM role produced such a catastrophic outcome, when either factor alone — the vulnerability without the excessive permissions, or the excessive permissions without the vulnerability being exploited — might have resulted in a far more limited or entirely prevented incident?

2. Explain, using today's content specifically, why the Principle of Least Privilege applies to *service accounts and application roles*, not just to human user accounts. Give one plausible example, beyond the Capital One case, of a service role that might realistically be granted excessive permissions in a typical organization.

3. Compare the Veterans Affairs and Capital One cases. One is a purely physical control failure with no sophisticated exploitation involved at all; the other is a purely technological, cloud-configuration failure. Which do you think is generally harder for an organization to fully prevent through policy alone, and why?

4. Three Technological controls — 8.10 (Information Deletion), 8.11 (Data Masking), and 8.12 (Data Leakage Prevention) — were all newly added in the 2022 revision. What does the addition of these three specific controls, together, suggest about how the industry's understanding of data-related risk had evolved between 2013 and 2022?

5. Revisit the recurring Bidii SACCO pilot reporting server. Using everything covered across today's session, name every Physical or Technological control you believe is relevant to properly resolving that single lingering risk, and explain why a decommissioning process that only addressed data deletion (8.10) without also addressing the server's ongoing network exposure (8.20/8.22) would still leave a meaningful gap.
