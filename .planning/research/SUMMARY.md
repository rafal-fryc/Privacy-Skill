# Project Research Summary

**Project:** FPF Privacy Research Skill
**Domain:** Knowledge-heavy Claude Code skill (data privacy research)
**Researched:** 2026-03-12
**Confidence:** HIGH

## Executive Summary

This project is a Claude Code skill -- not a web application, not a database-backed service. The entire deliverable is a set of markdown files: one SKILL.md that acts as a routing layer, plus reference files containing domain knowledge and site navigation guides. The skill invokes via `/privacy` and serves privacy professionals (lawyers, compliance officers, policy analysts) who need efficient, source-aware research across the fragmented privacy ecosystem. Experts build knowledge-heavy skills using progressive disclosure: SKILL.md stays under 500 lines and acts as a dispatcher, while reference files load on-demand so the knowledge base can scale without burning context tokens on every invocation. FPF (Future of Privacy Forum) is the primary cited source, supplemented by 15-20 other organizations, government regulators, and a static knowledge base covering major regulations.

The recommended approach is a three-layer architecture: (1) SKILL.md as the routing/classification layer with source priority logic, (2) source navigation guide files organized by source type (FPF, other orgs, government) that teach Claude how to navigate each website, and (3) static knowledge files for quick regulation lookups. The hybrid static/live design handles 80% of queries from pre-baked content (fast, reliable) and uses WebFetch for the remaining 20% requiring depth or currency. This is the standard Anthropic-recommended pattern for knowledge-heavy skills, with one key innovation: per-source navigation guides that encode institutional knowledge about website structure, making WebFetch dramatically more effective than generic browsing.

The primary risks are: hallucinated legal citations (LLMs hallucinate 58-88% on legal specifics -- mitigated by embedding actual citation data in reference files and explicit anti-hallucination instructions), WebFetch failures on JavaScript-heavy or bot-blocking sites (mitigated by pre-launch compatibility testing and heavier static content for unreliable sources), content staleness in a rapidly evolving regulatory domain (mitigated by separating time-sensitive from stable content and date-stamping everything), and absent legal disclaimers creating liability exposure (mitigated by requiring disclaimers in every output pathway before any content is written). All four risks have straightforward prevention strategies but each becomes much harder to fix after launch.

## Key Findings

### Recommended Stack

There is no runtime stack. The "technology" is the Claude Code skill framework itself: SKILL.md with YAML frontmatter, markdown reference files, and Claude's built-in tools. No database, no web framework, no external dependencies.

**Core technologies:**
- **Claude Code Skill (SKILL.md)**: Skill definition and invocation -- the only framework. YAML frontmatter configures name, description, tool access. Markdown body contains routing instructions.
- **Progressive disclosure file structure**: Organize 5,000-10,000 lines of knowledge across 30-45 files that load on demand, consuming zero tokens at rest.
- **WebFetch + WebSearch (built-in)**: Live web research using Claude's native tools. No custom scraping infrastructure. Navigation guides make these tools effective per-source.
- **Read + Grep + Glob (built-in)**: Reference file access for the progressive disclosure pattern. Claude navigates to relevant files based on SKILL.md routing logic.

**Critical decisions already made:**
- Single `/privacy` skill, not multiple domain-split skills (user requirement)
- Inline execution (no subagent fork) to preserve conversation context and avoid WebFetch/WebSearch access issues
- WebFetch for live research, not MCP servers (avoids overengineering)
- FPF source priority encoded as conditional rules in SKILL.md, not numeric ranking

### Expected Features

**Must have (table stakes):**
- FPF content index covering all 6 publication types and 20+ issue areas
- Major privacy org catalog (15-20 organizations minimum)
- Per-source navigation guides for FPF + 5-8 top sources with actual URL patterns, not vague instructions
- Quick reference for major regulations (CCPA/CPRA, GDPR, COPPA, HIPAA, FERPA, EU AI Act)
- Professional-grade language assuming domain knowledge
- Source attribution with FPF cited first when relevant
- Hybrid static/live architecture with graceful degradation

**Should have (differentiators):**
- Tiered research depth (quick lookup vs. deep multi-source research)
- Site-specific search strategies embedded in navigation guides
- Government regulator directory with jurisdiction mapping
- Regulation cross-reference for common comparison queries
- FPF program awareness (Center for AI, Youth Privacy, Privacy Papers for Policymakers)
- Regulatory timeline awareness for key dates

**Defer (v2+):**
- Think tank / academic center catalog
- International DPA coverage beyond EDPB/ICO/CNIL
- Sector-specific privacy guides (health, fintech, edtech, adtech)
- State-by-state U.S. privacy law navigator
- Multi-language support

### Architecture Approach

The architecture follows a router pattern: SKILL.md classifies incoming queries and dispatches to the appropriate reference files, which are organized by source type (not by topic). This source-based organization reflects how research actually works -- the question is "where to look," not "what to look for." SKILL.md handles topic-to-source mapping. All reference files are one level deep from SKILL.md (no nested references, per official guidance).

**Major components:**
1. **SKILL.md (routing layer)** -- Query classification, source priority logic, organization index, pointers to reference files. ~300-400 lines, loaded on every invocation.
2. **sources/FPF.md** -- Deep FPF navigation guide: URL patterns, content categories, program details, search strategies for fpf.org. Loaded when FPF content is relevant (most queries).
3. **sources/ORGS.md** -- Navigation guides for 15-20 privacy organizations. Loaded when non-FPF sources needed.
4. **sources/GOV.md** -- Government and regulatory body navigation (FTC, state AGs, EU DPAs). Loaded for regulatory queries.
5. **knowledge/REGULATIONS.md** -- Quick-lookup regulation summaries for the fast path. Loaded for factual lookups without web fetching.

### Critical Pitfalls

1. **Hallucinated legal citations** -- LLMs hallucinate 58-88% on legal specifics. Embed actual citation data (titles, dates, URLs) in reference files. Never instruct Claude to "cite FPF's position on X" without providing the actual position in reference data. Add explicit anti-fabrication instructions.

2. **WebFetch failures on 30-50% of target sites** -- Many privacy org and government sites block bots or use JavaScript rendering. Test WebFetch against every indexed source before writing navigation guides. Build a compatibility matrix. Lean static for unreliable sources, live for reliable ones. Always include graceful degradation instructions.

3. **Content staleness within 3-6 months** -- Privacy law evolves rapidly (8 new U.S. state laws in 2025 alone). Separate time-sensitive content (dates, law counts) from stable content (concepts, frameworks). Date-stamp everything. Avoid hard-coding specific numbers that change.

4. **Absent legal disclaimers creating liability** -- Risk assessment outputs (if any) could be relied upon for compliance decisions. Every output pathway must include disclaimers. Draft and approve disclaimer language before writing any content.

5. **Vague navigation guides that add no value** -- A guide saying "search the website" is useless. Each guide must contain actual URL patterns, content taxonomy, specific URLs, and tested search strategies. If Claude can answer equally well without the guide, the guide adds nothing.

## Implications for Roadmap

Based on research, suggested phase structure:

### Phase 1: Core Routing Layer + FPF Primary Source

**Rationale:** The SKILL.md routing layer is the backbone -- nothing works without it. FPF is the primary source and will be consulted on most queries. These two components have the tightest coupling and should be built and tested together. Anti-hallucination instructions and legal disclaimers must be baked in from the start, not retrofitted.
**Delivers:** Working `/privacy` skill that can answer FPF-related queries using the FPF navigation guide and route to other sources (even before those source files exist).
**Features addressed:** SKILL.md router, FPF content index, FPF-first citation priority, source attribution, professional-grade language, legal disclaimers.
**Pitfalls avoided:** Monolithic SKILL.md (by establishing the router pattern from day one), hallucinated citations (by embedding actual FPF citation data), missing disclaimers (by including them in the initial template).

### Phase 2: Static Knowledge Base (Regulations)

**Rationale:** The regulations quick-reference enables the fast path -- answering common factual queries without any web fetching. This is the second-highest-value component because it handles the most frequent query type ("What does COPPA require?"). Must be built before expanding to other sources because static knowledge is the fallback when WebFetch fails.
**Delivers:** Quick-lookup answers for major regulations (GDPR, CCPA/CPRA, COPPA, HIPAA, FERPA, EU AI Act). Regulation cross-reference for common comparisons.
**Features addressed:** Quick reference for major regulations, regulation cross-reference, hybrid static/live architecture (static layer), tiered research depth (quick mode).
**Pitfalls avoided:** Jurisdictional confusion (by organizing by jurisdiction, not concept), content staleness (by date-stamping and separating time-sensitive content).

### Phase 3: Secondary Sources (Organizations + Government)

**Rationale:** With SKILL.md routing and FPF navigation working, expand to the broader privacy ecosystem. This phase requires WebFetch compatibility testing for each new source before writing its navigation guide. Organizations and government sources are built together because they follow the same navigation guide template.
**Delivers:** Full privacy org catalog with navigation guides for IAPP, EPIC, CalPrivacy, CDT, EFF, EDPB, ICO, FTC, and others. Government regulator directory.
**Features addressed:** Major privacy org catalog, per-source navigation guides (remaining sources), government regulator directory, site-specific search strategies, FPF program awareness.
**Pitfalls avoided:** WebFetch failures (by testing each source before committing to a navigation guide), vague navigation guides (by requiring URL patterns and tested search strategies).

### Phase 4: Refinement + Testing

**Rationale:** With all content in place, this phase focuses on quality: testing every query path (quick lookup, FPF-first, multi-source, deep research), tuning routing logic based on real query behavior, adding edge case handling, and establishing the content freshness strategy.
**Delivers:** Validated skill that handles diverse query types correctly. Content freshness metadata and update process. Example query patterns.
**Features addressed:** Tiered research depth (deep mode), graceful degradation, regulatory timeline awareness, frameworks reference.
**Pitfalls avoided:** Content staleness (by establishing update cadence), jurisdictional confusion (by testing cross-jurisdictional queries).

### Phase Ordering Rationale

- **SKILL.md first** because it is the routing backbone -- every other component depends on correct query classification and source dispatching.
- **FPF paired with SKILL.md** because FPF is the primary source and most queries will hit it. Testing the router requires at least one source file to route to.
- **Regulations before other sources** because static knowledge is the fallback path. When WebFetch fails (and it will for some sources), Claude falls back to static knowledge. This must exist before expanding live fetching.
- **Other sources last** because they depend on the routing layer, benefit from lessons learned building the FPF guide, and require per-source WebFetch compatibility testing that is time-intensive.
- **Testing as a dedicated phase** because the interaction between routing logic, navigation guides, static knowledge, and live fetching creates emergent behavior that cannot be fully predicted. Real query testing is essential.

### Research Flags

Phases likely needing deeper research during planning:
- **Phase 1 (FPF Source):** Needs hands-on WebFetch testing against fpf.org to determine which page types render correctly. FPF's site structure must be mapped by actually navigating it and documenting URL patterns. This is empirical work, not something that can be planned from documentation alone.
- **Phase 3 (Secondary Sources):** Each new source requires individual WebFetch compatibility testing and site structure mapping. The navigation guide for IAPP will be completely different from the one for EPIC or the FTC. Budget significant time for per-source research.

Phases with standard patterns (skip deep research):
- **Phase 2 (Regulations):** Well-documented domain. Major regulation requirements (GDPR, CCPA, COPPA) are thoroughly documented in multiple authoritative sources. The challenge is curation and formatting, not discovery.
- **Phase 4 (Refinement):** Standard testing and iteration. The patterns are known; the work is execution.

## Confidence Assessment

| Area | Confidence | Notes |
|------|------------|-------|
| Stack | HIGH | Verified against official Claude Code skill documentation, Anthropic best practices, and reference implementations. The skill framework is well-documented and stable. |
| Features | MEDIUM-HIGH | Feature set derived from privacy professional pain points, competitive analysis, and project requirements. FPF-specific feature depth verified against fpf.org. Minor uncertainty around which features will actually get used most. |
| Architecture | HIGH | Progressive disclosure router pattern is the officially recommended approach. Verified against Anthropic's compliance skill, skill authoring best practices, and engineering blog. Source-based file organization is a defensible opinion backed by research. |
| Pitfalls | HIGH | Pitfalls verified against official docs (character budget, 500-line limit), academic research (hallucination rates), known GitHub issues (WebFetch limitations, WebSearch permissions), and real-world skill deployment experiences. |

**Overall confidence:** HIGH

### Gaps to Address

- **WebFetch compatibility matrix does not exist yet.** Must be created empirically by testing each target website during Phase 1 and Phase 3. No amount of planning substitutes for actually fetching pages and checking results. This is the single biggest unknown.
- **FPF site structure not yet mapped.** The FPF navigation guide -- the most important reference file -- requires hands-on site mapping. URL patterns, content taxonomy, and search behavior must be documented from the actual site, not assumed.
- **Optimal SKILL.md length is uncertain.** The 500-line limit is official guidance, but the effective limit for maintaining Claude's response quality may be lower. Must be tested empirically with real queries and monitored for context compaction.
- **WebSearch permission behavior.** GitHub issue #26530 indicates WebSearch wildcard permissions may not work. The skill should function well without WebSearch (using static knowledge + WebFetch with known URLs) and treat WebSearch as an enhancement.
- **Legal disclaimer language needs FPF review.** Disclaimer template should be drafted early and reviewed by someone with legal authority before any content goes live.

## Sources

### Primary (HIGH confidence)
- [Claude Code Skills Documentation](https://code.claude.com/docs/en/skills) -- skill spec, frontmatter, progressive disclosure
- [Skill Authoring Best Practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices) -- 500-line limit, naming, anti-patterns
- [Anthropic Compliance Skill](https://github.com/anthropics/knowledge-work-plugins/tree/main/legal/skills/compliance) -- reference implementation
- [Anthropic Skills Repository](https://github.com/anthropics/skills/) -- official examples
- [Hallucinating Law (Stanford HAI)](https://hai.stanford.edu/news/hallucinating-law-legal-mistakes-large-language-models-are-pervasive) -- 58-88% hallucination rates
- [Large Legal Fictions (Journal of Legal Analysis)](https://academic.oup.com/jla/article/16/1/64/7699227) -- specialized tool hallucination rates
- [Agent Skills Engineering Blog](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills) -- architecture rationale

### Secondary (MEDIUM confidence)
- [Claude Code Web Tools Analysis](https://mikhail.io/2025/10/claude-code-web-tools/) -- WebFetch vs WebSearch capabilities
- [WebFetch 403 Issues (GitHub #22846)](https://github.com/anthropics/claude-code/issues/22846) -- real-world blocking
- [Skills Not Triggering (Blog)](https://blog.fsck.com/2025/12/17/claude-code-skills-not-triggering/) -- character budget issues
- [IAPP U.S. State Privacy Legislation Tracker](https://iapp.org/resources/article/us-state-privacy-legislation-tracker) -- regulatory velocity data
- [ISACA 2025 Privacy Professional Survey](https://www.isaca.org/about-us/newsroom/press-releases/2025/63-percent-of-privacy-professionals-find-their-jobs--more-stressful-now-than-five-years-ago) -- user pain points

### Tertiary (needs validation during implementation)
- WebFetch compatibility with specific privacy organization websites -- must be tested empirically
- Optimal SKILL.md line count for maintaining response quality -- must be tested empirically
- FPF site URL patterns and content taxonomy -- must be mapped from live site

---
*Research completed: 2026-03-12*
*Ready for roadmap: yes*
