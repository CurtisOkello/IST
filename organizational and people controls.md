# Annex A Domains Part 1 — Organizational & People Controls
**Module:** Module 9 — Information Security Management System (ISMS) | **Unit:** Unit 3 — ISO/IEC 27001 Lead Auditor

---

## Session Objectives & Real-World Context

**What You Will Learn:**
- The complete structure of **ISO/IEC 27001:2022 Annex A** — 93 controls organized into 4 themes — and where today's two themes, Organizational and People, sit within that structure.
- A detailed working knowledge of the **Organizational Controls** theme (37 controls) — the largest of the four themes, covering governance, policy, asset management, access control, supplier relationships, incident management, and compliance — grouped into logical clusters so the sheer number of controls becomes manageable rather than overwhelming.
- A detailed working knowledge of the **People Controls** theme (8 controls) — covering the full employment lifecycle from pre-hire screening through post-termination obligations — and why, despite being the smallest theme by control count, it is consistently one of the highest-risk areas in real incidents.
- How today's controls connect directly back to concepts already covered this diploma — classification (Day 2), supplier/Partner risk (Day 2's Target case), independent audit (Unit 2), and the three-tier documentation hierarchy (Day 6) — because Annex A controls are never implemented in isolation from everything else you've learned.
- How to read and apply a **Statement of Applicability** entry for a specific control, a skill you will build on directly in later sessions covering the full certification lifecycle.

**Why It Matters to a Security Professional:** Annex A is the part of ISO 27001 that most closely resembles a checklist — but treating it as a checklist to be ticked off, rather than a structured set of genuine risk-based decisions, is exactly the mistake that produces a certified-but-hollow ISMS. Every control in Annex A exists because some category of real-world failure — exactly the kind you'll see in today's case study — made it clear that without a specific, deliberate control in that area, organizations reliably fail in predictable ways. A Lead Auditor's real skill isn't memorizing 93 control numbers; it's understanding *why* each control exists, what specific failure mode it prevents, and what genuine evidence would prove it's actually working — precisely the evidence-based thinking you built across Unit 2. Today and the following session build that understanding methodically, theme by theme.

---

## Core Theory & Technical Mechanics

### The Structure of Annex A: A Quick Orientation

Recall from Day 6 that the 2022 revision reorganized Annex A into 93 controls across four themes:

| Theme | Control Count | Focus |
|---|---|---|
| **Organizational** | 37 controls (5.1–5.37) | Governance, policy, asset management, access control, supplier relationships, incident management, compliance |
| **People** | 8 controls (6.1–6.8) | The employment lifecycle — screening through post-termination |
| **Physical** | 14 controls (7.1–7.14) | Facilities, equipment, and physical environment protection |
| **Technological** | 34 controls (8.1–8.34) | Technical/IT controls — access, cryptography, logging, network security |

Today covers the first two themes. Physical and Technological controls follow in your next session.

**A crucial mindset for today:** Annex A controls are not mandatory in the sense that every organization must implement every single one regardless of context. The core ISO 27001 requirement (covered formally later this unit) is that an organization conducts a genuine **risk assessment**, and then selects controls from Annex A — or, where genuinely justified, controls outside Annex A entirely — that are appropriate to the risks it has actually identified, documenting every inclusion *and* every exclusion with justification in a **Statement of Applicability (SoA)**. Today's session teaches you what the controls actually are and why they exist; a later session in this unit teaches you how the SoA formally documents an organization's specific selection and justification.

### Organizational Controls — Governance, Assets, and the Backbone of the ISMS

This is the largest theme in Annex A, and for good reason — it covers the governance backbone that everything else in the ISMS depends on. We'll work through it in logical clusters rather than a flat, disconnected list.

**Cluster: Policy and Governance Foundations (5.1–5.4)**
- **5.1 Policies for information security** — the formal requirement for top management to define, approve, and communicate information security policy — the literal Tier 1 documentation from Day 6's three-tier hierarchy, now understood as a specific, auditable Annex A requirement rather than just good practice.
- **5.2 Information security roles and responsibilities** — requires that security-relevant roles and responsibilities be clearly defined and allocated, addressing exactly the role-clarity theme from Day 5's discussion of audit roles, now applied to the organization's own internal security governance.
- **5.3 Segregation of duties** — requires that conflicting duties and areas of responsibility be separated to reduce the risk of unauthorized or unintentional modification or misuse of assets. This is one of the single most important controls in the entire annex, and directly foreshadows today's case study — a single individual (or a small, insufficiently separated group) holding both the ability to grant access *and* the ability to use that access without independent oversight is precisely the structural weakness segregation of duties exists to close.
- **5.4 Management responsibilities** — requires management to actively ensure staff apply information security in accordance with established policies — a control aimed squarely at preventing the common failure mode of a policy that exists on paper but is never actually reinforced or enforced by day-to-day management practice.

**Cluster: Threat Awareness and Project Integration (5.5–5.8)**
- **5.5 Contact with authorities** — requires appropriate contact points with relevant authorities (law enforcement, regulators, emergency services) to be established and maintained, ensuring the organization isn't scrambling to figure out who to call for the first time *during* an actual incident.
- **5.6 Contact with special interest groups** — requires maintaining contact with security forums, professional associations, and threat intelligence communities, supporting ongoing awareness of emerging threats and best practice.
- **5.7 Threat intelligence** (new in the 2022 revision) — requires the organization to actively collect and analyze information about existing and emerging threats relevant to its own context, directly connecting to Module 8's APT and threat actor content — this control formalizes what was previously often an informal, ad-hoc practice into a genuine, expected organizational capability.
- **5.8 Information security in project management** — requires that information security be integrated into project management from the outset, rather than treated as an afterthought bolted onto a project just before launch — a control that directly addresses the common real-world failure of security teams being brought in "too late" to meaningfully influence a system's design.

**Cluster: Asset and Information Management (5.9–5.14)**
- **5.9 Inventory of information and other associated assets** — requires an inventory of information and associated assets (including their owners) to be developed and maintained — the formal Annex A requirement behind every Asset Register exercise you've built throughout this diploma using the Bidii SACCO scenario, and directly relevant to the TalkTalk case study from Day 6, where an inherited legacy asset had apparently fallen outside effective inventory and management.
- **5.10 Acceptable use of information and other associated assets** — requires rules for the acceptable use of information and assets to be identified, documented, and implemented, governing exactly the kind of informal WhatsApp-group usage flagged repeatedly in the Bidii SACCO scenario across this unit.
- **5.11 Return of assets** — requires personnel to return all organizational assets in their possession upon change or termination of employment, directly connecting to today's People Controls theme and to the departed-loan-officer account scenario used throughout this unit (though that specific scenario concerns *access*, covered under 5.18 below, the same departure trigger also governs physical/equipment assets under this control).
- **5.12 Classification of information** — the formal Annex A requirement underlying the entire classification framework you studied in depth on Day 2 — this is a direct, explicit link between today's session and one of your very first sessions in this module.
- **5.13 Labelling of information** — requires an appropriate set of procedures for information labelling to be developed and implemented, ensuring that a classification decision (5.12) is actually visible and actionable to the people handling the information day-to-day, rather than existing only in an abstract policy document.
- **5.14 Information transfer** — requires rules, procedures, or agreements to be in place for information transfer between the organization and external parties, and between internal parties — directly relevant to the SMS gateway vendor relationship in the Bidii SACCO scenario.

**Cluster: Access Control (5.15–5.18)**
- **5.15 Access control** — the overarching requirement that rules to control physical and logical access to information and assets be established and implemented based on business and information security requirements — the formal Annex A anchor for the Principle of Least Privilege and RBAC concepts covered in Module 8.
- **5.16 Identity management** — requires the full lifecycle of identities to be managed, ensuring that the entities allowed access to systems can be properly identified and managed throughout their entire lifecycle.
- **5.17 Authentication information** — requires the allocation and management of authentication information (passwords, tokens, biometric data) to be controlled through a managed process, including guidance to personnel on appropriate handling.
- **5.18 Access rights** — requires access rights to information and other assets to be provisioned, reviewed, modified, and removed in accordance with the organization's access control policy — this is the exact, specific control that a properly functioning process would have satisfied in the recurring former-loan-officer scenario used throughout this unit; the persistent gap identified repeatedly in Bidii SACCO's account deprovisioning is, formally, a 5.18 nonconformity.

**Cluster: Supplier Relationships (5.19–5.23)**
- **5.19 Information security in supplier relationships** — requires processes and procedures to manage the information security risks associated with the use of supplier products and services, the formal Annex A anchor for the entire Partners discussion from Day 2's Target/Fazio case study.
- **5.20 Addressing information security within supplier agreements** — requires relevant information security requirements to be established and agreed with each supplier, based on the type of supplier relationship.
- **5.21 Managing information security in the ICT supply chain** — requires processes to manage the information security risks associated with the ICT products and services supply chain specifically, connecting directly to the SolarWinds case study from Day 4.
- **5.22 Monitoring, review, and change management of supplier services** — requires the organization to regularly monitor, review, and manage changes in supplier information security practices, addressing the common real-world failure of vetting a supplier thoroughly once at onboarding and never revisiting that assessment again as the relationship and the supplier's own risk profile evolve.
- **5.23 Information security for use of cloud services** (new in the 2022 revision) — requires processes for acquisition, use, management, and exit from cloud services to be established, a control added specifically because cloud adoption had become so significant since the 2013 revision that it warranted an explicit, dedicated control rather than being left to general supplier-relationship guidance alone.

**Cluster: Incident Management and Continuity (5.24–5.30)**
- **5.24 Information security incident management planning and preparation** — requires the organization to plan and prepare for managing information security incidents by defining, establishing, and communicating processes, roles, and responsibilities — directly connecting to the entire threat-response mindset built across Module 8.
- **5.25 Assessment and decision on information security events** — requires the organization to assess security events and decide whether they should be categorized as incidents.
- **5.26 Response to information security incidents** — requires incidents to be responded to in accordance with documented procedures.
- **5.27 Learning from information security incidents** — requires knowledge gained from analyzing and resolving incidents to be used to reduce the likelihood or impact of future incidents — a control that directly formalizes the root cause analysis techniques (5 Whys, Fishbone) you practiced in Unit 2's Day 4 session.
- **5.28 Collection of evidence** — requires the organization to establish and implement procedures for the identification, collection, acquisition, and preservation of evidence related to information security events — the formal Annex A bridge to the entire digital forensics methodology you will study in Module 11.
- **5.29 Information security during disruption** — requires the organization to plan how to maintain information security at an appropriate level during disruption, directly connecting to the Availability leg of the CIA Triad from Day 2.
- **5.30 ICT readiness for business continuity** (new in the 2022 revision) — requires ICT readiness to be planned, implemented, maintained, and tested based on business continuity objectives, formalizing disaster recovery and business continuity planning as an explicit, testable ICT-specific requirement.

**Cluster: Legal, Compliance, and Assurance (5.31–5.37)**
- **5.31 Legal, statutory, regulatory, and contractual requirements** — requires such requirements relevant to information security to be identified, documented, and kept up to date, forming a direct bridge to Module 10's cyber law content later in this diploma.
- **5.32 Intellectual property rights** — requires appropriate procedures to protect intellectual property rights.
- **5.33 Protection of records** — requires records to be protected from loss, destruction, falsification, unauthorized access, and unauthorized release — directly connecting to the Tier 3 records concept from Day 6, and to chain-of-custody concepts you'll formalize in Module 11.
- **5.34 Privacy and protection of PII** — requires the organization to identify and meet requirements regarding the preservation of privacy and protection of personally identifiable information, connecting directly to Module 10's GDPR/data-protection content.
- **5.35 Independent review of information security** — requires the organization's approach to managing information security to be reviewed independently at planned intervals — this is, quite literally, the formal Annex A requirement that mandates exactly the kind of independent auditing covered in full depth throughout Unit 2, including the independence-dimension content from Day 5.
- **5.36 Compliance with policies, rules, and standards for information security** — requires regular review of compliance with the organization's own information security policy, topic-specific policies, rules, and standards.
- **5.37 Documented operating procedures** — requires operating procedures for information processing facilities to be documented and made available to personnel who need them — the formal Annex A anchor for the Tier 2 Procedure layer from Day 6's three-tier hierarchy.

> **Key Term — Why grouping matters more than memorizing numbers:** You are not expected to recite "5.19" from memory in a professional setting — real practitioners work with the standard document open in front of them constantly. What you *are* expected to internalize is the logical grouping and the *purpose* behind each cluster, so that when a real-world scenario arises (a new cloud vendor, a departing employee, a security incident), you immediately know which cluster of Annex A controls is relevant, even if you need to look up the exact control number.

### People Controls — Securing the Entire Employment Lifecycle

The People Controls theme is deliberately structured to follow the natural chronological lifecycle of an individual's relationship with the organization — from before they're even hired, through their active employment, and beyond their departure. Despite having only 8 controls, this theme addresses one of the most consistently exploited weaknesses in real-world security incidents, as today's case study will demonstrate directly.

- **6.1 Screening** — requires background verification checks on candidates to be carried out prior to joining, proportional to business requirements, the classification of information to be accessed, and perceived risks. Note the direct connection to Day 2's classification content — the *degree* of screening required is explicitly meant to scale with the sensitivity of what a given role will have access to, not applied uniformly regardless of role.
- **6.2 Terms and conditions of employment** — requires employment contractual agreements to state personnel's and the organization's responsibilities for information security, ensuring security obligations are a formal, agreed part of the employment relationship rather than an informal expectation.
- **6.3 Information security awareness, education, and training** — requires personnel to receive appropriate awareness education and training, updated regularly in line with relevant policies and procedures — directly connecting to the security awareness training discussion from Module 8's social engineering content, now formalized as a specific, auditable requirement with an expected evidence trail (attendance records, completion rates — recall the Tier 3 record concept).
- **6.4 Disciplinary process** — requires a formalized and communicated disciplinary process to be in place to take action against personnel who have committed an information security policy violation, ensuring policy violations carry genuine, known consequences rather than existing as an unenforced formality.
- **6.5 Responsibilities after termination or change of employment** — requires information security responsibilities that remain valid after termination or change of employment to be defined, enforced, and communicated — this is the formal Annex A requirement most directly relevant to the recurring former-loan-officer scenario in this unit, working in tandem with 5.18 (Access Rights) and 5.11 (Return of Assets) covered above.
- **6.6 Confidentiality or non-disclosure agreements** — requires such agreements, reflecting the organization's needs for the protection of information, to be identified, documented, regularly reviewed, and signed by personnel and relevant external parties.
- **6.7 Remote working** — requires security measures to be implemented when personnel work remotely, to protect information accessed, processed, or stored outside the organization's premises. This control was significantly elevated in importance following the widespread, rapid shift to remote work in the early 2020s, and is directly relevant to today's case study.
- **6.8 Information security event reporting** — requires a mechanism for personnel to report observed or suspected information security events in a timely manner through appropriate channels, formalizing the "if you see something, say something" principle into a genuine, accessible, known reporting process rather than assuming staff will simply know what to do or who to tell.

### Non-Technical Analogies

> 🏢 **Organizational Controls as a Company's Constitution and Bylaws.** If Tier 1 policies (Day 6) are a country's constitution — stating fundamental principles and intent — then the Organizational Controls theme is the full set of implementing legislation and government agencies that actually make those constitutional principles operate in practice: an asset registry office (5.9), a border and immigration control system governing who may enter and under what conditions (5.15–5.18), foreign relations protocols for dealing with allied nations and international bodies (5.19–5.23, Supplier Relationships), an emergency response and disaster management agency (5.24–5.30), and a judiciary and audit office ensuring the whole system actually complies with its own laws (5.35–5.36). A constitution with no implementing legislation or enforcement agencies beneath it is a beautiful document with no practical effect — precisely the same relationship Annex A's Organizational controls have with the Tier 1 policy statements sitting above them.

> 🎓 **People Controls as a School's Full Enrollment-to-Graduation Journey.** Before a student is even admitted, the school checks their prior record and references (6.1 Screening). Upon enrollment, the student and school sign an agreement of mutual expectations (6.2). Throughout their time there, the student receives ongoing instruction in the school's code of conduct, updated as rules change (6.3). If a student breaks the rules, a known, consistent disciplinary process is followed (6.4). Even after a student transfers or graduates, certain obligations persist — they can't, for instance, keep using the school's library access indefinitely, and certain confidentiality expectations about what they learned internally may still apply (6.5, 6.6). If the student is enrolled in a remote-learning program, additional safeguards apply to how they access school systems from outside the building (6.7). And throughout it all, there's a clear, known way for any student to report a concern to a teacher or administrator (6.8). Skipping any single stage of this journey — admitting a student with no reference check, or graduating one with no exit process closing out their library card and building access — creates exactly the kind of gap real attackers, and real incidents, exploit.

---

## Multi-Perspective Breakdown

**Attacker's POV:** Sophisticated attackers specifically target the gaps between Organizational and People controls, because the *seam* between the two themes is where real-world implementation most often breaks down — an organization might have a strong 5.18 Access Rights policy on paper, but if 6.5 (Responsibilities After Termination) isn't tightly integrated with the HR offboarding process that actually triggers it, the seam between "HR knows someone left" and "IT actually revokes access" is exactly where an attacker exploiting a departed employee's still-active credentials (exactly the Bidii SACCO scenario used throughout this unit) will succeed. Attackers conducting social engineering, as in today's case study, specifically probe for weaknesses in 5.3 (Segregation of Duties) and 6.3 (Security Awareness Training) simultaneously — a single, insufficiently-segregated support role with broad administrative access, staffed by someone without adequately reinforced training on social engineering red flags, is a uniquely attractive target.

**Defender's / SOC Analyst's POV:** A SOC Analyst benefits from recognizing which Annex A control a given incident or alert actually maps to, because it immediately tells you who else in the organization needs to be involved in the response beyond the technical team alone — an incident traceable to a 6.5 gap (a terminated employee's access) needs HR and IT access-management involvement, not just SOC technical remediation, while an incident traceable to a 5.21 gap (ICT supply chain) needs procurement and vendor-management involvement. Thinking in Annex A terms during incident response also directly feeds 5.27 (Learning from Information Security Incidents) — a mature SOC doesn't just close a ticket, it identifies which specific control category failed and feeds that back into the organization's control review cycle.

**Auditor's / Forensic Investigator's POV:** When auditing Organizational and People controls specifically, an auditor should expect to triangulate across HR records, IT access logs, and policy documentation simultaneously — a genuinely thorough 6.5 audit, for example, cannot be completed by reviewing HR's termination records alone; it requires cross-referencing those termination dates against IT's actual access-revocation logs to verify the timing gap between the two, exactly the kind of CAAT-style cross-system data analysis introduced in Unit 2's Day 4 session. Forensic investigators examining an incident involving insider access or social engineering will very often find that the root cause traces back to a specific, identifiable Organizational or People control gap — meaning today's content isn't just relevant to prevention, but directly informs the root-cause-analysis phase of a post-incident forensic investigation.

---

## Real-World Case Study

**The 2020 Twitter Celebrity Account Hack — An Organizational and People Controls Failure**

**Incident Summary:** In July 2020, attackers gained access to Twitter's internal administrative tools and used them to take control of numerous high-profile verified accounts — including those belonging to Barack Obama, Joe Biden, Elon Musk, Bill Gates, and several major corporate accounts including Apple — posting a cryptocurrency scam soliciting Bitcoin payments with a promise of doubled returns. The scam generated over $100,000 from victims within hours before Twitter was able to regain control and remove the malicious posts.

**Root Cause & Vulnerability Exploited:** The attackers did not exploit a software vulnerability at all. Instead, they conducted a targeted **vishing (voice phishing)** social engineering campaign against a small number of Twitter employees, primarily those working remotely amid the COVID-19 pandemic, impersonating Twitter's own IT department to obtain employee credentials for internal systems. Critically, once inside, the attackers gained access to a powerful internal administrative tool that allowed direct manipulation of user accounts — including resetting associated email addresses and bypassing normal account security — and this tool was accessible to a broader set of employees and contractors than was strictly necessary for their day-to-day roles, with insufficient additional verification or segregation of duties controls around its most sensitive functions.

**Business & Legal Impact:** Twitter's stock price dropped following the incident, and the company faced significant reputational damage and regulatory scrutiny, including subsequent inquiries from U.S. state and federal regulators into its internal security controls and its handling of access to sensitive administrative tooling. The incident also raised broader public concern about the security and integrity of a platform used for significant public communication, given that verified accounts belonging to public officials and world leaders were directly compromised. Twitter subsequently made public commitments to review and restrict access to internal tools and to enhance employee security training.

**Key Lessons for Defenders & Auditors — connecting directly to today's two themes:** This case is a near-perfect illustration of an Organizational and People controls failure occurring together, rather than a purely technical exploit. On the **People** side: the attack specifically targeted employees working remotely (6.7), exploiting a social engineering vector that adequate, current security awareness training (6.3) should have specifically prepared staff to recognize — impersonation of internal IT requesting credentials is one of the most well-documented social engineering patterns in the industry, precisely the kind of scenario 6.3 training is meant to cover concretely, not just in generic terms. On the **Organizational** side: the breadth of access granted to the internal administrative tool represents a clear 5.15/5.18 (Access Control/Access Rights) gap — too many personnel had access to a tool capable of this level of impact, and the absence of adequate 5.3 (Segregation of Duties) meant that a single compromised employee credential, once obtained through social engineering, was sufficient to cause enormous, immediate, and highly visible damage without requiring any additional independent approval or verification step. An auditor applying today's framework, reviewing Twitter's ISMS beforehand, should have specifically asked: "Who has access to our most powerful internal tools, is that access proportionate to actual job need, and does any single compromised credential alone grant enough power to cause harm at this scale?" The honest answer, in hindsight, was clearly no on all counts — and the case remains one of the clearest illustrations in recent history of why People and Organizational controls must be assessed together, not as separate, unrelated compliance exercises.

---

## Interactive 35-Minute Lab

**Lab Title:** Map Bidii SACCO's Recurring Findings to Annex A — Organizational and People Controls

**Objective:** Take every finding, gap, and risk identified across this unit's ongoing Bidii SACCO scenario and formally map each one to the specific Annex A Organizational or People control it violates — practicing the exact skill a real ISO 27001 gap assessment requires.

**Required Environment / Tools:** Your accumulated Bidii SACCO materials from Days 1–6, a copy of today's control clusters for reference, a text editor or notebook.

**Note on class format:** Two pairs. Pair A maps every relevant finding to **Organizational Controls**; Pair B maps every relevant finding to **People Controls**. Several findings from earlier in this unit will plausibly map to controls in both themes — when this happens, both pairs should independently identify and record it, setting up a direct comparison in the debrief.

**Step-by-Step Execution Guide:**

1. **(5 min, individually)** Review your accumulated Bidii SACCO notes from Days 1–6 and list every distinct finding, gap, or identified risk you can recall — the departed loan officer accounts, the unmanaged WhatsApp group, the decommissioned pilot server, the SMS gateway vendor relationship, and any others your own notes captured.

2. **(15 min, in your assigned pair)** For each finding on your list, identify the **specific Annex A control number and title** (from today's session, within your assigned theme) that it most directly relates to. Where a finding could plausibly map to more than one control, note the primary one and briefly justify your choice.

3. **(10 min, same pair)** For your **three strongest matches**, write a brief **Statement of Applicability-style justification** — a short note stating why this control is applicable to Bidii SACCO given its identified risk (this is direct, hands-on preparation for the formal SoA content coming later in this unit).

4. **(5 min) Class debrief.** Both pairs present their full mapping side by side. The instructor will specifically highlight any finding that both pairs independently mapped to a control (confirming a genuine, high-confidence dual-theme issue) versus findings only one pair identified — prompting a discussion of why the other pair may have missed it.

**Expected Artifacts & Evidence:**

```
ANNEX A MAPPING — BIDII SACCO (Organizational & People Controls)

| Finding                                    | Control Number & Title           | Justification for Applicability                          |
|-----------------------------------------------|--------------------------------------|----------------------------------------------------------------|
| Former loan officer accounts remain active     | 5.18 Access Rights / 6.5 Responsibilities After Termination | Direct evidence of provisioning/deprovisioning failure tied to employment change |
| Unmanaged WhatsApp group used for ops discussions | 5.10 Acceptable Use of Assets      | No documented rules governing use of informal communication channels |
| Decommissioned pilot server never reviewed     | 5.9 Inventory of Information and Assets | Asset was never formally tracked to end-of-life/decommissioning |
| SMS gateway vendor relationship               | 5.19 Information Security in Supplier Relationships | No evidence of formal risk assessment of this third-party relationship |
```

---

## Mini-Project / Take-Home Challenge

**Challenge: Audit Yourself Against Two Real Controls**

Choose **one Organizational control** and **one People control** from today's session that are genuinely relevant to an organization you have real familiarity with (your workplace, internship, or another real organization). For each of the two chosen controls:

- State the control number, title, and what it requires in your own words.
- Assess, as honestly as you can, whether that organization genuinely satisfies it — citing specific evidence you're aware of (or specific evidence you notice is missing).
- If you identify a gap, briefly state which of today's case study lessons (Twitter) it most closely resembles, if any.

**Deliverable format:** A short written report (200–300 words covering both controls), submitted before the next session. Be ready to present your findings — as with previous challenges in this unit, expect all four students to share.

---

## Discussion Questions & Knowledge Check

Run this as an open round-table — every student answers each question before moving to the next.

1. The Twitter case involved a failure that spans both the Organizational theme (access control, segregation of duties) and the People theme (training, remote working). Why do you think Annex A separates these into two distinct themes at all, if real-world incidents so often involve failures in both simultaneously?

2. Control 5.7 (Threat Intelligence) was newly added in the 2022 revision. Using what you know from Module 8 about the modern threat landscape, explain why you think this control didn't exist as an explicit, standalone requirement in the 2013 version, and why it was considered important enough to add.

3. Segregation of Duties (5.3) can sometimes be genuinely difficult for a small organization to implement fully — Bidii SACCO, for instance, may simply not have enough staff to separate every conflicting duty perfectly. Propose one realistic compensating measure a small organization could adopt when full segregation of duties isn't practically achievable.

4. Using control 6.1 (Screening), explain why the control specifically requires screening to be "proportional to business requirements, the classification of information to be accessed, and perceived risks" rather than requiring the same, uniform level of background check for every single role in an organization. What would be the downside of applying the same maximum-intensity screening to every hire regardless of role?

5. Revisit the recurring former-loan-officer scenario used throughout this unit. Now that you have the formal Annex A vocabulary, name every control number you believe is relevant to fully resolving this single recurring finding, and briefly explain why more than one control is typically needed to close a gap that, on the surface, might look like a single simple problem.
