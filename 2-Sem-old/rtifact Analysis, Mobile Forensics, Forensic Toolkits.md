# Friday Combined Session: Artifact Analysis, Mobile Forensics, Forensic Toolkits & Full Diploma Capstone
**Module:** Module 11 — Cyber Forensics | **Units:** Unit 3 (Computer Forensics, concluded) & Unit 4 (Mobile Forensics) | **Diploma Capstone**

This session combines everything remaining in the diploma into one final teaching day: Artifact Analysis, Mobile Forensics Foundations, Extraction Types & Forensic Toolkits, and the full Module 11 / whole-diploma capstone review. Because this compresses four planned sessions into one, treat this as a marathon day — pace deliberately, and don't be afraid to let the discussion questions and labs run past the nominal 90 minutes where the class is genuinely engaged. This is the last day of the diploma.

---

## Session Objectives & Real-World Context

**What You Will Learn:**
- How to extract and interpret four of the most valuable Windows forensic artifacts — **Prefetch**, **Shimcache**, **Event Logs**, and the **Master File Table (MFT)** — using real tools (Autopsy and FTK Imager) to prove program execution and file activity even when an attacker has tried to cover their tracks.
- The foundational **Android and iOS architectures** that every mobile forensic investigation must understand before attempting any extraction.
- The three core **mobile extraction types** — Logical, File System, and Physical — and the specific technical challenges (Full Disk Encryption, the Secure Enclave, remote wiping) that make modern mobile forensics dramatically harder than it was a decade ago.
- The landscape of **mobile forensic toolkits**, from commercial platforms like Cellebrite to open-source alternatives, and how to reason about which tool fits which situation.
- A complete synthesis of **everything covered across Module 11**, and — for your final session — a synthesis of the **entire diploma**, from Module 8's malware content through today's mobile forensics conclusion.

**Why It Matters to a Security Professional:** This is the day everything comes together. Artifact analysis is what turns a memory dump and a disk image into a proven, defensible timeline of exactly what happened. Mobile forensics extends everything you've learned about disk and memory forensics into the device category most people now carry everywhere, and carries its own dramatically harder technical and legal challenges. And today's final capstone review is your last chance, before this diploma ends, to see the whole shape of what you've built — from Module 8's attacker tradecraft through Module 9's governance, Module 10's law, and Module 11's investigative method — as one connected professional skill set, not four separate courses.

---

# Part 1: Artifact Analysis — Prefetch, Shimcache, Event Logs & MFT

### Windows Prefetch

**Prefetch** is a Windows performance feature that creates a small file every time an executable is run, recording the program's name, the number of times it has been executed, and — critically for forensics — the **last execution timestamp** (and, in newer Windows versions, the last several execution timestamps). Prefetch files are stored in `C:\Windows\Prefetch` and persist even after the original program has been deleted, making Prefetch one of the single most valuable artifacts for proving that a specific program — including malware — was actually **executed**, not merely present on disk.

### Shimcache (Application Compatibility Cache)

**Shimcache**, technically the Application Compatibility Cache, is a Windows mechanism originally designed to track application compatibility information, but forensically valuable because it records the **full file path, file size, and last-modified timestamp** of executables that have been run or, in some cases, merely browsed to in Windows Explorer. Shimcache entries can persist even when Prefetch has been disabled or cleared, making it a valuable corroborating or fallback artifact — directly connecting to the "triangulation" principle from Module 9's Day 4: two independent artifacts agreeing on the same execution event is far stronger evidence than either alone.

### Windows Event Logs

Covered extensively via Sysmon throughout Module 8, native **Windows Event Logs** (Security, System, Application, and the specialized Sysmon Operational log) remain the backbone of host-based forensic timeline reconstruction. For today's artifact analysis focus, the key logs to recall are **Security Event ID 4624/4625** (successful/failed logon), **4688** (process creation, the native Windows equivalent of Sysmon's Event ID 1), and the Sysmon Event IDs 1, 3, 10, and 11 you've used throughout this diploma.

### The Master File Table (MFT)

The **Master File Table** is the core NTFS filesystem structure that records metadata about every single file and folder on an NTFS volume — including files that have since been deleted, since their MFT entry often persists until overwritten. Each MFT entry contains, among other attributes, two timestamp attributes forensically vital to know apart: **`$STANDARD_INFORMATION`** (the timestamps most tools and the OS itself display, and the ones most trivially altered by simple "timestomping" anti-forensic tools) and **`$FILE_NAME`** (a second, independent timestamp attribute that is considerably harder for an attacker to alter, since most common timestomping tools only modify `$STANDARD_INFORMATION`). **A discrepancy between these two attributes on the same file is one of the strongest possible indicators of deliberate timestamp manipulation** — directly extending today's recurring "compare two independent sources and treat any mismatch as a red flag" theme from Volatility's `pslist`/`psscan` and Module 8's GMER content.

### Practical Lab: MFT and Timeline Analysis with Autopsy

**Tool:** Autopsy (free, open-source, built on The Sleuth Kit).

**Objective:** Load a disk image into Autopsy, extract MFT timestamp data, and build a basic execution timeline using Prefetch and Event Log artifacts together.

**Step-by-Step Execution Guide:**

1. Open Autopsy and create a new case, adding your Day 5 E01 image (or a provided sample disk image) as a data source.
2. Once ingest modules complete, navigate to the **Recent Activity** and **File System** views. Locate the Prefetch folder under `Windows/Prefetch` and record the last-execution timestamp for two or three notable executables.
3. Use Autopsy's **Timeline** feature to build a combined visual timeline correlating file system events (from the MFT) with any available Event Log entries — directly practicing the multi-source correlation principle from today's theory.
4. For one file of interest, compare its `$STANDARD_INFORMATION` and `$FILE_NAME` timestamps (Autopsy exposes both under the file's detailed metadata view) and record whether they match.

**Expected Artifact:**
```
ARTIFACT ANALYSIS LOG
Prefetch findings: [executable, last-run timestamp] x2-3
Timeline correlation: [file event] aligned with [log event]
$STANDARD_INFORMATION vs $FILE_NAME: [Match/Mismatch] — Conclusion: ...
```

### Case Study Note: The 2016 DNC Hack (APT28/APT29)

The widely publicized investigation into the 2016 Democratic National Committee breach, attributed to Russian state-linked actors APT28 and APT29, relied heavily on exactly this kind of host-based forensic artifact analysis — execution timelines, log correlation, and file system metadata — to reconstruct the intrusion's timeline and build technical attribution, directly demonstrating why the artifacts covered today remain central to real, high-stakes investigations.

---

# Part 2: Mobile Forensics Foundations — Android & iOS Architectures

### Android Architecture

Android is built on a **Linux kernel**, with each application running in its own sandboxed process under a unique Linux user ID, enforcing app isolation at the OS level. Key forensic-relevant components: the **Android file system** (commonly EXT4), the **Dalvik/ART runtime** executing app bytecode, and critically, an extensive set of **SQLite databases** used by nearly every app to store local data — messages, call logs, browsing history, and app-specific data are very often directly recoverable from these database files, making SQLite literacy a genuinely valuable forensic skill.

### iOS Architecture

iOS is built on a **Darwin-based (Unix) kernel**, with a considerably more locked-down, vendor-controlled architecture than Android's more open ecosystem. Apple's **Secure Enclave** — a dedicated, physically isolated hardware security coprocessor — manages cryptographic keys and biometric data (Face ID/Touch ID) entirely separately from the main processor, meaning even a fully compromised main OS cannot directly extract these keys, a design specifically intended to resist exactly the kind of forensic extraction covered in Part 3 below.

---

# Part 3: Extraction Types, Mobile Challenges & Forensic Toolkits

### The Three Extraction Types

- **Logical Extraction** — the least invasive method, extracting data through the device's standard operating system APIs (similar in spirit to a backup) — fast and low-risk, but retrieves only what the OS is willing to expose, missing deleted data and hidden artifacts.
- **File System Extraction** — a deeper extraction accessing the device's full file system structure, retrieving considerably more than a logical extraction, including some application data not accessible through standard APIs.
- **Physical Extraction** — the deepest possible method, acquiring a bit-for-bit copy of the device's entire physical storage — directly analogous to the disk imaging covered in Day 5 — capable of recovering deleted data, but the hardest to achieve on modern, well-secured devices and often requiring specialized hardware or exploited vulnerabilities.

### The Core Mobile Forensic Challenges

- **Full Disk Encryption (FDE)** — modern Android and iOS devices encrypt their entire storage by default, meaning a physical extraction of an encrypted, locked device yields unreadable ciphertext without the correct decryption key or passcode.
- **The Secure Enclave** (and Android's equivalent, the Trusted Execution Environment/StrongBox) — as covered above, these dedicated hardware components are specifically engineered to resist exactly the kind of key-extraction techniques a forensic examiner would otherwise attempt.
- **Remote Wiping** — a device that remains connected to a network can potentially be remotely wiped by its owner or an attacker at any time before an examiner can isolate it, directly connecting to Day 5's first-responder network isolation content, now applied specifically to the mobile context — placing a seized device in a Faraday bag (blocking all radio signals) is a standard, essential first step for exactly this reason.

### Forensic Toolkits

**Cellebrite** is the best-known commercial mobile forensics platform, offering specialized hardware and software (notably the UFED — Universal Forensic Extraction Device) capable of performing logical, file system, and — for many supported device/OS version combinations — physical extractions, along with automated parsing and reporting of extracted data. **Open-source alternatives** include **ALEAPP** (Android Logs Events And Protobuf Parser) and **iLEAPP** (its iOS equivalent), both widely used, actively maintained tools for parsing already-extracted mobile file system data into human-readable artifacts, and Autopsy's own Android analysis module.

### Case Study: FBI v. Apple — The San Bernardino iPhone (2016)

Following the 2015 San Bernardino terrorist attack, the FBI sought to access the shooter's locked iPhone but was unable to bypass its passcode and encryption. The FBI legally compelled Apple to assist, and Apple **refused**, arguing that creating the requested tool — effectively a backdoor bypassing its own security — would create a dangerous precedent and a genuine security risk for all iPhone users if it were ever leaked or misused. Before the resulting legal battle was resolved in court, the FBI **paid a third-party company (widely reported to be a specialized security firm) to unlock the device using an undisclosed method**, and withdrew its legal action. This case is one of the most significant, widely-cited illustrations of the exact tension between the Secure Enclave/FDE challenges covered above and law enforcement's investigative needs — and remains a foundational reference point in ongoing global debates about encryption backdoors, directly connecting to Module 10's legal and privacy content (recall the Puttaswamy privacy judgment from Day 13).

---

# Full Module 11 Recap

```
Unit 1 (Cyber Crime): Classification (Economic/Espionage/Hacktivism, Diamond Model)
                       → Characteristics & Prevention (Routine Activity Theory, CERTs, INTERPOL/Europol)
Unit 2 (Foundations):  Digital Evidence, Locard's Principle, Chain of Custody
                       → Order of Volatility, 4-Phase Methodology
Unit 3 (Computer Forensics): First Responder Procedures, Write-Blocking, Disk Imaging (Raw/E01)
                       → Memory Acquisition & Volatility Framework (pslist/psscan)
                       → Artifact Analysis (Prefetch, Shimcache, Event Logs, MFT)
Unit 4 (Mobile Forensics): Android/iOS Architecture → Extraction Types, Challenges, Toolkits
```

## Case Study Marathon — Module 11

| Case | Pattern |
|---|---|
| Bangladesh Bank / Lazarus Group | Economic/espionage motivation blending in a single actor |
| Operation Payback / Anonymous | Hacktivism's visibility-seeking behavioral signature |
| Emotet Takedown (2021) | International cooperation as a prevention framework |
| Dennis Rader (BTK) | Locard's Principle via file metadata |
| Ross Ulbricht (Silk Road) | Volatility-aware live seizure done correctly |
| Daubert Standard | Why standardized procedure is a legal admissibility requirement |
| Stuxnet | Why deep analysis must not trust a system's own self-reporting |
| DNC Hack (2016) | Host artifact analysis building a real intrusion timeline |
| FBI v. Apple | The FDE/Secure Enclave vs. investigative access tension |

---

# Full Diploma Capstone — Modules 8 Through 11

```
MODULE 8: CYBER ATTACKS           → How attackers actually operate (malware, botnets,
                                     intrusion, persistence, OSINT)
MODULE 9: ISMS / ISO 27001        → How organizations govern and audit their defense
MODULE 10: CYBER LAW              → The legal frameworks governing all of the above
MODULE 11: CYBER FORENSICS        → How you prove, evidence, and investigate when
                                     prevention and governance still fail
```

Across four modules, you have built a genuinely complete professional loop: understanding the attacker (Module 8), building and auditing the defense (Module 9), knowing the law that governs it all (Module 10), and knowing exactly how to investigate and prove what happened when something still goes wrong (Module 11). Few diploma programs connect these four disciplines this explicitly — you now can.

---

## Final Capstone Lab (Extended)

**Objective:** In your merged four-person team, produce a single one-page "Case Brief" applying all four modules to one final scenario: *Bidii SACCO suffers a breach; a former loan officer's still-active account (Module 9) is used via a phishing-obtained credential (Module 8) to access member data; Bidii SACCO must determine its GDPR/Kenyan Data Protection Act notification obligations (Module 10) and properly forensically investigate the incident (Module 11).* Cover: the attack technique, the governance control that failed, the legal notification triggered, and the first three forensic steps you would take, in the correct order.

## Discussion Questions — Full Diploma Synthesis

1. Which single module changed your thinking the most over this diploma, and why?
2. If you had to explain "what does a cybersecurity professional actually do" to a stranger, using all four modules, what would you say in three sentences?
3. Looking at the FBI v. Apple case, where do you personally believe the right balance sits between encryption security and law enforcement access?
4. Of everything covered across all four modules, which single skill do you feel least confident in, and what is your plan to keep building it after this diploma ends?
