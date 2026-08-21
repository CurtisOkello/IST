# Security Auditing — Objectives, Threats to Information Assets & Security Parameters
**Module:** Module 9 — Information Security Management System (ISMS) | **Unit:** Unit 2 — Security Auditing

---

## Session Objectives & Real-World Context

**What You Will Learn:**
- What a **security audit** actually is, why it exists as a distinct discipline from day-to-day security operations, and the different **types of audits** an organization might commission or undergo.
- The core **objectives** every legitimate security audit is built around — and how to distinguish a genuine audit from a superficial "checkbox" review.
- A working **taxonomy of threats** to information assets — natural, environmental, human (intentional and unintentional), technical, and third-party — and the precise vocabulary distinction between a *threat*, a *vulnerability*, and a *risk*, which you will use for the rest of this diploma.
- What **security parameters** actually are in practice — the specific, measurable criteria an auditor checks an organization against, rather than vague impressions of "good" or "bad" security.
- How a single missing security parameter, left unaudited, can be the entire root cause of a catastrophic real-world incident.

**Why It Matters to a Security Professional:** Auditing is not a side skill you pick up once you're senior enough — it's a core competency that shows up constantly, even for analysts who never formally hold an "Auditor" job title. A SOC Analyst is regularly asked to produce evidence for an internal or external audit. An Incident Responder's post-incident report is, functionally, a mini-audit of what went wrong. A GRC Consultant's entire career is built on the objectives and taxonomy covered today. And critically, understanding *threats* and *security parameters* the way an auditor does — as specific, checkable, evidence-based items rather than vague concerns — is exactly what separates a security professional who can say "we should be more secure" from one who can say "here are the seven specific, unaudited parameters that represent our actual exposure, ranked by risk." The second person gets hired, promoted, and trusted with bigger budgets. Today builds that vocabulary from the ground up.

---

## Core Theory & Technical Mechanics

### What Is a Security Audit, and Why Does It Exist?

A **security audit** is a systematic, evidence-based examination of an organization's information systems, policies, and practices, conducted to determine whether they meet a defined set of requirements — whether those requirements come from internal policy, an industry standard (like ISO 27001, covered in Unit 3), a regulation, or a contractual obligation.

The word **systematic** is doing a lot of work in that definition, and it's worth pausing on. A systematic audit follows a defined methodology, uses consistent criteria applied the same way to every item being reviewed, and produces **evidence-based findings** — meaning every conclusion in the final report can be traced back to something the auditor actually observed, tested, or was shown, not something they simply assumed or were told verbally without proof. This is what separates a real audit from an informal "walk-through" — an auditor who writes "the organization appears to patch servers regularly" based on a conversation has produced an opinion; an auditor who writes "of a sample of 15 servers reviewed, 14 had patches applied within the organization's documented 30-day SLA; one (Server FIN-07) was 62 days overdue as of the review date" has produced an audit finding.

**Types of audits** you'll encounter and need to distinguish:

- **Internal audit** — conducted by the organization's own staff (or an internal audit function), typically as ongoing self-assessment and preparation for external scrutiny.
- **External / Third-party audit** — conducted by an independent outside party, providing assurance to external stakeholders (customers, regulators, the board) who wouldn't trust the organization's own self-assessment alone.
- **First-party, second-party, and third-party audits** — a more precise version of the above distinction used heavily in formal quality/certification contexts (and directly relevant to Unit 3): a *first-party* audit is an organization auditing itself; a *second-party* audit is one party auditing another party they have a direct business relationship with (e.g., a company auditing a key vendor — connecting directly to yesterday's Partners discussion); a *third-party* audit is conducted by a fully independent, unrelated certification body (the type of audit that leads to an actual ISO 27001 certificate).
- **Compliance audit** — checks conformance against a specific standard, regulation, or policy.
- **Technical / vulnerability audit** — closer to the technical penetration-testing and vulnerability-scanning work from Module 8, focused on identifying exploitable weaknesses rather than policy conformance.
- **Announced vs. surprise audit** — whether the organization is given advance notice. Surprise audits (or unannounced elements within a scheduled audit, like walking a data center floor unannounced) are specifically designed to observe genuine day-to-day practice rather than practice that's been temporarily tidied up for a known audit date.

### The Core Objectives of Security Auditing

Every legitimate security audit, regardless of type, is built around some combination of these objectives:

1. **Verify compliance** — confirm the organization actually meets the specific policy, standard, or regulatory requirements it claims to meet.
2. **Test control effectiveness, not just control existence.** This is the single most important, and most commonly misunderstood, objective. A control can *exist on paper* (a documented password policy) while being completely ineffective in practice (nobody actually enforces it, and half the passwords in the system don't meet the stated requirement). A competent auditor always tests whether a control *actually works*, not merely whether a policy document mentions it.
3. **Identify gaps and risks** that the organization may not have been aware of, providing the input needed for the risk treatment work you'll formalize in Unit 3.
4. **Provide independent assurance** to stakeholders — a board, a regulator, a customer, an insurer — who need confidence in the organization's security posture but cannot verify it themselves.
5. **Support continuous improvement.** Recall the PDCA cycle from Day 1 — the audit is the formal "Check" step, feeding directly into the "Act" step of correcting what was found.
6. **Provide a documented basis for certification**, where applicable — the entire ISO 27001 certification process you'll study in depth in Unit 3 is, at its core, a highly formalized version of exactly what's being introduced today.

> **Key Term — Objective Evidence:** the auditing profession's term for exactly the kind of proof described above — a specific document, log, screenshot, interview record, or observed test result that supports a finding. "The IT manager told me access reviews happen quarterly" is a claim. "I reviewed the access review log and confirmed four completed reviews in the last twelve months, dated within one week of each quarter's end" is objective evidence. You will be expected to think and write in terms of objective evidence for the rest of this diploma.

### Threats to Information Assets — A Working Taxonomy

Before an auditor can check whether controls are adequate, they need a clear, structured understanding of what they're actually defending against. A **threat** is any potential cause of an unwanted incident that could result in harm to an information asset. It's worth being precise about three terms that are easy to blur together, because you will use this exact distinction constantly starting in Unit 3:

- **Threat** — a potential *cause* of harm (a flood, a malicious hacker, a disgruntled employee, a hardware failure).
- **Vulnerability** — a *weakness* that a threat could exploit (an unpatched server, an untrained employee, a building in a flood plain, an unsupported hardware model).
- **Risk** — the *combination* of a threat and a vulnerability, generally expressed as some function of likelihood and impact — the actual thing an organization has to decide how to treat. A threat without a corresponding vulnerability produces no realistic risk (a flood threat means very little to a data center on the 40th floor of a building far from any waterway); a vulnerability with no plausible threat targeting it is a lower priority than one actively being exploited in the wild.

**A working taxonomy of threat categories:**

- **Natural threats** — fire, flood, earthquake, storm damage — events with no human intent behind them, but which can destroy physical systems and, if backups are inadequate, the information on them.
- **Environmental threats** — power failures, HVAC/cooling failures, structural building issues — technically "man-made" in origin but not the result of malicious intent, often overlapping with the natural category (a storm causing a power failure, for instance).
- **Human threats — intentional** — the category most students think of first: external hackers, malicious insiders, competitors engaged in corporate espionage, and nation-state actors (directly connecting to the APT discussion from Module 8).
- **Human threats — unintentional** — human error and negligence: an employee misconfiguring a cloud storage bucket, accidentally emailing a sensitive file to the wrong recipient, or falling for a phishing attempt without malicious intent themselves. Industry data consistently shows unintentional human error as a leading contributing factor across breaches broadly — this category is frequently under-weighted by organizations that focus disproportionately on external, intentional attackers.
- **Technical threats** — malware, system/hardware failure, software bugs, and the various malware and botnet mechanisms covered extensively in Module 8 — these are the *technical manifestation* of many of the intentional human threats above.
- **Third-party / supply chain threats** — exactly the Partners-category risk illustrated by yesterday's Target/Fazio case study: a threat entering through a vendor, contractor, or supply chain relationship rather than directly against the organization itself.

### Security Parameters — What Auditors Actually Measure

A **security parameter** is a specific, measurable criterion or setting that an auditor checks an organization's actual practice against — the concrete, checkable items that turn "we have good password security" from a vague claim into a testable statement. Security parameters are where audit objectives (verify, test, identify) actually meet the ground.

Representative examples across common domains you'll audit against repeatedly in this diploma:

- **Access control parameters** — minimum password complexity and length, mandatory Multi-Factor Authentication (MFA) enforcement, account lockout thresholds after failed login attempts, maximum password age, timely deprovisioning of accounts after employee departure.
- **Network security parameters** — firewall rule review frequency, number and justification of open/exposed ports, existence and enforcement of network segmentation between sensitive and general-purpose zones.
- **Patch and vulnerability management parameters** — defined patch SLA (e.g., "critical vulnerabilities patched within 14 days"), frequency of vulnerability scans, percentage of assets covered by the last completed scan.
- **Logging and monitoring parameters** — minimum log retention duration, whether logs are centrally aggregated (directly connecting to the SIEM/Sysmon work from Module 8), defined alert response time targets.
- **Physical security parameters** — CCTV coverage of sensitive areas, badge-access logging and review frequency, visitor sign-in and escort procedures.
- **Policy and documentation parameters** — mandatory policy review/re-approval cadence, percentage of staff who have completed required security awareness training within the last 12 months.

**The critical skill for today's session:** every one of these parameters is phrased as something you can actually *check* and *measure* — a number, a yes/no with evidence, a date. A finding that says "access control seems okay" is not an audit finding. A finding that says "MFA is enforced for 41 of 45 admin accounts reviewed; 4 legacy accounts, including one belonging to a departed contractor, do not have MFA enabled" is a genuine, evidence-based security-parameter finding — and, as today's case study will show, is exactly the kind of specific finding that, if caught in time, can prevent a catastrophic incident.

### Non-Technical Analogies

> 🚗 **Auditing as a Vehicle Roadworthiness Inspection.** A roadworthiness inspector doesn't just glance at a car and declare it "safe" — they check specific, measurable parameters: brake pad thickness against a minimum threshold, tire tread depth, headlight alignment, seatbelt function. Each check produces a pass/fail result backed by an actual measurement, not an impression. A car can *look* well-maintained (clean, shiny paint — the equivalent of good "Products" spending) while having dangerously worn brakes that only a specific, deliberate check would catch. This is exactly the difference between a superficial security review and a real audit against defined security parameters.

> 🌊 **Threats, Vulnerabilities, and Risk as Weather and a House.** A hurricane (the **threat**) is a real, external possibility regardless of anything a homeowner does. A house with a poorly secured roof (the **vulnerability**) is what actually turns that external possibility into a meaningful problem for this specific house. The **risk** is the realistic combination of the two: how likely is a hurricane in this region, and how badly would this particular roof fail if one hit? A homeowner in a hurricane zone with a reinforced roof has managed the risk without eliminating the threat (they can't stop hurricanes); a homeowner far from any hurricane-prone coastline doesn't need to spend money reinforcing their roof against that particular threat at all — the same vulnerability matters enormously in one context and barely at all in another, which is exactly why risk is always threat *and* vulnerability together, never either one alone.

---

## Multi-Perspective Breakdown

**Attacker's POV:** Sophisticated attackers effectively conduct their own informal "audit" of a target during reconnaissance — probing for exactly the kind of specific, unenforced security parameters described above, because these are consistently where the real gap between documented policy and actual practice lives. An attacker doesn't care that an organization's password policy document requires MFA — they care whether that requirement is actually, universally enforced, and they will actively search for the exceptions (a legacy account, a contractor account, a service account) where it isn't. This is precisely the exploitation pattern in today's case study.

**Defender's / SOC Analyst's POV:** A SOC Analyst benefits enormously from thinking in terms of security parameters proactively, not just reactively during an audit cycle. Rather than waiting for an annual audit to discover that four admin accounts lack MFA, a mature SOC function runs continuous, automated checks against its own key security parameters — treating the audit checklist as a living dashboard rather than a once-a-year event. When responding to an incident, correctly classifying the underlying threat category (human-intentional, technical, third-party) also directly shapes the appropriate response and, later, the appropriate audit recommendation to prevent recurrence.

**Auditor's / Forensic Investigator's POV:** This entire session is, in effect, an auditor's core job description. An auditor's value is measured almost entirely by their ability to define precise, testable security parameters relevant to the specific organization and its actual risk profile — a generic checklist copied from the internet without regard to context is weak auditing; a checklist built from a genuine understanding of the organization's threats (informed by exactly the taxonomy covered today) is strong auditing. A forensic investigator, after an incident, frequently works backward through this exact same framework: which security parameter was violated or absent, which threat category exploited it, and what evidence exists to prove the timeline — work that directly feeds Module 11 later in this diploma.

---

## Real-World Case Study

**The 2021 Colonial Pipeline Ransomware Attack**

**Incident Summary:** In May 2021, Colonial Pipeline — operator of the largest fuel pipeline system in the United States — suffered a ransomware attack that forced the company to proactively shut down pipeline operations for several days, causing fuel shortages and price spikes across a significant portion of the U.S. East Coast. The company ultimately paid a ransom of approximately $4.4 million, a portion of which was later recovered by U.S. law enforcement.

**Root Cause & Vulnerability Exploited:** Attackers gained initial access using a **single compromised password** for a legacy Virtual Private Network (VPN) account that was no longer in active use but had never been formally deactivated. Critically, this account **did not have Multi-Factor Authentication enabled** — a single username and password was sufficient to gain remote access into the company's network. The exact password is believed to have been exposed in a separate, unrelated data breach and reused on this account — meaning the vulnerability wasn't a sophisticated technical exploit at all, but the straightforward absence of two specific, easily-stated security parameters: **mandatory MFA on all remote-access accounts**, and a **defined account deprovisioning process for accounts no longer in active use**.

**Business & Legal Impact:** Beyond the $4.4 million ransom, Colonial Pipeline faced a $1 million fine from the U.S. Department of Transportation's Pipeline and Hazardous Materials Safety Administration for violations related to its pipeline restart and control room procedures, alongside a separate, undisclosed settlement with the Federal Energy Regulatory Commission. The incident triggered a U.S. federal state of emergency declaration for fuel transport and prompted a wave of new federal cybersecurity directives for pipeline operators. The reputational and political fallout extended well beyond the company itself, becoming a widely-cited example in national critical-infrastructure security policy discussions.

**Key Lessons for Defenders & Auditors:** This case is a near-perfect illustration of today's entire session working together. The **threat** was a human-intentional one (a criminal ransomware group). The exploited **vulnerability** was a specific, narrow gap: one legacy account without MFA. The resulting **risk** was catastrophic, disproportionate to how small and specific the underlying gap was — precisely because the account happened to provide access into a critical operational network. Most importantly for today's session: **a routine security audit checking the specific parameter "are all active remote-access accounts covered by mandatory MFA, and is there a documented process confirming inactive accounts are formally deactivated?" would very plausibly have caught this exact gap before it was exploited.** This is the clearest possible demonstration of why today's shift from vague security impressions to specific, testable security parameters isn't academic — it's the difference between catching a known, common gap in a routine review and reading about it afterward in a national news headline.

---

## Interactive 35-Minute Lab

**Lab Title:** Build a Security Parameter Checklist — From Threat to Testable Criterion

**Objective:** Practice the exact skill that separates strong auditors from weak ones: turning a general threat concern into a specific, evidence-based, testable security parameter — using the Bidii SACCO scenario you've now worked with across two prior sessions.

**Required Environment / Tools:** Your completed classification and control table from the previous session, a text editor or notebook.

**Note on class format:** Two pairs again today. Swap partners once more so that, across the first three sessions, everyone has now worked directly with each other classmate at least once.

**Step-by-Step Execution Guide:**

1. **(5 min, individually)** Looking back at the Bidii SACCO scenario (member portal, core banking app, physical filing room, HR system, informal WhatsApp group, the decommissioned pilot server, and the third-party SMS gateway), identify **one plausible threat** for each of the taxonomy categories covered today: one Natural/Environmental threat, one Human-Intentional threat, one Human-Unintentional threat, one Technical threat, and one Third-Party threat — each specifically relevant to this organization, not generic.

2. **(10 min, in your pairs)** For each of your five threats, identify the specific **vulnerability** at Bidii SACCO that would allow that threat to actually cause harm, and briefly state the resulting **risk** in one sentence, using the Threat + Vulnerability = Risk logic from today's session. (Example format: *Threat: a departed IT contractor retains access. Vulnerability: no documented account deprovisioning process exists. Risk: a disgruntled or careless former contractor could access member financial data indefinitely after their contract ends.*)

3. **(10 min, same pairs)** For your **two highest-risk items**, write a specific, testable **security parameter** an auditor could actually check — modeled directly on the Colonial Pipeline lesson. Your parameter must be phrased so that it can be answered with a measurable yes/no or a specific figure, not a vague impression. (Weak: "check if access is well managed." Strong: "confirm that 100% of accounts with remote or admin-level access to the core banking application have MFA enabled, and that a documented deprovisioning log shows account deactivation within 24 hours of an employee or contractor's departure date.")

4. **(5 min) Class debrief.** Both pairs present one Threat → Vulnerability → Risk → Security Parameter chain in full, side by side. The instructor will specifically challenge any parameter that isn't precisely measurable — this is the exact discipline real Lead Auditors are trained to enforce on themselves and each other.

**Expected Artifacts & Evidence:**

```
| Threat                         | Category            | Vulnerability                                  | Risk (one sentence)                                                  | Testable Security Parameter                                                                 |
|----------------------------------|------------------------|---------------------------------------------------|--------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| Departed contractor retains access | Human - Unintentional | No documented account deprovisioning process       | Former contractor could access member data indefinitely after contract end | 100% of admin/remote accounts covered by MFA; deprovisioning log shows deactivation within 24hrs |
| Ransomware via phishing            | Human - Intentional    | No MFA on core banking app remote access            | Attackers gain full access to member financial data and can halt operations | Mandatory MFA enforced on all remote-access accounts; verified quarterly with evidence log        |
```

---

## Mini-Project / Take-Home Challenge

**Challenge: Audit One Real System**

Choose **one real system** you have legitimate, authorized access to and reasonable knowledge of (a system at your workplace or internship — with appropriate discretion about what you share in class — or a personal account/service you manage, like your own email or a family shared cloud drive).

Write a short, structured mini-audit covering:
- One identified threat, using today's taxonomy, that is genuinely plausible for this specific system.
- The corresponding vulnerability and resulting risk, in the Threat → Vulnerability → Risk format practiced in today's lab.
- **Two specific, testable security parameters** you could realistically check yourself (e.g., "is MFA enabled on this account — yes/no, verified by checking the account's security settings directly") — and actually check them, honestly reporting the result.

**Deliverable format:** A short written report (200–300 words), submitted before the next session, including your two actual, honestly-reported parameter check results. **Be ready to briefly present your findings** — with a class of 4, expect everyone to share, including anyone whose honest check reveals a gap (this is normal, and is exactly the point of the exercise).

---

## Discussion Questions & Knowledge Check

Run this as an open round-table — every student answers each question before moving to the next.

1. Colonial Pipeline's breach traced back to one legacy VPN account without MFA. Why is it significant that this was a *routine, checkable security parameter* rather than a novel or highly sophisticated technical exploit? What does this imply about where organizations should focus a limited security budget?

2. Explain, in your own words and using a fresh example not already used in today's session, the difference between a threat, a vulnerability, and a risk. Make sure your example clearly shows why all three terms are necessary and cannot be collapsed into just one or two.

3. An auditor is told by an IT manager, "Don't worry, we definitely patch all our servers regularly." Using today's concept of objective evidence, explain exactly what the auditor should do next, and why simply accepting this statement would represent a failure of the audit's core objectives.

4. Of the five threat categories covered today (Natural, Environmental, Human-Intentional, Human-Unintentional, Technical, Third-Party — six if you count Environmental separately), which do you believe is most commonly under-prioritized by organizations in practice, and why? Defend your answer with reasoning, not just intuition.

5. Revisit the Bidii SACCO scenario's WhatsApp group, used informally by branch managers. Propose one specific, testable security parameter that could meaningfully reduce the risk associated with that particular system — and explain why a vague policy statement like "staff should be careful what they share" would fail to meet the standard of a real security parameter as defined today.
