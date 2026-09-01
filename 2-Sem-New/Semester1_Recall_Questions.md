# Semester 2 Kickoff — Semester 1 Recall Check

**Purpose:** A quick diagnostic to see what's stuck from Modules 1-5 before starting Module 6. Not graded — use it to spot which topics need a 5-minute refresher before you build on them.

**How to run it:** Pick 2-3 questions per module (don't burn the whole session on this), mix cold-call with "who wants to answer" to get a read on the room, and use the facilitator table at the end to flag weak spots as you go.

---

## Suggested Class Structure (90 minutes)

| Time | Segment | What happens |
|---|---|---|
| 0:00-0:10 | **Welcome back** | Frame the semester: where they've been (Modules 1-5), where they're headed (Modules 6-11: pentesting, SIEM/SOAR, AI in security, DevSecOps/Zero Trust, forensics, governance/law), and how it all connects to the capstone project in March. |
| 0:10-0:45 | **Recall check (all 5 modules)** | Work through 2-3 questions per module below, roughly 6-7 min per module. Keep pace brisk — this is a pulse-check, not a re-teach. If a question stalls the room for more than ~90 seconds, give the answer yourself and move on; log it as "shaky" and keep going. |
| 0:45-0:55 | **Rapid-fire round** | Pick the 4-5 weakest spots you just logged and hit them again as quick-fire questions to reinforce before moving on. |
| 0:55-1:15 | **Semester 2 roadmap walkthrough** | Preview Module 6 (Vulnerability Assessment & Pentesting) and how it directly builds on Module 4 (network scanning, IDS/IPS) and Module 5 (OWASP Top 10) — this is the natural bridge, so lean on it. |
| 1:15-1:25 | **Module 6, Unit 1 kickoff** | Start the actual first lesson: Introduction to Vulnerability Assessment (vulnerability vs. exploit vs. risk, reconnaissance). |
| 1:25-1:30 | **Wrap-up & expectations** | Lab environment check (Kali, VMs), CAT/assessment cadence reminder, and what to bring to the next session. |

---

## Module 1 — Introduction to Cybersecurity & Information Security

**1. What are the three pillars of the CIA Triad, and can you give a real example of each being violated?**
> Confidentiality, Integrity, Availability. Confidentiality violated = data breach/leak; Integrity violated = data tampered with in transit or at rest (e.g. a defaced webpage, altered financial record); Availability violated = a DDoS attack or ransomware taking a system offline.
> *Note:* This resurfaces constantly — SOC metrics (Module 7) and ISMS (Module 11) both hang off CIA. Worth nailing now.

**2. What's the difference between a threat, a vulnerability, and a risk?**
> Threat = a potential cause of harm (an actor or event). Vulnerability = a weakness that can be exploited. Risk = the likelihood × impact of a threat exploiting a vulnerability. Common mix-up: students often use "risk" and "threat" interchangeably.

**3. Name two types of threat actors and what typically motivates each.**
> e.g. Hacktivists (ideology/politics), nation-states (espionage, geopolitical advantage), cybercriminals (financial gain), insider threats (grievance, financial pressure, or unintentional negligence).

**4. Qualitative vs. quantitative risk analysis — what's the difference, and when would you use one over the other?**
> Qualitative = descriptive scales (low/medium/high), fast, good for early-stage or resource-constrained assessments. Quantitative = numeric (e.g. Annual Loss Expectancy), more precise but needs reliable data. Real orgs often blend both.
> *Note:* This comes back hard in Module 11 (Risk Management & Auditing) — flag if shaky.

---

## Module 2 — Desktop & Server Security

**5. What does UAC (User Account Control) actually protect against on Windows?**
> It prevents software (and malware) from making system-level changes without explicit user/admin consent — reduces silent privilege escalation.

**6. What's a registry hive, and why would a forensic investigator care about one?**
> A hive is a logical grouping of registry keys/values (e.g. HKLM, HKCU) backed by a file on disk. Investigators care because hives retain evidence of installed software, USB device history, recent files, and persistence mechanisms — directly relevant to Module 10 (Digital Forensics).

**7. What's the difference between a domain account and a local account in Active Directory?**
> Local account = authenticates only against that single machine's SAM database. Domain account = authenticates against Active Directory and works across every machine joined to the domain — centralized identity, which is the seed of the IAM conversation in Module 9.

**8. Name two Linux hardening practices we covered, and what each defends against.**
> e.g. Least-privilege file permissions (chmod/chown) — limits blast radius of a compromised account; disabling unused services — reduces attack surface; SELinux/AppArmor mandatory access control — contains what a compromised process can touch.

---

## Module 3 — Data Security & Cloud Computing

**9. Explain the Shared Responsibility Model — what's the cloud provider's job vs. the customer's job?**
> Provider secures "of the cloud" (physical infrastructure, hypervisor, network fabric). Customer secures "in the cloud" (data, identity/access config, OS patching depending on service model). The split shifts by model: more customer responsibility in IaaS, less in SaaS.
> *Note:* Central to Module 9's Advanced Cloud Security unit — worth a solid refresher if shaky.

**10. What's the difference between encryption and hashing? Which one can you reverse?**
> Encryption is reversible with the right key (confidentiality). Hashing is one-way — used for integrity checks and password storage, not for hiding data you intend to retrieve.

**11. Steganography vs. cryptography — how are they different, and why might an attacker prefer one?**
> Cryptography scrambles data so it's unreadable but obviously present. Steganography hides the *existence* of data inside something innocuous (an image, audio file). An attacker might prefer steganography for covert exfiltration since it doesn't look suspicious in transit.

**12. Name one control from each: hardware-based and software-based physical security.**
> Hardware: biometric scanners, mantraps, cable locks. Software: remote wipe, disk encryption tied to TPM, asset-tracking/geofencing software.

---

## Module 4 — Network Protocols & Infrastructure Security

**13. What problem does a VPN actually solve, and name one protocol we covered?**
> Creates an encrypted tunnel over an untrusted network so traffic stays confidential and (usually) authenticated between endpoints. Protocols: IPsec, OpenVPN, WireGuard.

**14. What's the difference between WPA2 and WPA3, at a high level?**
> WPA3 replaces WPA2's 4-way handshake (vulnerable to offline dictionary attacks like KRACK) with SAE (Simultaneous Authentication of Equals), which resists offline brute-forcing and adds forward secrecy.

**15. Stateful vs. next-gen firewall — what can a next-gen firewall see that a stateful one can't?**
> Stateful firewalls track connection state (source/dest IP, port, session) but not payload content. Next-gen firewalls add deep packet inspection, application-layer awareness, and often integrated IPS/threat intel — they can tell *what app* is generating traffic, not just which port it's on.

**16. IDS vs. IPS — which one can actively block traffic, and what's the trade-off of that?**
> IPS sits inline and can actively block/drop malicious traffic; IDS is typically out-of-band and only alerts. Trade-off: IPS gives you prevention but a false positive can block legitimate traffic — higher stakes if tuning is poor.

**17. Name two types of access control models we discussed.**
> e.g. DAC (Discretionary), MAC (Mandatory), RBAC (Role-Based), ABAC (Attribute-Based). RBAC/ABAC resurface directly in Module 9's IAM unit.

---

## Module 5 — Web Security & Application Protection

**18. What's the core idea behind SQL injection, and what's the #1 defense against it?**
> Attacker injects malicious SQL through an untrusted input field to manipulate the backend query (read/modify/delete data, bypass auth). #1 defense: parameterized queries/prepared statements (not just input sanitization alone).

**19. XSS vs. CSRF — what's the key difference in what each attack tricks?**
> XSS tricks the *browser* into executing attacker-supplied script in the context of a trusted site (targets other users). CSRF tricks the *user's browser* into submitting an unwanted authenticated request to a site the user is already logged into (targets the user's session, not the input field).

**20. What does a WAF actually filter, and where does it usually sit in the architecture?**
> Filters HTTP/S traffic against known attack signatures and behavioral rules (SQLi, XSS, etc.) before it reaches the web application — typically sits in front of the app server, often at the load balancer/CDN edge.
> *Note:* Directly relevant to Module 6 pentesting — students will be attacking apps that may sit behind a WAF.

**21. Name one API authentication mechanism we covered and what it's protecting against.**
> e.g. OAuth 2.0 (delegated authorization without sharing credentials), JWT (stateless, signed tokens for verifying identity/claims on each request). Protects against unauthorized/unauthenticated API access.

---

## Facilitator Notes (fill in during class)

| Module | Strong | Shaky — needs a refresher |
|---|---|---|
| 1 — Intro/InfoSec | | |
| 2 — Desktop & Server | | |
| 3 — Data & Cloud | | |
| 4 — Network Infra | | |
| 5 — Web Security | | |

**Takeaway for planning:** Anything marked "shaky" is worth a 5-10 minute callback during the relevant Module 6-11 session where it resurfaces — CIA Triad in Module 7 (SOC metrics), Shared Responsibility Model and encryption in Module 9 (Cloud/IAM), access control models in Module 9 (IAM), and OWASP/WAF concepts in Module 6 (pentesting).
