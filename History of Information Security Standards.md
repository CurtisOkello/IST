# History of Information Security Standards (ISO 17799 → 27001) & The 3 Tiers of ISMS
**Module:** Module 9 — Information Security Management System (ISMS) | **Unit:** Unit 3 — ISO/IEC 27001 Lead Auditor

---

## Session Objectives & Real-World Context

**What You Will Learn:**
- The full **historical lineage** of the modern ISO/IEC 27001 standard — from its origins as a British national standard through its adoption, renumbering, and successive major revisions into the standard used globally today.
- What **Annex SL** is, and why its introduction fundamentally changed how ISO 27001 relates to other management system standards (quality, environmental, and beyond).
- The precise difference between **ISO/IEC 27001** and **ISO/IEC 27002**, a distinction constantly confused by students and, frequently, by practitioners early in their careers.
- The **three-tier documentation hierarchy** every mature ISMS is built on — Policies, Procedures, and Work Instructions/Records — and how each tier maps directly onto the audit criteria, evidence-gathering, and finding-grading concepts from Unit 2.
- Why understanding *when* and *why* a standard changed is not just historical trivia, but a practical skill — because an organization's ISMS maturity is often directly visible in whether its documentation and controls have kept pace with the standard's evolution or quietly fallen behind it.

**Why It Matters to a Security Professional:** Every Lead Auditor qualification you might pursue after this diploma assumes fluency in exactly this history — you will be expected to know, without hesitation, why "ISO 27001" and "ISO 17799" are sometimes still confused in older documentation you'll encounter in real organizations, why an Annex A control numbered one way in a 2013-certified organization's documentation might not match a control you learned under the 2022 version, and why the three-tier documentation structure is the very first thing a competent auditor looks for when trying to understand how mature an organization's ISMS genuinely is before a single technical test is ever run. This is also directly practical, not just theoretical: right now, in 2026, there are still real organizations in the middle of — or worse, overdue on — their transition from the 2013 version of ISO 27001 to the 2022 version, and knowing this history lets you immediately recognize what that transition means and what to check for when you encounter it.

---

## Core Theory & Technical Mechanics

### The Origins: BS 7799

The lineage of the standard you'll spend the rest of this unit studying does not begin with ISO at all — it begins with the **British Standards Institution (BSI)**, the UK's national standards body.

- **BS 7799-1 (1995)** was published as a **code of practice** for information security management — a set of recommended controls and best practices, but explicitly *not* a certifiable specification. Organizations could read it and use it to guide their security programs, but there was no formal mechanism to be independently certified "compliant" against it.
- **BS 7799-2 (1998)** followed as the crucial complementary document — a **specification** defining the actual requirements for establishing, implementing, and maintaining an Information Security Management System, including the specific requirements needed to seek formal, independent **certification**. This is the direct conceptual ancestor of the ISO 27001 requirements you will study for the remainder of this unit — the idea of a management system that could be audited and certified, rather than merely a checklist of recommended technical controls, originates specifically here.

**Why this two-part split matters conceptually, and still echoes today:** From its very first formal incarnation, this lineage separated **"here is a management system framework you can be certified against"** (BS 7799-2, ancestor of today's ISO 27001) from **"here is detailed best-practice guidance on the actual controls"** (BS 7799-1, ancestor of today's ISO 27002). This exact split persists in the modern standard family and is one of the most consistently confused points among students and even early-career practitioners — addressed directly in the next section.

### From BS 7799 to ISO 17799 and the Birth of ISO 27001

- In **2000**, the International Organization for Standardization (ISO) adopted BS 7799-1 essentially unchanged as **ISO/IEC 17799:2000** — the code-of-practice document now carrying international rather than purely British standing. It was subsequently revised as **ISO/IEC 17799:2005**.
- In **2005**, ISO published **ISO/IEC 27001:2005**, adopting and formalizing BS 7799-2 as the internationally recognized specification for an ISMS — this is the point at which the certifiable standard you are studying in this unit formally came into existence under the name it still carries today.
- Also in 2005, to bring consistent numbering to the growing family of related standards, **ISO/IEC 17799 was renamed and became ISO/IEC 27002:2005** — the exact same code-of-practice content, simply renumbered to sit properly within the newly established **ISO/IEC 27000 family** of information security standards. This renaming is precisely why you will sometimes still encounter older documentation, older textbooks, or long-tenured practitioners referring to "17799" — they are referring to what is, today, ISO 27002.

### The ISO/IEC 27000 Family — Understanding the Wider Ecosystem

ISO 27001 does not exist in isolation — it is the anchor standard of a much larger family, each member serving a distinct, complementary purpose. Understanding this family prevents a very common student error: treating "ISO 27001" as though it's the only document that matters.

- **ISO/IEC 27000** — provides the overview and vocabulary for the entire family, defining shared terms used consistently across every other standard in the series (a genuinely useful reference document precisely because it prevents the same term being defined differently in different places).
- **ISO/IEC 27001** — the certifiable **requirements** standard: what an organization's ISMS *must* do to be certified. This is the standard an organization is actually audited and certified *against*.
- **ISO/IEC 27002** — the **code of practice / implementation guidance**, providing detailed guidance on how to actually implement the controls referenced in ISO 27001's Annex A. Critically: **an organization is never certified against ISO 27002 directly** — it is certified against 27001, and uses 27002 as a practical implementation reference for satisfying 27001's Annex A control requirements. This is the single most important distinction to memorize from today's session.
- **ISO/IEC 27005** — provides guidance specifically on information security **risk management**, directly supporting the risk assessment and treatment work that sits at the core of the ISO 27001 requirements (a topic you'll cover formally later in this unit).
- **ISO/IEC 27017 and 27018** — provide sector- and context-specific guidance for cloud services (27017 for cloud security controls generally, 27018 specifically for protecting personally identifiable information in public clouds) — examples of how the family has expanded over time to address technology contexts that didn't exist, or weren't yet significant, when the original standard was first developed.

> **Key Term — Why the 27001 vs. 27002 distinction is tested constantly:** Think of it this way: **27001 tells you *what* you must have; 27002 tells you *how* you might actually build it.** An auditor certifies an organization's ISMS against the *requirements* in 27001 (does a risk assessment process exist? does top management demonstrate leadership and commitment? is there a Statement of Applicability?) while using 27002 as a reference for judging whether the *specific controls* chosen to satisfy Annex A are genuinely well-implemented, drawing on 27002's detailed practical guidance for each control area.

### Major Revisions: 2005 → 2013 → 2022

Standards are not static documents frozen at publication — they are periodically and deliberately revised to remain relevant as technology, threats, and management practice evolve. Three major milestones define the standard's evolution:

**ISO/IEC 27001:2005** — the original certifiable specification, as covered above, containing an Annex A of 133 controls organized into 11 domains.

**ISO/IEC 27001:2013** — a major revision introducing two structural changes of lasting significance:
- **Annex SL** — a common **high-level structure (HLS)** mandated by ISO for all new and revised management system standards, ensuring that ISO 27001 (information security), ISO 9001 (quality management), ISO 14001 (environmental management), and other management system standards all share the same core clause structure, common terminology, and core requirements for things like leadership commitment, planning, support, operation, performance evaluation, and improvement. This was a deliberate design decision to make it dramatically easier for organizations to build and maintain an **Integrated Management System (IMS)** — running quality, environmental, and information security management under one coherent structure rather than as three entirely separate, disconnected systems with duplicated documentation and duplicated audit effort.
- The Annex A control set was reorganized into **114 controls across 14 domains** — a significant restructuring and expansion from the 2005 version's 133 controls across 11 domains, reflecting a decade of technological and threat-landscape change.

**ISO/IEC 27001:2022** — the current version of the standard, and the one this diploma's syllabus (and Module 8's Unit 3 content on Google Hacking and Windows Security, if you recall the Annex A control themes referenced there) is aligned with. The most significant change was a complete restructuring of Annex A from **114 controls across 14 domains down to 93 controls organized into just 4 themes**: **Organizational, People, Physical, and Technological** controls — the exact four-theme structure you will study in detail across the next several sessions in this unit. This restructuring wasn't merely cosmetic — it consolidated overlapping controls, introduced entirely new controls addressing technology and practice that had matured significantly since 2013 (including specific new controls addressing cloud security, threat intelligence, and data masking, among others), and simplified the overall structure to make the relationships between controls clearer.

**A genuinely current, practical fact worth knowing:** organizations certified under ISO 27001:2013 were given a formal **transition period** to migrate their certification to the 2022 version, with a final transition deadline set by international accreditation bodies. As of today, in 2026, that transition deadline has already passed — meaning any organization you encounter professionally that still claims certification under the 2013 version's control structure without having completed a documented transition audit is, at minimum, operating with an outdated or invalid certification claim, a genuinely useful real-world red flag for you to recognize immediately in practice.

### The Three Tiers of ISMS Documentation

Every mature, auditable ISMS organizes its documentation into a **three-tier hierarchy**, moving from the most strategic and stable at the top to the most operational and frequently-changing at the bottom. Understanding this hierarchy is essential both for building an ISMS and for auditing one — recall from Unit 2 that document review is one of the primary evidence-gathering techniques, and knowing *which tier* a given document belongs to tells you immediately what kind of scrutiny and what kind of evidence it should be paired with.

**Tier 1 — Policy**
The strategic, top-level statements of intent and direction, approved by top management (or the Board, for the most senior policies), answering the question **"what do we intend to achieve, and why does it matter to us as an organization?"** Policies are deliberately written to be relatively stable over time — a well-written Information Security Policy might remain substantively unchanged for several years, because it states principles and intent rather than specific technical detail that would need constant updating. Example: "Bidii SACCO is committed to protecting the confidentiality, integrity, and availability of member and organizational information, and will implement a risk-based Information Security Management System to achieve this."

**Tier 2 — Procedures / Processes**
The tactical, "how" layer — documents that translate policy intent into defined, repeatable processes, specifying who is responsible for what, in what sequence, and under what conditions. Procedures change more frequently than policies, as processes are refined, as responsible roles change, or as new systems are introduced. Example: a documented **Access Control Procedure** specifying the exact steps for requesting, approving, granting, reviewing, and revoking system access — directly connecting to the account deprovisioning gaps identified in earlier Bidii SACCO exercises this unit.

**Tier 3 — Work Instructions, Guidelines, and Records**
The operational, ground-level layer — highly specific, step-by-step technical instructions (a work instruction for exactly how to configure MFA on a specific system), supporting guidelines, and — critically — the actual **records** generated by following the procedures above: completed forms, approval logs, training completion records, access review logs, incident tickets. This tier changes most frequently of all, and is where the **objective evidence** concept from Unit 2 physically lives — a Tier 3 record is very often the exact artifact an auditor requests to prove a Tier 2 procedure was genuinely followed.

**How the three tiers connect directly to Unit 2's audit content:** An auditor checking conformance against a specific control typically has to examine **all three tiers together** to reach a defensible conclusion. The Policy tells the auditor what the organization *intends*; the Procedure tells the auditor *how* that intent is supposed to be operationalized; and the Records at the Work Instruction tier provide the *objective evidence* that the procedure was actually followed in practice. A gap at any single tier — a policy with no supporting procedure, a procedure with no evidence it was ever actually performed — is itself a specific, nameable type of audit finding. This is precisely the diagnostic tool a competent auditor uses within the first hour of any engagement: request the Tier 1 policy, the Tier 2 procedure it points to, and a sample of Tier 3 records demonstrating the procedure in action — if any one of the three is missing or doesn't align with the others, you have already identified your first likely finding before fieldwork has even properly begun.

> **Key Term — Document Control:** a specific, mandatory ISO 27001 requirement (covered formally later in this unit) that all three tiers of documentation must be properly version-controlled, approved by an appropriate authority, and kept current — an out-of-date, unapproved, or unofficially-edited policy or procedure document is itself a nonconformity, regardless of whether the outdated content happens to still be accurate.

### Non-Technical Analogies

> 🏛️ **The Standard's History as a Building's Renovation Record.** Think of ISO 27001 as a historic building that has been renovated multiple times, each time under a different generation of building codes. BS 7799 was the original 1990s construction. The 2005 version was a major renovation that brought the building up to newer international code and gave it its current name on the deed. The 2013 renovation added a shared foundation design (Annex SL) so this building could finally connect seamlessly to the plumbing and electrical systems of neighboring buildings on the same block (ISO 9001, ISO 14001) — before this, each building had its own incompatible infrastructure even though they sat right next to each other. The 2022 renovation reorganized the building's internal room layout entirely — fewer, more logically grouped rooms (93 controls in 4 themes instead of 114 in 14) — without changing the building's fundamental purpose. A building inspector who only knows the 1990s layout will get hopelessly lost trying to inspect the current structure — which is exactly the risk for a practitioner who never studies this history.

> 📚 **The Three Tiers as a Recipe Book, a Kitchen's Standard Operating Procedure, and Today's Actual Grocery Receipt.** The Policy is the restaurant's stated culinary philosophy — "we are committed to using only fresh, locally-sourced ingredients." The Procedure is the kitchen's standard operating recipe card — the specific steps every chef follows to prepare a given dish consistently, regardless of who's cooking that night. The Work Instruction/Record tier is today's actual, dated grocery delivery receipt proving that fresh, local ingredients genuinely arrived and were used this morning — not last month, and not from a different, cheaper supplier than the recipe card specifies. A restaurant that can proudly state its philosophy and hand you a beautifully bound recipe book, but cannot produce a single receipt proving today's ingredients matched either one, has a documentation hierarchy that looks complete on the surface but has no genuine evidentiary foundation underneath it — exactly the gap a competent auditor is trained to probe for first.

---

## Multi-Perspective Breakdown

**Attacker's POV:** A sophisticated attacker who gains any visibility into an organization's ISMS documentation — through a phishing-enabled document exfiltration, an exposed file share (recall Module 8's Google Dorking content), or simple public disclosure — immediately checks *which version* of the standard the organization claims certification against and *how current* its Tier 1/Tier 2 documents actually are. An organization still operating under a 2013-structure ISMS with clearly stale Tier 3 records is, to a knowledgeable attacker, a strong signal of an under-resourced or under-maintained security program — precisely the kind of documentation-hierarchy gap covered today, and one an attacker can identify almost as quickly as a trained auditor can.

**Defender's / SOC Analyst's POV:** SOC Analysts and technical implementers are overwhelmingly the people who actually *produce* Tier 3 evidence — the logs, the completed checklists, the access review records — even when they never personally touch the Tier 1 policy document that ultimately governs their work. Understanding this hierarchy helps a technical team recognize *why* seemingly bureaucratic record-keeping tasks (signing off on a completed patch cycle, logging a completed access review) actually matter far beyond internal housekeeping — that specific record may be the single piece of objective evidence standing between a clean audit finding and a nonconformity months later. Mature SOC teams increasingly build their own tooling to auto-generate and retain Tier 3 records as a byproduct of routine work, rather than treating record-keeping as separate, burdensome overhead — directly connecting to the continuous-auditing concept introduced in your previous session.

**Auditor's / Forensic Investigator's POV:** A Lead Auditor's very first document request in almost any engagement is designed to test the three-tier hierarchy directly — and knowing the standard's history matters immediately and practically, because an auditor reviewing an organization's Statement of Applicability (a document you'll study formally later this unit) must know instantly whether it references the 114-control 2013 structure or the 93-control 2022 structure, since referencing the wrong one is itself an immediate, unambiguous nonconformity. Forensic investigators, similarly, frequently need to establish what security standard and control set an organization was operating under *at the time* of an incident under investigation — a determination that depends entirely on the historical fluency built in today's session, since "the organization was ISO 27001 certified" means something meaningfully different depending on which version, and how recently the certification was actually verified against current requirements.

---

## Real-World Case Study

**The 2015 TalkTalk Data Breach — A Documentation Hierarchy Failure**

**Incident Summary:** In October 2015, UK telecommunications company TalkTalk suffered a significant data breach in which attackers exploited a SQL injection vulnerability to access the personal and financial data of over 150,000 customers, including bank account details and dates of birth for a substantial subset of victims. The breach caused significant, lasting reputational and financial damage to the company.

**Root Cause & Vulnerability Exploited:** Investigation revealed that the vulnerable web page had been inherited through a **prior corporate acquisition** and was, at the time of the breach, running outdated, unpatched web technology containing a well-known SQL injection flaw that had been publicly documented for several years before the breach occurred. The UK Information Commissioner's Office (ICO), in its subsequent investigation and enforcement action, found that TalkTalk had failed to take basic steps that should have prevented the attack — despite the company having documented information security policies in place at a strategic level.

**Business & Legal Impact:** The ICO fined TalkTalk £400,000 — at the time, the largest fine the regulator had issued for a data breach under the applicable legislation. The company also faced substantial remediation costs, significant customer attrition, and a sharp, sustained drop in its share price. The case remains one of the most frequently cited UK regulatory enforcement actions in security compliance training specifically because of how clearly it illustrates the gap between having a security *policy* and having genuinely operational security *practice*.

**Key Lessons for Defenders & Auditors — connecting directly to today's three-tier framework:** This case is an almost textbook illustration of a documentation hierarchy failure of exactly the kind described in today's theory section. TalkTalk very plausibly had a Tier 1 policy stating a commitment to protecting customer data — most organizations of that scale do. What the investigation strongly suggests was genuinely missing, or at least not being followed, was the Tier 2/Tier 3 operational reality beneath that policy: a documented, actively-followed **asset inventory and patch management procedure** that would have identified the inherited legacy web page as an unpatched, high-risk asset requiring urgent remediation, and **records** demonstrating that such a review had actually been performed and acted upon. This is precisely the diagnostic gap a competent auditor applying today's three-tier framework is trained to probe for: a policy exists, but where is the procedure that operationalizes it for exactly this kind of scenario (an inherited, legacy system from an acquisition), and where is the record proving that procedure was genuinely followed for this specific asset, at this specific time? The absence of a good answer to that second and third question is, in a very real sense, the entire root cause of the breach — a lesson in why a Tier 1 policy statement, however well-intentioned, provides essentially no actual protection without the Tier 2 and Tier 3 layers genuinely functioning underneath it.

---

## Interactive 35-Minute Lab

**Lab Title:** Build the Three-Tier Documentation Stack — Bidii SACCO's Access Control Gap

**Objective:** Practice constructing a genuine, connected three-tier documentation set (Policy → Procedure → Work Instruction/Record) for a specific Bidii SACCO control area, directly addressing the account deprovisioning gap first identified in Day 3's lab and referenced again in Day 5 — and then apply the TalkTalk case study's diagnostic method to a fresh scenario.

**Required Environment / Tools:** Your accumulated Bidii SACCO materials from Days 1–5, a text editor or notebook.

**Note on class format:** Two pairs, as established throughout this unit. Today's task is deliberately identical for both pairs (rather than split), so the class debrief can directly compare two independently-written attempts at the same three-tier stack and discuss where genuine, defensible documentation differs from documentation that merely looks complete.

**Step-by-Step Execution Guide:**

1. **(5 min, individually)** Recall the recurring Bidii SACCO finding from this unit: former loan officer accounts remaining active after departure. Write a single **Tier 1 Policy statement** (2–3 sentences) that a genuinely well-run Bidii SACCO would have in place to address this — remember, a policy states intent and principle, not specific steps.

2. **(10 min, in your pairs)** Write a **Tier 2 Procedure** — a numbered, step-by-step process — for account deprovisioning upon staff departure, specifying who initiates the process, who approves it, what system(s) are affected, and within what timeframe each step must occur. This procedure should be specific enough that two different staff members following it would produce the same outcome.

3. **(10 min, same pairs)** Design a **Tier 3 Work Instruction/Record** — the actual document or log template a staff member would complete each time the procedure in Step 2 is followed. This should be a genuinely usable template (e.g., a deprovisioning checklist with fields for date, employee name, systems affected, sign-off names) — not another paragraph of prose.

4. **(5 min, same pairs)** Apply the **TalkTalk diagnostic method** directly: imagine an auditor asks to see evidence that this three-tier stack was followed for the two former loan officers identified earlier in this unit. Write one sentence stating what specific evidence you would expect to find if the process had genuinely been followed, and one sentence stating what the *absence* of that evidence would imply about where in the three-tier stack the real failure occurred.

5. **(5 min) Class debrief.** Both pairs present their Tier 3 Work Instruction/Record template side by side. The instructor will specifically check whether each pair's three tiers are genuinely *connected* — does the Tier 3 record actually capture evidence of every step named in the Tier 2 procedure, and does the Tier 2 procedure genuinely operationalize the Tier 1 policy's stated intent — or whether any tier was written in isolation without real reference to the others, exactly the kind of disconnect that produced the TalkTalk outcome.

**Expected Artifacts & Evidence:**

```
THREE-TIER DOCUMENTATION STACK — Bidii SACCO Account Deprovisioning

TIER 1 — POLICY STATEMENT:
"..."

TIER 2 — PROCEDURE (numbered steps):
1. ...
2. ...
3. ...

TIER 3 — WORK INSTRUCTION / RECORD TEMPLATE:
[ ] Employee Name: __________
[ ] Departure Date: __________
[ ] Systems to be deactivated: __________
[ ] Deactivation completed by: __________ Date: __________
[ ] Verified by: __________ Date: __________

DIAGNOSTIC CHECK (TalkTalk Method):
Evidence expected if process was followed: ...
What the absence of that evidence would imply: ...
```

---

## Mini-Project / Take-Home Challenge

**Challenge: Find a Real Three-Tier Gap**

Using the same real organization you've been mapping across this unit's earlier take-home challenges, identify **one control area** (access control, data backup, incident reporting, physical security — your choice) and investigate, as honestly as you can, whether a genuine three-tier documentation stack actually exists for it:

- Does a Tier 1 policy statement exist (even informally — "we're supposed to...")?
- Does a Tier 2 procedure exist that specifically operationalizes it?
- Does Tier 3 evidence exist proving the procedure has actually been followed recently?

Write a short report (200–300 words) stating what you found at each tier, and — applying today's TalkTalk lesson directly — identify which tier, if any, represents the weakest link, and what realistic consequence that weakness could plausibly lead to if left unaddressed.

**Deliverable format:** A short written report, submitted before the next session. Be ready to present your finding — as with previous challenges in this unit, expect all four students to share.

---

## Discussion Questions & Knowledge Check

Run this as an open round-table — every student answers each question before moving to the next.

1. Explain, in your own words, why an organization can never be certified directly against ISO/IEC 27002. What does this tell you about the intended relationship between a "requirements" standard and a "guidance" standard more generally?

2. Annex SL was introduced specifically to let organizations run an Integrated Management System covering quality, environmental, and information security together. What are two realistic advantages, and one realistic risk or drawback, of combining these systems rather than keeping them entirely separate?

3. Using the TalkTalk case, argue for or against the following statement: "A company with a beautifully written Tier 1 security policy but no genuine Tier 2 or Tier 3 evidence underneath it is, in practical terms, no better protected than a company with no policy at all." Defend your position with specific reasoning from today's material.

4. If you encountered an organization today, in 2026, that proudly told you it was "ISO 27001 certified" but couldn't tell you which version (2013 or 2022) its certification was based on, what would that response alone suggest to you about the maturity of their ISMS, and what would be the very first follow-up question you'd ask?

5. Revisit your Day 5 take-home "personal code of conduct." Now that you understand the three-tier documentation hierarchy, which tier do you think your own code of conduct most closely resembles — a Policy, a Procedure, or a Work Instruction — and what would need to be added to turn it into something a real auditor could actually treat as objective evidence of your professional practice?
