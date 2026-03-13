# Phase 2: Regulation Knowledge Base - Research

**Researched:** 2026-03-13
**Domain:** Privacy regulation static knowledge base files, SKILL.md routing extension, cross-reference comparison architecture
**Confidence:** HIGH

## Summary

Phase 2 creates 8 new markdown reference files -- 6 individual regulation quick-reference files (GDPR, CCPA/CPRA, COPPA, HIPAA, FERPA, EU AI Act), 1 cross-reference comparison file, and 1 regulatory timeline file -- plus updates SKILL.md routing to auto-detect regulation queries and load the appropriate files. This phase builds on the proven progressive disclosure architecture from Phase 1 (reference files loaded on-demand by SKILL.md) and extends it with regulation-specific routing logic.

The content depth is "practitioner reference level" -- enough detail for a practicing privacy professional to recall or verify specifics about any major provision, but not full statute text. Each regulation file includes key provisions, individual rights, enforcement mechanisms, penalty structures, 3-5 landmark enforcement cases, and a compliance essentials checklist. The cross-reference file uses dimension-based tables comparing all 6 regulations across 6-8 common dimensions. The timeline file covers enacted milestones and upcoming deadlines for the 6 major regulations plus all ~20 U.S. states with comprehensive privacy laws.

All regulation reference files must work with the existing skill-behaviors.md response formatting rules (anti-hallucination tiers, source attribution, disclaimer). They must also stand alone as regulation references without requiring FPF context -- FPF enrichment comes from the existing fpf-reference.md being loaded alongside when relevant.

**Primary recommendation:** Create one regulation file at a time (each ~200-350 lines) following a consistent internal structure, then create the cross-reference and timeline files, then update SKILL.md routing with regulation keyword detection and conditional loading rules. Target total new content of ~2,500-3,000 lines across all 8 files, with SKILL.md growing by ~50-80 lines to accommodate the new routing logic.

<user_constraints>
## User Constraints (from CONTEXT.md)

### Locked Decisions
- One file per regulation: 6 separate files (gdpr-reference.md, ccpa-reference.md, coppa-reference.md, hipaa-reference.md, ferpa-reference.md, eu-ai-act-reference.md)
- Cross-reference and timeline are separate dedicated files (reg-cross-reference.md, reg-timeline.md)
- SKILL.md auto-detects which regulation file(s) to load by parsing query keywords -- no user-specified flags
- When a regulation query overlaps FPF coverage areas, load BOTH the regulation file AND fpf-reference.md for FPF-enriched answers (consistent with Phase 1 FPF-first prioritization)
- Cross-reference file loaded only for explicit comparison queries ("compare," "contrast," "how does X differ from Y"), not for single-regulation lookups
- Practitioner reference level: each major provision covered with enough detail for a practitioner to recall or verify specifics
- Include 3-5 key enforcement milestones per regulation: landmark cases practitioners commonly reference
- Each regulation file ends with a brief "Compliance Essentials" section: the 5-8 non-negotiable items a practitioner needs to get right
- EU AI Act covered through a privacy practitioner's lens: data governance obligations, DPIA-adjacent requirements, biometric restrictions, high-risk AI rules affecting personal data processing. Skip purely safety/liability provisions that don't touch privacy.
- Dimension-based tables comparing all 6 regulations across common dimensions
- Core set of 6-8 comparison dimensions: scope/applicability, legal basis/consent, individual rights, enforcement authority, penalties, breach notification, international transfers, children's provisions
- When a regulation has no provision for a dimension, mark as "N/A -- [brief reason]"
- Timeline organized by regulation, then chronological within each section
- Covers both enacted milestones and upcoming/recent deadlines
- File-level verification date ("Last verified: March 2026") -- not per-entry or per-regulation verification
- Includes all U.S. states with enacted comprehensive privacy laws (~20 states) beyond the 6 major regulations
- Defers to FPF's Key Dates Tracker for granular state-level details
- Regulation files should be usable without FPF context -- they stand alone
- State privacy law timeline should be concise (effective date + enforcement date per state) and point to FPF's Key Dates Tracker
- Cross-reference tables should be scannable

### Claude's Discretion
- Internal structure and section ordering within each regulation file
- Exact wording of compliance essentials per regulation
- Which enforcement milestones are most practitioner-relevant per regulation
- How to handle the EU AI Act's phased enforcement timeline within the privacy lens
- Exact comparison dimensions beyond the core set if additional ones add value

### Deferred Ideas (OUT OF SCOPE)
None -- discussion stayed within phase scope
</user_constraints>

<phase_requirements>
## Phase Requirements

| ID | Description | Research Support |
|----|-------------|-----------------|
| REG-01 | Quick reference covers GDPR key provisions (lawful basis, data subject rights, breach notification, DPO, international transfers) | GDPR is well-established (effective May 2018). Key provisions verified: 6 lawful bases, 8 data subject rights, 72-hour breach notification, mandatory DPO criteria, Chapter V transfer mechanisms. Landmark cases available (Meta EUR 1.2B, TikTok EUR 530M). Compliance essentials well-documented. |
| REG-02 | Quick reference covers CCPA/CPRA key provisions (consumer rights, opt-out, service provider requirements, timelines) | CCPA (2018) amended by CPRA (effective Jan 2023). Major regulatory amendments effective Jan 1, 2026 (consent mechanisms, youth privacy, sensitive PI). ADMT/cybersecurity audit provisions phased 2027-2030. Enforcement by both AG and CPPA. Landmark cases available (Sephora $1.2M, Healthline $1.55M, Tractor Supply $1.35M). |
| REG-03 | Quick reference covers COPPA key provisions (parental consent, operator obligations, safe harbor) | COPPA (1998) with major FTC rule amendments finalized Jan 2025, effective June 23, 2025, compliance date April 22, 2026. Key updates: separate consent for third-party disclosures, data retention limits, expanded PI definition (biometrics, government IDs), safe harbor transparency. Landmark cases available (Disney $10M, Epic Games $275M). |
| REG-04 | Quick reference covers HIPAA privacy provisions (covered entities, PHI, minimum necessary, BAAs) | HIPAA Privacy Rule (2003) with recent reproductive health amendments (April 2024, partially vacated June 2025). Security Rule update proposed Dec 2024, expected final May 2026. Enforcement via OCR. Landmark cases available (Montefiore $4.75M, Anthem $16M historically). Risk Analysis Initiative launched fall 2024. |
| REG-05 | Quick reference covers FERPA key provisions (education records, directory information, consent) | FERPA (1974) is the most stable of the 6 regulations. NPRM targeted for Jan 2026 to clarify education record definitions and nonconsensual disclosure. No monetary penalties -- enforcement via federal funding withdrawal. Key issues: ed-tech vendor management, cybersecurity gaps, AI in education. |
| REG-06 | Quick reference covers EU AI Act key provisions (risk tiers, prohibited practices, timeline) | EU AI Act entered into force Aug 1, 2024. Phased implementation: prohibited practices Feb 2, 2025; GPAI rules Aug 2, 2025; high-risk systems (Annex III) Aug 2, 2026; regulated products Aug 2, 2027. Privacy lens: biometric prohibitions, data governance for training data, DPIA interplay with GDPR, emotion recognition restrictions. |
| REG-07 | Regulation cross-reference enables side-by-side comparison on common dimensions | Research identified 8 core comparison dimensions matching CONTEXT.md requirements. N/A handling needed for sector-specific regulations (HIPAA, FERPA, COPPA) on dimensions like international transfers. Table format works well for markdown -- scannable with consistent column structure. |
| REG-08 | Regulatory timeline tracks key effective dates, comment periods, enforcement deadlines | Timeline research covers all 6 major regulations plus ~20 U.S. states with enacted comprehensive privacy laws. Multiple upcoming deadlines verified: COPPA compliance April 2026, EU AI Act high-risk Aug 2026, CCPA ADMT Jan 2027, HIPAA Security Rule expected late 2026. State law effective dates verified for 2025-2026 window. |
| DEPTH-01 | Quick lookup mode answers common factual questions from static knowledge only | Enabled by the 6 regulation reference files containing practitioner-level detail on key provisions, dates, thresholds, and penalty amounts. When a factual question matches a regulation keyword, SKILL.md loads the appropriate reference file and the answer comes directly from its content -- no web fetching needed. |
</phase_requirements>

## Standard Stack

### Core
| Component | Format | Purpose | Why Standard |
|-----------|--------|---------|--------------|
| gdpr-reference.md | Markdown | GDPR quick reference with key provisions, rights, enforcement, compliance essentials | One-file-per-regulation pattern from CONTEXT.md; consistent with fpf-reference.md pattern |
| ccpa-reference.md | Markdown | CCPA/CPRA quick reference with consumer rights, obligations, recent amendments | Same pattern; covers both CCPA and CPRA in single file since CPRA amends CCPA |
| coppa-reference.md | Markdown | COPPA quick reference with parental consent, operator obligations, 2025 rule updates | Same pattern; includes recent FTC rule amendments |
| hipaa-reference.md | Markdown | HIPAA privacy provisions quick reference with covered entities, PHI, BAAs | Same pattern; focused on privacy rule, not full HIPAA scope |
| ferpa-reference.md | Markdown | FERPA quick reference with education records, directory information, consent | Same pattern; most stable regulation, fewest updates |
| eu-ai-act-reference.md | Markdown | EU AI Act quick reference through privacy practitioner lens | Same pattern; filtered for privacy-relevant provisions only |
| reg-cross-reference.md | Markdown | Dimension-based comparison tables across all 6 regulations | Dedicated cross-reference file loaded only for comparison queries |
| reg-timeline.md | Markdown | Chronological milestones, deadlines, and state law effective dates | Dedicated timeline file with single file-level verification date |
| SKILL.md (update) | Markdown | Extended routing logic for regulation query detection and file dispatch | Extends existing routing layer; stays under 500-line limit |

### Supporting
| Component | Status | Purpose | When to Use |
|-----------|--------|---------|-------------|
| skill-behaviors.md | Existing (no changes) | Response formatting, attribution, anti-hallucination rules | Already loaded for every query; regulation files work within its rules |
| fpf-reference.md | Existing (no changes) | FPF knowledge base and navigation | Co-loaded when regulation query overlaps FPF coverage areas |

### Alternatives Considered
| Instead of | Could Use | Tradeoff |
|------------|-----------|----------|
| 6 separate regulation files | Single combined regulation file | Separate files allow selective loading (only load what's needed per query); combined file would load ~2000+ lines for every regulation question |
| Separate cross-reference file | Inline comparison sections in each regulation file | Dedicated file enables clean table format and is only loaded for comparison queries; inline would duplicate content across files |
| Separate timeline file | Timeline sections within each regulation file | Dedicated file enables chronological cross-regulation view and includes state laws; inline would miss the cross-regulation timeline perspective |

**Installation:** No installation needed. Files are plain markdown placed in `.claude/skills/privacy/` directory alongside existing files.

## Architecture Patterns

### File Organization
```
.claude/skills/privacy/
  SKILL.md                  # Routing layer (existing, updated)
  skill-behaviors.md        # Response rules (existing, unchanged)
  fpf-reference.md          # FPF knowledge (existing, unchanged)
  gdpr-reference.md         # NEW: GDPR quick reference
  ccpa-reference.md         # NEW: CCPA/CPRA quick reference
  coppa-reference.md        # NEW: COPPA quick reference
  hipaa-reference.md        # NEW: HIPAA privacy provisions
  ferpa-reference.md        # NEW: FERPA quick reference
  eu-ai-act-reference.md    # NEW: EU AI Act (privacy lens)
  reg-cross-reference.md    # NEW: Cross-regulation comparison
  reg-timeline.md           # NEW: Regulatory timeline + state laws
```

### Pattern 1: Consistent Regulation File Structure
**What:** Each of the 6 regulation files follows the same internal section structure for consistency and predictable navigation by both Claude and practitioners reading the output.
**When to use:** Every regulation reference file.

**Recommended internal structure per regulation file:**
```markdown
# [Regulation Name] -- Quick Reference

> Last verified: March 2026

## Overview
[1-2 paragraphs: what, when enacted, who it applies to, territorial scope]

## Key Provisions
[Major provisions with practitioner-level detail]
[Subsections as appropriate for the regulation]

## Individual Rights / Consumer Rights / Data Subject Rights
[Rights enumerated with brief scope description for each]

## Obligations and Requirements
[What regulated entities must do: DPO, DPIA, records, etc.]

## Enforcement and Penalties
[Enforcement authority, penalty structure with specific amounts/thresholds]

## Key Enforcement Milestones
[3-5 landmark cases with year, entity, amount, significance]

## Recent Developments
[Major amendments, proposed rules, regulatory trends as of March 2026]

## Compliance Essentials
[5-8 bullet checklist of non-negotiable compliance items]
```

**Why this structure:** Mirrors the response patterns already defined in skill-behaviors.md (Overview, Key Provisions, Compliance Considerations). Consistent across files means Claude can reliably navigate any regulation file to find specific information. The structure adapts naturally -- GDPR has "Data Subject Rights" while CCPA has "Consumer Rights" and HIPAA has "Patient Rights."

### Pattern 2: SKILL.md Regulation Routing
**What:** Extend SKILL.md with a new routing step between "Determine FPF Relevance" and "Compose Response" that detects regulation-specific queries and loads the appropriate reference file(s).
**When to use:** Every query that mentions or implies a specific regulation.

**Routing logic design:**
```
Step 2.5: Determine Regulation Relevance

For each of these keyword groups, check if the query matches:
- GDPR keywords: GDPR, General Data Protection, EU data protection, European privacy, data subject rights, lawful basis, DPO, data protection officer, SCC, adequacy decision, right to erasure, right to be forgotten, data portability
- CCPA/CPRA keywords: CCPA, CPRA, California privacy, California Consumer Privacy Act, California Privacy Rights Act, CPPA, CalPrivacy, opt-out right, do not sell, sensitive personal information (California context)
- COPPA keywords: COPPA, children's privacy, children's online privacy, parental consent, under 13, child-directed
- HIPAA keywords: HIPAA, PHI, protected health information, covered entity, business associate agreement, BAA, HITECH, health privacy, minimum necessary
- FERPA keywords: FERPA, education records, student privacy, directory information, education privacy, student records
- EU AI Act keywords: EU AI Act, AI Act, artificial intelligence act, AI regulation EU, prohibited AI practices, high-risk AI, AI risk tiers

If comparison detected ("compare", "contrast", "differ", "difference", "versus", "vs", "side by side"):
  Load reg-cross-reference.md + relevant individual regulation files

If timeline/dates detected ("timeline", "effective date", "when does", "deadline", "enforcement date", "compliance date"):
  Load reg-timeline.md + relevant individual regulation file if specific

Otherwise: Load the matching regulation file(s)
```

**Integration with existing routing:** This new step runs AFTER Step 2 (FPF Relevance) so both decisions are made independently. If a GDPR query also overlaps FPF coverage (it does -- Global Data Protection issue area), both gdpr-reference.md AND fpf-reference.md get loaded. The existing bias-to-load heuristic for FPF still applies.

### Pattern 3: Cross-Reference Table Design
**What:** Dimension-based comparison tables that are scannable in markdown.
**When to use:** The reg-cross-reference.md file.

**Table format:**
```markdown
## [Dimension Name]

| Aspect | GDPR | CCPA/CPRA | COPPA | HIPAA | FERPA | EU AI Act |
|--------|------|-----------|-------|-------|-------|-----------|
| [row]  | ...  | ...       | ...   | ...   | ...   | ...       |
```

**Why separate tables per dimension (not one giant table):** Markdown tables with 7+ columns are hard to read when each cell contains multi-sentence content. Separate tables per dimension allow each cell to contain meaningful detail (1-3 sentences) without the table becoming unreadable. This also makes it easy to reference a specific dimension.

### Anti-Patterns to Avoid
- **Reproducing full statute text:** The files are practitioner references, not legal databases. Include enough for recall and verification, not full section quotes.
- **Inconsistent structure across regulation files:** All 6 files must follow the same section pattern for predictable navigation. Variations in section names/ordering for regulation-specific content (e.g., GDPR has "International Transfers" while HIPAA does not) are fine, but the overall skeleton must be consistent.
- **Loading all regulation files for any regulation query:** Only load the specific regulation file(s) mentioned. Loading all 6 files for a GDPR-only question wastes ~1,500 lines of context.
- **Duplicating cross-reference content in individual files:** Individual regulation files stand alone; comparison content lives only in reg-cross-reference.md.
- **Stale dates without verification markers:** The "Last verified: March 2026" header is critical for practitioner trust. All specific dates, penalty amounts, and enforcement thresholds must be accurate as of this verification date.

## Don't Hand-Roll

| Problem | Don't Build | Use Instead | Why |
|---------|-------------|-------------|-----|
| Regulation content accuracy | Generating provisions from training data | Verified authoritative sources (official regulation text, enforcement tracker databases, official agency websites) | Regulatory facts require HIGH verification per skill-behaviors.md; incorrect penalty amounts or dates destroy practitioner trust |
| State privacy law tracking | Comprehensive state-by-state coverage | FPF Key Dates Tracker reference + concise effective date table | FPF maintains this authoritatively and keeps it updated; our static file is a snapshot that points there |
| Enforcement case details | Exhaustive enforcement database | 3-5 landmark cases per regulation that practitioners commonly reference | IAPP maintains an enforcement tracker; our role is providing context on landmark precedents, not being an exhaustive database |
| Regulation comparison logic | Dynamic comparison generation | Static cross-reference tables | Comparisons on fixed dimensions are stable content; dynamic generation risks hallucination on nuanced differences |

**Key insight:** The regulation reference files are a knowledge foundation layer, not a replacement for authoritative sources. They enable instant answers to common questions and make future web-augmented research (Phase 4) faster and smarter. Every file should point practitioners to authoritative sources for the most current information.

## Common Pitfalls

### Pitfall 1: Context Budget Overrun
**What goes wrong:** Loading too many reference files per query exhausts the context window, leaving insufficient room for the response.
**Why it happens:** A comparison query could theoretically trigger loading reg-cross-reference.md + 2 regulation files + fpf-reference.md + skill-behaviors.md = 5 files.
**How to avoid:** Each regulation file should target 200-350 lines. With the cross-reference file at ~200-250 lines, a worst-case comparison query loads ~900-1200 lines of reference content. This is well within budget when combined with existing files (skill-behaviors.md at 144 lines, fpf-reference.md at 319 lines). Monitor SKILL.md total size -- must stay under 500 lines after routing extension.
**Warning signs:** SKILL.md exceeding 450 lines; individual regulation files exceeding 400 lines; responses feeling truncated.

### Pitfall 2: Stale Regulatory Information
**What goes wrong:** Regulation content becomes outdated as new amendments, enforcement actions, and compliance deadlines pass.
**Why it happens:** Privacy law evolves rapidly -- CCPA had major amendments effective Jan 1, 2026; COPPA rule amendments effective June 2025 with April 2026 compliance date; EU AI Act has phased implementation through 2027.
**How to avoid:** Include "Last verified: March 2026" header on every file. Focus the "Recent Developments" section on developments within the past 12-18 months. Include upcoming deadlines with specific dates. The Phase 4 web-fetching capability will eventually supplement static knowledge with live information.
**Warning signs:** Users getting answers about deadlines that have already passed; enforcement cases described as "recent" that are years old.

### Pitfall 3: Wrong Abstraction Level
**What goes wrong:** Content is either too shallow (executive summary that doesn't help practitioners) or too deep (trying to reproduce the statute).
**Why it happens:** The "practitioner reference" level is a specific middle ground that requires judgment.
**How to avoid:** Apply the test: "Could a practicing privacy professional use this to recall or verify a specific provision without looking up the full text?" If yes, the depth is right. Include specific thresholds (e.g., "4% of global annual turnover"), specific rights (e.g., all 8 GDPR data subject rights listed individually), and specific requirements (e.g., "72-hour breach notification to supervisory authority"). Do not include full regulatory text, implementation guidance, or case law analysis.
**Warning signs:** Sections that could apply to any regulation ("organizations must comply with applicable law"); sections that read like a law school textbook.

### Pitfall 4: Inconsistent Routing Between Regulation and FPF Files
**What goes wrong:** A COPPA query loads coppa-reference.md but fails to also load fpf-reference.md, missing FPF's extensive Youth Privacy coverage.
**Why it happens:** Regulation routing is implemented as a separate step from FPF routing, and the two steps don't coordinate.
**How to avoid:** CONTEXT.md explicitly requires loading BOTH files when overlap exists. All 6 regulations have FPF coverage overlap: GDPR (Global Data Protection), CCPA (U.S. Legislation), COPPA (Youth and Education Privacy), HIPAA (Health Data), FERPA (Youth and Education Privacy), EU AI Act (Artificial Intelligence). The FPF routing step (Step 2) already handles this via the bias-to-load heuristic -- every regulation keyword also matches at least one FPF coverage area. Just ensure the regulation routing step (new Step 2.5) doesn't short-circuit the FPF step.
**Warning signs:** Regulation answers that never mention FPF resources; regulation answers that cite FPF but lack specific provision detail from the regulation file.

### Pitfall 5: SKILL.md Size Bloat
**What goes wrong:** Adding regulation routing logic pushes SKILL.md over the 500-line limit.
**Why it happens:** 6 regulations with keyword lists, cross-reference triggers, timeline triggers, and integration rules can expand quickly if not written concisely.
**How to avoid:** SKILL.md is currently at 164 lines with 336 lines of headroom. The regulation routing section should be 50-80 lines total. Use a compact keyword list format (one line per regulation, not one line per keyword). Reference files do the heavy lifting -- SKILL.md only needs to know which file to load, not what's in it. Keep example queries to 2-3 regulation-specific examples added to the existing set.
**Warning signs:** SKILL.md exceeding 250 lines after Phase 2; keyword lists growing beyond what's needed for reliable detection.

## Code Examples

### Regulation File Header Pattern
```markdown
# GDPR -- Quick Reference

> **Last verified:** March 2026. Regulatory details reflect the state of the law as of this date. For the most current enforcement actions and guidance, consult the [EDPB](https://edpb.europa.eu/) and relevant national DPA websites.

## Overview

The **General Data Protection Regulation (GDPR)** (Regulation (EU) 2016/679) is the European Union's comprehensive data protection framework...
```

### SKILL.md Routing Extension Pattern
```markdown
### Step 2.5: Determine Regulation Relevance (CONDITIONAL)

Check whether the query references a specific privacy regulation. Load the corresponding reference file(s) for detailed provision-level answers.

**Regulation detection:**
| Regulation | Load File | Keywords |
|------------|-----------|----------|
| GDPR | [gdpr-reference.md](gdpr-reference.md) | GDPR, General Data Protection, EU data protection, data subject rights, lawful basis, DPO, adequacy, SCC |
| CCPA/CPRA | [ccpa-reference.md](ccpa-reference.md) | CCPA, CPRA, California privacy, California Consumer Privacy Act, opt-out, do not sell, CPPA |
| COPPA | [coppa-reference.md](coppa-reference.md) | COPPA, children's online privacy, parental consent, child-directed, under 13 |
| HIPAA | [hipaa-reference.md](hipaa-reference.md) | HIPAA, PHI, protected health information, covered entity, BAA, health privacy |
| FERPA | [ferpa-reference.md](ferpa-reference.md) | FERPA, education records, student privacy, directory information |
| EU AI Act | [eu-ai-act-reference.md](eu-ai-act-reference.md) | EU AI Act, AI Act, artificial intelligence act, prohibited AI, high-risk AI, AI risk tiers |

**Comparison queries:** If the query contains comparison language ("compare," "contrast," "differ," "versus," "vs," "side by side," "how does X differ from Y"), also load [reg-cross-reference.md](reg-cross-reference.md).

**Timeline queries:** If the query asks about dates, deadlines, or timelines ("when does," "effective date," "deadline," "timeline," "enforcement date"), also load [reg-timeline.md](reg-timeline.md).

**Multiple regulations:** If the query mentions multiple regulations, load all matching files. For broad questions like "What privacy laws apply to children?" load all potentially relevant regulation files (COPPA, FERPA, and potentially CCPA for its minor provisions).

This step runs independently of Step 2 (FPF Relevance). Both routing decisions apply simultaneously -- a GDPR query loads both gdpr-reference.md (for regulation detail) and fpf-reference.md (for FPF's Global Data Protection resources) when FPF relevance is detected.
```

### Cross-Reference Table Pattern
```markdown
## Consent / Legal Basis

| Aspect | GDPR | CCPA/CPRA | COPPA | HIPAA | FERPA | EU AI Act |
|--------|------|-----------|-------|-------|-------|-----------|
| Consent model | Opt-in; consent is one of 6 lawful bases | Opt-out; consumers can opt out of sale/sharing | Opt-in; verifiable parental consent required before collecting PI from children under 13 | Authorization; written patient authorization required for most non-TPO uses | Consent; written consent required for disclosure outside enumerated exceptions | Risk-based; consent not primary mechanism; prohibitions and obligations based on risk tier |
| Other lawful bases | Contract, legal obligation, vital interests, public interest, legitimate interest | N/A -- CCPA does not use a lawful basis framework; opt-out model with business purpose exceptions | N/A -- parental consent is the primary mechanism; limited exceptions for internal use | TPO (treatment, payment, operations) exception; public health; research | Directory information exception; legitimate educational interest; health/safety emergency | N/A -- compliance based on risk classification, not consent |
```

### Timeline Entry Pattern
```markdown
## GDPR Timeline

| Date | Milestone | Status |
|------|-----------|--------|
| Apr 2016 | GDPR adopted by EU Parliament | Enacted |
| May 25, 2018 | GDPR becomes enforceable | Effective |
| Jul 2020 | Schrems II invalidates Privacy Shield (CJEU C-311/18) | Landmark ruling |
| Jun 2021 | New SCCs adopted by European Commission | Effective |
| Jul 2023 | EU-U.S. Data Privacy Framework adequacy decision | Effective |
| May 2023 | Meta receives record EUR 1.2B fine for illegal US data transfers | Enforcement milestone |
| 2026 | CEF priority: transparency obligations (Articles 12-14) coordinated enforcement | Ongoing |
```

### Compliance Essentials Pattern
```markdown
## Compliance Essentials

Non-negotiable items for GDPR compliance:

1. **Lawful basis identified** for every processing activity before processing begins
2. **Privacy notice** provided at or before the point of data collection, covering all Article 13/14 requirements
3. **Data subject rights processes** operational for all 8 rights with documented response procedures and 30-day response deadline
4. **Data Protection Officer** appointed if required (public authority, large-scale special category processing, or large-scale systematic monitoring)
5. **Records of processing activities** maintained under Article 30
6. **Data breach notification** process in place: 72 hours to supervisory authority, undue delay to data subjects when high risk
7. **International transfer mechanisms** in place for any transfer outside the EEA (SCCs, adequacy, BCRs, or DPF)
8. **Data processing agreements** with all processors meeting Article 28 requirements
```

## State of the Art

| Old Approach | Current Approach | When Changed | Impact |
|--------------|------------------|--------------|--------|
| CCPA as standalone law | CCPA as amended by CPRA with CPPA as enforcement agency | Jan 2023 (CPRA effective) + Jan 2026 (new regulations) | CCPA reference must cover CPRA amendments and 2026 regulatory updates as current state |
| COPPA Rule (2013 version) | COPPA Rule with 2025 FTC amendments | Jun 2025 (effective) / Apr 2026 (compliance) | Must include expanded PI definition, separate third-party consent, data retention limits |
| Privacy Shield for EU-US transfers | EU-U.S. Data Privacy Framework | Jul 2023 | GDPR international transfers section must cover DPF, not Privacy Shield |
| EU AI Act as proposal | EU AI Act as enacted law with phased enforcement | Aug 2024 (entry into force) | Coverage shifts from "proposed regulation" to "what's already enforceable vs. upcoming" |
| ~15 US state privacy laws | ~20 US state comprehensive privacy laws | 2025-2026 | Timeline file must include Kentucky, Rhode Island, Indiana (effective Jan 2026) and others |
| HIPAA Privacy Rule stable | HIPAA reproductive health amendments + Security Rule overhaul proposed | Apr 2024 / Dec 2024 | Must cover reproductive health protections (partially vacated) and proposed Security Rule modernization |

**Deprecated/outdated:**
- Privacy Shield: Invalidated by Schrems II (2020), replaced by EU-U.S. Data Privacy Framework (2023)
- Safe Harbor: Invalidated by Schrems I (2015), historical context only
- COPPA Rule (2013 version): Superseded by January 2025 FTC amendments

## Regulation-Specific Research Findings

### GDPR (Confidence: HIGH)
- **Effective:** May 25, 2018
- **6 lawful bases:** Consent, contract, legal obligation, vital interests, public interest, legitimate interest
- **8 data subject rights:** Access, rectification, erasure, restriction, portability, object, automated decision-making objection, withdraw consent
- **Penalties:** Up to EUR 20M or 4% global annual turnover (whichever higher) for substantive violations; EUR 10M or 2% for procedural violations
- **Breach notification:** 72 hours to supervisory authority; undue delay to data subjects when high risk
- **DPO required when:** Public authority, large-scale special category processing, large-scale systematic monitoring
- **Transfers:** Chapter V mechanisms -- SCCs, adequacy decisions, BCRs, EU-U.S. DPF
- **Landmark cases:** Meta EUR 1.2B (international transfers, 2023), TikTok EUR 530M (China transfers, 2025), Meta EUR 479M (consent manipulation), Amazon EUR 746M (targeted advertising, 2021), Google EUR 100M (cookie consent, CNIL)
- **2026 focus:** EDPB Coordinated Enforcement Framework targeting transparency obligations (Articles 12-14); cumulative fines now EUR 7.1B+

### CCPA/CPRA (Confidence: HIGH)
- **CCPA effective:** January 1, 2020; **CPRA effective:** January 1, 2023
- **2026 amendments effective:** January 1, 2026 (consent mechanisms, youth as sensitive PI, data breach timelines)
- **Consumer rights:** Know, delete, opt-out of sale/sharing, correct, limit use of sensitive PI, non-discrimination
- **Opt-out:** Right to opt out of sale and sharing of personal information; businesses must honor Global Privacy Control (GPC)
- **Service provider requirements:** Written contracts, limited use to business purpose, no further selling
- **Enforcement:** California AG + CPPA (California Privacy Protection Agency); civil penalties up to $7,500 per intentional violation, $2,500 per unintentional
- **Upcoming:** ADMT requirements Jan 2027; risk assessments and cybersecurity audits phased 2027-2030
- **Landmark cases:** Sephora $1.2M (2022, first CCPA enforcement), Healthline $1.55M (2025, AG largest settlement), Tractor Supply $1.35M (2025, CPPA largest)

### COPPA (Confidence: HIGH)
- **Statute:** 1998; **Original FTC Rule:** 2000, amended 2013
- **2025 Rule amendments:** Finalized January 16, 2025; effective June 23, 2025; compliance deadline April 22, 2026
- **Core requirement:** Verifiable parental consent before collecting PI from children under 13
- **2025 updates:** Separate consent for third-party disclosures, data retention limits, expanded PI definition (biometrics, government IDs), safe harbor transparency requirements
- **Operator obligations:** Direct notice to parents, verifiable consent, data minimization, data security, deletion upon request
- **Safe harbor:** FTC-approved programs must publicly disclose membership; revised guidelines due October 2025
- **Enforcement:** FTC; civil penalties per violation (adjusted for inflation)
- **Landmark cases:** Epic Games (Fortnite) $275M (2022, largest COPPA penalty), Disney $10M (2025, YouTube child-directed content), Apitor Technology $500K suspended (2024, geolocation collection via Chinese third party)

### HIPAA (Confidence: HIGH)
- **Privacy Rule effective:** April 14, 2003 (compliance April 2003 for most, April 2004 for small plans)
- **Covered entities:** Health plans, healthcare clearinghouses, healthcare providers who transmit electronically
- **PHI scope:** Individually identifiable health information held or transmitted by a covered entity or BA
- **Minimum necessary:** Use, disclose, and request only the minimum necessary PHI for the intended purpose
- **BAA required:** Written agreements with all business associates who access PHI
- **Patient rights:** Access, amendment, accounting of disclosures, request restrictions, confidential communications, notice of privacy practices
- **Breach notification:** Individual notification without unreasonable delay (no later than 60 days); HHS notification; 500+ breaches reported to media
- **Penalties:** Tiered structure from $141-$71,162 per violation depending on culpability; annual caps up to $2.19M (2026 inflation adjustment)
- **Recent:** Reproductive health privacy amendments (April 2024, partially vacated June 2025); Security Rule modernization proposed December 2024 (expected final May 2026)
- **Landmark cases:** Anthem $16M (2018, largest HIPAA settlement historically), Montefiore Medical Center $4.75M (2024), Solara Medical $3M (2025)

### FERPA (Confidence: HIGH)
- **Effective:** 1974 (most stable of the 6 regulations)
- **Scope:** Educational agencies and institutions receiving federal education funding
- **Education records:** Records directly related to a student, maintained by an educational agency/institution or party acting for it
- **Directory information:** Name, address, phone, dates of attendance, degrees -- can be disclosed without consent if notice given and opt-out period provided
- **Consent requirement:** Written consent from parent (or eligible student 18+) required before disclosing education records, with enumerated exceptions
- **Key exceptions:** School officials with legitimate educational interest, transfer to another school, health/safety emergency, directory information, judicial order
- **Enforcement:** Family Policy Compliance Office (DOE); no monetary penalties -- enforcement via withdrawal of federal funding
- **Upcoming:** NPRM targeted January 2026 to clarify education record definition and update nonconsensual disclosure provisions
- **Key issues:** Ed-tech vendor management (vendors as "school officials"), cybersecurity gaps, AI in education, April 2025 Dear Colleague letter on gender support plans

### EU AI Act (Privacy Lens) (Confidence: HIGH)
- **Entry into force:** August 1, 2024
- **Phased enforcement:** Prohibited practices Feb 2, 2025; GPAI rules Aug 2, 2025; High-risk Annex III Aug 2, 2026; Regulated products Aug 2, 2027
- **Prohibited practices (privacy-relevant):** Real-time remote biometric identification in public spaces (narrow law enforcement exceptions), untargeted facial image scraping for recognition databases, emotion recognition in workplace/educational settings (without safety justification), social scoring
- **High-risk AI (privacy-relevant):** Biometric identification/categorization systems, AI in critical infrastructure, education, employment, essential services, law enforcement, migration/border control
- **Data governance:** Training data must meet quality, representativeness, and bias requirements; special categories of personal data require GDPR-compliant safeguards
- **GDPR interplay:** AI Act DPIA-adjacent requirements (fundamental rights impact assessment for high-risk AI) complement GDPR DPIAs; both may apply to the same system; DPAs may be designated as national competent authorities for AI Act enforcement
- **Transparency:** Article 50 requirements for AI-generated content disclosure, deepfake labeling, and chatbot/AI interaction disclosure -- effective August 2026
- **Penalties:** Up to EUR 35M or 7% global annual turnover for prohibited practices; EUR 15M or 3% for high-risk obligations; EUR 7.5M or 1% for misleading information

### U.S. State Privacy Laws (~20 States) (Confidence: MEDIUM)
Research verified 20 states with enacted comprehensive privacy laws as of early 2026:
1. California (CCPA/CPRA) -- effective Jan 2020/2023
2. Virginia (VCDPA) -- effective Jan 2023
3. Colorado (CPA) -- effective Jul 2023
4. Connecticut (CTDPA) -- effective Jul 2023
5. Utah (UCPA) -- effective Dec 2023
6. Iowa (ICDPA) -- effective Jan 2025
7. Indiana (ICDPA) -- effective Jan 2026
8. Tennessee (TIPA) -- effective Jul 2025
9. Texas (TDPSA) -- effective Jul 2024
10. Florida (FDBR) -- effective Jul 2024
11. Montana (MCDPA) -- effective Oct 2024
12. Oregon (OCPA) -- effective Jul 2024
13. Delaware (DPDPA) -- effective Jan 2025
14. New Hampshire (SB 255) -- effective Jan 2025
15. New Jersey (SB 332) -- effective Jan 2025
16. Nebraska (NDPA) -- effective Jan 2025
17. Maryland (MODPA) -- effective Oct 2025
18. Minnesota (MCDPA) -- effective Jul 2025
19. Kentucky (KCDPA) -- effective Jan 2026
20. Rhode Island (RIDTPPA) -- effective Jan 2026

Note: The exact count and effective dates should be cross-verified with FPF's Key Dates Tracker when writing the timeline file. The CONTEXT.md specifies deferring to FPF for granular state-level details.

## File Size and Context Budget Analysis

### Current Context Load
| File | Lines | Loaded When |
|------|-------|-------------|
| SKILL.md | 164 | Every query (entry point) |
| skill-behaviors.md | 144 | Every query (mandatory) |
| fpf-reference.md | 319 | Most queries (bias-to-load) |
| **Total current** | **627** | **Typical query** |

### Projected Context Load After Phase 2
| File | Target Lines | Loaded When |
|------|-------------|-------------|
| SKILL.md (updated) | ~220-240 | Every query |
| skill-behaviors.md | 144 (unchanged) | Every query |
| fpf-reference.md | 319 (unchanged) | Most queries |
| Single regulation file | ~200-350 | Regulation-specific query |
| reg-cross-reference.md | ~200-250 | Comparison queries only |
| reg-timeline.md | ~150-200 | Timeline queries only |

**Worst-case scenario (comparison query with 2 regulations + FPF):**
~220 (SKILL) + 144 (behaviors) + 319 (FPF) + 350 + 350 (2 reg files) + 250 (cross-ref) = ~1,633 lines

**Typical regulation query (1 regulation + FPF):**
~220 (SKILL) + 144 (behaviors) + 319 (FPF) + 300 (1 reg file) = ~983 lines

Both scenarios are well within Claude's context capacity, leaving ample room for the response.

### SKILL.md Budget
- Current: 164 lines
- Limit: 500 lines
- New routing section: ~50-80 lines
- New reference file documentation: ~15-20 lines
- Updated examples (2-3 new): ~20-30 lines
- **Projected total: ~250-270 lines** (50-54% of budget)

## Open Questions

1. **Exact list of ~20 U.S. state privacy laws**
   - What we know: Multiple sources consistently cite 20 states with enacted comprehensive privacy laws as of early 2026. Individual state names and effective dates verified against multiple sources.
   - What's unclear: Whether any additional states enacted laws in the 2025-2026 legislative sessions that are not yet widely indexed.
   - Recommendation: Use the verified list of 20 states. Include a note in reg-timeline.md directing practitioners to FPF's Key Dates Tracker for the most current list. This aligns with the CONTEXT.md decision to defer granular state details to FPF.

2. **HIPAA Security Rule finalization timeline**
   - What we know: Proposed December 27, 2024. Expected finalization around May 2026 based on regulatory calendar.
   - What's unclear: Whether the Trump administration's regulatory priorities might delay or alter the proposed rule.
   - Recommendation: Document as "proposed" with expected timeline. Include in both the HIPAA reference file and the timeline file with appropriate hedging language.

3. **EU AI Act implementing acts and standards**
   - What we know: The high-level timeline is clear (phased through 2027). Harmonized standards and implementing acts are being developed.
   - What's unclear: Specific details of implementing acts for data governance and AI regulatory sandbox requirements.
   - Recommendation: Focus on the enacted regulation text and confirmed dates. Flag implementing acts as "in development" without speculating on their content. The privacy lens scoping helps here -- we can focus on confirmed privacy-relevant provisions.

## Validation Architecture

### Test Framework
| Property | Value |
|----------|-------|
| Framework | Manual testing via `/privacy` command invocation |
| Config file | None -- Claude Code skills are tested by invocation |
| Quick run command | `/privacy What does GDPR require?` (manual) |
| Full suite command | Run all 8 test queries below in sequence (manual) |

### Phase Requirements -> Test Map
| Req ID | Behavior | Test Type | Test Query | File Exists? |
|--------|----------|-----------|-----------|-------------|
| REG-01 | GDPR quick reference answers | manual | `/privacy What are the GDPR lawful bases for processing?` | N/A -- regulation file must exist |
| REG-02 | CCPA/CPRA quick reference answers | manual | `/privacy What consumer rights does the CCPA provide?` | N/A -- regulation file must exist |
| REG-03 | COPPA quick reference answers | manual | `/privacy What does COPPA require for parental consent?` | N/A -- regulation file must exist |
| REG-04 | HIPAA quick reference answers | manual | `/privacy What entities are covered by HIPAA?` | N/A -- regulation file must exist |
| REG-05 | FERPA quick reference answers | manual | `/privacy What are education records under FERPA?` | N/A -- regulation file must exist |
| REG-06 | EU AI Act quick reference answers | manual | `/privacy What AI practices does the EU AI Act prohibit?` | N/A -- regulation file must exist |
| REG-07 | Cross-regulation comparison | manual | `/privacy Compare GDPR and CCPA consent requirements` | N/A -- cross-reference file must exist |
| REG-08 | Regulatory timeline | manual | `/privacy When does the COPPA rule update take effect?` | N/A -- timeline file must exist |
| DEPTH-01 | Quick lookup from static knowledge | manual | `/privacy What are GDPR breach notification requirements?` (verify no web fetch triggered) | N/A -- routing + files must exist |

### Sampling Rate
- **Per task commit:** Invoke `/privacy` with a regulation-specific query and verify the response uses the regulation file content
- **Per wave merge:** Run all 8 test queries and verify correct file routing
- **Phase gate:** All 8 test queries produce structured, accurate answers from static knowledge before `/gsd:verify-work`

### Wave 0 Gaps
- [ ] `gdpr-reference.md` -- covers REG-01
- [ ] `ccpa-reference.md` -- covers REG-02
- [ ] `coppa-reference.md` -- covers REG-03
- [ ] `hipaa-reference.md` -- covers REG-04
- [ ] `ferpa-reference.md` -- covers REG-05
- [ ] `eu-ai-act-reference.md` -- covers REG-06
- [ ] `reg-cross-reference.md` -- covers REG-07
- [ ] `reg-timeline.md` -- covers REG-08
- [ ] SKILL.md routing update -- covers DEPTH-01 (enables routing to regulation files)

## Sources

### Primary (HIGH confidence)
- [FTC COPPA Rule Final Amendments](https://www.ftc.gov/news-events/news/press-releases/2025/01/ftc-finalizes-changes-childrens-privacy-rule-limiting-companies-ability-monetize-kids-data) -- 2025 COPPA rule changes, effective dates, key provisions
- [CPPA Regulations](https://cppa.ca.gov/regulations/) -- CCPA/CPRA regulatory amendments effective January 2026
- [EU AI Act Implementation Timeline](https://ai-act-service-desk.ec.europa.eu/en/ai-act/timeline/timeline-implementation-eu-ai-act) -- Official EU AI Act phased enforcement dates
- [EU AI Act Prohibited Practices](https://artificialintelligenceact.eu/article/5/) -- Article 5 prohibited AI practices
- [FPF Red Lines Analysis](https://fpf.org/blog/red-lines-under-the-eu-ai-act-understanding-prohibited-ai-practices-and-their-interplay-with-the-gdpr-dsa/) -- EU AI Act prohibited practices and GDPR interplay
- [HHS HIPAA Regulatory Initiatives](https://www.hhs.gov/hipaa/for-professionals/regulatory-initiatives/index.html) -- HIPAA proposed rule updates
- [HHS Resolution Agreements](https://www.hhs.gov/hipaa/for-professionals/compliance-enforcement/agreements/index.html) -- HIPAA enforcement settlements
- [IAPP US State Privacy Legislation Tracker](https://iapp.org/resources/article/us-state-privacy-legislation-tracker) -- State law enumeration and status
- [EDPB GDPR Enforcement Tracker](https://www.enforcementtracker.com/) -- GDPR fine amounts and case details
- [DOE Student Privacy](https://studentprivacy.ed.gov/) -- FERPA guidance and updates

### Secondary (MEDIUM confidence)
- [MultiState: 20 States Have Comprehensive Privacy Laws](https://www.multistate.us/insider/2026/2/4/all-of-the-comprehensive-privacy-laws-that-take-effect-in-2026) -- State law count and effective dates verified against IAPP tracker
- [Jackson Lewis CCPA FAQs](https://www.jacksonlewis.com/insights/navigating-california-consumer-privacy-act-30-essential-faqs-covered-businesses-including-clarifying-regulations-effective-1126) -- CCPA 2026 amendment details verified against CPPA
- [Greenberg Traurig CCPA Regulations](https://www.gtlaw.com/en/insights/2025/9/revised-and-new-ccpa-regulations-set-to-take-effect-on-jan-1-2026-summary-of-near-term-action-items) -- CCPA ADMT and cybersecurity audit phased implementation
- [IAPP: Biometrics in the EU](https://iapp.org/news/a/biometrics-in-the-eu-navigating-the-gdpr-ai-act) -- EU AI Act and GDPR biometrics interplay
- [White & Case: Tractor Supply CPPA Settlement](https://www.whitecase.com/insight-alert/california-privacy-protection-agency-issues-record-135-million-fine-against-tractor) -- CCPA enforcement milestone details

### Tertiary (LOW confidence)
- HIPAA Security Rule finalization timeline (expected May 2026) -- based on regulatory calendar analysis by multiple law firms, not official HHS confirmation
- Exact U.S. state count may shift as 2025-2026 legislative sessions conclude -- using 20 as verified count

## Metadata

**Confidence breakdown:**
- Standard stack: HIGH -- file format and architecture patterns are proven in Phase 1; no new technology decisions
- Architecture: HIGH -- extends existing SKILL.md routing pattern; all integration points well-understood from Phase 1
- Content accuracy (regulations): HIGH -- all 6 regulations verified against official sources and recent law firm analyses; specific dates, penalties, and provisions cross-referenced across multiple sources
- Pitfalls: HIGH -- context budget analysis is quantitative; routing conflicts identifiable from existing SKILL.md structure
- State law list: MEDIUM -- count verified but individual state details should be cross-checked with FPF tracker

**Research date:** 2026-03-13
**Valid until:** 2026-04-13 (30 days -- regulation content is relatively stable, but COPPA compliance deadline April 22, 2026 and EU AI Act Annex III deadline August 2, 2026 are approaching milestones)
