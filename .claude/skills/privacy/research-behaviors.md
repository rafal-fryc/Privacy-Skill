# Research Behaviors

These rules govern how the `/privacy` skill performs live web research using WebFetch. This file is loaded for every `/privacy` query alongside skill-behaviors.md.

This file teaches HOW to perform live research -- selecting sources, constructing URLs, fetching content, and integrating results. It complements skill-behaviors.md, which teaches HOW to format responses. This file does not contain substantive privacy knowledge.

---

## 1. Purpose and Loading

This file is loaded on every `/privacy` query as part of the research step in SKILL.md routing. It provides the complete live research workflow that augments static reference knowledge with current web content.

The research workflow follows this sequence: select sources, construct URLs, fetch content with WebFetch, integrate live content with static knowledge, and handle degradation when sources are unavailable.

Static knowledge from reference files (loaded in SKILL.md Steps 2-4) is always the foundation. Live-fetched content augments and enriches -- it never replaces the static foundation.

---

## 2. WebFetch Source Compatibility

Before selecting sources, consult the compatibility matrix in [research-reference.md](research-reference.md) Section 1. It lists which sources are accessible vs. blocked and the best URL patterns for each. Never attempt WebFetch on blocked sources (FTC, EPIC, CDT).

---

## 3. Source Selection

From the sources matched by SKILL.md routing (Steps 2-4), select up to 4 for live fetching. Only select sources that are both relevant to the query topic and listed as ACCESSIBLE in the compatibility matrix above.

**Priority order:**

1. **FPF first** (when relevant): Fetch `fpf.org/blog/` to check for recent FPF analysis on the query topic. FPF is included whenever the query overlaps with FPF's coverage areas.

2. **Primary regulatory source**: If the query involves a specific regulation, fetch that regulator's site:
   - EDPB for GDPR questions
   - CPPA for CCPA/CPRA questions
   - ICO for UK GDPR questions

3. **IAPP**: For broad privacy topics, IAPP resource articles provide cross-cutting analysis and tracking tools.

4. **Secondary source**: Choose based on topic relevance from remaining accessible sources. For example, ICO for a data protection enforcement question even if the query is not UK-specific.

**Source count guidance:**
- If fewer than 3 sources are relevant to the specific query, fetch fewer. Do not pad with irrelevant sources.
- The cap is 3-4 sources per query. Exceeding this wastes response time and context window space.
- Skip any accessible source that has no logical connection to the query topic.

---

## 4. URL Construction

For each selected source, construct a targeted content URL. Never fetch homepages or generic index pages (except FPF blog index). Consult [research-reference.md](research-reference.md) Section 2 for source-specific URL patterns and examples by query type. The nav guide files also provide URL patterns for each source.

---

## 5. WebFetch Execution

For each selected source, call WebFetch with a constructed URL and a focused, query-specific prompt.

**WebFetch call parameters:**
- **URL**: The targeted content URL from Section 4 (never a homepage or generic page)
- **Prompt**: A specific question tied to the user's query topic

**Prompt construction -- use focused questions, not generic summaries:**

- "What recent developments, enforcement actions, or regulatory updates related to [user's topic] are described on this page?"
- "What guidance or requirements related to [user's topic] does this page describe?"
- "List any publications, reports, or analysis related to [user's topic] with their titles, dates, and key findings."
- "What are the most recent posts or articles on this page related to [user's topic]? Include titles, dates, and brief descriptions."

WebFetch uses a small model to process content, so specific prompts produce substantially better results than vague ones like "summarize this page."

Execute all selected fetches in the same turn — call WebFetch for each source simultaneously rather than waiting for one to complete before starting the next. This is safe because all fetches are read-only and independent. If some fail while others succeed, use whatever content was retrieved and note the failures in the degradation handling (see [research-reference.md](research-reference.md) Section 3).

---

## 6. Content Integration

After fetching, integrate live content with static knowledge following these rules:

**Static knowledge is the foundation.** Reference files loaded in SKILL.md Steps 2-4 provide the authoritative baseline. Live-fetched content adds current developments, recent publications, enforcement updates, and amended provisions on top of this foundation.

**Theme-based interleaved synthesis.** Weave sources together by topic, not source-by-source. Do not structure responses as "According to IAPP: ... According to ICO: ..." in separate sections. Instead, organize by theme and cite sources inline as each contributes to a point.

**Contradiction handling.** When live-fetched information contradicts static knowledge, present both with dates and let the practitioner assess:
> "As of [static date], X applied. However, [live source] from [date] indicates Y."

Do not silently override static knowledge with live data or vice versa.

**Response length.** Multi-source synthesis responses may be 400-800 words (ceiling, not floor). If live content merely confirms static knowledge, a shorter response noting that live sources confirmed current accuracy is appropriate. The user can always ask for more depth.

**No source footer lists.** Inline citations are sufficient. Do not add a "Sources consulted" section at the bottom. Follow the inline citation format from skill-behaviors.md.

**Follow-up questions.** Content from WebFetch stays in the context window. For follow-up questions in the same conversation, use already-fetched content. Do not re-fetch the same URLs within the same conversation.

---

## 7. Degradation Handling

When sources are unavailable, consult [research-reference.md](research-reference.md) Section 3 for the degradation tier templates and rules. Key points to remember:

- **Known-blocked sources (FTC, EPIC, CDT) do not need degradation notes.** Their coverage always comes from static knowledge — the practitioner doesn't need to be told this every time.
- Only note degradation when a **normally-accessible source** (FPF, IAPP, EDPB, ICO, CPPA) unexpectedly fails.
- Place degradation notes before the topic heading, not at the bottom.

---

## 8. Follow-up Handling

Practitioner conversations are naturally multi-turn. Handle follow-ups based on their relationship to the original query:

**Narrowing follow-up** (e.g., "Tell me about COPPA" then "How does that apply to educational apps?"):
- Load additional reference files as needed (e.g., ferpa-reference.md for the education context)
- Reuse already-fetched WebFetch content in the context window -- do not re-fetch the same URLs
- Carry forward degradation context (if FTC was unavailable on query 1, note this for query 2)

**Topic shift** (e.g., "Tell me about COPPA" then "Now explain GDPR adequacy decisions"):
- Re-run full routing from SKILL.md Step 1 for the new topic
- New WebFetch calls are appropriate for the new topic
- Previous response context is available but should not constrain the new response

**Depth request** (e.g., "Can you go deeper on the enforcement trends you mentioned?"):
- Allow additional WebFetch calls to new URLs that were not fetched in the original response
- Do not re-fetch URLs already in the context window
- Expand the response length ceiling -- the user is explicitly asking for more depth

**General rules for all follow-ups:**
- Content from prior WebFetch calls remains in the context window -- use it
- The mandatory disclaimer footer applies to every response, including follow-ups
- FPF prioritization rules apply to every response, including follow-ups

---

*This file is loaded for every /privacy query. It governs the live research workflow: source selection, WebFetch execution, content integration, and follow-up handling. Reference data (compatibility matrix, URL patterns, degradation tiers) is in research-reference.md.*
