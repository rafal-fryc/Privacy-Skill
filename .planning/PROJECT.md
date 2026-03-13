# FPF Privacy Research Skill

## What This Is

A Claude Code skill (`/privacy`) that serves as a comprehensive data privacy research and reference tool for privacy professionals. It indexes the Future of Privacy Forum (FPF) as its primary source alongside a catalog of 30+ privacy organizations, government regulators, and academic centers. Each major source includes a site-specific navigation guide teaching the LLM how to search and extract information from that website. The skill uses a hybrid architecture: a pre-built knowledge base (6 regulation references, 3 org catalogs) for quick lookups combined with live WebFetch for multi-source deep research, with three-tier graceful degradation when web access fails.

## Core Value

When a privacy professional asks a question, the skill knows exactly where to look, how to navigate each source, and prioritizes FPF's public articles and papers first — turning what would be scattered manual research into a single, source-aware query.

## Requirements

### Validated

- ✓ Skill triggers via `/privacy` command with natural language queries — v1.0
- ✓ FPF index covering key offerings: major programs, publication categories, policy briefs, reports, blog posts, and event types — v1.0
- ✓ FPF sources cited first when relevant to the query — v1.0
- ✓ Comprehensive catalog of major privacy organizations (IAPP, CalPrivacy, EPIC, and all other relevant orgs) — v1.0
- ✓ Per-source navigation guide for each indexed website (how to find content, URL patterns, key sections, search tips) — v1.0
- ✓ Static knowledge base baked into the skill for quick factual lookups — v1.0
- ✓ Live web fetching capability for deeper research when static knowledge is insufficient — v1.0
- ✓ Supports both quick reference queries ("What does COPPA require?") and deep research questions ("Current state of children's privacy law") — v1.0
- ✓ Answers are tailored for privacy professionals (assumes domain knowledge, uses precise legal/regulatory terminology) — v1.0
- ✓ Built using the skill-creator skill already installed in the environment — v1.0
- ✓ Improvement over the Anthropic compliance skill reference: deeper coverage, source-aware, site navigation guides, live fetching — v1.0

### Active

(None — next milestone will define new requirements)

### Out of Scope

- Legal advice or compliance determinations — skill assists research, does not replace qualified legal review
- Internal/proprietary FPF content — only public-facing articles and papers
- Real-time regulatory alert monitoring or push notifications
- Case management or workflow automation (DPA review checklists, DSR tracking)
- Building a separate web application or API — this is a Claude Code skill only
- Exhaustive regulation text reproduction — link to authoritative full text instead
- All-jurisdiction depth (160+ countries) — cover major frameworks + pointers

## Context

Shipped v1.0 with 3,882 LOC across 22 markdown skill files.
Tech stack: Claude Code skill (SKILL.md + progressive reference file loading + WebFetch).
Architecture: 6-step routing pipeline (FPF → Regulation → Organization → Live Research → Compose Response).

22 skill files:
- 1 SKILL.md (304 lines, routing orchestrator)
- 2 behavioral files (skill-behaviors.md, research-behaviors.md)
- 1 FPF reference (319 lines)
- 6 regulation references (GDPR, CCPA, COPPA, HIPAA, FERPA, EU AI Act)
- 2 cross-cutting regulation files (cross-reference, timeline)
- 3 organization catalogs (advocacy, government, academic)
- 7 navigation guides (IAPP, EPIC, CDT, CPPA, FTC, EDPB, ICO)

Known considerations:
- SKILL.md at 304/500 lines — 196 lines headroom for future expansion
- WebFetch blocked for 3 sources (FTC/403, EPIC/timeout, CDT/Cloudflare) — documented workarounds via IAPP and WebSearch
- Legal disclaimer language not yet reviewed by counsel

## Constraints

- **Skill format**: Must be a valid Claude Code skill (SKILL.md with frontmatter) — no external services or databases
- **Source priority**: FPF must be the primary cited source when relevant; other sources supplement
- **Public content only**: Only reference publicly accessible content from all sources
- **Hybrid architecture**: Must work both offline (static knowledge base) and online (live fetching) — graceful degradation when web access unavailable

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| User decision: Single skill, not a suite | Simplicity — one `/privacy` command covers everything | ✓ Good |
| User decision: FPF cited first | FPF is the primary organization the user is associated with or prioritizes | ✓ Good |
| User decision: Hybrid static/live | Static for speed on common queries, live for depth and currency | ✓ Good |
| User decision: Thorough org coverage | Include all major privacy orgs, not just the four named | ✓ Good |
| User decision: Key offerings depth for FPF | Major programs and publication categories, not exhaustive mapping of every working group | ✓ Good |
| Three-tier anti-hallucination | Strict for FPF-specific, high for regulatory, standard for domain knowledge | ✓ Good |
| Every query attempts live fetch | No separate "deep research" mode — live fetching always runs, static is foundation | ✓ Good — simplifies routing |
| Sequential WebFetch execution | Simplest approach; revisit if latency becomes an issue | — Pending |
| Privacy lens for AI Act | Focus on data governance, biometrics, GDPR interplay rather than full AI Act scope | ✓ Good |
| FPF blog two-step fetch | Scan blog index, then fetch specific posts (both count within 3-4 source cap) | ✓ Good |

---
*Last updated: 2026-03-13 after v1.0 milestone*
