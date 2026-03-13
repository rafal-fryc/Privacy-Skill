# Phase 4: Deep Research + Validation - Research

**Researched:** 2026-03-13
**Domain:** Claude Code skill live fetching, WebFetch integration, multi-source synthesis, graceful degradation
**Confidence:** HIGH

## Summary

Phase 4 wires up multi-source live fetching to complete the hybrid architecture: static knowledge foundation + live web research in a single `/privacy` skill. The core deliverable is a new `research-behaviors.md` file that teaches the skill how to perform live research using WebFetch and the Phase 3 navigation guides as "site maps." SKILL.md gains a new routing step to trigger live fetching on every query.

The technical landscape is well-understood because all infrastructure exists from prior phases. The primary challenge is writing effective skill instructions (natural language markdown) that guide Claude to: (1) select 3-4 relevant sources per query, (2) construct targeted URLs from nav guide patterns, (3) use WebFetch to retrieve content, (4) synthesize live-fetched content with static knowledge, and (5) degrade gracefully when sources are unavailable. Empirical testing confirms FPF blog posts are fully WebFetch-accessible (complete article text), IAPP resource articles are accessible (some interactive content requires JS), EDPB and ICO are fully accessible, CPPA is fully accessible, while FTC (403 block), EPIC (timeout), and CDT (Cloudflare block) are not accessible.

**Primary recommendation:** Create research-behaviors.md as a focused instruction file (loaded on every query alongside skill-behaviors.md) that teaches the skill WebFetch usage patterns, source selection logic, URL construction from nav guides, synthesis approach, and degradation signaling. Modify SKILL.md Step 5 (Compose Response) to incorporate live fetching as a pre-composition step rather than adding a separate Step 5 (to stay within the 500-line limit).

<user_constraints>
## User Constraints (from CONTEXT.md)

### Locked Decisions

**Research Triggering:**
- Every query attempts live fetching -- no separate "deep research" vs "quick lookup" modes
- Static knowledge is always the foundation; live-fetched data augments and enriches on top
- Filter sources by WebFetch compatibility notes from nav guides -- don't waste time on known-broken sources (EPIC, CDT have documented limitations)
- Live fetching logic lives in a new dedicated file: research-behaviors.md (not in SKILL.md or skill-behaviors.md) -- loaded when live fetching is triggered
- SKILL.md routing adds a new step to load research-behaviors.md and trigger fetching

**Source Synthesis:**
- Theme-based, interleaved organization -- weave sources together by topic, not source-by-source sections (consistent with Phase 1 inline citation style)
- Deep research responses allow longer default (400-800 words) since multi-source synthesis naturally produces more material; user can ask for more or less
- When live-fetched info contradicts static knowledge, present both with dates and let the practitioner assess: "As of [static date], X applied. However, [live source] from [date] indicates Y."
- No "Sources consulted" footer list -- inline citations are sufficient for practitioners who read citations naturally

**Degradation Signals:**
- Brief header note when sources fail: name the specific failed sources so practitioner knows what to double-check
- Partial failure: "Note: EDPB and ICO were unavailable -- their coverage based on built-in knowledge."
- Total failure: shorter/simpler response acknowledging limitations, suggest user retry later or consult sources directly
- Use existing file-level "Last verified" dates (from Phase 2 decision) in degradation notes -- no new date infrastructure needed

**Fetch Strategy:**
- Cap at 3-4 most relevant sources per query (FPF always included when relevant)
- Use nav guide URL patterns and search strategies to construct targeted URLs -- don't just fetch homepages
- Slow/timeout sources: return partial answer from available sources + static knowledge, offer to retry the timed-out sources
- Natural conversation caching: fetched content stays in Claude's context window for follow-up questions -- no re-fetching within same conversation

### Claude's Discretion
- Exact WebFetch implementation details and error handling
- How to select the 3-4 most relevant sources from routing matches
- How to construct targeted URLs from nav guide patterns for a specific query
- Response structure adjustments when operating in degraded mode
- Validation test design for end-to-end query paths

### Deferred Ideas (OUT OF SCOPE)
None -- discussion stayed within phase scope

</user_constraints>

<phase_requirements>
## Phase Requirements

| ID | Description | Research Support |
|----|-------------|-----------------|
| ARCH-04 | Hybrid architecture: static knowledge for quick lookups, live WebFetch for deeper research | WebFetch compatibility matrix documented for all 8 sources; research-behaviors.md design pattern established; every query attempts live fetch with static as foundation |
| ARCH-05 | Graceful degradation when web access is unavailable (falls back to static knowledge) | Three-tier degradation model (partial failure, total failure, timeout) with specific user-facing language patterns; known-broken sources pre-filtered |
| DEPTH-02 | Deep research mode performs multi-source live fetching using navigation guides and synthesizes across organizations | URL construction patterns from nav guides verified; 3-4 source cap strategy; theme-based synthesis approach; WebFetch tested against primary sources |

</phase_requirements>

## Standard Stack

This phase involves no code libraries -- the entire implementation is natural language markdown files that instruct Claude's behavior within the Claude Code skill framework.

### Core
| Component | Type | Purpose | Why Standard |
|-----------|------|---------|--------------|
| research-behaviors.md | Skill instruction file | Teaches Claude how to perform live WebFetch research | Follows established pattern from skill-behaviors.md (behavioral instruction file loaded on demand) |
| SKILL.md modifications | Routing layer update | Adds live fetching trigger to query routing pipeline | Extends existing 5-step routing architecture |
| WebFetch | Built-in Claude Code tool | Fetches web page content and answers questions about it | Already available in every Claude Code session; no installation needed |

### Supporting
| Component | Type | Purpose | When Used |
|-----------|------|---------|-----------|
| Nav guides (7 files) | Existing reference files | Provide URL patterns and WebFetch compatibility for source targeting | Referenced by research-behaviors.md to construct fetch URLs |
| skill-behaviors.md | Existing instruction file | Governs response formatting, attribution, disclaimers | Unchanged; research-behaviors.md works alongside it |

### Not Applicable
No npm packages, no Python libraries, no build tools. This is a purely markdown-based skill extension.

## Architecture Patterns

### File Structure (additions/modifications only)
```
.claude/skills/privacy/
├── SKILL.md                  # MODIFIED: add research trigger step
├── research-behaviors.md     # NEW: live fetching instructions
├── skill-behaviors.md        # UNCHANGED: response formatting
├── fpf-reference.md          # UNCHANGED: static knowledge
├── *-nav.md (7 files)        # UNCHANGED: referenced as "site maps"
├── *-reference.md (6 files)  # UNCHANGED: static knowledge
└── *.md (3 catalogs)         # UNCHANGED: org catalogs
```

### Pattern 1: Behavioral Instruction File (research-behaviors.md)

**What:** A markdown file loaded into Claude's context that provides natural language instructions for how to perform a specific behavior (live web research). This follows the established pattern of skill-behaviors.md which instructs response formatting.

**When to use:** When Claude needs a complex, multi-step workflow that requires judgment (source selection, URL construction, synthesis). The instructions are directives, not templates.

**Structure:**
```markdown
# Research Behaviors

## 1. Source Selection
[Instructions for choosing 3-4 sources from routing matches]

## 2. URL Construction
[Instructions for building targeted URLs from nav guide patterns]

## 3. WebFetch Execution
[Instructions for calling WebFetch with constructed URLs]

## 4. Content Integration
[Instructions for weaving live content with static knowledge]

## 5. Degradation Handling
[Instructions for communicating source failures]
```

**Key design principle:** research-behaviors.md teaches HOW to research, just as skill-behaviors.md teaches HOW to format responses. It does not contain substantive privacy knowledge.

### Pattern 2: SKILL.md Routing Extension

**What:** Modify the existing routing pipeline to add a live fetching trigger. The existing pipeline is Steps 1-4 (load behaviors, check FPF, check regulations, check orgs) + Step 5 (compose response).

**Recommended approach:** Insert a new Step 5 (Research) before the current Step 5 (Compose), making the current Step 5 become Step 6. The new step loads research-behaviors.md and triggers live fetching.

**Line budget analysis:**
- Current SKILL.md: 275 lines
- 500-line limit: 225 lines headroom
- Estimated new Step 5 addition: 30-50 lines (routing trigger + brief description)
- Estimated metadata/example updates: 10-20 lines
- Total estimated addition: 40-70 lines
- Projected total: 315-345 lines (well within limit)

**Routing logic for new step:**
```
Step 5: Live Research (ALWAYS -- every query)
  1. Load research-behaviors.md
  2. Follow its instructions to select sources, construct URLs, fetch content
  3. Proceed to Step 6 (Compose Response) with both static and live context
```

### Pattern 3: WebFetch Source Compatibility Matrix

**What:** A lookup table embedded in research-behaviors.md that tells Claude which sources support WebFetch and which do not, so it never wastes time on known-broken sources.

**Verified matrix (March 2026):**

| Source | WebFetch Status | Best URL Pattern | Notes |
|--------|----------------|------------------|-------|
| FPF (fpf.org) | ACCESSIBLE | Blog posts: `fpf.org/blog/[slug]/` | Full article text available; issue area pages return 404 (URL pattern may differ) |
| IAPP (iapp.org) | ACCESSIBLE | Resource articles: `iapp.org/resources/article/[slug]/` | Full content on article pages; search results require JS |
| EDPB (edpb.europa.eu) | ACCESSIBLE | All pages with `_en` suffix | Full HTML content; document listings include metadata |
| ICO (ico.org.uk) | ACCESSIBLE | Guidance: `ico.org.uk/for-organisations/[topic]/` | Substantial inline content; enforcement register accessible |
| CPPA (cppa.ca.gov) | ACCESSIBLE | All pages | High reliability; server-side rendered; no blocking |
| FTC (ftc.gov) | BLOCKED (403) | None | Server-wide bot detection; use IAPP as alternative |
| EPIC (epic.org) | BLOCKED (Timeout) | None | Connection timeouts; use WebSearch as alternative |
| CDT (cdt.org) | BLOCKED (Cloudflare) | None | Cloudflare bot protection; use WebSearch as alternative |

### Pattern 4: URL Construction from Nav Guides

**What:** research-behaviors.md instructs Claude to use nav guide URL patterns + query context to construct specific, targeted URLs rather than fetching generic homepages.

**Examples of targeted URL construction:**
- Query about children's privacy law developments:
  - FPF: `fpf.org/blog/` (scan recent posts for relevant titles) OR construct slug from known topic patterns
  - IAPP: `iapp.org/resources/article/us-state-privacy-legislation-tracker/` (known tracker URL)
  - CPPA: `cppa.ca.gov/regulations/` (for CCPA/CPRA minor provisions updates)
  - ICO: `ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/childrens-information/` (children's code guidance)

- Query about GDPR enforcement trends:
  - FPF: `fpf.org/blog/` (scan for GDPR-related posts)
  - EDPB: `edpb.europa.eu/our-work-tools/general-guidance/guidelines-recommendations-best-practices_en`
  - ICO: `ico.org.uk/action-weve-taken/enforcement/` (enforcement register)
  - IAPP: Relevant resource article if known

**Key insight:** The nav guides were built in Phase 3 specifically to serve as "site maps" for this purpose. Each nav guide contains: URL patterns, key URLs, content type descriptions, and search strategies. research-behaviors.md should instruct Claude to read the loaded nav guide(s) and use their URL patterns to construct the most targeted URL for the specific query.

### Pattern 5: Degradation Communication

**What:** Three tiers of degradation with specific language patterns.

**Tier 1 -- Partial failure (some sources unavailable):**
```
> **Note:** [Source A] and [Source B] were unavailable during this research --
> their coverage is based on built-in knowledge (last verified [date from file]).
```

**Tier 2 -- Total web failure (all WebFetch attempts fail):**
```
> **Note:** Live source retrieval was unavailable for this query. This response
> draws from built-in reference knowledge. For the most current information,
> consult the sources cited directly, or retry this query later.
```

**Tier 3 -- Timeout/slow response (some sources still loading):**
Provide answer from available sources + static knowledge, note which sources timed out, offer to retry.

### Anti-Patterns to Avoid

- **Fetching homepages instead of targeted content pages:** Homepages waste the WebFetch content budget on navigation chrome. Always construct a specific content URL using nav guide patterns.
- **Fetching known-broken sources:** EPIC, CDT, and FTC are documented as inaccessible. Never attempt WebFetch on these -- use static knowledge and note it.
- **Source-by-source response organization:** Locked decision requires theme-based interleaved synthesis. Never structure responses as "According to IAPP: ... According to ICO: ..." in separate sections.
- **Overly alarming degradation language:** Privacy practitioners routinely deal with partial information. Degradation notes should be brief and factual, not apologetic.
- **Re-fetching within same conversation:** Content from WebFetch stays in Claude's context window. Follow-up questions should use already-fetched content, not re-fetch the same URLs.

## Don't Hand-Roll

| Problem | Don't Build | Use Instead | Why |
|---------|-------------|-------------|-----|
| Web content retrieval | Custom HTTP client or scraping logic | WebFetch (built-in Claude Code tool) | WebFetch handles HTTP, HTML-to-markdown conversion, content summarization, and caching |
| Source accessibility detection | Runtime probing of source availability | Pre-documented compatibility matrix in research-behaviors.md | Sources don't change accessibility frequently; probing wastes time and may produce confusing errors |
| URL pattern matching | Complex regex or template systems | Natural language instructions referencing nav guide URL patterns | Claude excels at pattern-based URL construction from examples; rigid templates are fragile |
| Content caching | Explicit cache management system | Claude's context window (conversation-level caching) | Content stays in context for follow-ups; no infrastructure needed |
| Response length management | Token counting or word limits | Natural language instruction ("400-800 words for multi-source synthesis") | Claude manages length well from natural language guidance |

**Key insight:** This is a Claude Code skill -- the entire system is natural language instructions that guide Claude's behavior. There is no code to write, only instructions to craft. The temptation to over-engineer with pseudo-code or rigid templates should be resisted in favor of clear, directive natural language.

## Common Pitfalls

### Pitfall 1: SKILL.md Line Limit Creep
**What goes wrong:** Adding a full research step with detailed instructions in SKILL.md pushes it past the 500-line limit.
**Why it happens:** The research step feels like it needs detailed explanation in the routing layer.
**How to avoid:** Keep the SKILL.md step minimal (just "load research-behaviors.md and follow its instructions"). All details live in research-behaviors.md. The routing step should be ~30 lines max.
**Warning signs:** SKILL.md exceeding 350 lines after modifications.

### Pitfall 2: WebFetch Prompt Engineering
**What goes wrong:** WebFetch returns unhelpful summaries because the prompt is too vague (e.g., "What's on this page?").
**Why it happens:** WebFetch uses a small model (Haiku) to process content, so vague prompts get vague answers.
**How to avoid:** research-behaviors.md should instruct Claude to craft specific, focused prompts for WebFetch. Example: "What recent enforcement actions or regulatory updates related to [query topic] are described on this page?" rather than "Summarize this page."
**Warning signs:** WebFetch returning generic site descriptions instead of topic-relevant content.

### Pitfall 3: FPF URL Pattern Mismatch
**What goes wrong:** Attempting to fetch FPF issue area pages (e.g., `fpf.org/issue/ai/`) returns 404.
**Why it happens:** FPF's issue area URL patterns may differ from what's documented in fpf-reference.md, or those pages may be dynamically rendered. Testing confirmed `fpf.org/issue/ai/` and `fpf.org/issue-areas/` both return 404.
**How to avoid:** For FPF, always target blog post URLs (`fpf.org/blog/[slug]/`) or the blog index (`fpf.org/blog/`). The blog index is confirmed accessible and shows recent post titles with URLs. Individual blog posts return complete article text.
**Warning signs:** 404 errors from fpf.org URLs that are not blog posts.

### Pitfall 4: Over-fetching Sources
**What goes wrong:** Attempting to fetch 6-7 sources per query, causing slow responses and context window bloat.
**Why it happens:** Wanting to be comprehensive for every query.
**How to avoid:** Hard cap at 3-4 sources (locked decision). FPF is always included when relevant, plus 2-3 others selected by topic relevance. Static knowledge covers the rest.
**Warning signs:** Responses taking noticeably longer than static-only responses; context window filling up with fetched content.

### Pitfall 5: Degradation Note Confusion
**What goes wrong:** Degradation notes reference sources the user didn't ask about, or fail to distinguish between "source was unavailable" and "source had no relevant content."
**Why it happens:** Degradation logic triggers for all selected sources, not just topic-relevant ones.
**How to avoid:** Only mention failed sources that were selected as relevant to the specific query. If a source was selected, fetched, and had no relevant content, that's not a degradation -- it just means the source didn't cover the topic.
**Warning signs:** Degradation notes listing sources that aren't logically connected to the query.

### Pitfall 6: Contradiction Handling Ambiguity
**What goes wrong:** When live content contradicts static knowledge, the response either ignores the contradiction or creates confusion about which is correct.
**Why it happens:** Not following the locked decision on contradiction handling.
**How to avoid:** Follow the prescribed pattern: present both with dates. "As of [static date], X applied. However, [live source] from [date] indicates Y." Let the practitioner assess.
**Warning signs:** Responses that silently override static knowledge with live data, or vice versa.

## Code Examples

This section contains verified patterns for skill instruction writing, not code.

### WebFetch Invocation Pattern (for research-behaviors.md)

The research-behaviors.md file will instruct Claude to use WebFetch like this (natural language instruction, not code):

```markdown
When fetching from a source, call WebFetch with:
- **URL:** A specific content page URL constructed from the source's nav guide URL patterns
  (never a homepage or search results page)
- **Prompt:** A focused question tied to the user's query. Examples:
  - "What recent developments, enforcement actions, or regulatory updates
    related to [user's topic] are described on this page?"
  - "What guidance or requirements related to [user's topic] does this page describe?"
  - "List any publications, reports, or analysis related to [user's topic]
    with their titles, dates, and key findings."
```

### Source Selection Logic (for research-behaviors.md)

```markdown
From the sources matched by SKILL.md routing (Steps 2-4), select up to 4 for live fetching:

1. **FPF first** (when relevant): Fetch fpf.org/blog/ to check for recent FPF
   analysis on the query topic
2. **Primary regulatory source**: If the query involves a specific regulation,
   fetch that regulator's site (EDPB for GDPR, CPPA for CCPA, ICO for UK GDPR)
3. **IAPP**: For broad privacy topics, IAPP resource articles provide
   cross-cutting coverage
4. **Secondary source**: Choose based on topic relevance from remaining
   accessible sources

**Skip known-inaccessible sources:** Do not attempt WebFetch on FTC (403 block),
EPIC (timeout), or CDT (Cloudflare block). Use static knowledge for these
and note in degradation header if they were relevant.
```

### SKILL.md Step Addition (approximate content)

```markdown
### Step 5: Live Research (ALWAYS -- every query)

Load [research-behaviors.md](research-behaviors.md) and follow its instructions to:
1. Select up to 3-4 relevant sources from the routing matches in Steps 2-4
2. Construct targeted URLs using the loaded nav guide URL patterns
3. Fetch each selected source using WebFetch with a focused, query-specific prompt
4. Note any sources that fail or are unavailable for degradation handling

This step augments your static knowledge with live information. Static knowledge
from reference files (loaded in Steps 2-4) remains the foundation. Live-fetched
content adds current developments, recent publications, and updated enforcement data.

After completing live research, proceed to Step 6 (Compose Response) with both
static reference knowledge and live-fetched content available.
```

### Degradation Header Pattern

```markdown
When one or more selected sources fail during WebFetch:

**Partial failure format (place at start of response, before topic heading):**
> **Note:** [Source names] were unavailable during this research -- their coverage
> is based on built-in knowledge (last verified [date]).

**Total failure format:**
> **Note:** Live source retrieval was unavailable for this query. This response draws
> from built-in reference knowledge. For the most current information, consult the
> sources cited directly, or retry this query later.

Degradation notes should be:
- Brief (one sentence for partial, two for total)
- Factual (name the specific sources, not "some sources")
- Not apologetic (practitioners routinely work with partial information)
- Placed before the topic heading, not at the bottom
```

## State of the Art

| Old Approach | Current Approach | When Changed | Impact |
|--------------|------------------|--------------|--------|
| Separate "quick lookup" vs "deep research" modes | Every query attempts live fetch; static knowledge is foundation | Phase 4 design (CONTEXT.md decision) | Simpler architecture; no mode-switching logic needed |
| Source-by-source response organization | Theme-based interleaved synthesis | Phase 1 pattern extended to live content (CONTEXT.md decision) | Consistent with inline citation style; more natural reading flow |
| Claude Code skills as static-only reference | Skills with live WebFetch integration | Claude Code tool availability (ongoing) | Enables hybrid static+live knowledge architecture |

## Open Questions

1. **FPF Blog URL Construction for Targeted Topics**
   - What we know: `fpf.org/blog/` index page lists recent posts with URLs and titles; individual blog post pages serve complete article text. Issue area pages (`fpf.org/issue/[area]/`) return 404 via WebFetch.
   - What's unclear: Whether there is a FPF blog category/tag URL pattern that filters posts by topic (e.g., `fpf.org/blog/?category=ai`). The blog index shows all recent posts, which may not be topic-relevant.
   - Recommendation: Fetch `fpf.org/blog/` and ask WebFetch to identify posts related to the query topic from the titles listed. If a relevant title is found, fetch that specific blog post URL for full content. This two-step approach (index scan + targeted fetch) works within the 3-4 source cap since both fetches are to FPF.

2. **WebFetch Concurrent Execution**
   - What we know: WebFetch has a 15-minute cache. Individual fetches complete in seconds.
   - What's unclear: Whether Claude Code executes multiple WebFetch calls sequentially or can issue them concurrently. Sequential fetching of 3-4 sources could add 10-20 seconds to response time.
   - Recommendation: Write instructions assuming sequential execution (simplest approach). If latency becomes an issue, this can be revisited. The user accepted that live-augmented responses may take longer.

3. **Response Length Calibration with Live Content**
   - What we know: Locked decision allows 400-800 words for multi-source synthesis. Current static-only responses target 200-400 words.
   - What's unclear: Whether 400-800 words is consistently achievable/desirable when live fetching produces limited new information (i.e., when live sources mostly confirm static knowledge).
   - Recommendation: 400-800 words is a ceiling, not a floor. If live content merely confirms static knowledge, a 300-word response with a note that "live sources confirmed current accuracy of [regulation/topic]" is appropriate.

## Validation Architecture

### Test Framework
| Property | Value |
|----------|-------|
| Framework | Manual end-to-end testing via `/privacy` command invocation |
| Config file | None -- skill is markdown-based, no automated test runner |
| Quick run command | `/privacy [test query]` in Claude Code session |
| Full suite command | Run all validation queries listed below sequentially |

### Phase Requirements to Test Map
| Req ID | Behavior | Test Type | Validation Command | Exists? |
|--------|----------|-----------|-------------------|---------|
| ARCH-04 | Live WebFetch augments static knowledge | manual e2e | `/privacy What is the current state of children's privacy law?` -- verify response includes live-fetched content alongside static COPPA/FERPA knowledge | No -- Wave 0 |
| ARCH-04 | FPF blog content accessible via live fetch | manual e2e | `/privacy What has FPF published about AI governance recently?` -- verify response cites specific recent FPF blog posts with dates | No -- Wave 0 |
| ARCH-05 | Graceful degradation on partial failure | manual e2e | Verify degradation header appears when specific sources are unavailable (FTC, EPIC, CDT queries will naturally trigger this) | No -- Wave 0 |
| ARCH-05 | Graceful degradation on total failure | manual e2e | Test in offline/restricted network mode -- verify response uses static knowledge with total failure note | No -- Wave 0 |
| DEPTH-02 | Multi-source synthesis | manual e2e | `/privacy Current state of AI regulation globally` -- verify response weaves content from 3+ sources in theme-based structure | No -- Wave 0 |
| DEPTH-02 | Source selection from routing matches | manual e2e | Verify that different query topics select different source combinations (regulation query vs. org query vs. cross-cutting query) | No -- Wave 0 |

### Sampling Rate
- **Per task:** Run 2-3 representative test queries after each file modification
- **Per wave/plan:** Run full validation suite (all 6 test queries above)
- **Phase gate:** All 6 validation queries produce correct behavior before `/gsd:verify-work`

### Wave 0 Gaps
- [ ] Validation query set needs to be designed as part of implementation planning (not a file gap -- these are manual interactive tests)
- [ ] No automated testing is possible for this phase -- all validation is manual skill invocation
- [ ] Framework install: N/A -- no test framework needed for markdown skill testing

## Sources

### Primary (HIGH confidence)
- Claude Code official skills documentation (code.claude.com/docs/en/skills) -- verified skill structure, frontmatter, progressive loading, WebFetch availability
- FPF blog WebFetch test (fpf.org/blog/) -- confirmed accessible, returns blog post titles and dates; individual posts return complete article text
- IAPP WebFetch test (iapp.org/resources/article/us-state-privacy-legislation-tracker/) -- confirmed accessible, content available but interactive elements require JS
- All 7 nav guide WebFetch Notes sections (edpb-nav.md, ico-nav.md, cppa-nav.md, iapp-nav.md, ftc-nav.md, epic-nav.md, cdt-nav.md) -- documented source accessibility from Phase 3 testing

### Secondary (MEDIUM confidence)
- WebFetch technical analysis (mikhail.io) -- Haiku 3.5 processing model, 100KB content limit, 125-char quote limit, 15-minute cache
- FPF issue area URL patterns -- `fpf.org/issue/[area]/` confirmed 404 via WebFetch (pattern may differ or require JS)

### Tertiary (LOW confidence)
- WebFetch concurrent execution behavior -- unclear from documentation whether multiple calls can execute in parallel

## Metadata

**Confidence breakdown:**
- Standard stack: HIGH -- no external libraries; using only built-in WebFetch tool and established skill instruction patterns
- Architecture: HIGH -- extends well-understood Phase 1-3 patterns (progressive loading, behavioral instruction files, routing pipeline)
- Pitfalls: HIGH -- all source accessibility tested empirically; common failure modes documented from direct testing
- WebFetch internals: MEDIUM -- processing pipeline documented by third party, not official Anthropic docs

**Research date:** 2026-03-13
**Valid until:** 2026-04-13 (30 days -- WebFetch tool behavior and source accessibility could change)
