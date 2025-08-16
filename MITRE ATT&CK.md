# MITRE & Threat-Informed Defense — One-Pager (Markdown)

> “At MITRE, we solve problems for a safer world. Through our federally funded R&D centers and public-private partnerships, we work across government to tackle challenges to the safety, stability, and well-being of our nation.” — *mitre.org*

MITRE is a US-based, non-profit R&D organization. Many practitioners first meet MITRE via the CVE list, but its impact on cybersecurity goes far beyond that—spanning frameworks, knowledge bases, and community research that help defenders understand, detect, and disrupt adversaries.

---

## Table of Contents

1. [Key Terms (APT & TTPs)](#key-terms-apt--ttps)  
2. [MITRE ATT&CK® Framework](#mitre-attck-framework)  
3. [MITRE CAR (Cyber Analytics Repository)](#mitre-car-cyber-analytics-repository)  
4. [MITRE Engage (Adversary Engagement)](#mitre-engage-adversary-engagement)  
5. [CTID — Center for Threat-Informed Defense](#ctid--center-for-threatinformed-defense)  
6. [ATT&CK® Adversary Emulation Plans (AEP)](#attck-adversary-emulation-plans-aep)  
7. [Putting It All Together: A Practical Workflow](#putting-it-all-together-a-practical-workflow)  
8. [Further Study & Notes](#further-study--notes)

---

## Key Terms (APT & TTPs)

**APT (Advanced Persistent Threat)**  
An APT is a threat group (often nation-state or well-resourced) that conducts long-term, goal-driven campaigns against organizations and/or countries. “Advanced” doesn’t always mean exotic zero-days—many APTs rely on common, well-documented techniques that can be detected and mitigated with sound defenses. (Security vendors like Mandiant/FireEye maintain public write-ups on many APT groups.)

**TTPs (Tactics, Techniques, and Procedures)**

- **Tactic** → the adversary’s *objective* (the “why”).  
- **Technique** → the general *method* to achieve that objective (the “how”).  
- **Procedure** → the specific *implementation* details (the “exactly how this time”).

You’ll see these terms everywhere in threat intel and ATT&CK. As you work through this doc, the distinctions become intuitive.

---

## MITRE ATT&CK® Framework

**What it is.**  
ATT&CK is a globally used, *behavior-centric* knowledge base cataloging how adversaries operate after initial access. It describes TTPs across real-world observations.

**Key pieces you’ll use:**

- **Matrices:** Enterprise, Mobile, and ICS, organized by **tactics** (columns) and **techniques/sub-techniques** (cells).  
- **Groups/Software:** Mappings between named threat groups, the tools/malware they use, and the techniques they’re known for.  
- **Detections & Mitigations:** Per-technique guidance for telemetry, analytics ideas, and defensive controls.  
- **Data Sources & Components:** What to collect (e.g., process creation, command line, registry, network flows) to enable detection.

**Why it matters.**

- **For Blue Teams:** Map detections to techniques, see gaps, plan telemetry and controls, prioritize engineering work.  
- **For Red/Purple Teams:** Plan realistic emulations, validate controls, and generate evidence to drive improvements.  
- **For Leadership:** Turn vague “Are we covered?” questions into measurable coverage and roadmap items.

**Pro tip:** Use the matrix to translate incidents and intel into shared language: “This campaign used *T1059.001 PowerShell* and *T1021.001 SMB lateral movement*—we cover one, we’re missing the other.”

---

## MITRE CAR (Cyber Analytics Repository)

> **Official definition:** “The MITRE Cyber Analytics Repository (CAR) is a knowledge base of analytics developed by MITRE based on the MITRE ATT&CK® adversary model. CAR defines a data model that is leveraged in its pseudocode representations but also includes implementations directly targeted at specific tools (e.g., Splunk, EQL) in its analytics. With respect to coverage, CAR is focused on providing a set of validated and well-explained analytics, in particular with regards to their operating theory and rationale.”

**What this means for you.**

- **Analytics you can reason about:** Each entry explains *why* the analytic should work (operating theory), potential blind spots, and needed data.  
- **From concept to implementation:** You get pseudocode plus example queries for specific tools (e.g., Splunk, EQL), helping you move faster from idea → dashboard/alert.  
- **Ties to ATT&CK:** CAR analytics map to ATT&CK techniques, letting you trace coverage and justify priorities.

**How to use CAR effectively.**

1. Start with a technique you care about (from ATT&CK).  
2. Pull the corresponding CAR analytic(s).  
3. Check data prerequisites (e.g., command-line logging, PowerShell logs, Sysmon, EDR events).  
4. Tailor the sample queries to your environment.  
5. Record assumptions, tune, and document known evasion paths.

---

## MITRE Engage (Adversary Engagement)

> **Per the website:** “MITRE Engage is a framework for planning and discussing adversary engagement operations that empowers you to engage your adversaries and achieve your cybersecurity goals.”

Engage operationalizes **Adversary Engagement** using two complementary pillars:

- **Cyber Denial** — Prevent or constrain an adversary’s ability to operate (e.g., frustrate recon, access, or lateral movement).  
- **Cyber Deception** — Intentionally plant artifacts (accounts, files, hosts, telemetry) to mislead, measure, and learn from the adversary.

**Why defenders care.**

- Moves you from purely reactive blocking to **shaping** the fight: buying time, gathering intel, and forcing attacker inefficiency.  
- Comes with a **Starter Kit** (whitepapers, checklists, processes) to stand up safe, ethical, and legally sound engagement.

**Practical examples (high-level):**

- Honey credentials/tokens, decoy file shares, instrumented canary services, deceptive network topologies.  
- Playbooks that define objectives, measures of success, escalation paths, and teardown criteria.

---

## CTID — Center for Threat-Informed Defense

MITRE formed the **Center for Threat-Informed Defense (CTID)**, a collaborative R&D initiative with participants from across industry. Its objective: research adversary TTPs and publish open, practical outputs that improve defense for everyone.

**Examples of participant organizations** (as noted): *AttackIQ (founder), Microsoft (founder), Red Canary (founder), Verizon, Splunk*, among others.

> **Mission (in their words):** “Together with Participant organizations, we cultivate solutions for a safer world and advance threat-informed defense with open-source software, methodologies, and frameworks. By expanding upon the MITRE ATT&CK knowledge base, our work expands the global understanding of cyber adversaries and their tradecraft with the public release of data sets critical to better understanding adversarial behavior and their movements.”

**What you get:** open-source tools, methods, datasets, mappings, and guidance that plug directly into ATT&CK-driven programs.

---

## ATT&CK® Adversary Emulation Plans (AEP)

The **Adversary Emulation Library** publishes step-by-step emulation plans contributed via CTID so blue/red/purple teams can test defenses against realistic tradecraft—safely and repeatably.

**Currently available exemplars include:** **APT3**, **APT29**, and **FIN6**.

**What’s inside an AEP (at a glance):**

- **Scope & Objectives:** What parts of the kill chain/ATT&CK it exercises.  
- **Environment & Safety Notes:** How to run safely in a lab.  
- **Ordered Steps:** Discrete actions that mimic the group’s behaviors.  
- **Mappings & Expected Signals:** Which techniques are exercised and what telemetry should appear.

**Why it’s useful:** If leadership asks, “How would we fare against APT29?”, you can run the AEP, collect evidence, and respond with concrete findings tied to ATT&CK techniques and CAR-style detections.

> ⚠️ **Safety & ethics:** Keep emulations in controlled environments. Avoid running intrusive actions on production systems unless you have formal approvals, guardrails, and rollback plans.

---

## Putting It All Together: A Practical Workflow

1. **Define the Threats (Intel → ATT&CK).**  
   Convert reports into ATT&CK techniques/sub-techniques; note tools and procedures.

2. **Assess Coverage (ATT&CK → Controls & Telemetry).**  
   Use the matrix to check which techniques you can currently *detect* or *prevent*. Document gaps.

3. **Engineer Detections (CAR).**  
   Pull CAR analytics for priority techniques, validate data sources, implement/tune queries in your SIEM/EDR.

4. **Shape the Fight (Engage).**  
   Add targeted denial/deception to frustrate high-risk techniques and generate high-fidelity early-warning signals.

5. **Prove It (AEP).**  
   Run relevant emulation plans (e.g., APT29) in a lab or tightly controlled production exercises; gather evidence.

6. **Report & Iterate.**  
   Communicate results in business terms (risk reduced, MTTD/MTTR improvements, residual gaps) and feed lessons back into steps 1–5.

**Mini example (conceptual):**

- Threat intel highlights **PowerShell-based execution** and **credential dumping**.  
- Map to ATT&CK: *T1059.001 (PowerShell)*, *T1003.* (OS Credential Dumping).  
- From CAR, implement/tune analytics for suspicious PowerShell usage and LSASS access attempts.  
- Deploy Engage deception: plant decoy credentials; monitor for use.  
- Exercise an AEP step that triggers these behaviors; verify alerts and incident flow.

---

## Further Study & Notes

- **ATT&CK Navigator:** A handy way to visualize technique coverage and roadmap.  
- **Data source hygiene:** Great analytics die without the right telemetry—ensure logging is robust, centralized, and retained.  
- **Metrics that matter:** Tie work to outcomes (e.g., earlier detection at Initial Access/Execution, fewer high-impact incidents).  
- **Legal & privacy:** Deception and engagement must follow applicable laws, policies, and ethical guidelines.
