# FPF Privacy Research Skill

## What This Is

A Claude Code skill (`/privacy`) that serves as a comprehensive data privacy research and reference tool for privacy professionals. It indexes the Future of Privacy Forum (FPF) as its primary source alongside a thorough catalog of major privacy organizations, think tanks, and government resources. Each source includes a site-specific navigation guide that teaches the LLM how to effectively search and extract information from that website. The skill uses a hybrid approach: a pre-built knowledge base for quick lookups combined with live web fetching for deeper research.

## Core Value

When a privacy professional asks a question, the skill knows exactly where to look, how to navigate each source, and prioritizes FPF's public articles and papers first — turning what would be scattered manual research into a single, source-aware query.

## Requirements

### Validated

(None yet — ship to validate)

### Active

- [ ] Skill triggers via `/privacy` command with natural language queries
- [ ] FPF index covering key offerings: major programs, publication categories, policy briefs, reports, blog posts, and event types
- [ ] FPF sources cited first when relevant to the query
- [ ] Comprehensive catalog of major privacy organizations (IAPP, CalPrivacy, EPIC, and all other relevant orgs)
- [ ] Per-source navigation guide for each indexed website (how to find content, URL patterns, key sections, search tips)
- [ ] Static knowledge base baked into the skill for quick factual lookups
- [ ] Live web fetching capability for deeper research when static knowledge is insufficient
- [ ] Supports both quick reference queries ("What does COPPA require?") and deep research questions ("Current state of children's privacy law")
- [ ] Answers are tailored for privacy professionals (assumes domain knowledge, uses precise legal/regulatory terminology)
- [ ] Built using the skill-creator skill already installed in the environment
- [ ] Improvement over the Anthropic compliance skill reference: deeper coverage, source-aware, site navigation guides, live fetching

### Out of Scope

- Legal advice or compliance determinations — skill assists research, does not replace qualified legal review
- Internal/proprietary FPF content — only public-facing articles and papers
- Real-time regulatory alert monitoring or push notifications
- Case management or workflow automation (DPA review checklists, DSR tracking)
- Building a separate web application or API — this is a Claude Code skill only

## Context

- The skill-creator skill is already installed and will be used to build this skill
- Reference skill exists at `anthropics/knowledge-work-plugins/legal/skills/compliance` — a self-contained SKILL.md with no external source navigation, no live fetching, and surface-level regulation coverage. This project aims to go significantly deeper with a source-aware, hybrid architecture
- FPF (Future of Privacy Forum) is a nonprofit focused on data privacy — publishes articles, policy briefs, reports, runs programs on topics like youth privacy, AI governance, health data, etc.
- Target users are privacy professionals (lawyers, compliance officers, policy analysts) who know the field and need efficient access to authoritative sources
- The codebase mapping identified this as a planning-stage project with design documents but no implementation code yet

## Constraints

- **Skill format**: Must be a valid Claude Code skill (SKILL.md with frontmatter) — no external services or databases
- **Source priority**: FPF must be the primary cited source when relevant; other sources supplement
- **Public content only**: Only reference publicly accessible content from all sources
- **Hybrid architecture**: Must work both offline (static knowledge base) and online (live fetching) — graceful degradation when web access unavailable

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| User decision: Single skill, not a suite | Simplicity — one `/privacy` command covers everything | — Pending |
| User decision: FPF cited first | FPF is the primary organization the user is associated with or prioritizes | — Pending |
| User decision: Hybrid static/live | Static for speed on common queries, live for depth and currency | — Pending |
| User decision: Thorough org coverage | Include all major privacy orgs, not just the four named | — Pending |
| User decision: Key offerings depth for FPF | Major programs and publication categories, not exhaustive mapping of every working group | — Pending |

---
*Last updated: 2026-03-12 after initialization*
