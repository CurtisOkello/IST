# Memory Dump Acquisition & the Volatility Framework
**Module:** Module 11 — Cyber Forensics | **Unit:** Unit 3 — Computer Forensics

---

## Session Objectives & Real-World Context

**What You Will Learn:**
- Why RAM capture is one of the single highest-value forensic activities in modern incident response — what specifically lives in memory that cannot be found anywhere on disk, including in-memory encryption keys, fileless malware, and injected code.
- The practical tools used to actually acquire a forensically sound memory image, and the specific precautions that distinguish a proper memory acquisition from simply "copying a file."
- The **Volatility Framework** — the industry-standard open-source memory forensics tool — including its core plugins for extracting processes, network connections, and hidden or injected malicious code from a raw memory dump.
- A direct, powerful connection back to Module 8's rootkit content: how Volatility's **`pslist`** vs. **`psscan`** plugins apply the exact same "compare two enumeration methods to reveal a hidden process" principle you learned with GMER, now applied specifically to memory forensics.
- Real, hands-on experience acquiring memory from a live system and analyzing it with Volatility, extracting genuine forensic artifacts yourself rather than reading about them in the abstract.

**Why It Matters to a Security Professional:** Every session so far in this unit has built toward this moment — you now understand *why* volatile evidence matters (Day 4), *how* to properly handle and image evidence (Day 5), and today you finally get your hands on the single richest, most information-dense evidence source available in a live incident: RAM itself. A skilled memory forensics analyst can often reconstruct almost the entire story of an intrusion — what ran, what it connected to, what it hid, and what it stole — from a single memory image, even when the attacker was sophisticated enough to leave almost nothing behind on disk.

---

## Core Theory & Technical Mechanics

### Why Memory Acquisition Matters So Much

RAM contains an extraordinary density of forensically valuable information that simply does not exist anywhere else, including:

- **Running processes and their full command-line arguments** — showing exactly what was executed and with what parameters, even for a process that has since terminated on disk but whose memory hasn't yet been overwritten.
- **Active network connections**, including connections that may have already closed by the time a disk-based investigation begins.
- **Encryption keys held only in memory** — a full-disk-encrypted volume, or an encrypted communication channel, may be completely unreadable from a disk image alone, but the decryption key actively in use is very often sitting in plaintext in RAM while the system is running, exactly the principle behind the Ross Ulbricht case from your Day 4 session.
- **Fileless malware and injected code** — recall Module 8's Living-off-the-Land content in depth: malware that never writes a file to disk leaves **no trace whatsoever** in a disk image, but it must, by definition, exist in memory while it's actually running. Memory forensics is very often the *only* way to detect and analyze this entire category of threat.
- **Clipboard contents, recently typed commands, and decrypted data** a user or attacker was actively working with at the moment of capture.

### Acquiring Memory — Tools and Precautions

Several dedicated tools exist specifically for forensically sound memory acquisition, including **FTK Imager's built-in "Capture Memory" feature**, **Magnet RAM Capture**, **WinPmem** and **DumpIt** (lightweight, portable Windows memory acquisition utilities), and **LiME (Linux Memory Extractor)** for Linux systems.

**Key precautions for memory acquisition, directly extending Day 5's imaging principles:**
- **Use a minimal-footprint tool.** The very act of running an acquisition tool consumes some memory and CPU time on the target system — a genuinely unavoidable, small self-interference effect, but one minimized by choosing lightweight, purpose-built tools rather than a heavy, general-purpose application.
- **Acquire memory before any other invasive action**, directly following the Order of Volatility priority from Day 4 — memory capture should happen as early as possible in the response process.
- **Hash the resulting memory image immediately upon completion**, exactly as with a disk image in Day 5 — a memory dump is still digital evidence, and it still requires the same chain-of-custody rigor.
- **Don't overlook related files on disk that may contain memory-resident data even after a reboot.** Windows' `pagefile.sys` (virtual memory swap file) and `hiberfil.sys` (hibernation file, which stores a full memory snapshot when a system hibernates rather than fully powering off) can both contain valuable memory-resident artifacts and should be collected as part of a thorough disk acquisition alongside the live memory capture itself.

### The Volatility Framework

**Volatility** is the leading open-source memory forensics framework, used to analyze a raw memory dump and extract structured, meaningful forensic artifacts from what would otherwise be an enormous, unstructured blob of raw bytes. The framework has evolved across two major versions: **Volatility 2** (Python 2-based, requiring the analyst to specify an exact OS "profile" matching the source system's build so the tool knows how to correctly interpret memory structures) and **Volatility 3** (a modern, Python 3-based rewrite with substantially improved automatic operating system detection via symbol tables, removing much of the manual profile-matching friction that made Volatility 2 more cumbersome to use correctly).

**Core Volatility plugins you will use directly in today's lab:**

- **`pslist`** — lists running processes by walking the operating system's own internal linked list of active process objects (the `EPROCESS` structure on Windows). This is fast and reliable for ordinary processes, but has a critical weakness described below.
- **`psscan`** — scans the entire memory image for process object *signatures* directly, independent of whether that process is properly linked into the operating system's own process list. This is the plugin's entire reason for existing: a sophisticated rootkit or malware family can use a technique called **DKOM (Direct Kernel Object Manipulation)** to *unlink* its own process from the list `pslist` reads, making it completely invisible to that plugin — but the process object itself still physically exists in memory, and `psscan`'s direct signature-based scan will still find it.
- **`netscan`** — extracts network connection artifacts directly from memory, including connections that may have already closed and would no longer appear in a live `netstat` command by the time an investigator gets to the system.
- **`malfind`** — specifically searches for memory regions showing signs of code injection or process hollowing (a technique where malware hides its code inside the memory space of a legitimate, trusted process), one of the most directly malware-hunting-oriented plugins in the framework.
- **`cmdline`** — extracts the full command-line arguments used to launch each identified process, directly extending the process list with exactly the kind of detail Sysmon Event ID 1 captures live, but recoverable here after the fact from a memory snapshot.
- **`hashdump`** — extracts password hash material present in memory, directly relevant to detecting credential-dumping activity (recall Module 8's Sysmon Event ID 10 / `lsass.exe` content — `hashdump` is, in effect, the after-the-fact forensic confirmation of exactly the live attack that Event ID 10 monitoring is designed to catch in real time).

> **Key Term — Why `pslist` vs. `psscan` is one of the most important lessons in this entire session.** This is the *exact same underlying principle* as the GMER rootkit detection technique from Module 8's Day 8 session — comparing two different enumeration methods and treating any discrepancy between them as a high-confidence signal of concealment. A process appearing in `psscan` but **not** in `pslist` is one of the single strongest, most reliable indicators of active rootkit or DKOM-based concealment an investigator can find, and recognizing this pattern immediately — rather than needing to be told what it means each time — is exactly the kind of pattern-recognition fluency this entire diploma has been building toward.

### Non-Technical Analogies

> 🧠 **Memory as a Chef's Active Kitchen Counter vs. the Pantry.** A disk image is like inspecting a restaurant's sealed pantry after hours — you can see every ingredient that's stored there, but you have no idea what the chef was actually cooking an hour ago, what was mixed together, or what's simmering right now that hasn't been written down in any recipe book. Memory is the chef's actual, active counter and stovetop, captured mid-service — showing exactly what's cooking right now, in what combination, even dishes that will never appear in any written recipe at all (fileless malware) because they only ever existed as an in-progress, temporary combination on that counter.

> 🕵️ **`pslist` vs. `psscan` as a Guest List vs. Physically Counting Heads in the Room.** `pslist` is like checking the venue's official guest list at the door — fast, easy, and accurate for every legitimate attendee who checked in properly. `psscan` is like physically walking through the entire room and counting every actual person present, regardless of whether they checked in. If your headcount from walking the room turns up someone who was never on the official guest list at all, you've just found someone who deliberately avoided being recorded — exactly the DKOM concealment technique `psscan` is specifically built to catch.

---

## Multi-Perspective Breakdown

**Attacker's POV:** Sophisticated malware authors specifically design anti-memory-forensics techniques — DKOM to unlink processes from `pslist`-visible structures, process hollowing and code injection specifically to hide malicious code inside the memory space of a legitimate, trusted process (exactly what `malfind` hunts for), and in some advanced cases, detecting the presence of memory acquisition tools themselves and altering behavior in response, mirroring the anti-VM/anti-sandbox evasion techniques from Module 8's Day 1 session applied specifically to the memory-analysis context.

**Defender's / SOC Analyst's POV:** A mature incident response capability has memory acquisition tools tested, validated, and ready to deploy *before* an incident occurs — attempting to research, download, and learn a memory acquisition tool for the first time during an active, time-pressured incident is a genuinely serious operational risk. Recall Module 10's CERT-In 6-hour reporting window content — an organization with pre-validated memory acquisition capability can move dramatically faster toward a confident understanding of an incident's scope than one starting from zero.

**Auditor's / Forensic Investigator's POV:** Memory analysis represents the practical heart of the "Analysis" phase from your Day 4 forensic methodology session — this is where an investigator moves from simply *having* evidence to genuinely *understanding* what happened. A `pslist`/`psscan` discrepancy discovered during analysis is exactly the kind of specific, evidence-based finding that satisfies the factual, evidenced standard for a forensic report's Presentation phase, directly echoing the audit-finding rigor from Module 9's Day 4.

---

## Real-World Case Study

**Stuxnet (2010) — Why Surface-Level Inspection Was Never Going to Be Enough**

**Incident Summary:** Stuxnet, discovered in 2010, remains one of the most sophisticated pieces of malware ever publicly documented — a highly targeted worm specifically designed to sabotage the industrial control systems (specifically, uranium enrichment centrifuges) at Iran's Natanz nuclear facility, widely reported to have been developed by state-level actors.

**Why Deep Forensic Analysis, Not Surface Inspection, Was Required:** Stuxnet employed extraordinarily sophisticated concealment techniques directly relevant to today's session. Its device drivers were digitally signed using **genuinely stolen legitimate code-signing certificates** from real hardware manufacturers, allowing the malware's kernel-level components to appear entirely trustworthy to any surface-level check of digital signatures — a form of "hiding in plain sight" conceptually similar to a process that appears completely normal in a shallow inspection but is exposed the moment a deeper, signature-based scan (exactly like `psscan`'s approach) is applied instead of trusting the operating system's own reporting. Unraveling Stuxnet's full behavior — its multi-stage payload, its extremely specific targeting logic checking for particular industrial equipment configurations before activating, and its self-propagation mechanisms exploiting multiple then-unknown (zero-day) vulnerabilities — required extensive deep technical and behavioral analysis by multiple security research teams over an extended period, far beyond what any surface-level or purely disk-based inspection could have revealed.

**Legal and Geopolitical Impact:** Stuxnet is widely credited with causing significant physical damage to Iran's uranium enrichment capability and remains one of the most consequential and most thoroughly studied examples of a cyberweapon causing real-world physical effects, fundamentally reshaping global discussion of cyber warfare and critical infrastructure security in the years that followed.

**Key Lessons for Defenders & Investigators — connecting directly to today's content:** Stuxnet is the clearest large-scale illustration of exactly the principle at the heart of today's `pslist`/`psscan` lesson: **a sufficiently sophisticated adversary will make their malicious activity look entirely legitimate to any inspection method that trusts the system's own self-reporting.** Stolen certificates fooled signature checks exactly the way DKOM fools `pslist`; in both cases, the defense is the same — apply an independent, deeper verification method that doesn't rely on the compromised system, or the compromised trust mechanism, telling you the truth about itself. For a future forensic investigator, Stuxnet is a permanent reminder that the most dangerous threats are rarely the ones that look obviously malicious — they are the ones specifically engineered to look completely normal to whatever check you were planning to rely on.

---

## Practical Labs — Memory Acquisition and Volatility Analysis

### Lab A: Acquiring a Live Memory Image

**Tool:** Magnet RAM Capture or FTK Imager's built-in "Capture Memory" feature (both free).

**Objective:** Capture a forensically sound memory image of your own lab machine, applying the same chain-of-custody discipline from Day 5's disk imaging lab.

**Step-by-Step Execution Guide:**

1. Before capturing, open a few ordinary applications and a couple of browser tabs on your lab machine — this ensures your memory capture will contain genuinely varied, analyzable content for Lab B.

2. Open your chosen memory acquisition tool and select an appropriate destination for the resulting memory image (ideally a separate drive, not the same disk being captured, following the same principle as Day 5's imaging destination practice).

3. Begin the capture. Note the tool's reported progress and completion time — memory capture is generally much faster than full disk imaging, but still takes real, measurable time proportional to the amount of installed RAM.

4. Once complete, immediately calculate the SHA-256 hash of the resulting memory image file, exactly as practiced in Day 5:
   ```
   certutil -hashfile memory_capture.mem SHA256
   ```
   or
   ```
   sha256sum memory_capture.mem
   ```

5. Record this acquisition in a short Chain of Custody entry, exactly matching the format from your Day 3 and Day 5 sessions.

**Expected Artifacts & Evidence:**

```
MEMORY ACQUISITION LOG

Tool Used:                 ...
Destination File:           memory_capture.mem
Capture Start/End Time:    ...
SHA-256 Hash:               ...
Applications Open During Capture: ...
```

### Lab B: Analyzing the Memory Image with Volatility

**Tool:** Volatility 3 (install via `pip install volatility3`, or use a pre-configured forensic environment if available).

**Objective:** Run core Volatility plugins against your captured memory image (or, for a more illustrative malicious-artifact demonstration, a publicly available known-infected sample memory image if your instructor has provided one) to extract processes, network connections, and check specifically for the `pslist`/`psscan` discrepancy described in today's theory section.

**Step-by-Step Execution Guide:**

1. Run the process list plugin against your captured image:
   ```
   vol -f memory_capture.mem windows.pslist
   ```

2. Run the process scan plugin on the same image:
   ```
   vol -f memory_capture.mem windows.psscan
   ```

3. **Compare the two outputs carefully.** On a clean lab machine, you should expect these lists to match closely — record this as your baseline finding. (If your instructor has provided a known-infected sample memory image specifically for this exercise, repeat this comparison against that sample instead, and look specifically for any process present in `psscan` output but absent from `pslist` output.)

4. Run the network connection scan:
   ```
   vol -f memory_capture.mem windows.netscan
   ```
   Compare this output against your own recollection of which applications and browser tabs you had open during Lab A's capture — can you identify the specific connections corresponding to your own browsing activity?

5. Run the injected-code detection plugin:
   ```
   vol -f memory_capture.mem windows.malfind
   ```
   Record whether any results are returned. On a clean personal lab machine, you would generally expect few or no findings here — discuss with your pair what a genuine `malfind` hit would actually look like and why it matters.

**Expected Artifacts & Evidence:**

```
VOLATILITY ANALYSIS LOG

Image Analyzed:            ...
pslist process count:       ...
psscan process count:       ...
Discrepancy found? [Y/N] — Details: ...
netscan notable connections identified: ...
malfind findings: [None / Details] ...

CONCLUSION: [Brief plain-language summary of what this memory image reveals about the system's
state at the moment of capture]
```

**Class Debrief (10 min):** Both pairs present their `pslist`/`psscan` comparison and `netscan` findings. The instructor will specifically connect any observed discrepancy (or the clean baseline, if none was found) directly back to Module 8's GMER rootkit detection content, reinforcing that this is the same underlying investigative principle applied in a new technical context.

---

## Mini-Project / Take-Home Challenge

**Challenge: Document a Volatility Plugin You Didn't Use in Class**

Research one Volatility plugin not covered in today's lab (options include `windows.filescan`, `windows.registry.hivelist`, `windows.dlllist`, or another of your choosing). Write a short report covering: what forensic artifact this plugin extracts, one realistic investigative scenario where it would be specifically valuable, and how you believe it connects to a concept from an earlier session in this diploma.

**Deliverable format:** A short written report (150–250 words), submitted before the next session. Be ready to present your findings — expect all four students to share.

---

## Discussion Questions & Knowledge Check

Run this as an open round-table — every student answers each question before moving to the next.

1. Explain, in your own words, why a `pslist`/`psscan` discrepancy is considered such a high-confidence indicator of compromise, connecting your answer directly to Module 8's GMER content.

2. Using the Stuxnet case, explain why relying purely on a system's own digital signature verification — without any deeper, independent analysis — would have been insufficient to detect this specific threat.

3. Fileless malware, covered extensively in Module 8, leaves no trace on disk. Using today's content, explain specifically why memory acquisition is not merely useful but often the *only* viable method for detecting this entire malware category at all.

4. A memory acquisition tool itself consumes some system memory and processing time while running. Does this self-interference effect undermine the value of memory forensics as evidence? Using today's Daubert Standard content from your previous session, explain how you would defend memory forensics against this specific challenge.

5. If you had only enough time during a live incident to run one single Volatility plugin before needing to move on to other response priorities, which of today's five plugins would you choose, and why?
