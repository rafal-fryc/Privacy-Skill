# Pitfalls Research

**Domain:** Knowledge-heavy Claude Code skill for data privacy research (FPF Plugin)
**Researched:** 2026-03-12
**Confidence:** HIGH (verified against official Claude Code docs, Anthropic skill best practices, and legal hallucination research)

## Critical Pitfalls

### Pitfall 1: Skill Description Character Budget Overflow

**What goes wrong:**
With 18 skills planned for Phase 1, the skill descriptions will collectively exceed the system prompt character budget. Claude Code allocates a budget that "scales dynamically at 2% of the context window, with a fallback of 16,000 characters" for all skill descriptions combined. Each skill's `description` field has a 1,024 character max, so 18 skills at even moderate description lengths (400-500 chars each) would consume 7,200-9,000 characters. But this project also needs to coexist with user's other installed skills (personal, enterprise, other plugins). If the user has 10+ other skills installed, the combined descriptions will blow past the budget, and Claude will silently drop skills -- it will not warn the user, it will just pretend some skills don't exist.

**Why it happens:**
The proposal treats each FPF domain as a separate auto-invoked skill. This works architecturally but ignores the shared character budget. 18 separate skills is at the upper bound of what a single plugin can deploy without crowding out other skills.

**How to avoid:**
- Consolidate the 15 domain skills into fewer, broader skills (5-7 domain clusters) with internal topic routing via supporting files. For example: "U.S. & Global Privacy Law" (covers U.S. legislation + global data protection), "AI & Emerging Tech" (covers AI governance + AI legislation + PETs + immersive tech), "Sector Privacy" (health + ad tech + open banking), "Community & Research" (smart communities + research ethics + cybersecurity), "Youth & Biometrics" (youth/education + biometrics + mobility/location).
- Keep each skill's `description` field under 200 characters. Use the 1,024 char max only when absolutely necessary.
- Use supporting reference files for topic depth rather than encoding detail in the description.
- Test with `SLASH_COMMAND_TOOL_CHAR_BUDGET` awareness: run `/context` to check for warnings about excluded skills.

**Warning signs:**
- Skills stop auto-activating on relevant queries.
- Running `/context` shows a warning about excluded skills.
- User has to manually invoke skills that should auto-trigger.

**Phase to address:**
Phase 0 (Architecture/Design) -- skill consolidation must happen before any skill content is written.

---

### Pitfall 2: SKILL.md Files Stuffed With Static Content

**What goes wrong:**
The natural temptation is to embed comprehensive regulatory knowledge, enforcement timelines, organization catalogs, and navigation guides directly in each SKILL.md. Official Anthropic guidance says "Keep SKILL.md under 500 lines" and to "move detailed reference material to separate files." But 500 lines is generous -- the real constraint is that every token in a loaded SKILL.md competes with conversation history and other context. A skill that tries to encode 50 state privacy laws, their enforcement dates, cure periods, and opt-out signal deadlines in a single file will consume thousands of tokens on every invocation, leaving less room for the user's actual research question and Claude's reasoning.

**Why it happens:**
The hybrid architecture (static knowledge + live fetching) encourages front-loading content "for quick lookups." Developers over-index on completeness, treating the SKILL.md as a reference manual rather than a navigation guide.

**How to avoid:**
- SKILL.md is an index and routing layer, not a knowledge base. It should tell Claude what to look for and where to find it, not contain the answers.
- Use progressive disclosure with one-level-deep references: `SKILL.md -> reference/us-state-laws.md`, `SKILL.md -> reference/enforcement-dates.md`.
- For the FPF Source Catalog skill specifically: don't list all 407+ resources inline. Instead, organize resources by topic in separate files and have the SKILL.md describe the catalog structure.
- Target SKILL.md body at 100-200 lines for domain skills, 200-300 for cross-cutting skills. Reserve the full 500-line budget for genuinely complex skills.
- Test with real queries to see how much context each skill consumes.

**Warning signs:**
- SKILL.md exceeds 300 lines of content (not counting frontmatter).
- Claude's responses become shallow or lose track of conversation context after a skill loads.
- Context compaction triggers frequently during skill-assisted conversations.

**Phase to address:**
Phase 1 (Foundation) -- enforce a strict skill template with size limits before writing any skill content.

---

### Pitfall 3: Navigation Guides That Tell Claude "Search the Website" Without Specifics

**What goes wrong:**
Per-source navigation guides are a core feature of this skill. But a guide that says "search fpf.org for relevant articles" or "check the IAPP website for resources" is useless -- Claude already knows how to search websites. The guide must encode structural knowledge Claude cannot infer: URL patterns, content organization, which sections contain what type of content, where the search function is, what query terms work best. Without this, the skill degrades to generic "go Google it" instructions that waste tokens without adding value.

**Why it happens:**
Writing effective site navigation guides requires actually mapping each website's structure -- understanding its URL patterns, content taxonomy, and search behavior. This is tedious work that gets skipped in favor of high-level descriptions.

**How to avoid:**
- For each indexed source, document: (1) URL structure patterns (e.g., `fpf.org/blog/YYYY/MM/DD/slug/` for blog posts, `fpf.org/reports/title/` for reports), (2) content taxonomy (what lives under which section), (3) search endpoint and effective query patterns, (4) content types and where they appear (policy briefs vs. blog posts vs. reports vs. infographics), (5) freshness indicators (how to tell if content is current).
- Test each navigation guide by having Claude actually use it to answer real questions. If Claude can answer as well without the guide, the guide adds no value.
- For FPF specifically: map the blog categories, report series, program pages, and issue area landing pages with actual URLs.

**Warning signs:**
- Navigation guides use verbs like "search for," "look up," "find" without specifying where or how.
- Guides don't contain any actual URLs or URL patterns.
- Claude's responses with the skill active are no better than responses without it.

**Phase to address:**
Phase 1 (Foundation) -- navigation guides must be written and tested during skill creation, not deferred.

---

### Pitfall 4: Hallucinated Legal Citations and Regulatory Details

**What goes wrong:**
Stanford research shows LLM legal hallucination rates of 58-88% when asked about specific legal cases. Even specialized legal research tools (LexisNexis, Westlaw AI) hallucinate 17-33% of the time. This skill will instruct Claude to cite specific FPF publications, reference specific regulatory provisions, and provide enforcement dates. Claude will confidently cite publications that don't exist, attribute positions FPF never took, or state incorrect enforcement dates. The privacy professional user will trust these citations because the skill is positioned as authoritative, and the consequences of acting on fabricated regulatory information are severe (compliance failures, legal liability).

**Why it happens:**
LLMs generate plausible text, not verified text. The skill's authority framing ("FPF cited first") increases user trust while doing nothing to reduce hallucination. Static content in the skill can reduce hallucination for the specific facts it contains, but anything the skill doesn't explicitly cover will be filled by Claude's training data -- which may be wrong.

**How to avoid:**
- Never instruct Claude to "cite FPF publication X" without providing the actual citation data (title, date, URL) in the skill's reference files. If the skill says "FPF published a report on children's privacy in 2024," include the exact title and URL.
- For enforcement dates and regulatory timelines: embed these as structured data in reference files (JSON or markdown tables) that Claude reads directly, rather than relying on Claude's training data.
- Instruct Claude to distinguish between "information from skill reference files" (verifiable) and "information from training data" (potentially stale or wrong).
- Add explicit instructions: "If you cannot find a specific FPF publication in the reference files, say so. Do not fabricate citations."
- For live WebFetch results: instruct Claude to quote the source text rather than paraphrase, reducing hallucination risk.

**Warning signs:**
- Skill instructions tell Claude to "reference FPF's position on X" without providing that position in reference data.
- Claude cites FPF publications with titles that sound right but don't exist.
- Enforcement dates in Claude's responses don't match the reference data.

**Phase to address:**
Phase 1 (Foundation) -- anti-hallucination instructions must be baked into every skill from the start. The FPF Source Catalog skill is the critical defense layer.

---

### Pitfall 5: Absent or Inadequate Legal Disclaimers

**What goes wrong:**
The skill provides privacy impact assessments (`/fpf:assess`), compliance checklists (`/fpf:checklist`), and risk ratings (GREEN/YELLOW/ORANGE/RED). A privacy professional uses the skill to assess whether their company's data practices comply with CCPA. The skill returns "GREEN -- compliant" based on incomplete information. The professional skips human review. The company faces regulatory action. FPF is implicated because the tool carried their brand and methodology. This is not hypothetical -- it happened with lawyers using ChatGPT-generated case citations (the "Mata v. Avianca" incident leading to court sanctions).

**Why it happens:**
The proposal acknowledges this risk (Open Question #5) but defers it. Legal disclaimers are treated as a nice-to-have rather than a pre-launch requirement. The severity classification system (GREEN/YELLOW/RED) gives outputs a false precision that encourages reliance.

**How to avoid:**
- Every skill, command, and agent output MUST include a disclaimer. Not optional, not configurable, not deferrable. Template: "This information is for research purposes only. It does not constitute legal advice. Compliance determinations require review by qualified legal professionals. Verify all citations and regulatory details independently."
- Risk assessment outputs (GREEN/YELLOW/RED) must include: "This classification is illustrative, not definitive. It is based on limited information and may not reflect your specific circumstances."
- Add escalation triggers: any RED classification automatically appends "Human expert review is required before acting on this assessment."
- Draft disclaimer language BEFORE Phase 1. Have FPF legal review it.

**Warning signs:**
- Any skill, command, or agent produces output without a disclaimer.
- Risk assessment commands return "GREEN -- compliant" without qualification.
- The word "advice" appears anywhere in skill output without the word "not."

**Phase to address:**
Phase 0 (Pre-implementation) -- disclaimers must be drafted and approved before any skill content is written.

---

### Pitfall 6: WebFetch Failures on Key Privacy Organization Websites

**What goes wrong:**
The skill's live fetching capability depends on WebFetch, which has severe limitations: no JavaScript rendering, 100KB text truncation, bot blocking by many sites, no authentication, and no dynamic URL construction. Many privacy organization websites (IAPP, government regulators like the FTC, EU data protection authorities) use JavaScript-heavy rendering, paywalls, CAPTCHAs, or anti-bot protection. The skill promises "live web fetching for deeper research" but in practice, WebFetch will fail silently on 30-50% of target sites, returning incomplete HTML, empty pages, or 403 errors. The user gets no result or garbled content and loses trust in the skill.

**Why it happens:**
WebFetch is designed for simple, public, server-rendered pages. Modern websites -- especially institutional and government sites -- increasingly use JavaScript rendering, CDN protections, and anti-bot measures. The skill's architecture assumes WebFetch reliability that doesn't exist.

**How to avoid:**
- Test WebFetch against every indexed organization's website BEFORE writing navigation guides. Create a compatibility matrix: which sites work, which are partially accessible, which are completely blocked.
- For sites where WebFetch fails: invest more in static reference content for those sources. The hybrid architecture should lean static for unreliable sites, live for reliable ones.
- Instruct Claude to gracefully degrade: "If WebFetch returns an error or empty content for a source, inform the user and suggest they visit the URL directly. Do not attempt to fabricate content."
- Provide fallback URL patterns: if a direct page fails, try the site's sitemap, RSS feed, or API if one exists.
- Document WebFetch limitations prominently in the skill so Claude doesn't over-promise.
- Note: Claude cannot dynamically construct URLs -- it can only fetch URLs explicitly provided by the user or found in previous search/fetch results. Navigation guides must provide exact URLs or URL templates, not instructions for Claude to construct URLs.

**Warning signs:**
- Navigation guides reference sites that haven't been tested with WebFetch.
- Skill promises "live research" without specifying which sources support it.
- Users report blank or garbled results from specific sources.

**Phase to address:**
Phase 1 (Foundation) -- WebFetch compatibility testing must happen during skill creation.

---

### Pitfall 7: Jurisdictional Confusion in Regulatory Guidance

**What goes wrong:**
The skill covers U.S. federal law, 50+ state privacy laws, GDPR, LGPD, POPIA, PIPEDA, PIPL, UK GDPR, and more. These laws use the same terms ("personal data," "consent," "data subject") with different definitions across jurisdictions. Claude will conflate definitions, apply GDPR standards to CCPA questions, or give advice based on one state's law when the user is asking about another. State privacy laws have different definitions of "sensitive data" -- what qualifies in one state doesn't in another. A skill that treats "sensitive data" as a universal concept will give wrong answers.

**Why it happens:**
LLMs compress similar concepts into shared representations. "Personal data" under GDPR and "personal information" under CCPA are different legal concepts, but they're semantically similar enough that Claude will blend them. The skill's multi-jurisdictional scope makes this worse by loading multiple regulatory frameworks into the same context.

**How to avoid:**
- Structure reference files by jurisdiction, not by concept. Don't create a single "personal data definitions" file -- create `reference/ccpa-definitions.md`, `reference/gdpr-definitions.md`, etc.
- In skill instructions, explicitly warn Claude: "Do not apply concepts from one jurisdiction to another. When answering about CCPA, use CCPA definitions and standards only. When answering about GDPR, use GDPR definitions and standards only."
- When a user's query doesn't specify a jurisdiction, instruct Claude to ask: "Which jurisdiction are you asking about?" rather than guessing.
- For the `/fpf:compare` command: this is where cross-jurisdictional work is appropriate, but the command must maintain clear labels ("Under GDPR: X. Under CCPA: Y.").
- Limit Phase 1 to a manageable set of jurisdictions (U.S. federal + 3-5 key states + GDPR + 1-2 others) rather than attempting comprehensive global coverage.

**Warning signs:**
- Reference files organize regulatory content by concept rather than by jurisdiction.
- Skills don't include jurisdiction-checking instructions.
- Claude's answers blend terminology from different legal frameworks.

**Phase to address:**
Phase 1 (Foundation) -- jurisdiction separation must be baked into the reference file structure.

---

### Pitfall 8: Content Staleness Within Months of Launch

**What goes wrong:**
Privacy law is one of the fastest-evolving legal domains. U.S. states pass new comprehensive privacy laws multiple times per year. Enforcement dates, cure periods, and opt-out deadlines change. GDPR enforcement actions create new precedent monthly. The skill encodes specific dates, law counts ("50+ state comprehensive privacy laws"), and enforcement timelines that become wrong within 3-6 months. A privacy professional who relies on an outdated enforcement date from the skill could miss a compliance deadline.

**Why it happens:**
Static content is a snapshot. The skill's value proposition is "authoritative privacy research tool," but static content authority decays rapidly in this domain. The proposal acknowledges this (FPF publishes ~50+ new resources/year) but doesn't specify an update strategy.

**How to avoid:**
- Separate time-sensitive content (enforcement dates, law counts, deadline calendars) from stable content (legal concepts, analytical frameworks, organizational descriptions).
- Time-sensitive content goes in clearly labeled reference files (e.g., `reference/enforcement-dates-2026-q1.md`) with a version date at the top.
- Include instructions in the skill: "The enforcement dates in this reference file were last updated on [DATE]. For current dates, verify with the source using WebFetch."
- Don't encode specific law counts. Instead of "50+ state comprehensive privacy laws," say "multiple state comprehensive privacy laws" and link to a reference file that lists them.
- Plan quarterly version bumps with content refresh as part of the plugin maintenance SLA.
- For the most volatile data (enforcement dates, new laws), prefer live fetching over static content.

**Warning signs:**
- Skill content includes specific numbers that change over time ("27 AI laws across 14 states").
- No version date on reference files.
- No defined content refresh cadence.

**Phase to address:**
Phase 0 (Pre-implementation) -- content freshness strategy must be decided before writing content.

---

## Technical Debt Patterns

Shortcuts that seem reasonable but create long-term problems.

| Shortcut | Immediate Benefit | Long-term Cost | When Acceptable |
|----------|-------------------|----------------|-----------------|
| Embedding all regulatory content directly in SKILL.md | Faster to write, single file to maintain | Blows context budget, forces loading irrelevant content on every invocation | Never -- always use progressive disclosure |
| Skipping WebFetch compatibility testing | Ship faster | Users hit failures on 30-50% of sources, erode trust in "live research" claim | Never -- test before listing a source |
| Using vague navigation guides ("search the site") | Faster to write than mapping site structure | Adds no value over Claude's default behavior, wastes tokens | Never -- every guide must add structural knowledge |
| One mega-skill instead of domain-separated skills | Simpler architecture | One massive context load on every query regardless of topic | Never for this project scope |
| Copying Anthropic's compliance skill structure verbatim | Proven pattern, fast start | Anthropic's compliance skill is shallow by design (overview-level regulation coverage); this project needs depth that requires a different architecture | Only as a starting template, not the final structure |
| Hardcoding law counts and enforcement dates in SKILL.md | Concrete, authoritative-sounding | Wrong within months, requires manual updates across multiple files | Only in dated reference files with explicit freshness metadata |
| Deferring legal disclaimers to "after launch" | Ship faster | Liability exposure from first user interaction; much harder to retrofit | Never -- disclaimers are a pre-launch requirement |

## Integration Gotchas

Common mistakes when connecting to external services.

| Integration | Common Mistake | Correct Approach |
|-------------|----------------|------------------|
| WebFetch on FPF.org | Assuming all FPF pages render with static HTML; JavaScript-rendered content returns empty/partial results | Test key page types (blog posts, reports, program pages, tools like Key Dates Tracker) before writing navigation guides; fall back to static content for JS-rendered pages |
| WebFetch on government sites (FTC, DPAs) | Assuming .gov sites are simple HTML; many use JavaScript frameworks and CDN protection | Test each government source; expect most to fail and invest in static reference content for these |
| WebFetch on IAPP.org | IAPP has paywalled content behind member login; WebFetch cannot authenticate | Only reference IAPP's publicly accessible content (blog posts, free trackers); note paywall boundaries in navigation guides |
| WebFetch URL construction | Attempting to have Claude dynamically construct URLs based on query parameters; WebFetch security restrictions prevent this | Provide explicit URL templates in reference files; Claude can only fetch URLs from user input, previous searches, or previous fetches |
| Claude Code plugin namespace | Assuming plugin skills can conflict with user's personal skills | Plugin skills use `plugin-name:skill-name` namespace and cannot conflict with other levels; but description budget is shared |
| Skill auto-activation | Assuming broad descriptions will reliably trigger the right domain skill | Write descriptions in third person, include specific trigger keywords, keep under 200 characters, test activation with diverse queries |

## Performance Traps

Patterns that work at small scale but fail as usage grows.

| Trap | Symptoms | Prevention | When It Breaks |
|------|----------|------------|----------------|
| Loading all 18 skills simultaneously | Context window fills with skill metadata, less room for conversation and reasoning | Consolidate to 5-7 skills; use `disable-model-invocation: true` for rarely-needed skills | When user has 15+ other skills installed alongside this plugin |
| Large reference files without internal structure | Claude reads entire file when only one section is needed; wastes tokens | Add table of contents to files over 100 lines; organize by section with clear headers so Claude can grep for relevant parts | When reference files exceed 200 lines |
| Deeply nested reference files | SKILL.md -> guide.md -> details.md causes Claude to partially read files (using `head -100` instead of full read) | Keep all references one level deep from SKILL.md | Any nesting beyond one level |
| WebFetch for every query | Slow responses, rate limiting, frequent failures on blocked sites | Use static content for common/stable queries; WebFetch only for time-sensitive or deep-dive research | When user asks rapid-fire questions or sites impose rate limits |
| Over-broad skill descriptions | Multiple domain skills activate simultaneously on a single query, each consuming context | Make descriptions specific with unique trigger keywords; avoid overlapping descriptions between skills | When user asks cross-domain questions that trigger 4+ skills |

## Security Mistakes

Domain-specific security issues beyond general web security.

| Mistake | Risk | Prevention |
|---------|------|------------|
| Encoding FPF member-only content in public plugin | Confidential content leaks to non-members; breach of FPF's member value proposition | Strict separation: public plugin contains only publicly available FPF content; member content exclusively in Phase 3 MCP server |
| Skill outputs that resemble legal advice | Users rely on AI-generated compliance determinations; regulatory penalties, lawsuits against user or FPF | Mandatory disclaimers on every output; escalation triggers on RED risk ratings; never use language like "you are compliant" |
| Adversarial use of biometrics/surveillance skill content | Bad actors use FPF's published research on facial recognition taxonomies or location tracking to develop privacy-invasive tools | Add responsible use notices to high-risk topic skills; acknowledge inherent risk of public knowledge dissemination |
| Token/credential leakage in Phase 3 MCP server | Member portal authentication tokens exposed in Claude conversation logs or context | Short-lived tokens with refresh; tokens stored in Claude sandbox, not conversation context; never log tokens |

## UX Pitfalls

Common user experience mistakes in this domain.

| Pitfall | User Impact | Better Approach |
|---------|-------------|-----------------|
| Skill gives confidently wrong enforcement dates | Privacy professional misses compliance deadline; legal consequences | Always cite the reference file date; instruct Claude to recommend verification for time-sensitive info |
| WebFetch failure with no explanation | User gets no result and doesn't know why; loses trust | Claude must report "I was unable to fetch content from [source] -- the site may be blocking automated access. Please visit [URL] directly." |
| Cross-jurisdictional answer without labeling | User applies GDPR advice to a CCPA question; compliance failure | Always label which jurisdiction's law is being discussed; ask for jurisdiction when ambiguous |
| Too many slash commands to remember | User can't remember which of 6 commands does what; defaults to free-text queries | Provide a `/fpf:help` command that lists available commands with one-line descriptions; keep Phase 1 to 2 commands max |
| Overly verbose skill output | Privacy professional wants a quick answer; gets a 2000-word essay | Include "concise mode" instructions: for quick lookups, give the answer first, then offer to elaborate |
| GREEN risk rating gives false confidence | User assumes GREEN means "no action needed"; may still have compliance gaps outside the assessed scope | GREEN rating must include: "This assessment covers [specific aspects]. Factors not assessed include [list]. This is not a comprehensive compliance determination." |

## "Looks Done But Isn't" Checklist

Things that appear complete but are missing critical pieces.

- [ ] **Navigation guides:** Often missing actual URL patterns and site structure -- verify each guide contains at least 5 specific URLs and the site's content taxonomy
- [ ] **Enforcement date tables:** Often missing jurisdiction-specific footnotes (cure periods, private right of action status, AG enforcement discretion) -- verify dates include all applicable qualifiers
- [ ] **Source catalog:** Often lists organizations without noting which have paywall content, which sites block WebFetch, or which require special search techniques -- verify each source has a tested access method
- [ ] **Skill descriptions:** Often written as human-readable summaries instead of Claude-optimized trigger text -- verify descriptions are in third person, include key trigger terms, and stay under 200 characters
- [ ] **Legal disclaimers:** Often added to the main SKILL.md but missing from command output templates and agent system prompts -- verify every output pathway includes a disclaimer
- [ ] **Cross-references between skills:** Often skills reference "see the AI Governance skill" without specifying which file or section -- verify cross-references point to specific files
- [ ] **WebFetch fallback behavior:** Often the "happy path" works but the failure path is undefined -- verify every WebFetch instruction includes what to do when it fails
- [ ] **Jurisdiction labeling:** Often answers reference "the law" without specifying which jurisdiction's law -- verify skill instructions require jurisdiction identification in every regulatory response

## Recovery Strategies

When pitfalls occur despite prevention, how to recover.

| Pitfall | Recovery Cost | Recovery Steps |
|---------|---------------|----------------|
| Skills exceed character budget | LOW | Consolidate skills; reduce description lengths; test with `/context` |
| SKILL.md files too large | LOW | Extract content to reference files; restructure with progressive disclosure |
| Hallucinated citations in user-facing output | MEDIUM | Add anti-hallucination instructions to all skills; audit reference files for completeness; instruct Claude to flag unverified claims |
| Missing legal disclaimers after launch | MEDIUM | Immediate hotfix release; add disclaimers to every skill/command/agent; FPF legal review |
| WebFetch failures on key sources | MEDIUM | Fall back to static content for affected sources; update navigation guides to reflect limitations; notify users of affected sources |
| Jurisdictional confusion in responses | HIGH | Restructure reference files by jurisdiction (not by concept); rewrite skill instructions with jurisdiction-checking requirements; re-test all commands |
| Content staleness after 6 months | MEDIUM | Quarterly content refresh; add freshness metadata to all reference files; instruct Claude to warn about potentially stale information |
| User relies on incorrect compliance assessment | HIGH | Cannot be recovered post-harm; prevention through disclaimers, qualified language, and escalation triggers is the only viable strategy |

## Pitfall-to-Phase Mapping

How roadmap phases should address these pitfalls.

| Pitfall | Prevention Phase | Verification |
|---------|------------------|--------------|
| Skill description character budget overflow | Phase 0 (Architecture) | Run `/context` with all skills loaded; no excluded skill warnings |
| SKILL.md content bloat | Phase 1 (Foundation) | Every SKILL.md under 300 lines; reference files used for detail |
| Vague navigation guides | Phase 1 (Foundation) | Each guide tested with real queries; measurably better results than no-skill baseline |
| Hallucinated citations | Phase 1 (Foundation) | Anti-hallucination instructions in every skill; reference files contain actual citation data |
| Missing legal disclaimers | Phase 0 (Pre-implementation) | Disclaimer template approved by FPF legal; disclaimer present in every output pathway |
| WebFetch failures | Phase 1 (Foundation) | Compatibility matrix created for all indexed sources; fallback behavior defined for each |
| Jurisdictional confusion | Phase 1 (Foundation) | Reference files organized by jurisdiction; skill instructions require jurisdiction labeling |
| Content staleness | Phase 0 (Pre-implementation) | Freshness strategy documented; reference files include version dates; update SLA defined |

## Sources

- [Extend Claude with skills - Claude Code Docs](https://code.claude.com/docs/en/skills) -- official skill structure, character budget, troubleshooting (HIGH confidence)
- [Skill authoring best practices - Claude API Docs](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices) -- progressive disclosure, 500-line limit, description guidelines (HIGH confidence)
- [Hallucinating Law: Legal Mistakes with Large Language Models](https://hai.stanford.edu/news/hallucinating-law-legal-mistakes-large-language-models-are-pervasive) -- 58-88% hallucination rates on legal queries (HIGH confidence)
- [Large Legal Fictions: Profiling Legal Hallucinations in Large Language Models](https://academic.oup.com/jla/article/16/1/64/7699227) -- specialized tools hallucinate 17-33% (HIGH confidence)
- [Inside Claude Code's Web Tools: WebFetch vs WebSearch](https://mikhail.io/2025/10/claude-code-web-tools/) -- WebFetch limitations, no JS rendering, 100KB truncation (MEDIUM confidence)
- [WebFetch returns 403 on Wikipedia and other sites - GitHub Issue](https://github.com/anthropics/claude-code/issues/22846) -- real-world WebFetch blocking issues (MEDIUM confidence)
- [Claude Code skills not triggering? It might not see them](https://blog.fsck.com/2025/12/17/claude-code-skills-not-triggering/) -- character budget issues with multiple skills (MEDIUM confidence)
- [IAPP U.S. State Privacy Legislation Tracker](https://iapp.org/resources/article/us-state-privacy-legislation-tracker) -- rapidly evolving state privacy law landscape (HIGH confidence)
- [Anthropic knowledge-work-plugins/legal](https://github.com/anthropics/knowledge-work-plugins/tree/main/legal) -- reference compliance skill structure (HIGH confidence)

---
*Pitfalls research for: FPF Privacy Research Skill (Claude Code Plugin)*
*Researched: 2026-03-12*
