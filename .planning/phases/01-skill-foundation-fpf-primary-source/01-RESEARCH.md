# Phase 1: Skill Foundation + FPF Primary Source - Research

**Researched:** 2026-03-13
**Domain:** Claude Code skill architecture, FPF content knowledge base, progressive disclosure patterns
**Confidence:** HIGH

## Summary

Phase 1 builds a single `/privacy` Claude Code skill that routes privacy questions to FPF-prioritized, source-attributed answers. The deliverable is a SKILL.md file (under 500 lines) that acts as a routing layer, two reference files (`fpf-reference.md` for FPF knowledge/navigation and `skill-behaviors.md` for attribution/disclaimer/anti-hallucination rules), and the foundational behaviors that all subsequent phases build upon.

The skill architecture is well-understood: Claude Code skills are markdown files with YAML frontmatter that follow the open Agent Skills standard. The SKILL.md serves as both entry point and progressive disclosure router -- it loads into context when triggered, then selectively reads reference files based on query type. This is the exact pattern used by Anthropic's own legal plugin, which is installed locally and provides a verified reference implementation.

**Primary recommendation:** Build the skill as a single directory at `.claude/skills/privacy/` containing `SKILL.md` (routing layer + example queries), `fpf-reference.md` (FPF knowledge base + navigation guide), and `skill-behaviors.md` (attribution, disclaimer, anti-hallucination instructions). Follow the legal plugin's structural patterns closely but adapt for the single-skill, content-knowledge architecture rather than multi-skill workflow suite.

<user_constraints>
## User Constraints (from CONTEXT.md)

### Locked Decisions
- Heading + organized sections format (Overview, Key Provisions, FPF Resources, etc.)
- Sections vary by query type -- not a rigid template
- Concise by default (200-400 words), user can ask for more depth
- No skill branding or header tags -- responses start directly with the topic heading
- Inline citations with links woven naturally into the answer text: "According to FPF's [Report Title](url), ..."
- All sources get equal treatment (FPF and non-FPF alike) -- FPF naturally appears first/more often due to prioritization logic
- FPF Resources section appears whenever FPF has relevant coverage; omitted silently when FPF has no coverage on the topic
- When FPF does not cover a topic, answer from other sources without commenting on FPF's absence
- Unified cohesive answer when query spans multiple issue areas (e.g., "AI and children's privacy")
- FPF Resources section lists materials from each relevant area -- no artificial subsections by area
- Footer on every response, minimal: `(warning) *Research aid only -- not legal advice.*`
- Generic disclaimer -- does not mention FPF by name
- No extra warnings for date-sensitive content, enforcement penalties, or other high-stakes topics
- Focus exclusively on articles and publications -- no events, trainings, or programs as organizational entities
- All 20+ FPF issue areas with full 2-3 sentence descriptions of coverage and key resource types
- All 6 FPF publication types (Reports, White Papers, Filings, Infographics, Blog Posts, Videos) with descriptions
- FPF specialized tools included as resources (Student Privacy Compass, Key Dates Tracker, PETs Repository, etc.)
- FPF navigation guide with tested fpf.org URL patterns, content taxonomy, and search strategies
- Two reference files: fpf-reference.md (knowledge + navigation combined) and skill-behaviors.md (attribution, disclaimer, anti-hallucination)
- Follow skill-creator convention for file placement
- Selective loading: SKILL.md detects query type and loads only what is needed per query
- SKILL.md includes 5-10 curated example queries spanning regulation questions, FPF-specific, and general privacy

### Claude's Discretion
- Anti-hallucination implementation approach
- Professional tone calibration (assumed: practitioner-practical for privacy professionals)
- Exact section names and ordering within responses
- How to handle queries clearly outside privacy domain
- Routing logic implementation in SKILL.md
- FPF-specific vs general privacy query detection heuristics

### Deferred Ideas (OUT OF SCOPE)
None -- discussion stayed within phase scope
</user_constraints>

<phase_requirements>
## Phase Requirements

| ID | Description | Research Support |
|----|-------------|-----------------|
| ARCH-01 | Skill triggers via `/privacy` command with natural language queries | Skill frontmatter `name: privacy` creates the `/privacy` slash command. `$ARGUMENTS` captures the natural language query. Verified via Claude Code skills documentation. |
| ARCH-02 | SKILL.md acts as routing layer under 500 lines, dispatching to reference files | Progressive disclosure pattern: SKILL.md links to reference files with `[file.md](file.md)` syntax. Claude reads them on demand. 500-line limit is official best practice. |
| ARCH-03 | Reference files use progressive disclosure (loaded on-demand, zero tokens at rest) | Confirmed: reference files in skill directory consume zero context tokens until Claude reads them. Files are loaded via filesystem Read tool when SKILL.md references them. |
| ARCH-06 | Professional-grade language assumes domain knowledge, uses precise legal/regulatory terminology | Implemented via `skill-behaviors.md` tone instructions. Privacy professional audience means no glossary for standard terms (DPA, DPIA, SCCs, lawful basis, etc.). |
| ARCH-07 | Anti-hallucination instructions embedded; regulatory facts come from reference files, not training data | Implemented via `skill-behaviors.md` with explicit instructions to cite from reference files, not generate regulatory facts from training data. Supported by example queries in SKILL.md. |
| ARCH-08 | Legal disclaimer in every output pathway stating skill assists research, not legal advice | Locked format: `(warning) *Research aid only -- not legal advice.*` as footer on every response. Embedded in `skill-behaviors.md` as mandatory output instruction. |
| FPF-01 | Skill indexes all 6 FPF publication types with counts and descriptions | Encoded in `fpf-reference.md`: Reports, White Papers, Filings, Infographics, Blog Posts, Videos with descriptions of each type's content and typical use. |
| FPF-02 | Skill indexes 20+ FPF issue areas with resource counts | Encoded in `fpf-reference.md`: comprehensive catalog of all issue areas with 2-3 sentence descriptions and key resource types per area. |
| FPF-03 | FPF navigation guide contains actual fpf.org URL patterns, content taxonomy, and tested search strategies | Encoded in `fpf-reference.md`: tested URL patterns like `fpf.org/issue/{area}/`, `fpf.org/blog/`, `fpf.org/wp-content/uploads/`, content taxonomy, search tips. |
| FPF-04 | FPF is cited first when the query topic falls within FPF's coverage areas | Implemented via `skill-behaviors.md` source prioritization rules: FPF sources appear first in citations when relevant, achieved through prioritization logic not explicit labeling. |
| FPF-05 | Skill knows major FPF programs (Center for AI, Youth Privacy, Privacy Papers for Policymakers, DC Privacy Forum, Training Program) | Encoded in `fpf-reference.md` as part of the FPF organizational knowledge, with each program's focus area and key outputs described. |
| ORG-04 | Source attribution appears in every answer with organization name and ideally URL | Implemented via `skill-behaviors.md` attribution rules: inline citations with links woven naturally, e.g., "According to FPF's [Report Title](url), ..." |
</phase_requirements>

## Standard Stack

### Core
| Component | Format | Purpose | Why Standard |
|-----------|--------|---------|--------------|
| SKILL.md | Markdown + YAML frontmatter | Skill entry point and routing layer | Required by Claude Code Agent Skills specification |
| fpf-reference.md | Markdown | FPF knowledge base + navigation guide | Progressive disclosure reference file pattern |
| skill-behaviors.md | Markdown | Attribution, disclaimer, anti-hallucination rules | Separates behavior rules from content knowledge |

### Supporting
| Component | Format | Purpose | When to Use |
|-----------|--------|---------|-------------|
| `$ARGUMENTS` variable | String substitution | Captures user's natural language query | Every skill invocation |
| `$CLAUDE_SKILL_DIR` variable | Path substitution | References files relative to skill directory | Portable file references |

### Alternatives Considered
| Instead of | Could Use | Tradeoff |
|------------|-----------|----------|
| Two reference files | Single reference file | Two files allows selective loading; single file is simpler but loads unnecessary content for some queries |
| Markdown reference files | JSON data files | Markdown is natively understood by Claude with zero parsing overhead; JSON would need interpretation |
| Single `/privacy` skill | Multi-skill suite (per issue area) | Single skill is the locked user decision; multi-skill would add context overhead for skill selection |

**Installation:** No installation needed. Skills are plain markdown files placed in the correct directory.

## Architecture Patterns

### Recommended Project Structure
```
.claude/skills/privacy/
    SKILL.md              # Routing layer (~300-450 lines)
    fpf-reference.md      # FPF knowledge + navigation (~unlimited)
    skill-behaviors.md    # Attribution + disclaimer + anti-hallucination (~200-400 lines)
```

### Pattern 1: Progressive Disclosure Router
**What:** SKILL.md acts as a lightweight router that detects query type from `$ARGUMENTS` and instructs Claude to read only the relevant reference file(s).
**When to use:** Always -- this is the core architectural pattern.
**Example:**
```markdown
---
name: privacy
description: Privacy research assistant with FPF-prioritized source attribution. Use when the user asks about data privacy, privacy regulations, FPF publications, privacy policy, AI governance, children's privacy, or any privacy-related topic.
---

# Privacy Research Skill

You are a privacy research assistant for privacy professionals. [routing instructions...]

## Reference Files

- For FPF knowledge, publications, issue areas, and fpf.org navigation: read [fpf-reference.md](fpf-reference.md)
- For response formatting, attribution rules, disclaimer, and anti-hallucination guidance: read [skill-behaviors.md](skill-behaviors.md)

## Query Routing

For ALL queries, first read [skill-behaviors.md](skill-behaviors.md) to understand response formatting rules.

If the query relates to FPF programs, publications, issue areas, or any topic FPF covers, also read [fpf-reference.md](fpf-reference.md).

[Example queries section...]
```
Source: Claude Code skills documentation (https://code.claude.com/docs/en/skills)

### Pattern 2: Inline Citation Attribution
**What:** Source attribution is woven into answer text as natural inline citations with markdown links, not as footnotes or reference sections.
**When to use:** Every response that references a source.
**Example:**
```markdown
## Attribution Rules

Cite sources inline using natural language:
- "According to FPF's [Children's Online Privacy: An Update](https://fpf.org/blog/...), ..."
- "The FTC's [enforcement guidance](https://www.ftc.gov/...) establishes that ..."
- "As analyzed in FPF's [State Privacy Legislation Tracker](https://fpf.org/issue/us-legislation/), ..."

FPF sources appear first when the topic falls within FPF's coverage areas.
When FPF does not cover a topic, cite other authoritative sources without
commenting on FPF's absence.
```
Source: CONTEXT.md locked decisions

### Pattern 3: Conditional FPF Resources Section
**What:** An "FPF Resources" section appears in the response whenever FPF has relevant publications, and is silently omitted when FPF has no coverage.
**When to use:** Controlled by the skill-behaviors.md instructions based on whether the query topic intersects FPF's 20+ issue areas.
**Example:**
```markdown
## FPF Resources Section

Include an "FPF Resources" section when:
- The query topic overlaps with any of FPF's 20+ issue areas
- FPF has published reports, white papers, or blog posts on the topic

Omit the section silently (do not mention its absence) when:
- The topic is entirely outside FPF's coverage areas
- No FPF publications are relevant

When included, list relevant FPF materials with direct links:
- [Report/Publication Title](url) -- brief description of relevance
```

### Pattern 4: Anti-Hallucination Guard
**What:** Explicit instructions that regulatory facts, dates, and legal provisions must come from reference file content, not from training data.
**When to use:** Always -- embedded in skill-behaviors.md.
**Example:**
```markdown
## Anti-Hallucination Rules

1. For regulatory facts (effective dates, penalty amounts, specific provisions):
   state only what is documented in the reference files or verifiable sources.
2. If a specific fact is not in the reference files, say "I'd recommend
   verifying the current [specific detail] directly at [authoritative source]"
   rather than generating a potentially outdated answer.
3. For FPF-specific information (publication titles, program names, issue
   area descriptions): use ONLY what appears in fpf-reference.md.
4. Clearly distinguish between established facts and analysis/interpretation.
```

### Anti-Patterns to Avoid
- **Nested file references:** SKILL.md should reference files directly (one level deep). Do not have fpf-reference.md reference additional sub-files -- this causes Claude to do partial reads. All references must be one level from SKILL.md.
- **Overly rigid response templates:** The CONTEXT.md locks "sections vary by query type." Do not create a fixed template that forces every response into the same structure.
- **Skill description that is too narrow:** The description field is the primary triggering mechanism. It must include broad terms like "data privacy, privacy regulations, FPF, AI governance, children's privacy" to ensure the skill activates for relevant queries.
- **Loading all reference files for every query:** The routing layer should detect when FPF reference material is needed vs. when only behavior rules suffice.

## Don't Hand-Roll

| Problem | Don't Build | Use Instead | Why |
|---------|-------------|-------------|-----|
| Skill triggering logic | Custom activation detection | YAML frontmatter `description` field | Claude's built-in skill discovery uses the description field; custom logic adds no value |
| Progressive disclosure | Custom file-loading system | Native markdown links `[file.md](file.md)` | Claude Code natively reads referenced files via filesystem tools; no custom loader needed |
| Argument parsing | Regex or structured parsing of user queries | `$ARGUMENTS` string substitution | Claude interprets natural language natively; structured parsing adds brittleness |
| Response formatting | JSON schemas or structured output formats | Markdown instructions in skill-behaviors.md | Claude excels at following prose formatting instructions; schemas over-constrain |
| FPF content indexing | JSON database of publications | Markdown catalog in fpf-reference.md | Markdown is Claude's native format; JSON adds parsing overhead with no benefit for this use case |

**Key insight:** Claude Code skills are prompt-based, not code-based. Every "feature" is implemented as clear prose instructions that Claude follows. Trying to build programmatic logic (parsers, formatters, databases) inside a skill adds complexity without improving output quality.

## Common Pitfalls

### Pitfall 1: Description Field Too Narrow
**What goes wrong:** The skill only triggers for queries that exactly match narrow keywords, missing legitimate privacy queries.
**Why it happens:** Writing a description that says "answers questions about FPF" instead of broadly covering the privacy domain.
**How to avoid:** Include all major topic areas in the description: data privacy, privacy regulations, GDPR, CCPA, children's privacy, AI governance, FPF, privacy policy, data protection, surveillance, consent, biometrics, health data, ad tech, PETs, etc.
**Warning signs:** Users report the skill does not activate for privacy-related queries.

### Pitfall 2: SKILL.md Exceeds 500 Lines
**What goes wrong:** The skill becomes slow to load and may compete with conversation context for token budget.
**Why it happens:** Putting FPF knowledge content directly in SKILL.md instead of reference files.
**How to avoid:** SKILL.md contains ONLY: frontmatter, routing instructions, reference file descriptions, and example queries. All substantive content goes in reference files.
**Warning signs:** Line count approaching 400+ means it is time to audit and move content to reference files.

### Pitfall 3: Reference Files Nested More Than One Level
**What goes wrong:** Claude partially reads files (e.g., `head -100`) when they are referenced from other referenced files, resulting in incomplete information.
**Why it happens:** Creating a hierarchy of reference files where fpf-reference.md links to sub-files.
**How to avoid:** Keep all reference files one level deep from SKILL.md. Both fpf-reference.md and skill-behaviors.md are referenced directly from SKILL.md and do not reference each other or additional files.
**Warning signs:** Claude gives incomplete answers that cut off mid-topic or miss sections that exist in deeply nested files.

### Pitfall 4: FPF URL Patterns Become Stale
**What goes wrong:** Navigation guide contains broken URLs that lead nowhere.
**Why it happens:** FPF website restructuring, content migration, or URL pattern changes.
**How to avoid:** Use general URL patterns (`fpf.org/issue/{area}/`) rather than specific article URLs where possible. For specific resources, use URLs that are structural (issue area pages, publication type pages) rather than individual blog post URLs that are more likely to change.
**Warning signs:** Users report "link not found" when following URLs in skill responses.

### Pitfall 5: Anti-Hallucination Instructions Too Restrictive
**What goes wrong:** The skill refuses to answer common questions because the answer is not literally in the reference files.
**Why it happens:** Instructions say "only state what is in reference files" for ALL information, not just regulatory facts.
**How to avoid:** Anti-hallucination rules target specific categories: regulatory facts (dates, penalty amounts, specific provisions), FPF-specific information (publication titles, program details), and legal requirements. General privacy domain knowledge that Claude reliably knows (what GDPR stands for, what consent means) should not require reference file verification.
**Warning signs:** Responses are excessively hedged or refuse to answer basic privacy questions.

### Pitfall 6: Forgetting the Disclaimer
**What goes wrong:** Some response pathways omit the legal disclaimer footer.
**Why it happens:** The disclaimer instruction is in skill-behaviors.md but the routing logic allows some queries to skip loading that file.
**How to avoid:** Make skill-behaviors.md loading mandatory for ALL queries (it contains the disclaimer which is required on every response). The routing decision is only about whether to ALSO load fpf-reference.md.
**Warning signs:** Responses without the `(warning) *Research aid only -- not legal advice.*` footer.

## Code Examples

Verified patterns from the Anthropic legal plugin and official Claude Code documentation:

### SKILL.md Frontmatter Pattern
```yaml
# Source: Anthropic legal plugin SKILL.md + Claude Code docs
---
name: privacy
description: Privacy research assistant with FPF-prioritized source attribution. Answers questions about data privacy, privacy regulations, GDPR, CCPA, COPPA, HIPAA, AI governance, children's privacy, FPF publications, biometrics, health data, ad tech, and any privacy-related topic. Use when the user asks about privacy law, data protection, FPF programs, or privacy policy analysis.
---
```

### Reference File Link Pattern
```markdown
# Source: Claude Code skills documentation - "Add supporting files" section
## Reference Files

- For FPF knowledge, issue areas, publication types, programs, and fpf.org
  navigation strategies: read [fpf-reference.md](fpf-reference.md)
- For response formatting, source attribution rules, legal disclaimer, and
  anti-hallucination instructions: read [skill-behaviors.md](skill-behaviors.md)
```

### Routing Logic Pattern
```markdown
# Source: Derived from legal plugin's skill-to-subskill dispatch pattern
## Query Routing

For every query:
1. Read [skill-behaviors.md](skill-behaviors.md) for response rules
2. Determine if the query topic overlaps with FPF's coverage areas
3. If yes, also read [fpf-reference.md](fpf-reference.md)
4. Compose response following the formatting and attribution rules
```

### Example Queries Pattern
```markdown
# Source: Derived from legal plugin command examples
## Example Queries

These examples show the range of queries this skill handles:

1. "What are the key provisions of COPPA?"
   → General regulation query. Load behaviors. FPF covers youth privacy, so also load FPF reference.

2. "What does FPF publish about AI governance?"
   → FPF-specific query. Load both reference files.

3. "Compare GDPR and CCPA consent requirements"
   → Regulation comparison. Load behaviors. FPF covers both US and global, so also load FPF reference.

4. "What is differential privacy?"
   → Technical privacy concept. Load behaviors. FPF has PETs Repository, so also load FPF reference.

5. "What privacy risks exist with facial recognition?"
   → Domain question. Load behaviors. FPF covers biometrics, so also load FPF reference.
```

### Disclaimer Footer Pattern
```markdown
# Source: CONTEXT.md locked decision
## Legal Disclaimer (MANDATORY on every response)

End every response with this exact footer:

---
(warning) *Research aid only -- not legal advice.*
```

### FPF Issue Area Catalog Entry Pattern
```markdown
# Source: FPF Plugin Proposal.md + fpf.org verified structure
## U.S. Legislation
FPF tracks comprehensive privacy legislation across 50+ states, maintaining the
Key Dates for State Privacy Laws tracker covering enforcement dates, cure periods,
and opt-out signal deadlines. Key resources include state law comparisons,
enforcement analysis, and legislative trend reports.
- Browse: https://fpf.org/issue/us-legislation/
- Key tool: Key Dates for State Privacy Laws tracker
```

## State of the Art

| Old Approach | Current Approach | When Changed | Impact |
|--------------|------------------|--------------|--------|
| `.claude/commands/` directory | `.claude/skills/` directory | Dec 2025 | Skills supersede commands; commands still work but skills add frontmatter, supporting files, and auto-discovery |
| Single monolithic SKILL.md | Progressive disclosure with reference files | Dec 2025 (Agent Skills spec) | Keeps context window efficient; SKILL.md under 500 lines |
| Plugin-specific formats | Universal `SKILL.md` Agent Skills standard | Dec 2025 | Same format works across Claude Code, Codex CLI, ChatGPT |
| Skills only for Claude Code | Agent Skills open standard | Dec 2025 | Skills are portable across AI tools; OpenAI adopted the format |

**Deprecated/outdated:**
- `.claude/commands/` directory: Still works but `.claude/skills/` is recommended. Skills support features commands do not (frontmatter, supporting files, auto-invocation control).
- `plugin.json` manifest registration: Not needed for individual skills; only for plugin bundles that package multiple skills/commands/agents together.

## Open Questions

1. **FPF Issue Area Completeness**
   - What we know: The proposal document lists 14+ issue areas with varying levels of detail. FPF's website shows 20+ distinct issue area pages.
   - What is unclear: Exact current count and whether all issue areas have the same level of published content.
   - Recommendation: Build the reference file with all known issue areas from the proposal document and fpf.org structure. Accept that resource counts may be approximate and note this in the reference file.

2. **SKILL.md Optimal Line Count**
   - What we know: Official guidance says "under 500 lines." The legal plugin's root SKILL.md is 57 lines (very thin router). Individual sub-skills like compliance are ~215 lines.
   - What is unclear: Whether a single-skill architecture (our case) can pack routing logic + example queries into 300-450 lines effectively, or whether it should be leaner.
   - Recommendation: Target 250-350 lines for SKILL.md. This leaves headroom and keeps the router lean. If it creeps past 400, audit and move content to reference files.

3. **fpf.org URL Stability**
   - What we know: FPF uses patterns like `fpf.org/issue/{area}/`, `fpf.org/blog/`, `fpf.org/wp-content/uploads/`.
   - What is unclear: How frequently these patterns change and whether all issue area slugs are stable.
   - Recommendation: Use structural URLs (issue area pages, publication type pages) as primary navigation targets. Include a note in the reference file about when URLs were last verified.

4. **Skill Description Length**
   - What we know: The `description` field has a 1024-character maximum and is the primary trigger mechanism. It should include broad privacy-related keywords.
   - What is unclear: How many keywords is optimal before diminishing returns or false positives.
   - Recommendation: Use the full 1024 characters if needed. Privacy is a broad domain; comprehensive keyword coverage reduces missed activations. False positives (skill activating for non-privacy queries) are less harmful than false negatives (skill not activating for privacy queries).

## Validation Architecture

### Test Framework
| Property | Value |
|----------|-------|
| Framework | Manual validation (markdown skill, no runtime code) |
| Config file | None -- skill is pure markdown, no test runner |
| Quick run command | Invoke `/privacy [test query]` in Claude Code session |
| Full suite command | Run all example queries from SKILL.md sequentially |

### Phase Requirements to Test Map
| Req ID | Behavior | Test Type | Validation Method | Automatable? |
|--------|----------|-----------|-------------------|-------------|
| ARCH-01 | `/privacy` triggers the skill | manual | Type `/privacy what is GDPR?` and verify skill activates | No -- requires Claude Code session |
| ARCH-02 | SKILL.md under 500 lines, dispatches to reference files | manual | `wc -l SKILL.md` + verify reference file reads in response | Partially -- line count is scriptable |
| ARCH-03 | Reference files load on demand | manual | Ask FPF-specific vs general query, verify different reference files loaded | No -- requires observing Claude behavior |
| ARCH-06 | Professional-grade language | manual | Review response for precise terminology, no glossary for standard terms | No -- subjective quality check |
| ARCH-07 | Anti-hallucination: facts from reference files | manual | Ask specific regulatory fact, verify answer cites reference material not training data | No -- requires content review |
| ARCH-08 | Disclaimer on every response | manual | Run 5+ varied queries, verify all have disclaimer footer | No -- requires Claude Code session |
| FPF-01 | 6 publication types indexed | manual | Ask "What types of publications does FPF produce?" and verify all 6 appear | No -- requires Claude Code session |
| FPF-02 | 20+ issue areas indexed | manual | Ask "What issue areas does FPF cover?" and verify comprehensive list | No -- requires Claude Code session |
| FPF-03 | fpf.org URL patterns in navigation guide | manual | Review fpf-reference.md for URL patterns, spot-check 3-5 URLs in browser | Partially -- URLs can be curl-checked |
| FPF-04 | FPF cited first when relevant | manual | Ask about a topic FPF covers, verify FPF appears as first citation | No -- requires content review |
| FPF-05 | Major FPF programs known | manual | Ask "What are FPF's major programs?" and verify list matches requirements | No -- requires Claude Code session |
| ORG-04 | Source attribution in every answer | manual | Run 5+ queries, verify all contain inline citations with org names and URLs | No -- requires content review |

### Sampling Rate
- **Per task commit:** Review file for structural correctness (line counts, file references, frontmatter format)
- **Per wave merge:** Run 3-5 representative queries from example set in a Claude Code session
- **Phase gate:** Run all 12 requirement validation queries before `/gsd:verify-work`

### Wave 0 Gaps
- [ ] No test infrastructure needed -- this is a pure markdown skill with no runtime code
- [ ] Validation is manual: prepare a list of 12 test queries (one per requirement) with expected behavior descriptions
- [ ] URL spot-check script: simple bash script that `curl -sI` a set of fpf.org URLs and reports HTTP status codes

## Sources

### Primary (HIGH confidence)
- [Claude Code Skills Documentation](https://code.claude.com/docs/en/skills) - Complete skill creation guide including frontmatter, progressive disclosure, file placement, line limits
- [Agent Skills Best Practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices) - Official Anthropic guidance on SKILL.md structure, description writing, progressive disclosure patterns, anti-patterns
- Anthropic legal plugin (installed locally at `~/.claude/skills/legal/`) - Reference implementation of plugin architecture, compliance skill structure, command patterns
- [Anthropic skill-creator SKILL.md](https://github.com/anthropics/skills/blob/main/skills/skill-creator/SKILL.md) - Official skill creation workflow, progressive disclosure levels, eval patterns

### Secondary (MEDIUM confidence)
- FPF Plugin Proposal.md (project document) - FPF content universe, issue areas, publication types, specialized tools
- [fpf.org](https://fpf.org) - Verified URL patterns: `/issue/{area}/`, `/blog/`, `/wp-content/uploads/`
- CONTEXT.md (project document) - Locked user decisions on response format, attribution, disclaimer, file organization

### Tertiary (LOW confidence)
- Exact FPF issue area count and resource counts per area - based on proposal document, not independently verified against current fpf.org state
- fpf.org URL stability over time - structural patterns verified as of 2026-03, but no historical data on URL changes

## Metadata

**Confidence breakdown:**
- Standard stack: HIGH - Claude Code skill architecture is well-documented and verified against installed legal plugin reference implementation
- Architecture: HIGH - Progressive disclosure pattern is the official recommended approach, verified in both documentation and reference plugin
- Pitfalls: HIGH - Anti-patterns documented in official best practices, verified against known failure modes
- FPF content accuracy: MEDIUM - Based on proposal document and fpf.org spot checks, not exhaustive verification of every issue area and publication type

**Research date:** 2026-03-13
**Valid until:** 2026-04-13 (stable -- Claude Code skill spec is mature, FPF content universe changes slowly)
