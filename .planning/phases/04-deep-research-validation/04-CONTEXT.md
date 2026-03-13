# Phase 4: Deep Research + Validation - Context

**Gathered:** 2026-03-13
**Status:** Ready for planning

<domain>
## Phase Boundary

Wire up multi-source live fetching using WebFetch and the Phase 3 navigation guides. Every `/privacy` query attempts live fetching (static knowledge as foundation, live data augments). Implement graceful degradation when sources are unavailable. Validate all query paths end-to-end. This phase completes the hybrid architecture: static knowledge base + live web research in a single skill.

</domain>

<decisions>
## Implementation Decisions

### Research Triggering
- Every query attempts live fetching — no separate "deep research" vs "quick lookup" modes
- Static knowledge is always the foundation; live-fetched data augments and enriches on top
- Filter sources by WebFetch compatibility notes from nav guides — don't waste time on known-broken sources (EPIC, CDT have documented limitations)
- Live fetching logic lives in a new dedicated file: research-behaviors.md (not in SKILL.md or skill-behaviors.md) — loaded when live fetching is triggered
- SKILL.md routing adds a new step to load research-behaviors.md and trigger fetching

### Source Synthesis
- Theme-based, interleaved organization — weave sources together by topic, not source-by-source sections (consistent with Phase 1 inline citation style)
- Deep research responses allow longer default (400-800 words) since multi-source synthesis naturally produces more material; user can ask for more or less
- When live-fetched info contradicts static knowledge, present both with dates and let the practitioner assess: "As of [static date], X applied. However, [live source] from [date] indicates Y."
- No "Sources consulted" footer list — inline citations are sufficient for practitioners who read citations naturally

### Degradation Signals
- Brief header note when sources fail: name the specific failed sources so practitioner knows what to double-check
- Partial failure: "Note: EDPB and ICO were unavailable — their coverage based on built-in knowledge."
- Total failure: shorter/simpler response acknowledging limitations, suggest user retry later or consult sources directly
- Use existing file-level "Last verified" dates (from Phase 2 decision) in degradation notes — no new date infrastructure needed

### Fetch Strategy
- Cap at 3-4 most relevant sources per query (FPF always included when relevant)
- Use nav guide URL patterns and search strategies to construct targeted URLs — don't just fetch homepages. This is why nav guides were built in Phase 3
- Slow/timeout sources: return partial answer from available sources + static knowledge, offer to retry the timed-out sources
- Natural conversation caching: fetched content stays in Claude's context window for follow-up questions — no re-fetching within same conversation

### Claude's Discretion
- Exact WebFetch implementation details and error handling
- How to select the 3-4 most relevant sources from routing matches
- How to construct targeted URLs from nav guide patterns for a specific query
- Response structure adjustments when operating in degraded mode
- Validation test design for end-to-end query paths

</decisions>

<specifics>
## Specific Ideas

- research-behaviors.md is the key new file — it teaches the skill HOW to do live research, complementing skill-behaviors.md which teaches HOW to format responses
- The nav guides from Phase 3 are the core infrastructure: research-behaviors.md should reference them as "site maps" for constructing fetching targets
- The "always attempt live" approach means even "What does COPPA require?" tries to fetch, but the static COPPA reference file provides the foundation and live fetch adds any recent enforcement actions or amendments
- Degradation should feel natural, not alarming — privacy practitioners routinely deal with partial information

</specifics>

<code_context>
## Existing Code Insights

### Reusable Assets
- SKILL.md (275/500 lines): 5-step routing pipeline — needs a new step for research/fetching trigger
- skill-behaviors.md: response formatting, attribution, anti-hallucination rules — governs how live-fetched content is presented
- 7 nav guides (iapp, epic, cppa, cdt, ftc, edpb, ico) + fpf-reference.md: URL patterns, WebFetch compatibility notes, search strategies — the "site maps" for live fetching
- 3 catalog files (advocacy-orgs.md, gov-regulators.md, academic-centers.md): org context for routing decisions
- 6 regulation reference files: static knowledge foundation that live data augments

### Established Patterns
- Progressive disclosure: reference files loaded on-demand by SKILL.md routing
- Independent additive routing steps (1-4): new research step follows same pattern
- Three-tier anti-hallucination (strict/high/standard): applies to live-fetched content verification
- File-level verification dates: reused for degradation date references

### Integration Points
- SKILL.md needs new Step 5 (or modified Step 5): load research-behaviors.md and trigger fetching
- research-behaviors.md references nav guides for URL construction
- Degradation notes integrate with existing disclaimer footer from skill-behaviors.md
- WebFetch tool already available in Claude Code — no external tooling needed

</code_context>

<deferred>
## Deferred Ideas

None — discussion stayed within phase scope

</deferred>

---

*Phase: 04-deep-research-validation*
*Context gathered: 2026-03-13*
