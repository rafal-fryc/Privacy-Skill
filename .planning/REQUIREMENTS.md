# Requirements: FPF Privacy Research Skill

**Defined:** 2026-03-12
**Core Value:** When a privacy professional asks a question, the skill knows exactly where to look, how to navigate each source, and prioritizes FPF first.

## v1 Requirements

### FPF Primary Source

- [x] **FPF-01**: Skill indexes all 6 FPF publication types (Reports, White Papers, Filings, Infographics, Blog Posts, Videos) with counts and descriptions
- [x] **FPF-02**: Skill indexes 20+ FPF issue areas (U.S. Legislation, Global, AI, Youth Privacy, Health, etc.) with resource counts
- [x] **FPF-03**: FPF navigation guide contains actual fpf.org URL patterns, content taxonomy, and tested search strategies
- [x] **FPF-04**: FPF is cited first when the query topic falls within FPF's coverage areas
- [x] **FPF-05**: Skill knows major FPF programs (Center for AI, Youth Privacy, Privacy Papers for Policymakers, DC Privacy Forum, Training Program)

### Organization Catalog

- [ ] **ORG-01**: Skill catalogs 15-20 major privacy organizations with name, focus area, website, and key resource types
- [ ] **ORG-02**: Navigation guides exist for top 8 sources (FPF, IAPP, EPIC, CalPrivacy/CPPA, CDT, FTC, EDPB, ICO) with URL patterns and search strategies
- [ ] **ORG-03**: Each navigation guide contains site-specific URL patterns, content organization, key sections, and search tips
- [x] **ORG-04**: Source attribution appears in every answer with organization name and ideally URL
- [ ] **ORG-05**: Government regulator directory covers FTC, EDPB, ICO, CNIL, state AGs with jurisdiction and powers
- [ ] **ORG-06**: Think tank and academic center catalog includes Georgetown Privacy Center, Berkman Klein, Stanford HAI, Brookings, and others

### Knowledge Base

- [ ] **REG-01**: Quick reference covers GDPR key provisions (lawful basis, data subject rights, breach notification, DPO, international transfers)
- [ ] **REG-02**: Quick reference covers CCPA/CPRA key provisions (consumer rights, opt-out, service provider requirements, timelines)
- [ ] **REG-03**: Quick reference covers COPPA key provisions (parental consent, operator obligations, safe harbor)
- [ ] **REG-04**: Quick reference covers HIPAA privacy provisions (covered entities, PHI, minimum necessary, BAAs)
- [ ] **REG-05**: Quick reference covers FERPA key provisions (education records, directory information, consent)
- [x] **REG-06**: Quick reference covers EU AI Act key provisions (risk tiers, prohibited practices, timeline)
- [ ] **REG-07**: Regulation cross-reference enables side-by-side comparison of major frameworks on common dimensions (consent, rights, enforcement, penalties)
- [ ] **REG-08**: Regulatory timeline tracks key effective dates, comment periods, and enforcement deadlines for major laws

### Skill Architecture

- [x] **ARCH-01**: Skill triggers via `/privacy` command with natural language queries
- [x] **ARCH-02**: SKILL.md acts as routing layer under 500 lines, dispatching to reference files
- [x] **ARCH-03**: Reference files use progressive disclosure (loaded on-demand, zero tokens at rest)
- [ ] **ARCH-04**: Hybrid architecture: static knowledge for quick lookups, live WebFetch for deeper research
- [ ] **ARCH-05**: Graceful degradation when web access is unavailable (falls back to static knowledge)
- [x] **ARCH-06**: Professional-grade language assumes domain knowledge, uses precise legal/regulatory terminology
- [x] **ARCH-07**: Anti-hallucination instructions embedded; regulatory facts come from reference files, not training data
- [x] **ARCH-08**: Legal disclaimer in every output pathway stating skill assists research, not legal advice

### Research Depth

- [ ] **DEPTH-01**: Quick lookup mode answers common factual questions from static knowledge only
- [ ] **DEPTH-02**: Deep research mode performs multi-source live fetching using navigation guides and synthesizes across organizations

## v2 Requirements

### Extended Coverage

- **EXT-01**: Sector-specific privacy guides (health, fintech, edtech, adtech)
- **EXT-02**: State-by-state U.S. privacy law navigator
- **EXT-03**: International DPA coverage beyond EDPB/ICO/CNIL (APAC, Latin America, Africa)
- **EXT-04**: Multi-language support for non-English DPA resources

### Enhanced Features

- **ENH-01**: Enforcement action lookup via IAPP Enforcement Database navigation
- **ENH-02**: Expanded navigation guides for remaining cataloged organizations
- **ENH-03**: Privacy professional certification prep support (CIPP/US, CIPP/E, CIPM)

## Out of Scope

| Feature | Reason |
|---------|--------|
| Legal advice / compliance determinations | Liability risk; skill assists research only, not legal review |
| Exhaustive regulation text reproduction | Bloats responses; link to authoritative full text instead |
| Real-time regulatory alert monitoring | Claude Code skills cannot run persistently; recommend IAPP/OneTrust |
| Internal/proprietary FPF content | Skill accesses public content only |
| Case management / workflow automation | Wrong tool category; recommend OneTrust, TrustArc, BigID |
| All-jurisdiction depth (160+ countries) | Impossible to maintain accurately; cover major frameworks + pointers |
| Enforcement action database | IAPP maintains this authoritatively; provide navigation guide instead |

## Traceability

| Requirement | Phase | Status |
|-------------|-------|--------|
| FPF-01 | Phase 1 | Complete |
| FPF-02 | Phase 1 | Complete |
| FPF-03 | Phase 1 | Complete |
| FPF-04 | Phase 1 | Complete |
| FPF-05 | Phase 1 | Complete |
| ORG-01 | Phase 3 | Pending |
| ORG-02 | Phase 3 | Pending |
| ORG-03 | Phase 3 | Pending |
| ORG-04 | Phase 1 | Complete |
| ORG-05 | Phase 3 | Pending |
| ORG-06 | Phase 3 | Pending |
| REG-01 | Phase 2 | Pending |
| REG-02 | Phase 2 | Pending |
| REG-03 | Phase 2 | Pending |
| REG-04 | Phase 2 | Pending |
| REG-05 | Phase 2 | Pending |
| REG-06 | Phase 2 | Complete |
| REG-07 | Phase 2 | Pending |
| REG-08 | Phase 2 | Pending |
| ARCH-01 | Phase 1 | Complete |
| ARCH-02 | Phase 1 | Complete |
| ARCH-03 | Phase 1 | Complete |
| ARCH-04 | Phase 4 | Pending |
| ARCH-05 | Phase 4 | Pending |
| ARCH-06 | Phase 1 | Complete |
| ARCH-07 | Phase 1 | Complete |
| ARCH-08 | Phase 1 | Complete |
| DEPTH-01 | Phase 2 | Pending |
| DEPTH-02 | Phase 4 | Pending |

**Coverage:**
- v1 requirements: 29 total
- Mapped to phases: 29
- Unmapped: 0

---
*Requirements defined: 2026-03-12*
*Last updated: 2026-03-13 — FPF-01 corrected: "Events" replaced with "Blog Posts" per CONTEXT.md locked decision*
