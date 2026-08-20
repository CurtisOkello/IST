# Classification of Information & The 4 Ps of Information Security
**Module:** Module 9 — Information Security Management System (ISMS) | **Unit:** Unit 1 — Introduction to ISMS | **Date:** August 20, 2026 | **Duration:** 90 Minutes | **Class Size:** 4 Students

---

## Session Objectives & Real-World Context

**What You Will Learn:**
- How to formally **classify information** by sensitivity, and why classification is the single decision that every other control in an ISMS depends on.
- The **CIA Triad** — Confidentiality, Integrity, and Availability — as the three properties every security control ultimately exists to protect, including how to tell them apart in a real incident.
- The **4 Ps of Information Security** — People, Process, Products, and Partners — as the four categories of control an organization has available to protect any given piece of information.
- How to apply both frameworks together to a real information asset, turning yesterday's raw asset map into a properly classified, control-mapped register entry.
- Why third-party ("Partner") relationships are consistently one of the most under-controlled and most exploited categories in real breaches — illustrated today through one of the most-cited case studies in the industry.

**Why It Matters to a Security Professional:** Every control decision you will ever justify — in a SOC ticket, an audit report, or a budget proposal — ultimately answers one of two questions: *"which CIA property am I protecting?"* and *"which of the 4 Ps is the actual gap?"* These two frameworks are the vocabulary of the entire security industry. When a SOC Analyst writes an incident summary, when an auditor writes a finding, when a CISO justifies a budget line to the board — all of them are, whether they say so explicitly or not, speaking in terms of Confidentiality/Integrity/Availability impact and People/Process/Products/Partners root cause. Fluency in this vocabulary is what lets you walk into any security conversation, at any level of seniority, and immediately understand what's actually being discussed.

---

## Core Theory & Technical Mechanics

### Why Classification Comes First

Yesterday, you built an Information Asset Register listing what information an organization holds and roughly rating it High/Medium/Low. Today we formalize that rating into a proper **classification scheme** — a defined, organization-wide set of sensitivity labels, each with clear rules attached about how information at that level must be handled.

**Classification has to come before almost every other security decision**, because the correct level of protection for a given piece of information cannot be determined until you know how sensitive it is. Encrypting a public marketing brochure the same way you encrypt a customer's national ID number isn't extra security — it's wasted effort that could have gone toward properly protecting the ID number instead. Classification is what allows an organization to spend its limited security budget where it actually matters.

### Common Classification Schemes

Most organizations use a **four-tier classification scheme**, though the exact labels vary by industry and jurisdiction:

- **Public** — information explicitly intended for open, unrestricted release (marketing material, published financial results, job postings). No harm results from disclosure.
- **Internal / Internal Use Only** — information not meant for external release, but whose disclosure would cause only minor, everyday inconvenience rather than serious harm (internal meeting notes, general staff directories).
- **Confidential** — information whose unauthorized disclosure would cause meaningful harm to the organization or its people (financial records, contracts, employee performance reviews, most customer data).
- **Restricted / Secret** — the highest tier, reserved for information whose disclosure would cause severe harm (trade secrets, national security information, health records, payment card data, national ID numbers).

Each tier is typically paired with **mandatory handling rules** — who may access it, whether it may be emailed externally, whether it must be encrypted at rest, how long it must be retained, and how it must be destroyed. A classification label without attached handling rules is decoration, not security — the label only has value if it actually changes how people are required to behave around that information.

### The CIA Triad — Confidentiality, Integrity, and Availability

Every security control that has ever been designed exists to protect one, or more, of exactly three properties. This is the most foundational model in the entire field, and you will use it in every remaining unit of this diploma.

**Confidentiality** — ensuring information is accessible only to those authorized to access it.
- *Failure example:* an attacker reads a database of customer passwords they were never authorized to see.
- *Typical controls:* encryption, access control lists, the Principle of Least Privilege, classification and handling rules like those above.

**Integrity** — ensuring information is accurate, complete, and has not been altered by unauthorized parties.
- *Failure example:* an attacker doesn't steal a bank's transaction database, but quietly changes a handful of account balances.
- *Typical controls:* hashing and digital signatures, version control, file integrity monitoring, audit logging, change-approval processes.

**Availability** — ensuring information and the systems that hold it are accessible to authorized users when needed.
- *Failure example:* a ransomware attack encrypts a hospital's patient records system, and doctors can no longer retrieve patient histories during active treatment.
- *Typical controls:* redundancy and failover systems, backups, capacity planning, DDoS protection, disaster recovery planning.

**A critical skill: learning to tell these three apart in a real scenario.** Students very commonly default to labeling everything a "confidentiality" issue, because "someone might see something they shouldn't" is the most intuitive framing of security. But a huge proportion of real, high-impact incidents are actually **integrity** or **availability** failures — and misdiagnosing which property was actually harmed leads directly to the wrong response. If an attacker altered financial records rather than merely viewing them, your response needs to include verifying and restoring data accuracy, not just revoking access — an entirely different, and often more difficult, recovery process.

### Beyond CIA: A Brief Note on the Parkerian Hexad

Some practitioners extend the CIA Triad into six properties (the **Parkerian Hexad**, proposed by Donn Parker), adding **Possession/Control**, **Authenticity**, and **Utility** to account for edge cases the original three don't fully capture — for example, an attacker who steals an *encrypted* backup tape hasn't violated Confidentiality (they can't read the contents), but they have violated Possession/Control (the organization no longer has exclusive custody of it). You are not required to memorize the Hexad for this diploma, but you should recognize the term if you encounter it in industry reading — CIA remains the standard vocabulary you'll be tested on and expected to use professionally.

### The 4 Ps of Information Security — People, Process, Products, Partners

If CIA answers *"what am I protecting?"*, the 4 Ps answer *"what kind of control do I actually have available?"* Every real-world control an organization implements falls into exactly one of these four categories.

**People** — the human element: employees, contractors, and anyone with legitimate access to information. Controls in this category include hiring screening, security awareness training, role-based responsibilities, and disciplinary policies. People are simultaneously an organization's most necessary asset and, as covered extensively in Module 8, its most commonly exploited attack surface.

**Process** — the documented policies, procedures, and workflows that define how information must be handled. This is where classification schemes themselves live, along with incident response procedures, access request/approval workflows, and change management. A process exists to make security behavior *consistent and repeatable*, rather than dependent on any one person's judgment on any given day.

**Products** — the technology: hardware, software, and technical controls (firewalls, encryption tools, EDR platforms, the SIEM and Sysmon tooling you used extensively in Module 8). Products are usually where organizations spend the largest share of their security budget, and — as you'll see in today's case study — are also where organizations most commonly *over-invest relative to the other three Ps*, creating a false sense of security.

**Partners** — third parties who have some level of access to, or responsibility for, an organization's information or systems: vendors, contractors, cloud providers, managed service providers, and supply chain relationships. This is the P most frequently left out of an organization's threat thinking entirely, and — as today's case study demonstrates in detail — is consistently one of the highest-value targets for attackers precisely *because* it's under-scrutinized.

**Why the order matters less than the balance.** A genuinely resilient organization invests across all four Ps in rough proportion to actual risk, rather than defaulting to whichever P is easiest to buy a solution for (almost always Products). A security program that is 90% Products and 10% everything else is not a balanced ISMS — it's a technology purchase with a security label attached.

### Non-Technical Analogies

> 🏥 **The CIA Triad as a Hospital.** Confidentiality is the curtain around a patient's bed — only authorized staff should see what's happening behind it. Integrity is the accuracy of the patient's chart — a nurse administering medication based on an altered or incorrect chart could cause real harm, even if no one "stole" anything. Availability is the hospital's ability to pull up that chart instantly during an emergency — a chart that's perfectly accurate and perfectly private is still useless if the system is down when a doctor needs it most. All three properties matter simultaneously, and a hospital that only worries about one of them is not actually secure.

> 🏰 **The 4 Ps as a Castle's Defenses.** People are the guards on the wall — well-trained, alert, and trustworthy, or not. Process is the standing orders the guards follow — when to raise the drawbridge, who to challenge at the gate, what to do if someone claims to be a messenger from the king. Products are the wall, the moat, and the weapons themselves — the physical technology of defense. Partners are the neighboring lord who supplies the castle's grain and, critically, has his own private gate key for deliveries — a gate the castle's own guards don't watch nearly as closely, because "it's just the grain merchant." An attacker who can't scale the wall will very often simply befriend, bribe, or impersonate the grain merchant instead.

---

## Multi-Perspective Breakdown

**Attacker's POV:** A sophisticated attacker performs their own informal CIA/4P analysis of a target before choosing an approach. If Confidentiality controls (encryption, access control) are strong, but the target relies heavily on a Partner with weaker security practices, the attacker will pursue the Partner relationship as the path of least resistance — exactly the logic behind today's case study. Attackers also specifically favor **Integrity** attacks against organizations that have invested almost entirely in Confidentiality controls, because those organizations frequently have far less mature detection for *quiet, unauthorized alteration* of data than they do for unauthorized *viewing* of it — a blind spot created directly by an imbalanced approach to the CIA Triad.

**Defender's / SOC Analyst's POV:** Every alert a SOC Analyst triages can, and should, be mentally tagged against CIA — is this an attempted Confidentiality breach (data being read/exfiltrated), an Integrity concern (unexpected file or database modification), or an Availability concern (a system going down or becoming unresponsive)? This single-word tag immediately shapes the correct response playbook. Analysts should also apply the 4 Ps lens to their own environment proactively: "we have excellent Products protecting this system — but do we have an equally mature Process for what happens when our Partner's system, which also touches this data, is compromised instead?"

**Auditor's / Forensic Investigator's POV:** An auditor's core methodology, formalized fully in Unit 2 and Unit 3, is built directly on these two frameworks: for every information asset in scope, verify that Confidentiality, Integrity, and Availability controls all exist and are proportionate to the asset's classification — and verify that controls exist across all 4 Ps, not just Products. A finding of "the organization has strong technical (Product) controls but no documented Partner due-diligence process" is one of the single most common — and most consequential — findings in real ISO 27001 gap assessments, directly foreshadowing a topic you'll return to formally in Unit 3.

---

## Real-World Case Study

**The 2013 Target Corporation Breach — A 4 Ps Case Study**

**Incident Summary:** In late 2013, U.S. retailer Target suffered a breach that exposed the payment card data of approximately 40 million customers, along with the personal information of up to 70 million customers overall, during the peak holiday shopping season.

**Root Cause & Vulnerability Exploited:** The intrusion did not begin with an attack on Target's own network defenses. Attackers first compromised the network of **Fazio Mechanical Services**, a small HVAC (heating, ventilation, and air conditioning) contractor that had remote network access to Target's systems for billing and project management purposes — a textbook **Partner** relationship. The contractor was compromised via a phishing email, harvesting credentials that were then used to gain a foothold inside Target's own network. From there, attackers moved laterally into Target's point-of-sale (POS) payment card processing systems and installed memory-scraping malware that captured card data directly from the POS terminals' memory as cards were swiped — a direct **Confidentiality** violation at the point of data capture, executed via a **People/Partner** weakness far removed from the actual payment systems being targeted.

**Business & Legal Impact:** Target's total costs associated with the breach — including settlements, legal fees, and remediation — have been estimated at well over $200 million, including a $18.5 million multistate settlement with U.S. state attorneys general and a separate settlement with payment card networks. The company's CEO and CIO both resigned in the aftermath, and Target's earnings and reputation suffered significant, sustained damage during the following fiscal year.

**Key Lessons for Defenders & Auditors:** This case is one of the clearest illustrations available of why the 4 Ps model matters. Target's **Products** — its payment security technology — were, by industry standards of the time, reasonably mature. But its **Partner** oversight was not: the HVAC contractor was granted a level of network access disproportionate to its actual business need (a direct Least Privilege failure), and Target's own network segmentation failed to adequately isolate a third-party-facing system from its most sensitive payment infrastructure — meaning a compromise of the *weakest* connected party became a compromise of the entire chain. An auditor applying today's framework, reviewing Target's ISMS beforehand, should have asked: "Do we have a documented Partner due-diligence and network-segmentation policy specifically governing vendors with any form of remote access — and is that policy actually enforced with the same rigor as our internal People and Process controls?" The honest answer, in hindsight, was no — and the resulting breach remains, over a decade later, the case study most consistently cited across the industry when explaining why the Partners P cannot be an afterthought.

---

## Interactive 35-Minute Lab

**Lab Title:** Classify and Control — Applying CIA and the 4 Ps to Yesterday's Asset Register

**Objective:** Take the Information Asset Register built in yesterday's lab (the "Bidii SACCO" scenario) and formally classify each item, identify which CIA properties are most at risk for each, and map at least one control from each of the 4 Ps against the two highest-sensitivity items.

**Required Environment / Tools:** Yesterday's completed Asset Register table (bring it to class), a text editor or notebook.

**Note on class format:** With a class of 4, this lab again runs as two pairs, exactly as yesterday — but today, swap your pair partner from Day 1 if possible, so that every student practices defending their classification reasoning to a different peer with a different first instinct.

**Step-by-Step Execution Guide:**

1. **(5 min, individually)** Retrieve your Bidii SACCO Asset Register from yesterday. For each information item, assign a formal classification label — Public, Internal, Confidential, or Restricted — using the four-tier scheme from today's session, replacing your rougher High/Medium/Low rating from yesterday with this more precise label.

2. **(10 min, in your pairs)** For each item classified Confidential or Restricted, identify **which CIA property is most at risk** and briefly justify why. For example: is the national ID copy data primarily a Confidentiality concern, or could there also be a plausible Integrity risk (someone altering a loan application after submission) or Availability risk (the filing room flooding, destroying the only copies)? Most items will have more than one relevant property — identify the *primary* one and explain your reasoning.

3. **(10 min, same pairs)** For your **two highest-sensitivity items**, propose one realistic control from **each of the 4 Ps** — a People control, a Process control, a Products control, and a Partners control (even if there's no current partner involved for that item, describe what a Partner-related risk *could* look like if one were introduced, e.g., outsourcing filing room management to an external records company).

4. **(5 min) Class debrief.** Both pairs present their control mapping for the same item (e.g., "national ID copies") side by side. The instructor will specifically probe any pair whose four proposed controls lean heavily toward Products — this is a deliberate check against the most common real-world imbalance discussed in today's theory section.

**Expected Artifacts & Evidence:** An expanded version of yesterday's table, now including:

```
| Information Item     | Classification | Primary CIA Property at Risk | People Control        | Process Control          | Products Control       | Partners Control                          |
|------------------------|-----------------|---------------------------------|--------------------------|------------------------------|---------------------------|-----------------------------------------------|
| National ID copies     | Restricted      | Confidentiality                 | Background-checked filing staff | Documented retention/disposal SOP | Locked, fireproof filing cabinet | If outsourced: vetted records-management vendor contract |
| Member account balances| Confidential    | Integrity                       | Segregation of duties among tellers | Dual-approval for balance adjustments | Core banking app with audit logging | N/A — no partner currently involved |
```

---

## Mini-Project / Take-Home Challenge

**Challenge: Find Your Own "Target/Fazio" Relationship**

Reflect on the organization you mapped in yesterday's take-home challenge (your employer, internship, student club, or household). Identify **one real Partner relationship** that organization has — a vendor, contractor, cloud service, freelancer, or even an informal arrangement (a family member with access to a shared account, for instance) — and answer the following in a short written paragraph:

- What level of access does this Partner actually have to information you classified yesterday?
- Is that level of access proportionate to what the Partner actually needs to do their job (Least Privilege), or broader than necessary?
- If this Partner were compromised tomorrow exactly the way Fazio Mechanical was, what is the realistic worst-case chain of consequences?
- Propose one specific control — from any of the 4 Ps — that would meaningfully reduce that risk.

**Deliverable format:** A short written paragraph (150–250 words), submitted before the next session. Be ready to briefly share your finding — with a class of 4, expect every student to present, exactly as with yesterday's challenge.

---

## Discussion Questions & Knowledge Check

Run this as an open round-table — every student answers each question before moving to the next.

1. A ransomware attack encrypts a company's entire customer database, but the attackers never actually view or exfiltrate any of the data — they simply lock it. Which CIA property was violated, and does your answer change if the company later discovers the attackers *did* quietly view some records before encrypting them?

2. Using the Target/Fazio case study, argue for or against the following statement: "An organization's security is only as strong as its weakest connected Partner, regardless of how strong its own internal People, Process, and Products controls are." Defend your position with a specific example from today's material.

3. Think of a real product or service you personally use that involves a third party you rarely think about as a security risk (a payment app, a cloud photo backup service, a food delivery app that stores your address). Applying today's 4 Ps framework, which "P" do you have the least visibility into as a customer, and why does that matter?

4. A colleague says: "We classified this database as Restricted, so we're covered." Explain, in your own words, why a classification label alone — without specific handling rules attached — provides little to no actual protection.

5. Revisit yesterday's "pilot reporting server" scenario from the Bidii SACCO case. Using today's CIA framework, which property do you think is currently most at risk on that decommissioned server, and has your answer changed at all now that you have the full CIA vocabulary to describe it more precisely than you could yesterday?
