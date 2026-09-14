# Cyber Crime — Classifications: Economic vs. Espionage vs. Hacktivism
**Module:** Module 11 — Cyber Forensics | **Unit:** Unit 1 — Cyber Crime

---

## Session Objectives & Real-World Context

**What You Will Learn:**
- A precise, working definition of **cybercrime** and the three core classification categories this session focuses on — **Economic**, **Espionage**, and **Hacktivism** — including the distinct motivations, typical actors, tradecraft, and targets associated with each.
- Why real-world threat actors frequently **blur these categories** rather than fitting neatly into one — including a specific, well-documented example of a single nation-state group operating across both economic and espionage motivations.
- The **Diamond Model of Intrusion Analysis** — a professional framework (Adversary, Capability, Infrastructure, Victim) used across the industry to structure exactly this kind of classification analysis systematically, rather than by gut feeling.
- Hands-on, practical experience using **two real, industry-standard threat intelligence tools** — the MITRE ATT&CK Groups database and VirusTotal — to research and classify real threat actors and malware samples yourself.
- Why correctly classifying a cybercrime's motivation early in an investigation directly shapes legal handling, resourcing, and response priority — connecting forward to the forensic methodology you'll build across the rest of this module.

**Why It Matters to a Security Professional:** Welcome to Module 11 — Cyber Forensics. Before you can properly investigate a cybercrime, you need a clear, professional vocabulary for *what kind* of cybercrime you're actually looking at, because motivation shapes almost everything downstream: how the attacker likely behaved, what evidence they likely left, how urgently the incident needs to be escalated, and even which law from Module 10 applies. A SOC Analyst or forensic investigator who can quickly, correctly answer "is this financially motivated, is this espionage, or is this a protest?" is already several steps ahead in shaping the right response — and today gives you real, hands-on practice doing exactly that classification work using the same tools working analysts use every day.

---

## Core Theory & Technical Mechanics

### Defining Cybercrime and Why Classification Matters

**Cybercrime** is any criminal activity that involves a computer, computer network, or digital device, either as the target of the crime or as the tool used to commit it. This broad definition covers an enormous range of activity — but not all cybercrime is committed for the same reason, and understanding *why* a given act was committed is one of the most practically useful classification exercises a security professional can perform, because motivation directly predicts behavior.

### Economic Cybercrime

**Economic (financially motivated) cybercrime** is committed primarily for direct or indirect financial gain. This is, by a wide margin, the most common motivation category across the global threat landscape.

- **Typical actors:** organized cybercriminal groups, Ransomware-as-a-Service operators and affiliates (recall Module 8's LockBit/BlackCat content), carding and fraud rings, Business Email Compromise (BEC) fraudsters.
- **Typical tradecraft:** ransomware deployment, banking Trojans and InfoStealers, cryptojacking, payment card fraud, cryptocurrency theft, and increasingly, direct manipulation of financial transfer systems.
- **Typical targets:** any organization or individual with money, valuable data that can be monetized (sold, ransomed, or used for further fraud), or access to payment infrastructure — targeting tends to be broad and opportunistic rather than narrowly selective, since the goal is maximizing return rather than achieving a specific strategic outcome.
- **Behavioral signature:** economically motivated actors generally prioritize **speed and scale of monetization** over long-term stealth — once access is achieved, the goal is typically to extract value (encrypt and ransom, steal and sell, transfer funds) relatively quickly, since prolonged dwell time increases detection risk without necessarily increasing financial return.

### Espionage-Motivated Cybercrime

**Espionage** is committed to gather intelligence — political, military, economic, or technological — typically on behalf of a nation-state, though corporate espionage (a company targeting a competitor) is a related, distinct category.

- **Typical actors:** state-sponsored Advanced Persistent Threat (APT) groups, often with formal or informal ties to a national intelligence apparatus.
- **Typical tradecraft:** highly targeted spear-phishing, custom-built malware designed to evade detection for extended periods, supply chain compromise (recall the SolarWinds case from Module 9), and prolonged, carefully managed persistence within a target network.
- **Typical targets:** government agencies, defense contractors, critical infrastructure operators, research institutions, and specific companies holding valuable intellectual property or strategic information — targeting is highly deliberate and selective, not opportunistic.
- **Behavioral signature:** espionage-motivated actors prioritize **stealth and prolonged access** above almost everything else — the entire value of an espionage operation depends on remaining undetected for as long as possible, since the intelligence value comes from sustained access, not a single extraction event. This is precisely why espionage-linked intrusions are so often associated with the extended dwell times covered throughout Module 8 and Module 9's Marriott/Starwood case study.

### Hacktivism

**Hacktivism** is cybercrime committed to advance a political, social, or ideological cause, typically aiming to draw public attention to that cause, embarrass a target, or disrupt a target's operations as a form of protest.

- **Typical actors:** loosely organized or decentralized collectives (the collective known as "Anonymous" being the most widely recognized example), issue-specific activist groups, and sometimes individual actors acting alone under a cause-driven banner.
- **Typical tradecraft:** website defacement, Distributed Denial of Service (DDoS) attacks against a target's public-facing infrastructure, and data leaks specifically intended to embarrass or expose a target (as opposed to being sold for profit).
- **Typical targets:** organizations or governments the group perceives as acting unethically, oppressively, or contrary to the cause being championed — targeting is driven by symbolic or political relevance rather than financial value.
- **Behavioral signature:** hacktivists frequently prioritize **visibility and public attribution** over stealth — unlike economic or espionage actors, a hacktivist action often loses much of its value if no one knows it happened or who claims responsibility, leading to public announcements, defaced pages left clearly visible, and leaked data deliberately publicized rather than quietly sold.

### Why Real-World Actors Blur These Categories

These three categories are a useful analytical starting point, but real-world threat actors very often don't fit cleanly into just one. The clearest, most consistently cited example is **North Korea's Lazarus Group**, which has been linked to activity spanning multiple categories simultaneously: large-scale, clearly economically-motivated operations (cryptocurrency theft, bank fraud, covered in today's primary case study) alongside operations with a strong espionage or even destructive/political dimension. This blending reflects North Korea's specific position as a heavily sanctioned state using state-sponsored cyber operations partly as a direct revenue-generation mechanism, alongside more traditional espionage and geopolitical objectives — a genuinely unique motivational profile that doesn't map cleanly onto any single one of today's three categories alone.

> **Key Term — Why this blurring matters practically:** A security analyst who assumes "this looks like ransomware, so it must be purely economic" may miss a broader espionage or geopolitical dimension to an intrusion, and vice versa. Classification is a genuinely useful analytical starting point, but it should always be treated as a working hypothesis to be tested against evidence, not a box to check once and never revisit.

### The Diamond Model of Intrusion Analysis

A widely used professional framework for structuring exactly this kind of classification and analysis work is the **Diamond Model of Intrusion Analysis**, which models any intrusion event as four core, interconnected features:

- **Adversary** — who is conducting the activity (even if only characterized by behavior rather than a confirmed real-world identity).
- **Capability** — the tools, techniques, and malware the adversary uses.
- **Infrastructure** — the physical or logical infrastructure (servers, domains, IP addresses) the adversary uses to deliver capabilities or maintain C2 (recall Module 8's C2 content).
- **Victim** — who or what is being targeted.

Analysts using this model examine relationships between these four features across multiple observed events to build a confident picture of an adversary's identity, motivation, and likely future behavior — precisely the systematic, evidence-based approach you'll practice in today's labs, rather than guessing at motivation from a single, isolated data point.

### Non-Technical Analogies

> 🕵️ **The Three Categories as Three Different Kinds of Intruders in a Museum.** An **economic** intruder breaks in specifically to steal the most valuable, easily-resold items and leave as quickly as possible — smash and grab, prioritizing speed over subtlety. An **espionage** intruder doesn't take anything visible at all — they photograph blueprints, security schedules, and layouts, then leave everything exactly as they found it, hoping the museum never even realizes anyone was there, because the entire value of what they took depends on nobody knowing it's gone. A **hacktivist** intruder breaks in, spray-paints a political slogan across the main gallery wall in bold, unmissable letters, and specifically wants security footage of the act to be seen and shared — the entire point is that everyone knows it happened and why.

> 💎 **The Diamond Model as a Detective's Standard Case Board.** A detective investigating a series of connected incidents doesn't just ask "who did this?" in isolation — they map out the suspect (Adversary), the specific tools and methods used (Capability), the getaway vehicles and safehouses (Infrastructure), and the pattern of victims chosen (Victim), then looks for consistent connections across all four categories across multiple incidents to build genuine, evidence-based confidence in who's responsible and why — exactly the systematic approach the Diamond Model brings to intrusion analysis.

---

## Multi-Perspective Breakdown

**Attacker's POV:** An actor's underlying motivation directly shapes their own operational security choices — an espionage actor accepts a much slower, more patient operational tempo specifically to preserve stealth, while an economically motivated ransomware affiliate accepts a much higher detection risk in exchange for faster monetization, since their business model depends on volume across many targets rather than sustained access to one. A hacktivist, in stark contrast to both, may deliberately accept even higher detection risk in exchange for guaranteed public visibility, since anonymity itself often works against their actual objective.

**Defender's / SOC Analyst's POV:** Correctly hypothesizing an intrusion's likely motivation early in an incident directly shapes triage and escalation decisions — a suspected espionage-motivated intrusion targeting sensitive data warrants immediate, discreet escalation to senior leadership and possibly national authorities, given the potential Section 66F cyberterrorism/national security dimension from Module 10's Day 15, while a suspected hacktivist DDoS against a public website, while still serious, generally follows a very different response and communications playbook, often including public-facing incident communication rather than discretion.

**Auditor's / Forensic Investigator's POV:** Motivation classification has genuine legal weight, not just analytical value — recall Module 10's Section 66F specifically criminalizes cyber terrorism with dramatically more severe penalties than ordinary economic cybercrime offenses, meaning a forensic investigator's classification work can directly influence which legal provision ultimately applies to a case, which investigating authority takes the lead, and how a court eventually sentences a convicted offender.

---

## Real-World Case Study

**Primary Case Study: The 2016 Bangladesh Bank Heist — Lazarus Group and the Economic/Espionage Blend**

**Incident Summary:** In February 2016, attackers attempted to steal $951 million from Bangladesh Bank's account held at the Federal Reserve Bank of New York, using fraudulent SWIFT (Society for Worldwide Interbank Financial Telecommunication) payment instructions. Most of the fraudulent transfers were blocked, but attackers successfully diverted approximately **$81 million**, laundered through casinos in the Philippines, in what remains one of the largest successful bank heists in history.

**Root Cause & Vulnerability Exploited:** Attackers had gained access to Bangladesh Bank's systems and obtained legitimate SWIFT credentials, allowing them to issue payment instructions that appeared entirely authentic to the receiving institutions. The vast majority of the attempted transfers were ultimately halted specifically because one fraudulent instruction misspelled the recipient organization's name ("fandation" instead of "foundation"), triggering a manual fraud review that caught the anomaly — a detail that has become a widely cited, almost cautionary example of how a single small procedural check can limit catastrophic loss even after a sophisticated technical compromise has already succeeded.

**Attribution and Motivation:** The attack has been widely attributed by security researchers and multiple governments to **Lazarus Group**, an actor associated with North Korea. This case is included specifically because Lazarus Group's broader body of documented activity spans both a clearly **economic** motivation (this heist, along with extensive documented cryptocurrency theft operations) and activity more consistent with **espionage** and geopolitically-driven objectives elsewhere in its history — making it one of the clearest real-world illustrations of exactly the category-blurring described in today's theory section.

**Key Lessons for Defenders & Investigators — connecting directly to today's content:** This case demonstrates that classification frameworks, while genuinely useful, must be applied with appropriate humility — Lazarus Group cannot be filed away as purely "an economic actor" or purely "an espionage actor" without missing a significant part of the real picture. For a forensic investigator, the lesson is to use classification as a starting hypothesis that shapes initial investigative priorities (in this case, immediately involving financial fraud investigators and international banking security teams, given the clear economic signature), while remaining open to the broader geopolitical and espionage dimensions a nation-state-linked actor's activity may also carry.

**Secondary Case Study: Operation Payback (2010) — Anonymous and Hacktivism**

**Incident Summary:** In late 2010, the decentralized hacktivist collective known as Anonymous conducted a coordinated series of Distributed Denial of Service (DDoS) attacks, under the banner "Operation Payback," against the websites of PayPal, Visa, and Mastercard, after these companies suspended payment processing services to WikiLeaks following its release of sensitive diplomatic cables.

**Root Cause & Motivation:** The attacks were explicitly framed by their participants as a protest against what they viewed as corporate censorship and retaliation against WikiLeaks, using freely available DDoS tools distributed and coordinated openly across online forums and social media, deliberately inviting broad, decentralized participation rather than being executed by a small, covert team.

**Business & Legal Impact:** The targeted companies experienced significant, if temporary, service disruption, and the operation generated substantial global media coverage — directly achieving the visibility-focused objective described in today's theory section. Several individuals connected to the operation were later identified, prosecuted, and convicted under computer misuse legislation in multiple countries, illustrating that the openly coordinated, low-technical-barrier nature of hacktivist campaigns, while effective for visibility, also tends to leave a comparatively traceable evidentiary footprint compared to the deliberately covert operations of economic or espionage-motivated actors.

**Key Lessons for Defenders & Investigators:** This case is a clean, contrasting illustration of the hacktivism behavioral signature described in today's theory section — public, openly coordinated, visibility-seeking, and using comparatively unsophisticated but effective tools (volumetric DDoS) rather than the stealthy, custom-built tradecraft associated with espionage, or the fraud-focused financial tradecraft associated with economic crime. For an investigator, the openly declared motivation and public coordination channels themselves become valuable investigative evidence — a stark contrast to the deliberately obscured attribution trail typical of the Bangladesh Bank case above.

---

## Practical Labs — Using Real Threat Intelligence Tools

Today's session includes **two separate hands-on labs**, each using a different real, industry-standard, publicly accessible tool — giving you direct experience with the actual resources working threat intelligence analysts and SOC teams use every day to perform exactly this kind of classification work.

### Lab A: Classifying Real Threat Groups Using the MITRE ATT&CK Groups Database

**Tool:** MITRE ATT&CK Groups database (`attack.mitre.org/groups/`) — the same MITRE ATT&CK framework you used extensively for technique mapping in Module 8, now used for its catalog of documented, named threat actor groups.

**Objective:** Research three real, named threat groups and classify each by primary motivation using today's framework, backed by the group's actual documented behavior.

**Step-by-Step Execution Guide:**

1. Navigate to the MITRE ATT&CK Groups page and select **one group widely associated with nation-state espionage** (for example, APT28 or APT29). Read its group profile summary and note: which sectors/countries it typically targets, and what its documented objectives appear to be (data theft, persistent access, etc.).

2. Select **one group widely associated with financially motivated cybercrime** (for example, FIN7 or Wizard Spider). Read its profile and compare: does its targeting pattern look broad and opportunistic, or narrow and strategic, compared to the espionage group above?

3. Attempt to find a group in the database that could be classified as **hacktivist-motivated**. You will likely find this difficult or impossible within MITRE ATT&CK's Groups catalog specifically. **This is itself an important finding, not a failure of the exercise** — record your observation and hypothesize, in one or two sentences, why a framework built primarily around persistent, sophisticated threat actors might not extensively catalog loosely-organized hacktivist collectives in the same structured way.

4. For your two successfully profiled groups (espionage and economic), record: the group's documented associated software/tools listed on its profile page, and at least one specific, named technique associated with it that you recognize from Module 8's content.

**Expected Artifacts & Evidence:**

```
MITRE ATT&CK GROUPS RESEARCH LOG

Group 1 (Espionage-associated): ________
  Primary targets/sectors: ...
  Documented tools/software: ...
  Recognized technique(s) from Module 8: ...

Group 2 (Economic-associated): ________
  Primary targets/sectors: ...
  Documented tools/software: ...
  Recognized technique(s) from Module 8: ...

Hacktivist Group Search Finding:
  Was a clear hacktivist entry found? [Y/N]
  Hypothesis for why/why not: ...
```

### Lab B: Investigating a Malware Sample's Motivation Signature Using VirusTotal

**Tool:** VirusTotal (`virustotal.com`) — a free, legitimate, widely used online malware and URL scanning service, previously referenced conceptually in Module 8's sandbox lab context, now used directly for classification research.

**Objective:** Search for a well-documented, publicly known malware family or hash associated with a specific historical campaign, and use VirusTotal's detection tags, community comments, and any linked behavioral or technique information to infer the sample's likely motivation category.

> ⚠️ **Safety Note:** This lab involves only searching for and reading publicly available information about already-known, well-documented malware samples via VirusTotal's web interface — never download, execute, or handle any actual malicious file directly.

**Step-by-Step Execution Guide:**

1. In VirusTotal's search bar, search for a well-known malware family name associated with a campaign discussed in this diploma so far (for example, "WannaCry" or "Lazarus AppleJeus," a malware family publicly documented as linked to Lazarus Group's cryptocurrency-theft operations).

2. Review the top matching results. Note the **detection names** applied by different antivirus vendors (these often hint at the malware's classified family and sometimes its associated threat actor).

3. Check the **Community** tab (where available) for analyst comments, and note whether any comments reference a specific threat actor, campaign name, or stated objective (data theft, financial fraud, destructive payload, etc.).

4. Based purely on what you found — vendor detection names, any community attribution comments, and your own prior knowledge from Module 8 and today's session — classify the sample's most likely primary motivation category (Economic, Espionage, or a blend, as with Lazarus Group), and write a two-to-three sentence justification citing the specific evidence you found.

**Expected Artifacts & Evidence:**

```
VIRUSTOTAL MALWARE CLASSIFICATION LOG

Malware Family Searched: ________
Sample/Hash Reviewed: ________
Vendor Detection Names Noted: ...
Community/Attribution Comments Found: ...
Classified Motivation Category: [Economic / Espionage / Blend / Hacktivism]
Justification (2-3 sentences): ...
```

**Class Debrief for Both Labs (10 min):** Both pairs present one finding from Lab A and one from Lab B. The instructor will specifically probe whether the classification conclusions in Lab B are genuinely supported by the specific evidence found, or whether they rely on prior assumption alone — reinforcing the evidence-based standard built throughout Module 9's audit content.

---

## Mini-Project / Take-Home Challenge

**Challenge: Classify a Breach Not Yet Covered in This Diploma**

Using either the MITRE ATT&CK Groups database or a public threat intelligence write-up of your choosing, research **one real cyberattack or breach not already discussed in this diploma**, and write a short classification report covering:

- A brief summary of what happened.
- Your classification of its primary motivation (Economic, Espionage, Hacktivism, or a justified blend), citing specific evidence.
- One sentence applying the Diamond Model — name at least the Adversary and Victim elements as documented in your source.

**Deliverable format:** A short written report (200–300 words), submitted before the next session. Be ready to present your findings — expect all four students to share.

---

## Discussion Questions & Knowledge Check

Run this as an open round-table — every student answers each question before moving to the next.

1. Using the Bangladesh Bank case, explain why classifying Lazarus Group as purely "economic" or purely "espionage" would each be an incomplete picture. What specific evidence from the case supports a blended classification?

2. Compare the behavioral signatures of Operation Payback (hacktivism) and the Bangladesh Bank heist (economic/espionage blend). Which do you think would be easier for a forensic investigator to attribute to a specific responsible party, and why?

3. During Lab A, you likely found it difficult to locate a clearly hacktivist-classified group in the MITRE ATT&CK Groups database. What does this tell you about the kinds of threats that formal, structured threat intelligence tooling is built to track most thoroughly, and which kinds might require different research approaches?

4. If a SOC Analyst discovers an intrusion showing characteristics of both stealthy, prolonged access (suggesting espionage) and a ransomware payload eventually deployed (suggesting economic motivation), what would you recommend as the correct initial response priority, and why?

5. Thinking back to Module 10's Section 66F (Cyber Terrorism), under what circumstances do you think a hacktivist action could potentially escalate into being legally classified as cyberterrorism rather than ordinary hacktivism? Where do you think the line should be drawn?
