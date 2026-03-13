# Technology Stack

**Project:** FPF Privacy Research Skill
**Researched:** 2026-03-12

## Recommended Stack

This is a Claude Code skill -- a SKILL.md file with bundled reference files. There is no runtime language, no database, no web framework. The entire "stack" is the Claude Code skill framework: markdown files with YAML frontmatter, organized using progressive disclosure patterns, leveraging Claude's built-in tools (WebFetch, WebSearch, Read, Grep) for both static knowledge lookups and live web research.

### Core Framework

| Technology | Version | Purpose | Why |
|------------|---------|---------|-----|
| Claude Code Skill (Agent Skills open standard) | Current (2025-12 spec) | Skill definition and invocation | The only framework that matters. This is a SKILL.md-based skill, not a web app. The Agent Skills spec is an open standard adopted by both Anthropic and OpenAI. Skills are markdown files with YAML frontmatter that Claude loads on demand. |
| Markdown + YAML frontmatter | N/A | Skill content and metadata | Required format for SKILL.md. YAML frontmatter configures name, description, invocation behavior, tool access. Markdown body contains instructions Claude follows. |

### Knowledge Base Architecture

| Technology | Version | Purpose | Why |
|------------|---------|---------|-----|
| Progressive disclosure file structure | N/A | Organize large knowledge base across reference files | SKILL.md stays under 500 lines (official recommendation). Detailed content lives in separate reference files that Claude loads only when relevant to the query. This is the official Anthropic pattern for knowledge-heavy skills. The amount of bundled content is effectively unbounded because files only consume context tokens when actually read. |
| Domain-organized reference files (.md) | N/A | Per-topic knowledge (organizations, regulations, navigation guides) | Following the "domain-specific organization" pattern from Anthropic's best practices. Each privacy domain gets its own reference file. Claude reads only the file(s) relevant to the current query, keeping context usage efficient. |
| Site navigation guide files (.md) | N/A | Per-source website navigation instructions for LLM-assisted browsing | Unique to this project. Each major privacy organization gets a navigation guide that teaches Claude how to search, navigate URL patterns, find key content sections, and extract information from that specific website. These guides make WebFetch calls dramatically more effective. |

### Live Research Tools (Built-in to Claude Code)

| Technology | Version | Purpose | Why |
|------------|---------|---------|-----|
| WebSearch (Claude Code built-in) | Current | Discover relevant pages and sources when static knowledge is insufficient | Built into Claude Code, no installation required. Returns search result links and titles. Use for ecosystem discovery and finding current content. The skill instructs Claude when and how to use WebSearch for privacy research queries. |
| WebFetch (Claude Code built-in) | Current | Fetch and extract content from known URLs | Built into Claude Code, no installation required. Accepts a URL + prompt, returns extracted content. This is the primary tool for live deep research -- the skill provides URL patterns and navigation guides so Claude knows exactly what URLs to fetch and what to extract. |
| Read, Grep, Glob (Claude Code built-in) | Current | Access bundled reference files | Core tools Claude uses to navigate the skill's file structure. Read loads reference files on demand. Grep searches across reference files for specific terms. These enable the progressive disclosure pattern. |

### Supporting Infrastructure

| Technology | Version | Purpose | Why |
|------------|---------|---------|-----|
| Git | Current | Version control for skill files | Track changes to knowledge base content. Enable version-tagged releases. The skill is a collection of files that should be version-controlled like any codebase. |
| Skill-creator skill | Installed in environment | Bootstrap skill creation | Already installed per PROJECT.md. Use to scaffold the initial SKILL.md structure, then customize. Saves time on boilerplate. |

## Architecture: How the Pieces Fit Together

### The Three-Layer Knowledge Architecture

**Layer 1: SKILL.md (Router + Core Instructions)**
- Under 500 lines
- Contains: skill description, query routing logic, tool usage instructions, navigation index to reference files
- Always loaded when skill is invoked
- Tells Claude: "For FPF content, check `reference/fpf-index.md`. For IAPP, check `reference/orgs/iapp.md`. For live research, follow the navigation guide in `guides/[org-name].md`."

**Layer 2: Static Reference Files (Domain Knowledge)**
- Loaded on demand via Read tool
- Organization catalog: one file per major privacy organization
- FPF deep index: programs, publications, policy briefs, reports
- Regulation quick-reference: key privacy laws and frameworks
- Loaded only when relevant to the query

**Layer 3: Site Navigation Guides (Live Research Enablers)**
- Loaded on demand when live fetching is needed
- Per-source files teaching Claude how to navigate each organization's website
- URL patterns, search endpoints, content structure, key sections
- Transforms WebFetch from generic page fetching into targeted, expert-level research

### Query Flow

```
User asks "/privacy [question]"
  |
  v
SKILL.md loads (Layer 1)
  - Routes query to relevant domain
  - Determines: static answer sufficient? Or live research needed?
  |
  +---> Static path: Read relevant reference file(s) from Layer 2
  |     Return answer with source citations
  |
  +---> Live research path:
        1. Read navigation guide for target source (Layer 3)
        2. Use WebSearch to find specific pages (if URL unknown)
        3. Use WebFetch with navigation guide's URL patterns
        4. Synthesize findings with static knowledge
        Return answer with live source citations
```

## Recommended Skill File Structure

```
privacy/
  SKILL.md                          # Main skill (under 500 lines)
  reference/
    fpf-index.md                    # FPF programs, publications, key offerings
    org-catalog.md                  # Master catalog of all privacy organizations
    regulations-quickref.md         # Key regulations quick reference
    orgs/                           # Per-organization detail files
      iapp.md
      epic.md
      calprivacy.md
      eff.md
      nist.md
      edpb.md
      ... (one per org)
  guides/                           # Site navigation guides for live research
    fpf-navigation.md               # How to navigate fpf.org
    iapp-navigation.md              # How to navigate iapp.org
    epic-navigation.md              # How to navigate epic.org
    ... (one per org that supports WebFetch)
```

**Why this structure:**
- `SKILL.md` is the router -- it tells Claude where to find things but does not contain the knowledge itself
- `reference/` files are the static knowledge base -- loaded on demand, one topic per file
- `guides/` files are the live research enablers -- loaded only when Claude needs to fetch from a specific site
- One level deep from SKILL.md (official best practice: avoid nested references)
- Descriptive file names (official best practice: `fpf-index.md` not `ref1.md`)
- Each reference file should have a table of contents at the top if over 100 lines (official best practice)

## Critical Technical Decisions

### Decision 1: Single SKILL.md, Not Multiple Skills

**Chosen:** One skill (`/privacy`) with progressive disclosure via reference files.
**Why:** PROJECT.md explicitly scopes this as "a single `/privacy` command." Multiple skills would fragment the user experience and create routing complexity. A single skill with well-organized reference files achieves the same depth without the overhead. The progressive disclosure pattern means the amount of bundled knowledge is effectively unbounded.
**Confidence:** HIGH -- this aligns with both the project requirements and Anthropic's recommended pattern for knowledge-heavy skills.

### Decision 2: WebFetch for Live Research, Not MCP Servers

**Chosen:** Use Claude Code's built-in WebFetch and WebSearch tools for live web research.
**Not chosen:** Custom MCP servers for web scraping, Playwright/Puppeteer browser automation.
**Why:** WebFetch is built into Claude Code, requires zero infrastructure, and works with any publicly accessible URL. MCP servers add deployment complexity and maintenance burden. The skill only needs to fetch public web pages, which WebFetch handles directly. The key innovation is the *navigation guides* that teach Claude how to effectively use WebFetch on each specific site, not a custom fetching infrastructure.
**Limitation:** WebFetch does not support JavaScript-rendered pages. If a privacy organization's site is heavily JS-rendered (SPAs), WebFetch will return the initial HTML, not the rendered DOM. The navigation guides should note this per-site and provide fallback strategies (e.g., direct API endpoints, sitemap URLs, or cached/static versions).
**Confidence:** HIGH -- WebFetch is the standard tool for this use case. MCP servers would be overengineering.

### Decision 3: Skill Runs Inline, Not in Subagent

**Chosen:** Default invocation (no `context: fork`). The skill runs inline in the user's conversation context.
**Why:** The skill needs to maintain conversation context -- users will ask follow-up questions, refine their research, and reference previous answers. A forked subagent loses conversation history. Additionally, there is a known unresolved issue (GitHub #21318, closed not-planned) where marketplace plugin subagents cannot access WebSearch and WebFetch tools. Running inline avoids this entirely.
**Trade-off:** Inline execution means the skill's reference file content competes for context window space with conversation history. This is mitigated by the progressive disclosure pattern -- only load the reference files needed for the current query.
**Confidence:** HIGH.

### Decision 4: FPF-First Source Priority via Skill Instructions

**Chosen:** Encode FPF source priority in SKILL.md instructions, not in file structure or tooling.
**Why:** The skill instructs Claude: "When the query is relevant to FPF's work, check FPF sources first and cite them first. Then supplement with other organizations." This is a prompt-level instruction, not an architectural constraint. It keeps the knowledge base neutral and reusable while ensuring FPF gets priority citation in outputs.
**Confidence:** HIGH -- this is the natural way to express source priority in a skill.

### Decision 5: Navigation Guides as Separate Files, Not Embedded in Org Profiles

**Chosen:** Separate `guides/` directory with per-site navigation files, distinct from `reference/orgs/` profile files.
**Why:** Navigation guides serve a different purpose than organization profiles. Profiles answer "What does this org do? What content do they publish?" Navigation guides answer "How do I fetch content from this org's website?" Keeping them separate means Claude only loads the navigation guide when it needs to do live fetching. For static knowledge queries, the navigation guide is never loaded, saving context window space.
**Confidence:** MEDIUM -- this could alternatively be a section within each org's reference file. Separate files are better for progressive disclosure but add more files to manage. The recommendation is separate files for organizations with complex sites (FPF, IAPP, EPIC) and embedded sections for simpler sites.

## Alternatives Considered

| Category | Recommended | Alternative | Why Not |
|----------|-------------|-------------|---------|
| Skill format | Single SKILL.md + reference files | Multiple skills (one per domain) | PROJECT.md explicitly requires single `/privacy` command. Multiple skills create routing complexity and could exceed the skill description character budget (2% of context window). |
| Live research | WebFetch + WebSearch (built-in) | Custom MCP server for web scraping | Overengineering. WebFetch handles public pages. MCP adds deployment/maintenance burden for zero additional capability on public content. |
| Live research | WebFetch + WebSearch (built-in) | Playwright/Puppeteer via Bash scripts | Heavy dependency, security concerns, fragile selectors. WebFetch is simpler and sufficient for most privacy org sites. |
| Knowledge format | Markdown reference files | JSON data files | Markdown is more token-efficient for LLM consumption. JSON is better for structured queries but adds parsing overhead. Claude reads markdown natively. |
| Knowledge format | Markdown reference files | SQLite database via Bash queries | Unnecessary complexity. The knowledge base is not large enough to justify a database. Markdown files with Grep provide sufficient search capability. |
| Execution context | Inline (default) | `context: fork` (subagent) | Subagents lose conversation history and have known issues with WebSearch/WebFetch access in plugin contexts. |
| Content freshness | Hybrid static + live fetch | Purely static (version bumps only) | Static-only becomes stale within months. FPF publishes ~50+ new resources/year. Live fetching ensures currency for deep research. |
| Content freshness | Hybrid static + live fetch | Purely live (no static knowledge) | Too slow for common queries. Static knowledge enables instant answers for "What does COPPA require?" without web fetching. |

## Tool Access Configuration

### Frontmatter Configuration

```yaml
---
name: privacy
description: Comprehensive data privacy research and reference tool. Provides instant access to FPF (Future of Privacy Forum) publications, privacy organization catalogs, regulatory frameworks, and live web research across major privacy sources. Use when researching privacy law, data protection regulations, privacy organizations, compliance requirements, or privacy policy analysis. Covers GDPR, CCPA, COPPA, state privacy laws, AI governance, children's privacy, health data, ad tech, biometrics, and all major privacy domains.
allowed-tools: Read, Grep, Glob, WebFetch, WebSearch
---
```

**Why these allowed-tools:**
- `Read`: Load reference files on demand (core progressive disclosure mechanism)
- `Grep`: Search across reference files for specific terms, regulations, or organizations
- `Glob`: Discover available reference files in the skill directory
- `WebFetch`: Fetch live content from privacy organization websites
- `WebSearch`: Discover new/current content when static knowledge is insufficient

**Why `allowed-tools` matters:** Without this field, Claude would need per-use user approval for each tool invocation. For a research skill that routinely reads multiple reference files and fetches web pages, this would create constant approval prompts. The `allowed-tools` field grants these tools automatically when the skill is active.

### Important: WebSearch Permission Considerations

WebSearch currently lacks wildcard permission support in Claude Code (GitHub #26530). Users may need to manually approve WebSearch calls even with `allowed-tools` configured. The skill should be designed to work well without WebSearch (using static knowledge + WebFetch with known URLs from navigation guides) and treat WebSearch as an enhancement for discovery.

## What NOT to Do

### Do NOT put the entire knowledge base in SKILL.md
SKILL.md has a 500-line recommended limit. The compliance skill from Anthropic's knowledge-work-plugins puts everything in one file and is limited in depth as a result. This project's value proposition is *deeper* coverage -- that requires reference files.

### Do NOT build multiple skills for different domains
The project requirement is one `/privacy` command. Splitting into `/privacy-gdpr`, `/privacy-coppa`, etc. fragments the user experience and makes the skill harder to discover. Use reference files for domain separation, not separate skills.

### Do NOT create custom scripts for web fetching
WebFetch is built-in and handles public pages. Writing Python/Node scripts to scrape websites adds fragile dependencies, maintenance burden, and security concerns. Let the navigation guides make WebFetch effective instead of replacing it.

### Do NOT deeply nest reference files
Anthropic's official guidance: keep references one level deep from SKILL.md. `reference/orgs/iapp.md` is acceptable (two levels from SKILL.md). `reference/orgs/iapp/publications/reports/2024.md` is too deep -- Claude may only partially read deeply nested files.

### Do NOT use JSON for the knowledge base
Markdown is the native format for Claude skills. It is more token-efficient than JSON for prose content, more readable for human editors, and does not require parsing. Use JSON only if you need structured data that benefits from schema validation (e.g., a machine-readable regulations registry), and even then, keep it supplementary to the markdown knowledge base.

### Do NOT assume WebFetch works on all sites
WebFetch does not execute JavaScript. Sites that are SPAs (React/Angular/Vue rendered client-side) will return incomplete content. The navigation guides should document per-site whether WebFetch works effectively and provide fallback strategies.

### Do NOT embed time-sensitive dates in static reference files without flagging them
Enforcement dates, cure periods, and regulatory deadlines change. Static reference files should flag time-sensitive content with markers like `[VERIFY-CURRENT]` so users and maintainers know what to check during updates.

## Content Sizing Estimates

| Component | Estimated Lines | Files |
|-----------|----------------|-------|
| SKILL.md (router + instructions) | 300-450 | 1 |
| FPF index (programs, publications) | 400-600 | 1 |
| Organization catalog (master list) | 200-300 | 1 |
| Regulations quick reference | 300-400 | 1 |
| Per-organization detail files | 100-200 each | 15-25 |
| Per-site navigation guides | 50-150 each | 10-15 |
| **Total** | **~5,000-10,000** | **~30-45 files** |

This is well within the skill framework's capacity. Only SKILL.md and the 1-3 relevant reference files load per query (typically 500-1,000 lines of context), leaving ample room in the context window for conversation history and Claude's reasoning.

## Sources

### Official Documentation (HIGH confidence)
- [Claude Code Skills Documentation](https://code.claude.com/docs/en/skills) -- Complete skill specification, frontmatter reference, progressive disclosure patterns, file organization
- [Skill Authoring Best Practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices) -- Official Anthropic guidance on progressive disclosure, naming, testing, anti-patterns
- [Agent Skills Overview](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview) -- Architecture, runtime environment, how skills load content
- [Anthropic knowledge-work-plugins: compliance skill](https://github.com/anthropics/knowledge-work-plugins/tree/main/legal/skills/compliance) -- Reference implementation for knowledge-heavy legal/compliance skill
- [Anthropic skills repository](https://github.com/anthropics/skills/) -- Official skill examples and templates
- [Web Fetch Tool Documentation](https://platform.claude.com/docs/en/agents-and-tools/tool-use/web-fetch-tool) -- WebFetch capabilities and limitations

### Technical Analysis (HIGH confidence)
- [Agent Skills: A First Principles Deep Dive](https://leehanchung.github.io/blogs/2025/10/26/claude-skills-deep-dive/) -- Architecture analysis of progressive disclosure and skill loading
- [Claude Code Web Tools: WebFetch vs WebSearch](https://mikhail.io/2025/10/claude-code-web-tools/) -- Detailed comparison of web tools available in Claude Code

### Known Issues (HIGH confidence)
- [GitHub #21318: Plugin agents lack WebSearch/WebFetch access](https://github.com/anthropics/claude-code/issues/21318) -- Subagent tool access limitation (closed not-planned)
- [GitHub #26530: WebSearch wildcard permissions](https://github.com/anthropics/claude-code/issues/26530) -- WebSearch permission system limitation
- [GitHub #27862: WebSearch permission cannot be persistently allowed](https://github.com/anthropics/claude-code/issues/27862) -- WebSearch approval UX limitation

### Community Patterns (MEDIUM confidence)
- [Claude Code Customization Guide](https://alexop.dev/posts/claude-code-customization-guide-claudemd-skills-subagents/) -- Practical skill creation patterns
- [Progressive Disclosure Pattern](https://alexop.dev/posts/stop-bloating-your-claude-md-progressive-disclosure-ai-coding-tools/) -- Context management strategies
- [Equipping agents for the real world](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills) -- Anthropic engineering blog on Agent Skills design

---

*Stack research: 2026-03-12*
