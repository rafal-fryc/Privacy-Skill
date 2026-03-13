# Phase 2: Regulation Knowledge Base - Context

**Gathered:** 2026-03-13
**Status:** Ready for planning

<domain>
## Phase Boundary

Create static quick-reference files for 6 major privacy regulations (GDPR, CCPA/CPRA, COPPA, HIPAA, FERPA, EU AI Act) plus cross-reference comparison and regulatory timeline capabilities. These files serve as a **knowledge foundation layer** — not a replacement for web fetching, but a baseline that enables instant answers to common questions AND makes web-augmented research (Phase 4) faster, smarter, and more targeted. The static knowledge gives the skill context to ask better questions when fetching and to validate web-fetched information against known provisions. Update SKILL.md routing to auto-detect regulation queries and load the appropriate reference files.

</domain>

<decisions>
## Implementation Decisions

### File Organization
- One file per regulation: 6 separate files (gdpr-reference.md, ccpa-reference.md, coppa-reference.md, hipaa-reference.md, ferpa-reference.md, eu-ai-act-reference.md)
- Cross-reference and timeline are separate dedicated files (reg-cross-reference.md, reg-timeline.md)
- SKILL.md auto-detects which regulation file(s) to load by parsing query keywords — no user-specified flags
- When a regulation query overlaps FPF coverage areas, load BOTH the regulation file AND fpf-reference.md for FPF-enriched answers (consistent with Phase 1 FPF-first prioritization)
- Cross-reference file loaded only for explicit comparison queries ("compare," "contrast," "how does X differ from Y"), not for single-regulation lookups

### Content Depth
- Practitioner reference level: each major provision covered with enough detail for a practitioner to recall or verify specifics (e.g., all 6 GDPR lawful bases with 1-sentence descriptions, all data subject rights with practical scope, specific penalty thresholds)
- Not full statute text, not executive summary — the middle ground where practitioners can answer "what does this provision actually require?"
- Include 3-5 key enforcement milestones per regulation: landmark cases practitioners commonly reference (e.g., GDPR: Meta transfer fine, CCPA: Sephora settlement)
- Each regulation file ends with a brief "Compliance Essentials" section: the 5-8 non-negotiable items a practitioner needs to get right
- EU AI Act covered through a privacy practitioner's lens: data governance obligations, DPIA-adjacent requirements, biometric restrictions, high-risk AI rules affecting personal data processing. Skip purely safety/liability provisions that don't touch privacy.

### Cross-Reference Format
- Dimension-based tables comparing all 6 regulations across common dimensions
- Core set of 6-8 comparison dimensions: scope/applicability, legal basis/consent, individual rights, enforcement authority, penalties, breach notification, international transfers, children's provisions
- When a regulation has no provision for a dimension, mark as "N/A — [brief reason]" (e.g., "N/A — HIPAA is sector-specific, no cross-border transfer mechanism")
- File loaded only for comparison queries, not single-regulation lookups

### Timeline Presentation
- Organized by regulation, then chronological within each section
- Covers both enacted milestones (enactment, effective dates, major amendments) and upcoming/recent deadlines (enforcement starts, compliance deadlines, amendment effective dates)
- File-level verification date ("Last verified: March 2026") — not per-entry or per-regulation verification
- Includes all U.S. states with enacted comprehensive privacy laws (currently ~18-20 states) beyond the 6 major federal/international regulations — covers enactment dates, effective dates, enforcement start dates
- Defers to FPF's Key Dates Tracker for granular state-level details (cure periods, opt-out signal deadlines)

### Claude's Discretion
- Internal structure and section ordering within each regulation file
- Exact wording of compliance essentials per regulation
- Which enforcement milestones are most practitioner-relevant per regulation
- How to handle the EU AI Act's phased enforcement timeline within the privacy lens
- Exact comparison dimensions beyond the core set if additional ones add value

</decisions>

<specifics>
## Specific Ideas

- Regulation files should be usable without FPF context — they stand alone as regulation references, and FPF enrichment comes from loading fpf-reference.md alongside when relevant
- State privacy law timeline should be concise (effective date + enforcement date per state) and explicitly point practitioners to FPF's Key Dates Tracker for the detailed view
- Cross-reference tables should be scannable — a practitioner glancing at the table should quickly see how GDPR and CCPA differ on consent without reading paragraphs

</specifics>

<code_context>
## Existing Code Insights

### Reusable Assets
- SKILL.md (164/500 lines): existing routing layer that dispatches to fpf-reference.md and skill-behaviors.md — needs extension for regulation file routing
- skill-behaviors.md: response formatting, attribution, anti-hallucination rules — already handles "regulatory facts require HIGH verification" which aligns with serving facts from regulation reference files
- fpf-reference.md: FPF knowledge base — loaded alongside regulation files when FPF coverage overlaps

### Established Patterns
- Reference files loaded on-demand by SKILL.md routing (progressive disclosure pattern from Phase 1)
- FPF coverage quick-reference list in SKILL.md used for fast relevance detection — same pattern can be used for regulation keyword detection
- Three-tier anti-hallucination (strict/high/standard) already configured in skill-behaviors.md

### Integration Points
- SKILL.md routing needs new regulation detection logic and file dispatch rules
- Regulation files must work with existing skill-behaviors.md response formatting
- FPF coverage overlap detection: when a regulation query also touches FPF issue areas, both files loaded
- Cross-reference and timeline files need their own routing triggers in SKILL.md

</code_context>

<deferred>
## Deferred Ideas

None — discussion stayed within phase scope

</deferred>

---

*Phase: 02-regulation-knowledge-base*
*Context gathered: 2026-03-13*
