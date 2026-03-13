# Phase 3: Organization Catalog + Government Sources - Context

**Gathered:** 2026-03-13
**Status:** Ready for planning

<domain>
## Phase Boundary

Expand the privacy skill from FPF-only to the full privacy ecosystem: 15-20 organizations, government regulators, and academic centers. Each source gets a catalog entry; the top 8 get detailed navigation guides with tested URL patterns. Update SKILL.md routing to detect org/regulator queries and dispatch to appropriate files. This phase creates the "where to look" layer — Phase 4 will wire up the "go fetch" capability using these navigation guides.

</domain>

<decisions>
## Implementation Decisions

### File Organization
- Three grouped catalog files by type: advocacy-orgs.md, gov-regulators.md, academic-centers.md
- Each catalog file contains structured summary entries for all orgs in that category
- Top 8 orgs get separate nav guide files (iapp-nav.md, epic-nav.md, cppa-nav.md, cdt-nav.md, ftc-nav.md, edpb-nav.md, ico-nav.md) — FPF keeps existing fpf-reference.md as-is
- Orgs with nav guides also get enforcement/profile entries in their catalog file — catalog files are self-contained references, nav guides are site-specific navigation tools
- No refactoring of fpf-reference.md — it serves a dual knowledge + navigation role unique to the primary source

### Catalog Entry Format
- Structured summary per org: name, focus area (1-2 sentences), website URL, key resource types (reports, tools, databases), and 1-2 notable resources worth knowing about
- Enough for the skill to cite and route to them, not enough to navigate their site
- Catalog files are loadable as standalone references without nav guides

### Navigation Guide Structure
- All 7 nav guides follow a consistent template: Site Overview, URL Patterns, Key URLs, Key Sections, Content Types, Search Strategy, Tips, WebFetch Notes
- Template adapted per source (e.g., regulators have guidance documents and enforcement databases instead of blog posts) but same skeleton
- URL patterns documented as structural patterns (e.g., iapp.org/resources/article/{slug}) PLUS 3-5 specific high-value URLs for known important resources
- WebFetch compatibility notes included: server-side vs JS rendering, rate limits, known scraping behavior
- URLs tested via WebFetch during creation — not deferred to Phase 4

### Government Regulators
- Enforcement-focused profiles in gov-regulators.md: jurisdiction scope, enforcement powers/tools, key enforcement areas/priorities, complaint filing, notable recent actions
- Covers FTC, EDPB, ICO, CPPA, CNIL as individual entries
- State AGs covered as a general overview section (not per-state): role, most active states (CA, NY, TX, CT, CO), powers, multi-state coalition trends
- 4 regulators with nav guides (FTC, EDPB, ICO, CPPA) get both profile in gov-regulators.md AND separate nav guide files
- CNIL gets profile in gov-regulators.md but no separate nav guide

### SKILL.md Routing
- New Step 4: Organization Routing — query-intent detection, not just keyword matching
- Routes based on what user is asking for: org name mentions load nav guide + catalog; "where can I find..." loads relevant catalog + matching nav guides; enforcement questions load gov-regulators.md
- All 4 routing steps (behaviors, FPF, regulation, organization) are independent and additive — when a query triggers multiple steps, all fire
- Routing table inline in SKILL.md (estimated ~320/500 lines after additions, ~180 lines headroom for Phase 4)
- Add 3-4 org-focused example queries to existing examples section (org navigation, regulator enforcement, academic research)

### Claude's Discretion
- Which 15-20 organizations to include beyond the named ones (IAPP, EPIC, CPPA, CDT, EFF, Access Now, etc.)
- Which academic centers and think tanks beyond the named ones (Georgetown, Berkman Klein, Stanford HAI, Brookings)
- Internal ordering of entries within each catalog file
- Exact wording of WebFetch compatibility notes per source
- How to handle orgs that span categories (e.g., CDT does both advocacy and research)

</decisions>

<specifics>
## Specific Ideas

- Nav guides should be practically useful for Phase 4's WebFetch integration — they're not just documentation, they're instructions for the LLM to navigate these sites
- The skill should be able to answer "Where can I find IAPP's enforcement tracker?" with the specific URL, not just "check iapp.org"
- Regulator profiles complement regulation files: Phase 2 covers "what the law requires," Phase 3 covers "who enforces and how"
- State AGs overview should mention the multi-state coalition trend since that's increasingly how enforcement happens

</specifics>

<code_context>
## Existing Code Insights

### Reusable Assets
- SKILL.md (220 lines): existing routing layer with Steps 1-3 (behaviors, FPF, regulation) — needs Step 4 for organization routing
- fpf-reference.md: FPF knowledge + navigation combined — serves as the model for what a nav guide covers, though new nav guides are navigation-only (no knowledge base content)
- skill-behaviors.md: response formatting, attribution, anti-hallucination — governs responses for org queries too
- 6 regulation reference files: enforcement sections in these files will be cross-referenced by regulator profiles

### Established Patterns
- Reference files loaded on-demand via SKILL.md routing (progressive disclosure)
- Keyword detection tables in SKILL.md for regulation routing — org routing uses intent detection instead
- FPF coverage quick-reference list for fast relevance detection
- One file per domain entity (regulation files) — org catalog uses grouped-by-type instead

### Integration Points
- SKILL.md Step 4 runs after Steps 1-3, all steps are additive
- Nav guide files referenced from catalog entries ("See iapp-nav.md for navigation guide")
- Gov-regulators.md cross-references Phase 2 regulation files for enforcement overlap
- Nav guide WebFetch notes prepare Phase 4 integration

</code_context>

<deferred>
## Deferred Ideas

None — discussion stayed within phase scope

</deferred>

---

*Phase: 03-organization-catalog-government-sources*
*Context gathered: 2026-03-13*
