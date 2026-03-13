# Architecture Research

**Domain:** Knowledge-heavy Claude Code skill (data privacy research)
**Researched:** 2026-03-12
**Confidence:** HIGH

## System Overview

The project's central constraint is that Claude Code skills use **progressive disclosure**: at startup, only skill metadata (name + description) loads into context. The full SKILL.md loads only when the skill is invoked. Supporting files load only when Claude reads them on-demand. This means a skill's knowledge base can be effectively unbounded -- reference files sitting on the filesystem consume zero tokens until accessed.

This is the key architectural insight: **the SKILL.md is not the knowledge base. It is the routing layer.** The actual knowledge lives in reference files that Claude navigates to selectively.

```
                          INVOCATION LAYER
  ┌──────────────────────────────────────────────────────┐
  │  /privacy [query]                                    │
  │  Metadata loaded at startup (name + description)     │
  │  Full SKILL.md loaded on invocation (~300-400 lines) │
  └───────────────────────┬──────────────────────────────┘
                          │
                    ROUTING LAYER
  ┌───────────────────────┴──────────────────────────────┐
  │                    SKILL.md                           │
  │  - Source priority logic (FPF first)                  │
  │  - Organization index (name + what + when)            │
  │  - Navigation to reference files                      │
  │  - Live fetch instructions                            │
  │  - Query classification rules                         │
  └─────┬─────────┬──────────┬──────────┬───────────────┘
        │         │          │          │
  REFERENCE LAYER (loaded on-demand, zero tokens at rest)
  ┌─────┴──┐ ┌───┴────┐ ┌───┴────┐ ┌───┴─────────────┐
  │FPF.md  │ │GOV.md  │ │ORGS.md │ │REGULATIONS.md   │
  │Primary │ │Gov     │ │Think   │ │Quick-lookup     │
  │source  │ │sources │ │tanks & │ │regulation       │
  │guide   │ │guide   │ │advocacy│ │summaries        │
  └────────┘ └────────┘ └────────┘ └─────────────────┘
```

### Component Responsibilities

| Component | Responsibility | Token Cost |
|-----------|----------------|------------|
| SKILL.md (routing) | Query classification, source prioritization, org index with one-liners, pointers to reference files | ~300-400 lines, loaded on invocation |
| FPF.md (primary source) | Deep FPF navigation guide, URL patterns, content categories, program details | Loaded when FPF content is relevant (most queries) |
| ORGS.md (org guides) | Per-organization navigation guides for 15-20 privacy orgs | Loaded when non-FPF sources needed |
| GOV.md (government sources) | Government and regulatory body navigation (FTC, state AGs, EU DPAs, ICO) | Loaded for regulatory queries |
| REGULATIONS.md (static KB) | Quick-lookup regulation summaries (GDPR, CCPA, COPPA, etc.) | Loaded for factual lookups |

## Recommended Skill Directory Structure

```
privacy/
├── SKILL.md                    # Routing layer (~300-400 lines)
├── sources/
│   ├── FPF.md                  # FPF deep navigation guide (~200-300 lines)
│   ├── ORGS.md                 # Privacy org catalog + navigation (~300-400 lines)
│   └── GOV.md                  # Government/regulatory sources (~150-200 lines)
├── knowledge/
│   ├── REGULATIONS.md          # Regulation quick-reference (~200-300 lines)
│   └── FRAMEWORKS.md           # Privacy frameworks & methodologies (~150-200 lines)
└── examples/
    └── QUERY-PATTERNS.md       # Example queries & expected approaches (~100 lines)
```

### Structure Rationale

- **`SKILL.md` at root:** Required by the skill spec. Contains the routing intelligence -- how to classify queries and which reference files to consult. Stays under 500 lines (the official recommendation).
- **`sources/` directory:** Organized by source type, not by topic. This is deliberate: when Claude needs to look something up, it needs to know *where* to look (which source), not *what* to look up (the topic determines the source via SKILL.md routing). One level deep from SKILL.md -- no nested references.
- **`knowledge/` directory:** Static knowledge that does not require web fetching. Regulation summaries, framework descriptions. Pre-baked content for fast answers.
- **`examples/` directory:** Shows Claude what good research output looks like. Loaded only when Claude needs guidance on response format.

## Architectural Patterns

### Pattern 1: Router SKILL.md (Core Pattern)

**What:** SKILL.md acts as a dispatcher, not a knowledge container. It classifies the incoming query, determines which sources are relevant, and directs Claude to the appropriate reference files. The actual knowledge lives in reference files.

**When to use:** Any skill where the knowledge base exceeds ~200 lines of content. This project's knowledge base is 1000+ lines across all sources -- far beyond what should live in SKILL.md.

**Trade-offs:**
- Pro: SKILL.md stays lean (under 500 lines), Claude loads only what it needs per query
- Pro: Each reference file can be independently updated without touching the routing logic
- Con: Claude must make an extra file read per query (minor latency)
- Con: If routing logic is wrong, Claude reads the wrong file

**SKILL.md structure:**

```markdown
---
name: privacy
description: Researches data privacy topics using authoritative sources.
  FPF (Future of Privacy Forum) primary source. Covers regulations,
  organizations, policy analysis. Use when asked about privacy law,
  data protection, privacy organizations, or regulatory compliance.
---

# Privacy Research Skill

## Source Priority

When answering privacy questions, consult sources in this order:

1. **FPF (Future of Privacy Forum)** -- always check first when topic
   overlaps with FPF coverage areas. See [sources/FPF.md](sources/FPF.md)
2. **Static knowledge base** -- for quick factual lookups about
   regulations. See [knowledge/REGULATIONS.md](knowledge/REGULATIONS.md)
3. **Other privacy organizations** -- for perspectives beyond FPF.
   See [sources/ORGS.md](sources/ORGS.md)
4. **Government sources** -- for official regulatory positions.
   See [sources/GOV.md](sources/GOV.md)
5. **Live web fetch** -- when static knowledge is insufficient
   or currency matters

## Organization Index

[Compact table: org name | coverage area | when to consult]

## Query Classification

[Rules for determining which files to read]

## Live Fetch Protocol

[When and how to fetch from the web]
```

### Pattern 2: Navigation Guide Structure (Per-Source Pattern)

**What:** Each source reference file follows a consistent internal structure: identity, coverage areas, URL patterns, search strategy, content types, and key pages. This teaches Claude *how to navigate* each website, not just *what the website contains*.

**When to use:** For every source that Claude might need to fetch content from live. The navigation guide is what makes this skill more valuable than a generic web search -- it encodes institutional knowledge about site structure.

**Trade-offs:**
- Pro: Claude can efficiently find content on unfamiliar sites
- Pro: URL patterns let Claude construct direct links without searching
- Pro: Knowledge of content types helps Claude evaluate source quality
- Con: Navigation guides become stale as sites restructure (mitigation: note last-verified date)

**Navigation guide template:**

```markdown
## [Organization Name]

**URL:** [base URL]
**Coverage:** [one-line scope description]
**Last verified:** [date]

### Content Types
- [Type 1]: [description, where to find, quality/depth]
- [Type 2]: [description, where to find, quality/depth]

### URL Patterns
- Blog posts: [base]/blog/[slug]
- Reports: [base]/reports/[title-slug]
- Policy briefs: [base]/policy/[topic]/

### Search Strategy
1. [How to find content on this site]
2. [Key landing pages or indexes]
3. [Search URL pattern if available]

### Key Pages
| Page | URL | What It Contains |
|------|-----|------------------|
| [name] | [url] | [description] |

### Strengths & Limitations
- Strong on: [topics]
- Weak on: [topics]
- Note: [any access restrictions, paywalls, etc.]
```

### Pattern 3: Source Priority Encoding

**What:** Source priority is encoded as an ordered list in SKILL.md with explicit decision rules, not just a numeric ranking. The rules specify *when* to consult each source and *why* FPF comes first.

**When to use:** Any skill where multiple sources exist and one must be preferred.

**Trade-offs:**
- Pro: Claude consistently checks FPF first without explicit user instruction
- Pro: Decision rules prevent Claude from skipping relevant sources
- Con: Rigid priority can miss cases where a non-primary source is clearly better (mitigation: include override conditions)

**Encoding approach:**

```markdown
## Source Priority

### Tier 1: FPF (Always check first)
Check FPF sources for ANY query about:
- Children's/youth privacy, education data, student privacy
- AI governance and AI policy
- U.S. state privacy legislation
- Ad tech and digital advertising privacy
- Health data privacy
- Biometrics and facial recognition
- Privacy-enhancing technologies (PETs)
- Immersive technology privacy (AR/VR/XR)
- Mobility and location data

If FPF has relevant coverage, cite FPF first. Supplement
with other sources as needed.

### Tier 2: Static Knowledge Base (Quick lookups)
For factual questions about specific regulations (GDPR
requirements, CCPA timelines, COPPA thresholds), check
knowledge/REGULATIONS.md before web fetching.

### Tier 3: Specialized Organizations
When the query concerns a topic where another org has
deeper expertise than FPF (e.g., IAPP for certification
programs, EPIC for litigation history), consult ORGS.md.

### Tier 4: Government Sources
For official regulatory text, enforcement actions,
guidance documents. See GOV.md.

### Tier 5: Live Web Fetch
When static knowledge is outdated or insufficient.
Always attempt static sources first.
```

### Pattern 4: Hybrid Static/Live Architecture

**What:** The skill contains pre-baked knowledge for common queries (regulation summaries, organization profiles) and instructions for live web fetching when deeper or more current information is needed. Static content handles the 80% case; live fetching handles the 20%.

**When to use:** When the knowledge domain changes over time (regulations evolve, new reports are published) but many queries are about established facts.

**Trade-offs:**
- Pro: Fast responses for common queries (no web fetch latency)
- Pro: Graceful degradation when web access is unavailable
- Pro: Web fetching provides currency that static content cannot
- Con: Static content becomes stale (mitigation: date-stamp entries, instruct Claude to note when info might be outdated)
- Con: Live fetching consumes more tokens and time

**Implementation in SKILL.md:**

```markdown
## Response Strategy

### Step 1: Check static knowledge first
Read knowledge/REGULATIONS.md or knowledge/FRAMEWORKS.md
for the answer. If the static knowledge fully answers the
question with sufficient depth, respond using it.

### Step 2: Check source navigation guides
If the query needs more depth or recency than static
knowledge provides, read the appropriate source file
(sources/FPF.md, sources/ORGS.md, sources/GOV.md) to
determine where to look.

### Step 3: Live web fetch (when needed)
Use WebFetch to retrieve content from the URLs identified
in Step 2. Follow the navigation guide's URL patterns
and search strategies.

### Step 4: Synthesize and cite
Combine findings from all sources consulted. Always note
which sources were used. Cite FPF sources first when
they contributed to the answer.
```

## Data Flow

### Query Processing Flow

```
User: /privacy [query]
    |
    v
SKILL.md loads into context
    |
    v
Classify query type:
    |--- Quick factual lookup? --> Read knowledge/REGULATIONS.md --> Respond
    |--- FPF-relevant topic?  --> Read sources/FPF.md --> Follow nav guide
    |--- Multi-org question?  --> Read sources/ORGS.md --> Identify sources
    |--- Regulatory question? --> Read sources/GOV.md --> Follow nav guide
    |--- Deep research?       --> Read multiple source files --> Web fetch
    |
    v
Synthesize answer with source citations (FPF cited first when relevant)
    |
    v
Response to user
```

### Key Data Flows

1. **Quick lookup flow:** User asks factual question (e.g., "What does COPPA require?") --> SKILL.md routes to knowledge/REGULATIONS.md --> Claude reads COPPA section --> responds with static knowledge. No web fetch needed. Fastest path.

2. **FPF-first research flow:** User asks about a topic FPF covers (e.g., "Current state of children's privacy law") --> SKILL.md identifies this as FPF-relevant --> Claude reads sources/FPF.md for navigation instructions --> fetches from fpf.org using URL patterns --> supplements with other sources from ORGS.md if needed --> responds with FPF cited first.

3. **Cross-source research flow:** User asks a broad question (e.g., "Compare US and EU approaches to AI regulation") --> SKILL.md identifies multiple relevant sources --> Claude reads sources/FPF.md (AI governance coverage) + sources/GOV.md (EU/US regulatory bodies) + sources/ORGS.md (other orgs with AI policy work) --> fetches from multiple sources --> synthesizes with FPF cited first for topics they cover.

## Scaling Considerations

| Concern | Current (MVP) | Growth Path |
|---------|---------------|-------------|
| Number of orgs | 15-20 in ORGS.md | Split ORGS.md into ORGS-THINKTANKS.md, ORGS-ADVOCACY.md, ORGS-INDUSTRY.md if it exceeds ~400 lines |
| FPF coverage depth | Major programs and publication categories | Add sources/FPF-PROGRAMS.md for per-program deep dives if FPF.md grows past 300 lines |
| Regulation count | 8-10 major regulations | Add knowledge/REGULATIONS-STATE.md for US state-by-state detail |
| Skill description budget | One skill, ~200 chars description | Monitor via `/context` for excluded-skill warnings if many skills exist |
| Reference file size | Each file under 400 lines | Split by sub-domain if any file exceeds 500 lines |

### Scaling Priorities

1. **First scaling concern: ORGS.md size.** With 15-20 organizations each needing navigation guides, this file will be the largest. If it approaches 500 lines, split by organization type (think tanks, advocacy, industry, international).
2. **Second scaling concern: Static knowledge currency.** Regulations change. Add a "last updated" date to each regulation entry in REGULATIONS.md and instruct Claude to flag potentially outdated information.

## Anti-Patterns

### Anti-Pattern 1: Monolithic SKILL.md

**What people do:** Put all knowledge -- org guides, regulation summaries, URL patterns, fetch instructions -- into a single SKILL.md file.
**Why it is wrong:** Exceeds the 500-line recommendation. Every invocation loads the entire knowledge base into context, consuming tokens even for simple queries. Claude's performance degrades with overly long prompts (primacy/recency bias -- content in the middle gets underweighted).
**Do this instead:** Use SKILL.md as a router. Move knowledge into reference files organized by access pattern (source type, not topic).

### Anti-Pattern 2: Topic-Based File Organization

**What people do:** Organize reference files by topic (ai-governance.md, health-data.md, youth-privacy.md).
**Why it is wrong:** A single query about "AI governance" might need to check FPF, OECD, NIST, and EU Commission sources. Topic-based organization forces Claude to read multiple files to understand where to look for one topic. The routing decision is about *which source to consult*, not *which topic is relevant*.
**Do this instead:** Organize by source type (FPF.md, ORGS.md, GOV.md). Each file contains navigation guides for multiple topics within that source category. SKILL.md handles the topic-to-source mapping.

### Anti-Pattern 3: Deeply Nested References

**What people do:** SKILL.md references sources/FPF.md, which references sources/fpf-programs/youth-privacy.md, which references sources/fpf-programs/youth-privacy-coppa-detail.md.
**Why it is wrong:** Official best practices explicitly warn against this. Claude may partially read files when references are nested more than one level deep (using `head -100` to preview rather than reading fully). Information gets lost.
**Do this instead:** Keep all references one level deep from SKILL.md. Every reference file is directly linked from SKILL.md, never from another reference file.

### Anti-Pattern 4: Encoding Priority as a Number

**What people do:** Assign numeric priority scores to sources (FPF = 1, IAPP = 2, EPIC = 3) and expect Claude to follow the ranking.
**Why it is wrong:** Claude does not reliably follow abstract numeric rankings. A number does not tell Claude *when* or *why* to consult a source.
**Do this instead:** Encode priority as explicit rules with topic associations. "Check FPF first for ANY query about children's privacy, AI governance, ad tech..." is more effective than "FPF priority: 1."

### Anti-Pattern 5: Duplicating Claude's Existing Knowledge

**What people do:** Include lengthy explanations of what GDPR is, what privacy means, how the internet works.
**Why it is wrong:** Claude already knows this. Every token spent on information Claude already has is a token wasted from the context window. The official best practices state: "Only add context Claude doesn't already have."
**Do this instead:** Focus static knowledge on things Claude does NOT know well: FPF-specific programs, org-specific URL patterns, navigation strategies for specific websites, niche regulatory details. For common regulations, include only the quick-reference details professionals need (deadlines, thresholds, specific requirements) rather than general explanations.

## Integration Points

### External Services

| Service | Integration Pattern | Notes |
|---------|---------------------|-------|
| FPF website (fpf.org) | WebFetch via navigation guide URLs | Primary source; navigation guide in sources/FPF.md |
| Privacy org websites | WebFetch via per-org navigation guides | 15-20 orgs indexed in sources/ORGS.md |
| Government websites | WebFetch via gov navigation guides | FTC, state AGs, DPAs in sources/GOV.md |

### Internal Boundaries

| Boundary | Communication | Notes |
|----------|---------------|-------|
| SKILL.md to reference files | File read via `[link](path)` references | One level deep only |
| Static knowledge to live fetch | Decision logic in SKILL.md | Static checked first, live fetch when insufficient |
| FPF priority to other sources | Source priority rules in SKILL.md | FPF always checked first when relevant |

## Build Order Implications

The architecture dictates a specific build order based on dependencies:

### Phase 1: Core Routing Layer
Build SKILL.md first. This is the backbone. Without correct routing logic, the reference files cannot be used effectively. Includes:
- YAML frontmatter with name and description
- Source priority logic
- Organization index (compact table)
- Query classification rules
- Pointers to reference files (even before they exist)
- Live fetch protocol
- Response format guidance

### Phase 2: Primary Source (FPF)
Build sources/FPF.md second. This is the most-consulted reference file since FPF is the primary source. Includes:
- FPF identity and scope
- Content types and where to find them
- URL patterns for direct access
- Key programs and their coverage areas
- Search strategy for fpf.org
- Key pages table

### Phase 3: Static Knowledge Base
Build knowledge/REGULATIONS.md third. This enables the fast-path (quick lookups without web fetching). Includes:
- Major regulation summaries (GDPR, CCPA, COPPA, LGPD, POPIA, PIPEDA, etc.)
- Key dates, thresholds, and requirements
- Cross-regulation comparison points
- Professional-level detail (not general explanations)

### Phase 4: Secondary Sources
Build sources/ORGS.md and sources/GOV.md. These complete the source catalog. Includes:
- Navigation guides for each privacy organization
- Navigation guides for government/regulatory sources
- Consistent structure per the navigation guide template

### Phase 5: Refinement
Build knowledge/FRAMEWORKS.md and examples/QUERY-PATTERNS.md. These are enhancement files:
- Privacy frameworks and methodologies
- Example queries and expected research approaches
- Edge case handling

### Phase 6: Testing and Iteration
Test with real queries across all paths:
- Quick lookups (static knowledge)
- FPF-first research
- Multi-source research
- Live fetch scenarios
- Edge cases (ambiguous queries, topics FPF does not cover)

## Key Architectural Decisions

| Decision | Rationale | Trade-off |
|----------|-----------|-----------|
| Source-based file organization (not topic-based) | Queries need to know *where to look*, not *what to look for*. SKILL.md handles topic-to-source mapping. | A researcher wanting "everything about COPPA" must check multiple source files. Acceptable because SKILL.md routing handles this automatically. |
| SKILL.md as router, not knowledge container | Official recommendation is under 500 lines. Knowledge base is 1000+ lines total. Progressive disclosure means reference files cost zero tokens until accessed. | Extra file read per query (minor latency). Worth it for keeping SKILL.md lean. |
| Priority as explicit rules, not numeric ranking | Claude responds better to conditional rules ("check FPF first for X, Y, Z topics") than abstract numbers ("FPF priority: 1"). | More verbose than a simple ranking. But more reliable. |
| Single /privacy skill, not 15+ domain skills | User decided. One command covers everything. Simpler UX. Routing happens inside the skill, not at the skill-selection layer. | SKILL.md routing logic must be comprehensive. But this keeps the skill description budget low (one skill uses ~200 chars, not 15 skills using 3000+ chars). |
| Hybrid static/live architecture | Static for speed on common queries; live for depth and currency. Graceful degradation when web access is unavailable. | Static content becomes stale. Mitigation: date-stamp entries, flag potential staleness. |

## Sources

- [Claude Code Skills Documentation](https://code.claude.com/docs/en/skills) -- official skill structure, frontmatter, supporting files, progressive disclosure (HIGH confidence)
- [Skill Authoring Best Practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices) -- 500-line limit, progressive disclosure patterns, domain-specific organization, reference file patterns (HIGH confidence)
- [Anthropic Compliance Skill](https://github.com/anthropics/knowledge-work-plugins/tree/main/legal/skills/compliance) -- reference implementation of a knowledge-heavy legal skill, single SKILL.md with ~250 lines of regulatory content (HIGH confidence)
- [Anthropic Skills Repository](https://github.com/anthropics/skills/) -- official skill examples and spec (HIGH confidence)
- [Skill Creator SKILL.md](https://github.com/anthropics/skills/blob/main/skills/skill-creator/SKILL.md) -- official skill for building skills, iterative testing methodology (HIGH confidence)
- [Agent Skills Engineering Blog](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills) -- progressive disclosure architecture, unbounded skill knowledge bases (HIGH confidence)

---
*Architecture research for: FPF Privacy Research Skill*
*Researched: 2026-03-12*
