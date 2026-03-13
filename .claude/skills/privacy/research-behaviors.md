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

Before selecting sources for live fetching, consult this verified compatibility matrix. Never attempt WebFetch on blocked sources.

| Source | Status | Best URL Pattern | Notes |
|--------|--------|------------------|-------|
| FPF (fpf.org) | ACCESSIBLE | `fpf.org/blog/` and `fpf.org/blog/[slug]/` | Blog index lists recent posts; individual posts return full article text. Do NOT use `fpf.org/issue/` URLs (confirmed 404). |
| IAPP (iapp.org) | ACCESSIBLE | `iapp.org/resources/article/[slug]/` | Full content on article pages; search results require JS and are not accessible. |
| EDPB (edpb.europa.eu) | ACCESSIBLE | Pages with `_en` suffix | Full HTML content; document listings include metadata. |
| ICO (ico.org.uk) | ACCESSIBLE | `ico.org.uk/for-organisations/[topic]/` | Substantial inline content; enforcement register accessible. |
| CPPA (cppa.ca.gov) | ACCESSIBLE | Direct page URLs | High reliability; server-side rendered; no blocking. |
| FTC (ftc.gov) | BLOCKED (403) | -- | Server-wide bot detection. Use static knowledge from ftc-nav.md. |
| EPIC (epic.org) | BLOCKED (Timeout) | -- | Connection timeouts. Use static knowledge from epic-nav.md. |
| CDT (cdt.org) | BLOCKED (Cloudflare) | -- | Cloudflare bot protection. Use static knowledge from cdt-nav.md. |

When a blocked source is relevant to the query, use static knowledge from its reference and nav guide files. Note the source in the degradation header with its "Last verified" date from the nav guide file.

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

For each selected source, construct a targeted content URL using the URL patterns from that source's nav guide file. The nav guides were built as "site maps" for exactly this purpose.

**Key principle:** NEVER fetch homepages or generic index pages (except FPF blog index). Always construct a specific content URL that is likely to contain information relevant to the query.

**Source-specific URL construction:**

- **FPF**: Fetch `fpf.org/blog/` first (the blog index is confirmed accessible and lists recent post titles). Ask WebFetch to identify posts related to the query topic. If a relevant title is found, fetch that specific blog post URL (`fpf.org/blog/[slug]/`) for full content. This two-step approach (index scan + targeted fetch) counts as FPF within the source cap.

- **IAPP**: Use `iapp.org/resources/article/[slug]/` for known resource articles. For example, `iapp.org/resources/article/us-state-privacy-legislation-tracker/` for state privacy law queries. Consult iapp-nav.md for available article slugs.

- **EDPB**: Use pages with the `_en` suffix. For example, `edpb.europa.eu/our-work-tools/general-guidance/guidelines-recommendations-best-practices_en` for GDPR guidance. Consult edpb-nav.md for section URL patterns.

- **ICO**: Use `ico.org.uk/for-organisations/[topic]/` for guidance pages. For example, `ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/childrens-information/` for children's data queries. Consult ico-nav.md for topic paths.

- **CPPA**: Use direct page URLs from cppa-nav.md. For example, `cppa.ca.gov/regulations/` for CCPA/CPRA regulatory updates.

**URL construction examples by query type:**

- *Children's privacy law developments*: FPF blog index, IAPP state legislation tracker, CPPA regulations page, ICO children's information guidance
- *GDPR enforcement trends*: FPF blog index, EDPB guidelines/best practices page, ICO enforcement register, IAPP relevant resource article
- *AI regulation updates*: FPF blog index, EDPB AI-related guidance page, ICO AI and data protection guidance

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

Execute fetches sequentially -- one source at a time. If a fetch fails or times out, note the failure and proceed to the next source. Do not retry failed fetches during the same response.

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

When sources are unavailable during live research, communicate this with brief, factual notes. Practitioners routinely work with partial information -- degradation notes should be informative, not apologetic.

**Tier 1 -- Partial failure (some sources unavailable):**

Place this note before the topic heading:

> **Note:** [Source A] and [Source B] were unavailable during this research -- their coverage is based on built-in knowledge (last verified [date from file]).

**Tier 2 -- Total web failure (all WebFetch attempts fail):**

Place this note before the topic heading:

> **Note:** Live source retrieval was unavailable for this query. This response draws from built-in reference knowledge. For the most current information, consult the sources cited directly, or retry this query later.

**Tier 3 -- Timeout/slow (some sources still loading):**

Provide the answer from available sources and static knowledge. Note which sources timed out and offer to retry:

> **Note:** [Source name] timed out during this research. The response below uses available sources and built-in knowledge. I can retry [source name] if you'd like.

**Degradation note rules:**
- Only mention failed sources that were selected as relevant to the specific query
- Known-blocked sources (FTC, EPIC, CDT) that are relevant to the query: include them in the degradation note as "based on built-in knowledge" with their "Last verified" date from their nav guide files
- Place degradation notes BEFORE the topic heading, not at the bottom of the response
- Keep notes to one or two sentences -- brief and factual
- A source that was fetched successfully but contained no relevant content is NOT a degradation -- it simply means the source did not cover the topic

---

*This file is loaded for every /privacy query. It governs live web research workflow: source selection, URL construction, WebFetch invocation, content integration with static knowledge, and graceful degradation.*
