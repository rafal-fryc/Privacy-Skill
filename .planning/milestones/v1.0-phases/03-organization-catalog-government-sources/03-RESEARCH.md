# Phase 3: Organization Catalog + Government Sources - Research

**Researched:** 2026-03-13
**Domain:** Privacy ecosystem knowledge base -- organization catalog, government regulator profiles, academic center directory, navigation guides, SKILL.md routing
**Confidence:** HIGH

## Summary

Phase 3 expands the privacy skill from FPF-only to the full privacy ecosystem. The work is entirely content authorship -- no code, no libraries, no build systems. The deliverables are structured markdown files following established patterns from Phases 1 and 2: catalog files (grouped by type), navigation guide files (per top source), government regulator profiles, and SKILL.md routing updates.

The primary technical risk is SKILL.md line budget. At 220 lines currently, adding Step 4 (Organization Routing) with intent-detection routing, a routing table, and 3-4 example queries must stay under ~320 lines to preserve ~180 lines of headroom for Phase 4. This is achievable given that regulation routing (Step 3) uses ~50 lines for keywords + rules + examples.

WebFetch compatibility testing reveals that most target sites render server-side and are accessible, but several (epic.org, cdt.org, ftc.gov) block automated access with 403 errors or Cloudflare protection. Navigation guides must document these constraints honestly for Phase 4 integration.

**Primary recommendation:** Follow the file structure from CONTEXT.md exactly -- three catalog files, seven nav guides, SKILL.md Step 4 addition. Test every URL via WebFetch during creation. Budget nav guides at roughly equal length for consistency.

<user_constraints>
## User Constraints (from CONTEXT.md)

### Locked Decisions
- Three grouped catalog files by type: advocacy-orgs.md, gov-regulators.md, academic-centers.md
- Each catalog file contains structured summary entries for all orgs in that category
- Top 8 orgs get separate nav guide files (iapp-nav.md, epic-nav.md, cppa-nav.md, cdt-nav.md, ftc-nav.md, edpb-nav.md, ico-nav.md) -- FPF keeps existing fpf-reference.md as-is
- Orgs with nav guides also get enforcement/profile entries in their catalog file -- catalog files are self-contained references, nav guides are site-specific navigation tools
- No refactoring of fpf-reference.md
- Catalog entry format: name, focus area (1-2 sentences), website URL, key resource types, 1-2 notable resources
- All 7 nav guides follow consistent template: Site Overview, URL Patterns, Key URLs, Key Sections, Content Types, Search Strategy, Tips, WebFetch Notes
- URL patterns documented as structural patterns PLUS 3-5 specific high-value URLs
- WebFetch compatibility notes included; URLs tested via WebFetch during creation
- Government regulators: enforcement-focused profiles with jurisdiction, powers, enforcement areas, complaint filing, notable actions
- Covers FTC, EDPB, ICO, CPPA, CNIL as individual entries; state AGs as general overview section
- 4 regulators with nav guides (FTC, EDPB, ICO, CPPA); CNIL gets profile only
- SKILL.md Step 4: Organization Routing with query-intent detection (not keyword matching)
- All 4 routing steps independent and additive
- Routing table inline in SKILL.md (~320/500 lines target, ~180 lines headroom for Phase 4)
- 3-4 org-focused example queries added to existing examples section

### Claude's Discretion
- Which 15-20 organizations to include beyond the named ones (IAPP, EPIC, CPPA, CDT, EFF, Access Now, etc.)
- Which academic centers and think tanks beyond the named ones (Georgetown, Berkman Klein, Stanford HAI, Brookings)
- Internal ordering of entries within each catalog file
- Exact wording of WebFetch compatibility notes per source
- How to handle orgs that span categories (e.g., CDT does both advocacy and research)

### Deferred Ideas (OUT OF SCOPE)
None -- discussion stayed within phase scope
</user_constraints>

<phase_requirements>
## Phase Requirements

| ID | Description | Research Support |
|----|-------------|-----------------|
| ORG-01 | Skill catalogs 15-20 major privacy organizations with name, focus area, website, and key resource types | Catalog files (advocacy-orgs.md, gov-regulators.md, academic-centers.md) with structured entries per CONTEXT.md format. Research identified 18-20 candidate organizations across all three categories. |
| ORG-02 | Navigation guides exist for top 8 sources (FPF, IAPP, EPIC, CalPrivacy/CPPA, CDT, FTC, EDPB, ICO) with URL patterns and search strategies | FPF already has fpf-reference.md (existing). Seven new nav guide files following consistent template. WebFetch testing reveals site accessibility varies -- documented per source. |
| ORG-03 | Each navigation guide contains site-specific URL patterns, content organization, key sections, and search tips | Research gathered URL patterns, site structures, and content organization for all 7 sources via WebFetch and WebSearch. Template structure defined in CONTEXT.md. |
| ORG-05 | Government regulator directory covers FTC, EDPB, ICO, CNIL, state AGs with jurisdiction and powers | gov-regulators.md with enforcement-focused profiles. Research captured jurisdiction, powers, enforcement priorities, recent actions, and complaint filing for all 5 entities plus state AG overview. |
| ORG-06 | Think tank and academic center catalog includes Georgetown Privacy Center, Berkman Klein, Stanford HAI, Brookings, and others | academic-centers.md with structured entries. Research identified 6-8 candidate institutions with focus areas and key outputs. |
</phase_requirements>

## Standard Stack

This phase involves no code, no libraries, no package management. All deliverables are markdown files added to the existing Claude Code skill directory.

### Core
| Asset | Type | Purpose | Why Standard |
|-------|------|---------|--------------|
| Markdown files | Content | Catalog entries, nav guides, regulator profiles | Established pattern from Phases 1-2 |
| SKILL.md routing | Content | Query dispatch to reference files | Existing architecture pattern |

### File Inventory (New Files)
| File | Type | Approximate Size |
|------|------|-----------------|
| advocacy-orgs.md | Catalog | ~150-200 lines |
| gov-regulators.md | Catalog + profiles | ~250-350 lines |
| academic-centers.md | Catalog | ~100-150 lines |
| iapp-nav.md | Navigation guide | ~150-200 lines |
| epic-nav.md | Navigation guide | ~120-160 lines |
| cppa-nav.md | Navigation guide | ~120-160 lines |
| cdt-nav.md | Navigation guide | ~120-160 lines |
| ftc-nav.md | Navigation guide | ~150-200 lines |
| edpb-nav.md | Navigation guide | ~150-200 lines |
| ico-nav.md | Navigation guide | ~120-160 lines |

### Files Modified
| File | Change | Impact |
|------|--------|--------|
| SKILL.md | Add Step 4 (Organization Routing), 3-4 example queries, update Reference Files section, bump version | ~100 lines added (220 -> ~320) |

## Architecture Patterns

### Established Patterns to Follow

**1. Progressive Disclosure (from Phase 1)**
Reference files loaded on-demand via SKILL.md routing. Catalog files and nav guides are only loaded when organization-related queries are detected. Zero tokens at rest.

**2. Grouped Reference Files (from Phase 2)**
Phase 2 used individual files per regulation. Phase 3 uses grouped catalog files by type (advocacy, government, academic) because individual catalog entries are short summaries, not full knowledge bases. Nav guides get individual files because they are longer and loaded selectively.

**3. Routing Table Pattern (from Phase 2 Step 3)**
Step 3 uses a keyword-to-file mapping table. Step 4 uses intent-detection instead of keyword matching because organization queries are more diverse ("Where can I find...", org name mentions, enforcement questions). The table maps query intents to file loading decisions.

**4. Nav Guide Template (adapted from fpf-reference.md Section 6)**
fpf-reference.md combines knowledge base + navigation in one file. New nav guides are navigation-only (the catalog files provide the knowledge base). The nav guide template sections:

```
# [Organization] Navigation Guide

## Site Overview
[1-2 paragraphs: what the site contains, primary audience, content model]

## URL Patterns
[Table: content type, URL pattern, example]

## Key URLs
[3-5 specific high-value URLs with descriptions]

## Key Sections
[Site's main content areas with descriptions]

## Content Types
[What kinds of documents/resources the site publishes]

## Search Strategy
[How to find specific content on this site]

## Tips
[Practical tips for navigating or using the site effectively]

## WebFetch Notes
[Accessibility from WebFetch: server-side rendering, JS requirements, rate limits, known blocks]
```

**5. Catalog Entry Format (new pattern)**
```markdown
### [Organization Name]
**Focus:** [1-2 sentences]
**Website:** [URL]
**Key resources:** [resource types]
**Notable:** [1-2 specific noteworthy resources or tools]
```

**6. Government Regulator Profile Format (new pattern)**
```markdown
### [Regulator Name]
**Jurisdiction:** [geographic and legal scope]
**Governing law:** [primary legislation enforced]
**Enforcement powers:** [tools available]
**Key enforcement areas:** [current priorities]
**Complaint filing:** [how to file, URL]
**Notable recent actions:** [1-2 significant cases]
```

### Recommended File Structure
```
.claude/skills/privacy/
  SKILL.md                    # Updated with Step 4
  skill-behaviors.md          # Unchanged
  fpf-reference.md            # Unchanged
  [6 regulation files]        # Unchanged
  reg-cross-reference.md      # Unchanged
  reg-timeline.md             # Unchanged
  advocacy-orgs.md            # NEW -- catalog
  gov-regulators.md           # NEW -- catalog + profiles
  academic-centers.md         # NEW -- catalog
  iapp-nav.md                 # NEW -- navigation guide
  epic-nav.md                 # NEW -- navigation guide
  cppa-nav.md                 # NEW -- navigation guide
  cdt-nav.md                  # NEW -- navigation guide
  ftc-nav.md                  # NEW -- navigation guide
  edpb-nav.md                 # NEW -- navigation guide
  ico-nav.md                  # NEW -- navigation guide
```

### Anti-Patterns to Avoid
- **Duplicating knowledge across catalog and nav guide:** Catalog entries give the "what" (org summary); nav guides give the "how" (site navigation). Do not repeat org descriptions in nav guides beyond a brief overview.
- **Inventing URLs:** Only include URLs that have been verified via WebFetch or WebSearch. If a URL cannot be verified, document it with a caveat.
- **Over-loading SKILL.md:** The routing table should be concise -- intent patterns mapped to file loads, not detailed descriptions of each organization.
- **Keyword-only routing for Step 4:** Organization queries require intent detection ("Where can I find...", "Who enforces...", "What organizations work on...") not just keyword matching on org names.

## Don't Hand-Roll

| Problem | Don't Build | Use Instead | Why |
|---------|-------------|-------------|-----|
| URL verification | Manual URL checking | WebFetch during file creation | URLs must be tested for Phase 4 compatibility |
| Org research | Training data only | WebSearch + WebFetch verification | Organization details change; need current info |
| Enforcement data | Summarizing enforcement history from memory | Authoritative sources (IAPP enforcement DB, FTC case library) | Enforcement facts require HIGH verification per skill-behaviors.md |

## Common Pitfalls

### Pitfall 1: URL Rot in Navigation Guides
**What goes wrong:** URLs included in nav guides become invalid, leading to broken navigation in Phase 4.
**Why it happens:** Government and organization websites restructure frequently. Individual article URLs are particularly unstable.
**How to avoid:** Prefer structural/section URLs over individual page URLs. Document URL patterns rather than exhaustive URL lists. Favor URLs verified via WebFetch during creation.
**Warning signs:** WebFetch returning 404 or redirect chains during testing.

### Pitfall 2: SKILL.md Line Budget Overrun
**What goes wrong:** Adding Step 4 routing, routing table, example queries, and Reference Files updates pushes SKILL.md past the ~320 line target or uncomfortably close to 500.
**Why it happens:** Intent-detection routing requires more explanation than simple keyword matching. Example queries add ~15-20 lines each.
**How to avoid:** Keep routing table compact. Use 3 example queries, not 4. Keep intent descriptions to one line each. Reference Files list can be condensed using category headers.
**Warning signs:** Draft Step 4 exceeding 60 lines before examples.

### Pitfall 3: WebFetch Blocked Sites
**What goes wrong:** Nav guides promise WebFetch capability for sites that actually block automated access.
**Why it happens:** Sites like epic.org (timeout), cdt.org (Cloudflare), ftc.gov (403) block non-browser access.
**How to avoid:** Test every site via WebFetch during nav guide creation. Document blocks honestly in WebFetch Notes. For blocked sites, nav guides still provide value for manual navigation guidance.
**Warning signs:** WebFetch returning 403, timeout, or Cloudflare challenge pages.

### Pitfall 4: Inconsistent Catalog Depth
**What goes wrong:** Some catalog entries are detailed paragraphs while others are single lines, creating uneven quality.
**Why it happens:** More information is available about well-known orgs (IAPP, EFF) than smaller ones.
**How to avoid:** Stick to the fixed format from CONTEXT.md: name, focus (1-2 sentences), website, key resource types, notable resources. Same depth for every entry.
**Warning signs:** Catalog entries varying from 3 lines to 15 lines.

### Pitfall 5: Regulator Profiles Overlapping Phase 2 Regulation Files
**What goes wrong:** gov-regulators.md repeats what GDPR, CCPA regulation files already cover, creating maintenance burden.
**Why it happens:** Enforcement is discussed in regulation files (fines, penalties) and regulator profiles (enforcement powers, priorities).
**How to avoid:** Regulation files cover "what the law requires." Regulator profiles cover "who enforces and how." Cross-reference rather than duplicate. E.g., "For GDPR provisions, see gdpr-reference.md."
**Warning signs:** Regulator profiles explaining specific statutory provisions rather than enforcement behavior.

## Code Examples

These are content templates, not code -- but they serve the same purpose of showing the exact format to follow.

### Catalog Entry Example (advocacy-orgs.md)
```markdown
### International Association of Privacy Professionals (IAPP)
**Focus:** The world's largest privacy professional organization, providing certification (CIPP, CIPM, CIPT), training, and industry resources for privacy, AI governance, and digital responsibility practitioners.
**Website:** [iapp.org](https://iapp.org)
**Key resources:** Certification programs, Global Privacy and Data Protection Enforcement Database, US State Privacy Legislation Tracker, tools and trackers, research articles, web conferences
**Notable:** The [Global Enforcement Database](https://iapp.org/resources/global-privacy-and-data-protection-enforcement-database/) catalogs enforcement actions worldwide. The [US State Privacy Legislation Tracker](https://iapp.org/resources/article/us-state-privacy-legislation-tracker/) monitors comprehensive state privacy bills.

> See [iapp-nav.md](iapp-nav.md) for site navigation guide.
```

### Navigation Guide Template Example (excerpt)
```markdown
# IAPP Navigation Guide

## Site Overview

IAPP (International Association of Privacy Professionals) is the world's largest privacy professional organization. The site serves as both a membership portal and a public resource hub for privacy, AI governance, and digital responsibility content.

## URL Patterns

| Content Type | URL Pattern | Example |
|---|---|---|
| Resource articles | `iapp.org/resources/article/{slug}/` | `iapp.org/resources/article/us-state-privacy-legislation-tracker/` |
| Topic collections | `iapp.org/resources/topics/{topic}/` | `iapp.org/resources/topics/enforcement/` |
| News articles | `iapp.org/news/a/{slug}` | — |
| Tools and trackers | `iapp.org/resources/article/iapp-tools-and-trackers/` | — |
| Enforcement database | `iapp.org/resources/global-privacy-and-data-protection-enforcement-database/` | — |

## Key URLs

- **Enforcement Database:** https://iapp.org/resources/global-privacy-and-data-protection-enforcement-database/ -- Global enforcement actions searchable database
- **US State Privacy Tracker:** https://iapp.org/resources/article/us-state-privacy-legislation-tracker/ -- Comprehensive state privacy bill tracker
- **Tools and Trackers Hub:** https://iapp.org/resources/article/iapp-tools-and-trackers/ -- Central listing of all IAPP tools
- **Resource Center:** https://iapp.org/resources -- Main resource hub with search

## WebFetch Notes

IAPP's main pages render server-side and are accessible via WebFetch. Resource article pages load content successfully. The site uses a member portal (myiapp.org) for gated content -- WebFetch can access public pages but not member-only resources. Search functionality available at the resource center.
```

### Government Regulator Profile Example (gov-regulators.md)
```markdown
### Federal Trade Commission (FTC)
**Jurisdiction:** United States (federal). Enforces consumer protection laws including privacy and data security provisions under Section 5 of the FTC Act (unfair or deceptive acts or practices), COPPA, FCRA, Health Breach Notification Rule, and other sector-specific statutes.
**Enforcement powers:** Administrative complaints, consent decrees, civil penalties (COPPA violations up to $50,120 per violation), monetary redress, injunctive relief, 20-year compliance orders with monitoring, referral to DOJ for federal court enforcement.
**Key enforcement areas (2025-2026):** Youth privacy and COPPA enforcement, health data and Health Breach Notification Rule, data broker practices, commercial surveillance, AI-related deception, dark patterns.
**Complaint filing:** [ftc.gov/complaint](https://www.ftc.gov/complaint)
**Notable recent actions:** Disney/Epic Games $10M settlement for children's data collection; GM/OnStar consent order for geolocation data practices; Avast settlement for deceptive privacy claims.

> For FTC site navigation, see [ftc-nav.md](ftc-nav.md). For COPPA provisions, see [coppa-reference.md](coppa-reference.md).
```

### SKILL.md Step 4 Routing Example
```markdown
### Step 4: Determine Organization Relevance (CONDITIONAL)

Assess whether the query involves a privacy organization, government regulator, or academic center. This step uses intent detection rather than keyword matching -- look at what the user is asking for, not just which words appear.

**Organization routing triggers:**

| Query Intent | Load Files | Examples |
|---|---|---|
| Org name mention + navigation need | Relevant nav guide + catalog file | "Where can I find IAPP's enforcement tracker?" |
| "Where can I find..." + privacy resource | Relevant catalog file(s) + matching nav guides | "Where can I find enforcement action data?" |
| Enforcement/regulator question | gov-regulators.md + relevant nav guide(s) | "Who enforces GDPR?", "What powers does the FTC have?" |
| Organization comparison or overview | Relevant catalog file(s) | "What organizations work on children's privacy?" |
| Academic/research institution query | academic-centers.md | "What privacy research does Georgetown do?" |

**File loading rules:**
- When a specific org is named and has a nav guide, load both the nav guide and the parent catalog file.
- When the query is broad ("privacy organizations"), load all relevant catalog files.
- Gov-regulators.md is loaded for any enforcement, regulator, or jurisdiction question.
- Academic-centers.md is loaded for research institution, think tank, or academic privacy queries.
- This step runs independently of Steps 2 and 3 -- all routing decisions are additive.
```

## State of the Art

### WebFetch Compatibility Results (tested March 2026)

| Site | WebFetch Status | Rendering | Notes |
|------|----------------|-----------|-------|
| iapp.org | Accessible | Server-side | Public pages load; member content gated |
| epic.org | TIMEOUT | Unknown | Connection timeout -- likely rate limiting or JS-heavy |
| cdt.org | BLOCKED | Cloudflare | Security challenge blocks automated access |
| cppa.ca.gov | Accessible | Server-side | Clean HTML, all pages load |
| ftc.gov | BLOCKED (403) | Server-side | Blocks non-browser User-Agent on many pages |
| edpb.europa.eu | Accessible | Server-side | Multi-language; append `_en` for English |
| ico.org.uk | Accessible | Server-side | Clean HTML, guidance pages load |

### Organization Landscape (Current as of March 2026)

**Advocacy Organizations (recommended 8-10 for catalog):**
- IAPP -- Professional association, certifications, tools, trackers
- EPIC -- Public interest research, litigation, advocacy
- EFF -- Digital rights, litigation, tools (Privacy Badger, Certbot)
- CDT -- Nonpartisan, policy research, DC + Brussels + SF
- Access Now -- International digital rights, RightsCon, Digital Security Helpline
- Privacy International -- UK-based, global surveillance and privacy rights
- Privacy Rights Clearinghouse -- Consumer privacy, Data Breach Chronology database
- ACLU (Privacy & Technology) -- Civil liberties, litigation, policy advocacy
- Public Knowledge -- Broadband privacy, telecom policy (smaller scope)

**Government Regulators (5 individual + state AG overview per CONTEXT.md):**
- FTC -- U.S. federal, Section 5, COPPA, Health Breach Notification Rule
- EDPB -- EU-wide, GDPR coordination, guidelines, binding decisions
- ICO -- UK, UK GDPR + DPA 2018, enforcement notices, guidance
- CPPA -- California, CCPA/CPRA enforcement, rulemaking, DELETE Act/DROP
- CNIL -- France, GDPR enforcement, 2025-2028 strategic priorities (AI, children, health)
- State AGs -- Consortium of 9 states, GPC enforcement sweeps, multi-state coalitions

**Academic Centers and Think Tanks (recommended 6-8 for catalog):**
- Georgetown Center on Privacy and Technology -- Surveillance, marginalized communities, empirical research
- Berkman Klein Center (Harvard) -- Internet & society, Privacy Tools Project, privacy & security
- Stanford HAI -- Human-centered AI, AI Index Report, privacy policy research
- Brookings Institution -- AI governance, technology policy, regulatory frameworks
- Stanford Center for Internet and Society -- Internet law, intermediary liability, privacy
- RAND Corporation -- Health information privacy, research privacy
- CSET Georgetown -- AI security implications, data-driven policy analysis
- Pew Research Center -- Public opinion polling on privacy and technology attitudes

### Key URL Patterns Verified

| Organization | Pattern | Verified |
|---|---|---|
| IAPP | `iapp.org/resources/article/{slug}/` | Yes |
| IAPP | `iapp.org/resources/topics/{topic}/` | Yes |
| IAPP | `iapp.org/resources/global-privacy-and-data-protection-enforcement-database/` | Yes |
| EDPB | `edpb.europa.eu/our-work-tools/general-guidance/guidelines-recommendations-best-practices_en` | Yes (WebFetch) |
| EDPB | `edpb.europa.eu/our-work-tools/documents/our-documents_en` | Yes |
| EDPB | `edpb.europa.eu/our-work-tools/consistency-findings/opinions_en` | Yes |
| ICO | `ico.org.uk/for-organisations/` | Yes (WebFetch) |
| ICO | `ico.org.uk/action-weve-taken/enforcement/` | Yes |
| CPPA | `cppa.ca.gov/regulations/` | Yes (WebFetch) |
| CPPA | `cppa.ca.gov/regulations/consumer_privacy_act.html` | Yes |
| CPPA | `cppa.ca.gov/data_broker_registry` | Yes |
| FTC | `ftc.gov/business-guidance/privacy-security` | Yes (WebSearch, not WebFetch) |
| FTC | `ftc.gov/legal-library/browse/cases-proceedings` | Yes (WebSearch, not WebFetch) |
| FTC | `ftc.gov/news-events/topics/protecting-consumer-privacy-security/privacy-security-enforcement` | Yes (WebSearch) |
| CDT | `cdt.org/areas-of-focus/` | Yes (WebSearch, not WebFetch) |
| CDT | `cdt.org/area-of-focus/privacy-data/` | Yes (WebSearch) |
| EFF | `eff.org/issues/privacy` | Yes |
| EFF | `eff.org/issues/{issue-slug}` | Yes |
| EPIC | `epic.org/issues/` | Yes (WebSearch) |
| CNIL | `cnil.fr/en` | Yes |
| CNIL | `cnil.fr/en/investigation-powers-cnil/sanctions-issued-cnil` | Yes |

## Open Questions

1. **EPIC and CDT site accessibility for Phase 4**
   - What we know: Both sites block WebFetch (epic.org times out, cdt.org shows Cloudflare). Their content is still valuable for manual reference.
   - What's unclear: Whether these blocks are permanent or configuration-dependent. Future WebFetch improvements might resolve.
   - Recommendation: Document blocks in nav guide WebFetch Notes. Nav guides still provide value for manual navigation. Phase 4 can attempt with different approaches.

2. **FTC WebFetch workaround**
   - What we know: ftc.gov returns 403 on direct WebFetch. FTC content is available via IAPP's curated FTC resources.
   - What's unclear: Whether specific FTC URL paths are more permissive than others.
   - Recommendation: Test additional FTC URLs during nav guide creation. Document partial accessibility.

3. **Exact organization count**
   - What we know: Research identified ~20 candidates across all three categories. CONTEXT.md says "15-20."
   - What's unclear: Whether some orgs are too marginal to include (Public Knowledge, RAND).
   - Recommendation: Include 18-19 organizations. Better to be comprehensive within the 15-20 range. Marginal orgs get shorter catalog entries.

4. **Cross-category organizations**
   - What we know: CDT does both advocacy and research. CSET Georgetown is both academic and policy.
   - What's unclear: CONTEXT.md marks this as Claude's Discretion.
   - Recommendation: Place each org in its primary category. Add a cross-reference note ("Also relevant to [other category]") where applicable. Do not duplicate entries.

## Validation Architecture

### Test Framework
| Property | Value |
|----------|-------|
| Framework | Manual validation (content-only phase, no code) |
| Config file | None -- no automated test infrastructure applicable |
| Quick run command | Manual review of file structure and SKILL.md routing |
| Full suite command | End-to-end test: invoke `/privacy` with org-related queries |

### Phase Requirements to Test Map
| Req ID | Behavior | Test Type | Automated Command | File Exists? |
|--------|----------|-----------|-------------------|-------------|
| ORG-01 | 15-20 orgs cataloged with required fields | manual-only | Count entries in advocacy-orgs.md + gov-regulators.md + academic-centers.md | Wave 0 |
| ORG-02 | 8 nav guides exist (FPF + 7 new) | manual-only | Verify 7 new nav guide files created + fpf-reference.md exists | Wave 0 |
| ORG-03 | Nav guides contain URL patterns, content org, key sections, search tips | manual-only | Check each nav guide has all template sections | Wave 0 |
| ORG-05 | Gov regulator directory covers FTC, EDPB, ICO, CNIL, state AGs | manual-only | Verify gov-regulators.md has all 5 regulator entries + state AG section | Wave 0 |
| ORG-06 | Academic center catalog includes Georgetown, Berkman Klein, Stanford HAI, Brookings | manual-only | Verify academic-centers.md has required entries | Wave 0 |

**Manual-only justification:** This phase produces markdown content files for a Claude Code skill. There is no executable code, no API endpoints, no UI components. Validation is structural (files exist, contain required sections) and qualitative (content accuracy, URL validity). Automated testing is not applicable.

### Sampling Rate
- **Per task commit:** Verify new files created, count catalog entries, check nav guide sections
- **Per wave merge:** Full SKILL.md routing review, verify all cross-references resolve
- **Phase gate:** Invoke `/privacy` with test queries from each routing intent category

### Wave 0 Gaps
None -- no test infrastructure needed for content-only deliverables. Validation is structural review during implementation.

## Sources

### Primary (HIGH confidence)
- WebFetch of iapp.org -- site structure, content organization (tested successfully)
- WebFetch of edpb.europa.eu -- guidelines page, URL patterns, filtering (tested successfully)
- WebFetch of ico.org.uk -- site structure, guidance organization (tested successfully)
- WebFetch of cppa.ca.gov -- regulations page, URL patterns, content areas (tested successfully)
- Existing skill files (SKILL.md, fpf-reference.md, skill-behaviors.md) -- established patterns

### Secondary (MEDIUM confidence)
- WebSearch for IAPP resources URL patterns -- verified against multiple IAPP URLs
- WebSearch for FTC site structure -- verified via multiple law firm summaries and FTC page titles
- WebSearch for CDT areas of focus -- verified via Wikipedia, MacArthur Foundation, PSU analysis
- WebSearch for EDPB URL patterns -- verified via official EDPB pages
- WebSearch for CNIL enforcement powers -- verified via ICLG, Chambers, CNIL official pages
- WebSearch for state AG enforcement trends -- verified via multiple law firm analyses and FPF enforcement retrospective
- WebSearch for Georgetown, Berkman Klein, Stanford HAI, Brookings -- verified via institutional websites
- Georgetown Law Privacy Research Guide -- comprehensive list of NGOs, think tanks, and academic centers

### Tertiary (LOW confidence)
- WebSearch for Privacy International specifics -- limited to Wikipedia and general descriptions
- WebSearch for Access Now details -- based on Wikipedia and organizational self-descriptions
- EPIC site structure -- could not verify via WebFetch (timeout); relying on WebSearch results

## Metadata

**Confidence breakdown:**
- Standard stack: HIGH -- this is content authoring following established Phase 1-2 patterns
- Architecture: HIGH -- file organization, routing pattern, and template structure all decided in CONTEXT.md
- Pitfalls: HIGH -- WebFetch testing done empirically; SKILL.md budget calculated from current line count
- Organization data: MEDIUM -- organization details verified via WebSearch and WebFetch where possible, but org websites change

**Research date:** 2026-03-13
**Valid until:** 2026-04-13 (30 days -- stable domain; org websites may restructure but structural patterns persist)
