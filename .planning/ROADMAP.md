# Roadmap: FPF Privacy Research Skill

## Overview

This roadmap delivers a Claude Code skill (`/privacy`) that serves as a comprehensive data privacy research tool for privacy professionals. The skill is built in four phases: first establishing the routing backbone and FPF as the primary source, then layering in a static regulation knowledge base for fast lookups, then expanding to the broader privacy organization ecosystem, and finally wiring up multi-source deep research with end-to-end validation. Each phase delivers a coherent, testable capability -- the skill is usable after Phase 1 and gets progressively more powerful.

## Phases

**Phase Numbering:**
- Integer phases (1, 2, 3): Planned milestone work
- Decimal phases (2.1, 2.2): Urgent insertions (marked with INSERTED)

Decimal phases appear between their surrounding integers in numeric order.

- [ ] **Phase 1: Skill Foundation + FPF Primary Source** - Build the SKILL.md routing layer, FPF navigation guide, and all foundational skill behaviors (attribution, disclaimers, anti-hallucination)
- [ ] **Phase 2: Regulation Knowledge Base** - Create static quick-reference files for 6 major privacy regulations plus cross-reference and timeline capabilities
- [ ] **Phase 3: Organization Catalog + Government Sources** - Expand to 15-20 privacy organizations and government regulators with per-source navigation guides
- [ ] **Phase 4: Deep Research + Validation** - Wire up multi-source live fetching, graceful degradation, and validate all query paths end-to-end

## Phase Details

### Phase 1: Skill Foundation + FPF Primary Source
**Goal**: Privacy professionals can invoke `/privacy` and get source-attributed, FPF-prioritized answers about FPF programs, publications, and issue areas
**Depends on**: Nothing (first phase)
**Requirements**: ARCH-01, ARCH-02, ARCH-03, ARCH-06, ARCH-07, ARCH-08, FPF-01, FPF-02, FPF-03, FPF-04, FPF-05, ORG-04
**Success Criteria** (what must be TRUE):
  1. User can type `/privacy [question]` and receive a structured, professional-grade answer
  2. Answers about FPF topics cite FPF as the primary source with organization name and URL
  3. Every answer includes a legal disclaimer stating the skill assists research, not legal advice
  4. The skill can answer questions about FPF publication types, issue areas, and major programs from its built-in knowledge without web fetching
  5. SKILL.md stays under 500 lines and dispatches to reference files that load on demand
**Plans**: 2 plans

Plans:
- [ ] 01-01-PLAN.md — Create reference files (skill-behaviors.md + fpf-reference.md)
- [ ] 01-02-PLAN.md — Create SKILL.md routing layer + verify complete skill

### Phase 2: Regulation Knowledge Base
**Goal**: Privacy professionals can get instant, accurate answers to common regulation questions without any web fetching
**Depends on**: Phase 1
**Requirements**: REG-01, REG-02, REG-03, REG-04, REG-05, REG-06, REG-07, REG-08, DEPTH-01
**Success Criteria** (what must be TRUE):
  1. User asking "What does COPPA require?" gets a structured answer from static knowledge covering key provisions, without triggering web fetching
  2. User can ask for a comparison between two regulations (e.g., GDPR vs CCPA on consent) and receive a structured side-by-side response
  3. User asking about regulatory deadlines or effective dates gets accurate timeline information with date-stamps indicating when the data was last verified
  4. All six major regulations (GDPR, CCPA/CPRA, COPPA, HIPAA, FERPA, EU AI Act) have quick-reference coverage with key provisions
**Plans**: 4 plans

Plans:
- [ ] 02-01-PLAN.md — Create GDPR and CCPA/CPRA quick-reference files
- [ ] 02-02-PLAN.md — Create COPPA, HIPAA, and FERPA quick-reference files
- [ ] 02-03-PLAN.md — Create EU AI Act quick-reference file (privacy lens)
- [ ] 02-04-PLAN.md — Create cross-reference, timeline, and update SKILL.md routing

### Phase 3: Organization Catalog + Government Sources
**Goal**: Privacy professionals can discover and navigate the full ecosystem of privacy organizations, government regulators, and academic centers through source-aware guidance
**Depends on**: Phase 1
**Requirements**: ORG-01, ORG-02, ORG-03, ORG-05, ORG-06
**Success Criteria** (what must be TRUE):
  1. User asking "Where can I find IAPP's enforcement tracker?" gets a response with the specific URL pattern, site section, and search strategy for IAPP
  2. Navigation guides exist for at least 8 major sources (FPF, IAPP, EPIC, CPPA, CDT, FTC, EDPB, ICO) with tested URL patterns and content organization
  3. User asking about a government regulator (e.g., "What enforcement powers does the FTC have over privacy?") gets a response covering jurisdiction, powers, and key enforcement areas
  4. User asking "What privacy think tanks publish research on AI governance?" gets a response listing relevant academic centers and think tanks with their focus areas
**Plans**: 4 plans

Plans:
- [ ] 03-01-PLAN.md — Create advocacy organization catalog + IAPP navigation guide
- [ ] 03-02-PLAN.md — Create government regulator catalog + CPPA and FTC navigation guides
- [ ] 03-03-PLAN.md — Create EDPB, ICO, EPIC, and CDT navigation guides
- [ ] 03-04-PLAN.md — Create academic centers catalog + update SKILL.md organization routing

### Phase 4: Deep Research + Validation
**Goal**: Privacy professionals can conduct multi-source deep research queries that synthesize live information across organizations, with reliable fallback when web access fails
**Depends on**: Phase 1, Phase 2, Phase 3
**Requirements**: ARCH-04, ARCH-05, DEPTH-02
**Success Criteria** (what must be TRUE):
  1. User asking a deep research question (e.g., "Current state of children's privacy law") gets a synthesized answer drawing from multiple sources via live fetching, with each claim attributed to its source
  2. When web fetching is unavailable or fails for specific sources, the skill falls back to static knowledge and clearly indicates which information is from cached knowledge versus live sources
  3. The skill correctly routes between quick lookup mode (static-only, fast) and deep research mode (multi-source live fetching) based on query complexity
**Plans**: TBD

Plans:
- [ ] 04-01: TBD

## Progress

**Execution Order:**
Phases execute in numeric order: 1 -> 2 -> 3 -> 4
Note: Phase 2 and Phase 3 have no dependency on each other and could theoretically execute in either order, but Phase 2 first ensures the static fallback exists before expanding live-fetch sources.

| Phase | Plans Complete | Status | Completed |
|-------|----------------|--------|-----------|
| 1. Skill Foundation + FPF Primary Source | 0/2 | Planning complete | - |
| 2. Regulation Knowledge Base | 0/4 | Planning complete | - |
| 3. Organization Catalog + Government Sources | 0/4 | Planning complete | - |
| 4. Deep Research + Validation | 0/1 | Not started | - |
