# Phase 1: Skill Foundation + FPF Primary Source - Context

**Gathered:** 2026-03-12
**Status:** Ready for planning

<domain>
## Phase Boundary

Build the `/privacy` skill routing layer, FPF knowledge base (articles and publications focus), and foundational skill behaviors (attribution, disclaimer, anti-hallucination). Privacy professionals can invoke `/privacy [question]` and get source-attributed, FPF-prioritized answers about FPF publications and issue areas from built-in knowledge without web fetching.

</domain>

<decisions>
## Implementation Decisions

### Response Structure
- Heading + organized sections format (Overview, Key Provisions, FPF Resources, etc.)
- Sections vary by query type — not a rigid template
- Concise by default (200-400 words), user can ask for more depth
- No skill branding or header tags — responses start directly with the topic heading

### Source Attribution
- Inline citations with links woven naturally into the answer text: "According to FPF's [Report Title](url), ..."
- All sources get equal treatment (FPF and non-FPF alike) — FPF naturally appears first/more often due to prioritization logic
- FPF Resources section appears whenever FPF has relevant coverage; omitted silently when FPF has no coverage on the topic
- When FPF doesn't cover a topic, answer from other sources without commenting on FPF's absence

### Cross-Cutting Queries
- Unified cohesive answer when query spans multiple issue areas (e.g., "AI and children's privacy")
- FPF Resources section lists materials from each relevant area — no artificial subsections by area

### Legal Disclaimer
- Footer on every response, minimal: `⚠️ *Research aid only — not legal advice.*`
- Generic — does not mention FPF by name
- No extra warnings for date-sensitive content, enforcement penalties, or other high-stakes topics
- Standard disclaimer is sufficient; professionals understand its implications

### FPF Knowledge Scope
- Focus exclusively on articles and publications — no events, trainings, or programs as organizational entities
- All 20+ FPF issue areas with full 2-3 sentence descriptions of coverage and key resource types
- All 6 FPF publication types (Reports, White Papers, Filings, Infographics, Blog Posts, Videos) with descriptions
- FPF specialized tools included as resources (Student Privacy Compass, Key Dates Tracker, PETs Repository, etc.)
- FPF navigation guide with tested fpf.org URL patterns, content taxonomy, and search strategies

### Reference File Organization
- Two reference files: fpf-reference.md (knowledge + navigation combined) and skill-behaviors.md (attribution, disclaimer, anti-hallucination)
- Follow skill-creator convention for file placement
- Selective loading: SKILL.md detects query type and loads only what's needed per query
- SKILL.md includes 5-10 curated example queries spanning regulation questions, FPF-specific, and general privacy

### Claude's Discretion
- Anti-hallucination implementation approach
- Professional tone calibration (assumed: practitioner-practical for privacy professionals)
- Exact section names and ordering within responses
- How to handle queries clearly outside privacy domain
- Routing logic implementation in SKILL.md

</decisions>

<specifics>
## Specific Ideas

- FPF should be cited first when relevant but without explicitly calling out when FPF doesn't cover something — seamless fallback to other sources
- The skill should feel like asking a knowledgeable privacy colleague, not reading a database — inline citations over footnotes
- Keep disclaimer minimal and unobtrusive; target audience are professionals who understand the implications

</specifics>

<code_context>
## Existing Code Insights

### Reusable Assets
- No implementation code exists yet — greenfield project
- Codebase maps (.planning/codebase/) provide architectural reference but no reusable code
- FPF Plugin Proposal.md contains detailed FPF content universe (issue areas, publication types, tools) that can inform reference file content

### Established Patterns
- Anthropic's legal plugin structure (skills/, commands/, .claude-plugin/) serves as reference architecture
- Skill-creator skill is already installed and will handle file placement conventions

### Integration Points
- Skill triggers via `/privacy` command — needs skill-creator registration
- Reference files loaded on-demand by SKILL.md routing layer
- No external service integrations in Phase 1 (web fetching comes in Phase 4)

</code_context>

<deferred>
## Deferred Ideas

None — discussion stayed within phase scope

</deferred>

---

*Phase: 01-skill-foundation-fpf-primary-source*
*Context gathered: 2026-03-12*
