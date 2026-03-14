# Research Reference Data

Reference material for the `/privacy` skill's live research workflow. This file is consulted as-needed during research — it is NOT loaded in full on every query. The main research workflow is in [research-behaviors.md](research-behaviors.md).

---

## 1. WebFetch Source Compatibility

Verified compatibility matrix. Never attempt WebFetch on blocked sources.

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

When a blocked source is relevant to the query, use static knowledge from its reference and nav guide files. Do not mention blocked sources in degradation notes (see Section 3, Tier 0).

---

## 2. URL Construction Patterns

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

## 3. Degradation Handling

When sources are unavailable during live research, communicate this with brief, factual notes. Practitioners routinely work with partial information — degradation notes should be informative, not apologetic.

**Tier 0 -- Known-blocked sources (no note needed):**

Sources documented as permanently blocked in the compatibility matrix (FTC, EPIC, CDT) do not warrant a degradation note. Their coverage is always from static knowledge — the practitioner doesn't need to be told this every time. Only note a source failure when a normally-accessible source (FPF, IAPP, EDPB, ICO, CPPA) unexpectedly fails.

**Tier 1 -- Unexpected source failure (some accessible sources unavailable):**

Place this note before the topic heading:

> **Note:** [Source A] and [Source B] were unexpectedly unavailable during this research — their coverage is based on built-in knowledge (last verified [date from file]).

**Tier 2 -- Total web failure (all WebFetch attempts fail):**

Place this note before the topic heading:

> **Note:** Live source retrieval was unavailable for this query. This response draws from built-in reference knowledge. For the most current information, consult the sources cited directly, or retry this query later.

**Tier 3 -- Timeout/slow (some sources still loading):**

Provide the answer from available sources and static knowledge. Note which sources timed out and offer to retry:

> **Note:** [Source name] timed out during this research. The response below uses available sources and built-in knowledge. I can retry [source name] if you'd like.

**Degradation note rules:**
- Only mention failed sources that were selected as relevant to the specific query
- Known-blocked sources (FTC, EPIC, CDT) are covered by Tier 0 — do not include them in degradation notes
- Place degradation notes BEFORE the topic heading, not at the bottom of the response
- Keep notes to one or two sentences — brief and factual
- A source that was fetched successfully but contained no relevant content is NOT a degradation — it simply means the source did not cover the topic

---

*This file contains reference data for the research workflow. It is consulted as-needed, not loaded on every query. The main workflow is in research-behaviors.md.*
