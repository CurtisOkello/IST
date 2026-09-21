# First Responder Procedures, Write-Blocking & Disk Imaging (Raw DD / E01)
**Module:** Module 11 — Cyber Forensics | **Unit:** Unit 3 — Computer Forensics

---

## Session Objectives & Real-World Context

**What You Will Learn:**
- The specific responsibilities and decision-making framework a **First Responder** — often a SOC Analyst or IT staff member, not a dedicated forensic examiner — must follow at the moment a potential incident is discovered, including the critical, nuanced question of exactly *when* it becomes correct to power off a system, directly building on yesterday's Order of Volatility content.
- What a **write blocker** actually does at a technical level, why even innocently opening a file browser on original evidence media can silently alter it, and the difference between hardware and software write-blocking approaches.
- The two dominant forensic disk image formats — **Raw/DD** and **E01 (Expert Witness Format)** — their structural differences, and why E01's built-in hashing and metadata have made it the de facto industry standard.
- Real, hands-on experience creating a forensic image using **FTK Imager**, a free, industry-standard tool, and separately using the **dd** command to understand raw imaging and manual hash verification from first principles.
- Why standardized, validated forensic procedures — exactly the kind covered today — are not merely good practice, but the specific legal standard evidence must meet to survive an admissibility challenge in court.

**Why It Matters to a Security Professional:** Yesterday you learned what to capture and in what order. Today answers the next critical question: how do you capture it in a way that will actually hold up — technically and legally — under scrutiny? A brilliant analysis built on an improperly acquired, unverified disk image is worth nothing in a courtroom, and often worth very little in a serious internal investigation either. Today gives you the actual mechanics — write-blocking and hash-verified imaging — that transform "I looked at the evidence" into "I can prove, mathematically, that what I analyzed is an exact, unaltered copy of the original."

---

## Core Theory & Technical Mechanics

### First Responder Procedures

A **First Responder** in digital forensics is the first person to arrive at, or discover, a potential incident — and critically, this is very often **not** a dedicated forensic examiner at all, but a SOC Analyst, an IT staff member, a security guard, or even a curious employee who noticed something unusual. Because whoever is first on the scene has the greatest power to either preserve or accidentally destroy critical evidence, understanding correct first-responder procedure is directly relevant to your day-to-day SOC work, not just to specialists.

**Core first responder responsibilities:**

- **Secure the scene, physically and digitally.** Prevent unauthorized access to the device and surrounding area, and control who is permitted to touch anything — this is the literal starting point of the chain of custody covered in your Day 3 session.
- **Document everything observed, before touching anything.** Photograph the screen exactly as found (using a separate device, never the suspect system itself), note the exact time, date, and who was present, and record the visible state of the system — open programs, visible windows, any unusual displays.
- **Determine power state, and follow the correct decision path.** This is where yesterday's Order of Volatility becomes an operational decision, not just theory:
  - If the device is **powered on**, do not shut it down immediately. Follow proper volatile-data capture procedure first (memory, network connections, running processes — exactly as covered in your previous session), because shutting down immediately destroys this evidence permanently.
  - If the device is **powered off**, do **not** turn it on. Booting a powered-off system can alter file metadata, trigger scheduled tasks, and in the worst case, activate anti-forensic or destructive routines an attacker may have deliberately configured to trigger on startup.

**A critical nuance building directly on yesterday's lesson.** Yesterday's session established that carelessly "pulling the plug" before capturing volatile evidence is a serious mistake. Today adds an important refinement: **once volatile evidence capture is genuinely complete**, many forensic practitioners specifically recommend pulling the power directly, rather than using the operating system's normal shutdown sequence — because a graceful shutdown can trigger shutdown scripts, clear temporary files, flush caches in ways that destroy remaining forensic value, or in the case of a deliberately booby-trapped system, execute an attacker-configured wipe routine specifically designed to run during an orderly shutdown. The lesson is not "always pull the plug" or "never pull the plug" — it is **know exactly what stage of evidence capture you're in, and choose the shutdown method appropriate to that specific stage.**

- **Isolate the device from the network** where appropriate, balancing the need to stop an active attacker from causing further damage or remotely wiping the device against the volatility considerations from yesterday's session — this decision should ideally follow, not precede, volatile data capture wherever operationally possible.
- **Avoid using the suspect device for any responder activity** — no browsing its files "just to check," no running antivirus scans on it directly, no logging into email from it — every such action risks altering timestamps, generating new log entries, or overwriting exactly the evidence you're trying to preserve.
- **Locate and secure related media** — external drives, phones, sticky notes with passwords, and any other physical items that might hold relevant evidence or provide access to encrypted data.

### Write-Blocking

A **write blocker** is a hardware device or software mechanism that sits between a forensic examiner's workstation and the original evidence media, allowing **read** commands to pass through normally while physically or logically **blocking every write command** — guaranteeing that the act of examining or imaging the original evidence cannot, under any circumstances, alter it in any way.

**Why this is absolutely necessary, not merely cautious.** Most students initially assume that simply "being careful" while looking at a drive is sufficient — but modern filesystems, particularly NTFS, **automatically update metadata the instant a drive is mounted or accessed**, even without a single deliberate action by the examiner. Last-accessed timestamps update, filesystem journal entries are written, and in some cases, the operating system may even attempt automatic repairs of a filesystem it perceives as improperly unmounted. **Simply plugging original evidence media into an ordinary computer and opening File Explorer can measurably alter it** — precisely the kind of evidence-integrity failure that directly undermines the "Authentic" and "Reliable" standards from your Day 3 session.

**Types of write blockers:**
- **Hardware write blockers** — a dedicated physical device (well-known examples include Tableau and CRU forensic bridges) that the original drive connects through before reaching the examiner's workstation, intercepting write commands at the hardware/firmware level. This is generally considered the gold standard, since it operates independently of the examiner's own operating system and cannot be bypassed by an operating-system-level bug or misconfiguration.
- **Software write blockers** — write-blocking enforced at the operating system or driver level, often used within specialized forensic boot environments specifically designed to mount drives read-only by default.

### Disk Imaging — Raw/DD and E01

Once the original evidence is properly write-protected, the investigator creates a **forensic image** — an exact, bit-for-bit copy of the entire storage media — and performs all subsequent analysis on this copy, never the original, which is sealed and stored as the preserved master evidence.

**Raw / DD format.** Named after the Unix `dd` ("data dump") command traditionally used to create it, a raw image is simply an exact, unstructured, bit-for-bit copy of every byte on the source media, with no embedded metadata, no compression, and no built-in integrity verification.
- **Advantages:** universally compatible with virtually every forensic tool in existence, and conceptually the simplest possible format — what you see is genuinely, exactly what was on the disk.
- **Disadvantages:** the resulting image file is exactly the same size as the source media (no compression), carries no embedded case information or examiner notes, and — critically — provides **no built-in hash verification at all**, meaning the examiner must manually calculate and separately record hash values before and after imaging to prove integrity.

**E01 (Expert Witness Format).** Originally developed by Guidance Software for the EnCase forensic suite, E01 has become a de facto industry standard, now supported by a wide range of forensic tools well beyond EnCase itself (including FTK Imager and, via the open-source `libewf` library, Autopsy).
- **Built-in compression**, reducing the resulting image file's size compared to the source media.
- **Embedded metadata** — case number, examiner name, acquisition date and time, and free-text notes are stored directly within the image file itself, travelling with the evidence rather than existing only in a separate paper log.
- **Embedded, automatic hash verification** — this is the single biggest practical advantage over raw/DD. E01 acquisition tools calculate CRC32 checksums for individual data blocks **during** acquisition, and calculate an overall MD5 and/or SHA-1 (and often SHA-256) hash of the entire source **and** the resulting image automatically, then compare them and report a clear pass/fail verification result — turning what is a separate, manual, easy-to-forget step in raw/DD imaging into an integrated, automatic part of the E01 acquisition process itself.
- **Segmentation support** — a single large image can be automatically split into multiple smaller files (conventionally named with extensions like .E01, .E02, .E03...), useful for storage media limitations and easier transport.
- **Built-in error handling** — an E01 acquisition can continue past unreadable "bad" sectors on damaged source media, logging exactly which sectors failed, rather than the entire acquisition process failing outright.

**Other formats worth knowing:** **AFF (Advanced Forensic Format)**, an open-source alternative offering similar embedded-metadata and hashing benefits to E01, and **AD1**, a proprietary logical evidence format associated with AccessData's FTK product line, generally used for targeted collections of specific files rather than a full physical disk image.

### Non-Technical Analogies

> 🚧 **A Write Blocker as a One-Way Turnstile at a Museum Archive.** Imagine a museum's most precious archival documents can only be viewed through a special reading room turnstile that physically allows visitors to walk in and look, but has no mechanism whatsoever to let anyone carry anything back out through it, write on anything while inside, or leave any trace behind — no pens allowed, no photocopying, no notes taken directly on the documents. A write blocker enforces exactly this one-way relationship at the hardware level: the examiner can look at everything, but the original simply cannot be altered, no matter what the examiner does or doesn't intend.

> 📸 **Raw/DD vs. E01 as a Plain Photocopy vs. a Notarized, Sealed Photocopy.** A raw/DD image is like taking a perfect photocopy of an original document — genuinely identical content, but nothing on the copy itself proves it's identical; you'd need a separate, manually-kept record comparing the two. An E01 image is like a notarized photocopy, sealed in an envelope stamped with the exact date, the notary's name, a wax seal that would visibly break if anyone tampered with it afterward, and a certificate directly attached stating "this copy was verified against the original and found to be identical" — the proof of integrity travels with the document itself, rather than living separately in a notebook that could be lost or questioned on its own.

---

## Multi-Perspective Breakdown

**Attacker's POV:** Sophisticated attackers specifically design systems and malware to exploit first-responder behavior — booby-trapped shutdown scripts that wipe logs or trigger destructive routines during an orderly shutdown, "dead man's switch" logic that destroys data if power isn't cut in a specific sequence, or malware that specifically detects when a drive has been connected through a write blocker or forensic imaging tool and alters its own behavior in response, attempting to evade detection during the imaging process itself.

**Defender's / SOC Analyst's POV:** Most real-world "first responders" to an actual incident are SOC Analysts, not certified forensic examiners — meaning the procedures covered today are directly, immediately relevant to your own future on-the-job decisions, not abstract specialist knowledge. A SOC Analyst who understands exactly why not to casually browse a suspect machine, run a live antivirus scan on it, or perform an ordinary shutdown is protecting evidence value that a later, more specialized forensic examiner will depend on entirely.

**Auditor's / Forensic Investigator's POV:** Recall Module 9's control 5.28 (Collection of Evidence) once again — an auditor assessing an organization's genuine incident response and forensic readiness should specifically ask whether the organization actually has access to write-blocking hardware and validated imaging tools (whether owned internally or contracted through an external forensic vendor), since a documented evidence-collection procedure with no actual technical capability to execute it correctly is a procedure that exists only on paper.

---

## Real-World Case Study

**The Daubert Standard — Why Validated, Standardized Forensic Procedures Are a Legal Requirement, Not Just Best Practice**

**Background:** *Daubert v. Merrell Dow Pharmaceuticals, Inc.* (1993) is a landmark United States Supreme Court case that, while originating in a pharmaceutical liability dispute entirely unrelated to digital forensics, established the modern standard governing when expert and scientific testimony — including digital forensic evidence and testimony — is admissible in U.S. federal courts. The resulting **Daubert Standard** has become one of the most frequently cited legal frameworks in digital forensics training worldwide, because it directly explains *why* the specific procedures covered in today's session are not optional formalities.

**The Standard's Core Test:** Under Daubert, a trial judge acts as a "gatekeeper," assessing whether proposed expert or scientific evidence is sufficiently reliable to be presented to a jury at all, generally considering factors including: **(1)** whether the theory or technique can be and has been tested, **(2)** whether it has been subjected to peer review and publication, **(3)** its known or potential error rate, and **(4)** whether it has gained general acceptance within the relevant scientific or professional community.

**Direct Application to Today's Content:** Apply these four factors directly to write-blocking and hash-verified imaging. **Testability** — cryptographic hashing is a mathematically testable, reproducible process; anyone can independently recalculate a hash and verify the result. **Known error rate** — the collision probability of a properly implemented cryptographic hash algorithm like SHA-256 is understood and can be stated with mathematical precision, an extraordinarily low, well-characterized error rate. **General acceptance** — write-blocking and E01 hash-verified imaging are overwhelmingly standard, widely taught, and near-universally used across the digital forensics profession precisely because they have been validated and generally accepted over decades of practice. An investigator who instead used an ad-hoc, uncontrolled, unverified copying method — plugging original evidence directly into an ordinary computer with no write protection and no hash verification — would very plausibly fail this admissibility test entirely, regardless of how experienced or well-intentioned that investigator personally was.

**Key Lessons for Defenders & Investigators — connecting directly to today's content:** The Daubert Standard is the direct legal explanation for why this entire session's content exists as rigid, standardized procedure rather than flexible personal judgment. Write-blocking and E01's built-in hash verification are not merely "good practice recommendations" — they are the specific, concrete mechanisms that allow a forensic examiner's methodology to satisfy testability, known error rate, and general acceptance under exactly this kind of judicial scrutiny. For a future investigator or GRC professional, understanding Daubert (or its equivalent standard in your own jurisdiction) reframes today's technical procedures from "the correct way to do things" into "the specific standard your evidence must meet to be usable at all" — precisely the same connection Module 10 drew between technical ISMS controls and legal compliance requirements.

---

## Practical Labs — Forensic Imaging with Real Tools

### Lab A: Creating an E01 Forensic Image with FTK Imager

**Tool:** FTK Imager (free, industry-standard, downloadable directly from AccessData/Exterro).

**Objective:** Create a properly hash-verified E01 forensic image of a small USB drive or virtual disk, directly experiencing E01's built-in integrity verification workflow.

**A note on write-blocking for this lab:** A real hardware write blocker is unlikely to be available in a classroom setting. For today's exercise, use a **USB drive with its physical write-protect switch enabled** if available, or simulate the concept by setting your USB port to read-only via your operating system (on Windows, this can be done via the `WriteProtect` registry value under `StorageDevicePolicies`; document this step explicitly in your lab notes as your "simulated write-blocking" measure, and discuss with your pair why a real forensic engagement would use dedicated hardware instead).

**Step-by-Step Execution Guide:**

1. Install and open FTK Imager. Select **File → Create Disk Image**.

2. Choose **Physical Drive** (or **Logical Drive** if imaging a specific partition rather than an entire device) as your source, and select your write-protected USB drive from the list.

3. Add a destination image type of **E01**, and complete the case information fields — Case Number, Evidence Number, Examiner name, and Notes — directly experiencing E01's embedded metadata capability described in today's theory section.

4. Set a destination folder and image filename, and begin the imaging process.

5. Ensure **"Verify images after they are created"** is checked before starting — this triggers FTK Imager's automatic hash calculation and verification step.

6. Once complete, review FTK Imager's verification report. Record the reported **MD5** and **SHA-1** hash values for both the source and the resulting image, and confirm the tool reports them as matching.

**Expected Artifacts & Evidence:**

```
FTK IMAGER — E01 ACQUISITION LOG

Source Device:            ...
Simulated Write-Protection Method Used: ...
Case Number / Examiner:   ...
Image Format:             E01
Source MD5:                ...
Image MD5:                 ...
Source SHA-1:               ...
Image SHA-1:                 ...
Verification Result:      [Match / Mismatch]
```

### Lab B: Raw/DD Imaging and Manual Hash Verification

**Tool:** `dd` (Linux/macOS) or a raw-imaging equivalent, plus `sha256sum`/`certutil` from your Day 3 session.

**Objective:** Create a raw image of the same or a similar small storage device, and manually perform the hash verification steps that E01 handles automatically — directly experiencing the practical difference between the two formats.

**Step-by-Step Execution Guide:**

1. **Before imaging**, calculate the SHA-256 hash of the source device directly:
   ```
   sha256sum /dev/sdX
   ```
   (Replace `/dev/sdX` with your actual, carefully-confirmed source device identifier — double-check this extremely carefully, since `dd` and hashing commands operate directly on raw devices with no undo.)

2. Create the raw image using `dd`:
   ```
   dd if=/dev/sdX of=evidence_image.dd bs=4M status=progress
   ```

3. **After imaging**, calculate the SHA-256 hash of the resulting image file:
   ```
   sha256sum evidence_image.dd
   ```

4. **Manually compare** the two hash values from Steps 1 and 3 — this manual comparison step is precisely the work that E01's built-in verification in Lab A performed automatically for you.

5. In your lab notes, write two to three sentences comparing your experience across both labs: which format required more manual, error-prone steps to achieve the same integrity assurance, and which embedded that assurance directly into the acquisition process itself?

**Expected Artifacts & Evidence:**

```
RAW/DD ACQUISITION LOG

Source Device:              ...
Pre-Imaging SHA-256:         ...
Image Filename:              evidence_image.dd
Post-Imaging SHA-256:         ...
Manual Verification Result: [Match / Mismatch]

COMPARISON NOTE (Raw/DD vs. E01):
...
```

**Class Debrief (10 min):** Both pairs present their FTK Imager verification report and their manual `dd` hash comparison. The instructor will specifically ask which format they would choose for a real, time-pressured investigation and why — reinforcing that E01's automated verification isn't just a convenience, but a genuine reduction in the risk of human error in an evidentiary process that the Daubert Standard demands be reliable.

---

## Mini-Project / Take-Home Challenge

**Challenge: Write a First Responder Quick-Reference Card**

Using everything from today's session, create a one-page "First Responder Quick-Reference Card" — a genuinely usable, concise checklist a non-specialist SOC Analyst could keep at their desk and follow correctly under real pressure during their very first minutes at a suspected incident. It must cover: scene security, the powered-on vs. powered-off decision branch, what never to do to the suspect device, and when (and how) it becomes appropriate to power the device down.

**Deliverable format:** A single-page reference card (any reasonable format), submitted before the next session. Be ready to present your findings — expect all four students to share.

---

## Discussion Questions & Knowledge Check

Run this as an open round-table — every student answers each question before moving to the next.

1. Explain, in your own words, why simply plugging original evidence media into an ordinary computer — even without deliberately opening or editing anything — can still alter it, and why this makes write-blocking mandatory rather than merely advisable.

2. Using today's session, explain the specific nuance in the "should I pull the plug?" question — why is the correct answer different depending on whether volatile evidence capture has already been completed?

3. Apply the Daubert Standard's four factors (testability, peer review, error rate, general acceptance) to a hypothetical investigator who instead relied on personally copying files by hand, one at a time, with no hashing at all. Which specific factor(s) would this approach most clearly fail?

4. Comparing your two labs today, describe one specific scenario where you would deliberately choose Raw/DD over E01 despite E01's built-in verification advantages, if any such scenario exists.

5. A first responder is a SOC Analyst, not a certified forensic examiner. Using today's content, explain why understanding these procedures is still directly relevant to that SOC Analyst's job, even if a specialist forensic examiner will ultimately take over the formal investigation.
