# Cyber Threat Intelligence Lifecycle — A Narrative Walkthrough

Cyber Threat Intelligence (CTI) follows a six-phase intelligence lifecycle that transforms raw data into contextualised and action-oriented insights geared towards triaging security incidents.  
This walkthrough follows **Alex**, a SOC Level 1 analyst, as they apply CTI to protect **TryHatMe’s production PostgreSQL database**.

---

## 📌 The CTI Lifecycle Loop

Before diving into the phases, it’s important to understand two core concepts:

### Traffic Light Protocol (TLP) — Sharing Guidance

TLP is a four-colour scheme (FIRST.org) that governs how widely intel may be shared:

| TLP Label  | Sharing Boundary                                  | Typical SOC L1 Behaviour |
|------------|---------------------------------------------------|---------------------------|
| **TLP: CLEAR** | No restriction | Post to internal wiki/platform. |
| **TLP: GREEN** | Peer community, but not public | Upload to MISP/Slack with partner SOCs. |
| **TLP: AMBER** | Org-wide, external only with need-to-know | Keep in CTI platform; reference in tickets. |
| **TLP: RED**   | Named recipients only | Store in encrypted note; never post without clearance. |

⚠️ **Key Point:** An IOC’s TLP label must travel with it across all platforms and tickets to avoid breaches of trust or contracts.

---

### Intel Formats

Threat intel comes in various formats. One widely adopted standard is **STIX (Structured Threat Information Expression)**, a JSON schema for describing indicators, relationships, and context in a machine-readable way.

---

## 🔐 Scenario: TryHatMe Corp

- **Primary Asset**: PostgreSQL production database  
- **Business Risk**: GDPR fines, loss of customer trust  
- **Controls**: NGFW (IP/domain blocking), EDR (file hash quarantine)  
- **CTI Goal**: Ingest threat feeds to block suspicious IPs/domains and detect malicious file hashes

---

# 🌀 The Six Phases

## 1. Direction — Defining the Mission
Alex translates management’s mandate into actionable questions:

- **Q1:** Which IPs/domains are used to exploit PostgreSQL or exfiltrate records?  
- **Q2:** Which malware families targeting PostgreSQL credentials are active this week, and what are their hashes?

---

## 2. Collection — Assembling Raw Intel
Alex gathers intel from four sources:

| Source | Why Chosen | Example Artefacts |
|--------|------------|-------------------|
| NGFW vendor feed | Tailored, high-fidelity | 37 IPs flagged as PgSQL exfil C2 |
| AbuseIPDB (tag: PostgreSQL-brute-force) | Fast, community-driven | 15 IPs, 4 domains |
| Internal MISP | Historical incidents | 2 SHA-256 hashes of credential stealers |
| Vendor threat report | Strategic insight | 1 new hash, 3 C2 domains |

All intel is stored in STIX/CSV format inside the SOC’s **“raw-intel” S3 bucket** for reproducibility.

---

## 3. Processing — Normalising and Correlating
Alex runs Python scripts to:

- **Normalise** (lowercase domains, compress IPv6, strip subnet masks).  
- **Correlate** with existing indicators (deduplicate, tag with source/date/TLP).  
- **Output action files**:  
  - `firewall_blocklist.csv` (indicator, action, comments)  
  - `edr_hash_rules.yar` (YARA hash rules for EDR)  

⚠️ Collision spotted:  
- NGFW feed labels IP as **TLP: AMBER**.  
- AbuseIPDB labels same IP as **TLP: CLEAR**.  
- **Resolution:** Stricter label wins → TLP: AMBER.

---

## 4. Analysis — From Information to Judgement
Alex validates indicators:

- **Firewall indicators (Q1):**  
  Splunk logs show an NGFW IP attempted TCP 5432 → ✅ applicable.
- **Hash indicators (Q2):**  
  Hash linked to **PgSteal malware family** (via OpenCTI). Sandbox analysis confirms credential theft.  
  Since TryHatMe uses the vulnerable ODBC driver, marked **high priority**.

### Confidence Grading
| Confidence | Source Agreement | Local Sightings | Action |
|------------|------------------|-----------------|--------|
| **High** | ≥2 sources | ≥1 local hit | Block immediately |
| **Medium** | Trusted source only | No local hits | Alert-only |
| **Low** | OSINT only | No context | Monitor for 14 days |

**Result:** 7 IPs + 1 hash = **High confidence**. Others → medium/monitoring.

---

## 5. Dissemination — Delivering to Stakeholders
Alex tailors output by audience:

| Stakeholder | Format | Why |
|-------------|--------|-----|
| Firewall team | CSV + change-ticket | They manage block rules |
| Endpoint team | YARA rules in EDR | Deploy hash-based detections |
| CTI platform | Full tagged indicators | Preserve history + TLP |
| Management | 200-word memo | ROI + risk posture summary |

---

## 6. Feedback — Closing the Loop
After 2 weeks:

| KPI | Baseline | After Cycle |
|-----|-----------|-------------|
| Median dwell time of brute-force IPs | 48h | **0h** (pre-emptive block) |
| False positives | N/A | **0%** |

✅ **Outcome:** Success. Management approves next phase → expand to **DNS tunnelling IOCs**.

---

# 🔄 Continuous Improvement
CTI is cyclical:  
**Direction → Collection → Processing → Analysis → Dissemination → Feedback → Direction (again).**

Alex closes the loop and schedules the next sprint.

---
