# Codebase Concerns

**Analysis Date:** 2026-03-12

## Project Stage Assessment

This project is in **design/planning phase with no implementation yet**. The following concerns are architectural and strategic, identified from the feature specifications and design documentation.

---

## Tech Debt & Architectural Concerns

### 1. Content Freshness & Knowledge Decay

**Issue:** FPF publishes ~50+ new resources per year, but the skill knowledge bases are static encoded documents. They will grow stale within months.

**Files:** `FPF Plugin Proposal.md` (lines 194-202)

**Impact:**
- Encoded regulatory timelines become inaccurate (enforcement dates, cure periods)
- New legislation (state AI laws, privacy laws) won't be reflected
- U.S. Privacy Legislation skill references "50+ state comprehensive privacy laws" — this number will change
- Users will receive outdated guidance, eroding trust in the plugin

**Fix approach:**
- Decide on content update strategy before implementation: (a) semantic versioning bumps every quarter, (b) hybrid approach with static skills + dynamic web fetch for time-sensitive data, or (c) scheduled retraining pipeline
- For Tier 2 (member portal), build MCP server to fetch live content rather than encoding static snapshots
- Document update SLA in plugin manifest

---

### 2. Member Portal Technical Feasibility Unresolved

**Issue:** Tier 2 (members-only plugin) assumes MCP server can access the member portal, but no feasibility study has been completed.

**Files:** `FPF Plugin Idea.md` (line 9), `FPF Plugin Proposal.md` (lines 194-197, 202)

**Impact:**
- Tier 2 may not be technically feasible if portal uses JavaScript rendering, IP blocking, or doesn't expose an API
- Time estimate for Phase 3 is unknown
- Scope creep risk: MCP server complexity was underestimated in earlier projects ("I was able to complete a similar configuration without any changes to the website" — this may not hold for FPF's portal)
- Authentication/token refresh handling could be fragile if portal uses sessions instead of API keys

**Fix approach:**
- Conduct technical audit of FPF member portal BEFORE Phase 3 planning:
  - Does it expose a REST API or GraphQL endpoint?
  - What authentication method (OAuth, API keys, session tokens)?
  - Are there rate limits or IP restrictions?
  - Is content dynamically rendered or server-side?
- If portal requires web scraping/browser automation, document maintenance burden and fragility risk
- Add contingency: define fallback scope if portal integration is not feasible (e.g., members-only skills without live portal access)

---

### 3. Disclaimer & Legal Liability Not Defined

**Issue:** Plugin provides compliance guidance and risk assessments (e.g., `/fpf:assess`, `/fpf:checklist`), but legal disclaimers are not yet written.

**Files:** `FPF Plugin Proposal.md` (line 200)

**Impact:**
- Users may rely on plugin output as legal advice, creating liability exposure for FPF
- Similar plugins (Anthropic's legal plugin) prominently disclaim "results require professional review"
- No guidance on when escalation to human experts is required (e.g., risk assessments rated "RED")
- Privacy assessments could be wrong, leading to regulatory violations if users treat them as authoritative

**Fix approach:**
- Draft legal disclaimer templates before Phase 1 implementation
- Define escalation rules for each skill/command (e.g., RED severity → "human expert review required")
- Add metadata to every output: "This is for reference only; consult FPF experts or legal counsel before relying on this analysis"
- Have FPF legal team review disclaimer language before release

---

### 4. Skill Knowledge Base Validation & Review Not Assigned

**Issue:** 15 domain skills encoding regulatory frameworks, best practices, and analytical methodologies require subject matter expert review, but responsibility is unassigned.

**Files:** `FPF Plugin Proposal.md` (line 199: "Which FPF staff/teams should review the analytical frameworks encoded in skills?")

**Impact:**
- Skills may contain inaccuracies or outdated regulatory interpretations
- AI Governance skill references "EU AI Act conformity assessment steps" and "prohibited practices" — if wrong, users get incorrect guidance
- U.S. Privacy Legislation skill references enforcement timelines — if dates are wrong, compliance failures result
- No feedback loop to fix mistakes once plugin is in production

**Fix approach:**
- Assign each domain skill to a subject matter expert from FPF's corresponding center/team (Center for AI for AI skills, etc.)
- Require expert sign-off before each skill is finalized
- For Phase 1, prioritize expert review for highest-risk skills: AI Governance, U.S. Privacy Legislation, Global Data Protection
- Document review checklist: accuracy of laws/timelines, alignment with FPF's published positions, alignment with FPF's analytical methodology
- Plan for ongoing review cadence (quarterly or after major FPF publications)

---

## Scaling & Maintenance Concerns

### 5. Skill Proliferation Risk

**Issue:** Phase 1 alone requires building 18 skills (3 cross-cutting + 15 domain). Phase 2 adds agents. This is high maintenance surface area.

**Files:** `FPF Plugin Proposal.md` (lines 89-120, 174-175)

**Impact:**
- Each skill requires documentation, validation, and maintenance
- Cross-domain interactions not modeled (e.g., "AI Governance" + "U.S. Privacy Legislation" overlap on AI laws)
- If a regulatory update affects multiple skills, each must be updated independently
- Skill quality may degrade as team grows — no shared patterns for skill design

**Fix approach:**
- Create skill design pattern documentation before implementation (template, required sections, example)
- Define clear scope boundaries between overlapping domains (e.g., U.S. state AI laws live in U.S. Privacy Legislation, not AI Legislation)
- Build internal skill registry: track each skill's SME, last review date, next scheduled review
- For Phase 2+, consider domain consolidation: merge related skills (e.g., "Immersive Tech" + "Youth Privacy" → "Youth Immersive Tech") if they share SME

---

### 6. Command Consistency & Design Pattern Risk

**Issue:** Commands are designed to be independent, but no shared command framework exists.

**Files:** `FPF Plugin Proposal.md` (lines 122-131)

**Impact:**
- `/fpf:brief` outputs "Background, Key Issues, Stakeholder Perspectives, Recommendations" but `/fpf:landscape` outputs undefined format
- `/fpf:assess` uses "GREEN/YELLOW/ORANGE/RED" severity, but unclear if other commands use same classification
- Users won't know what to expect from each command; inconsistency erodes trust
- Future commands added in Phase 2+ may not follow the same pattern

**Fix approach:**
- Document command design framework before implementation:
  - Standard command input validation
  - Output format specifications (markdown structure, tables, severity classifications)
  - Error handling (e.g., what if user provides invalid regulation name?)
- Create command template/reference implementation
- For Phase 1 (`/fpf:brief`, `/fpf:landscape`), validate output consistency across different topic inputs before release

---

## Security & Privacy Concerns

### 7. Authentication & Token Management (Tier 2)

**Issue:** Member portal MCP server requires authentication, but token refresh strategy is unclear.

**Files:** `FPF Plugin Proposal.md` (lines 144-149)

**Impact:**
- Stale tokens → MCP server fails mid-session, degrading UX
- Token exposure → credentials leaked in Claude conversation logs (if not properly isolated)
- Session hijacking risk if member portal uses non-secure session tokens
- No guidance on token revocation if member account is suspended

**Fix approach:**
- Before Phase 3, define token lifecycle: how are tokens provisioned, refreshed, revoked?
- Use short-lived tokens (15-30 min) with refresh tokens for long-lived sessions
- Store tokens in secure Claude sandbox, not in conversation context
- Log all portal API calls for audit trail
- Test token expiration scenarios and graceful fallback behavior

---

### 8. Information Disclosure Risk (Public Plugin)

**Issue:** Public plugin compiles FPF research into skills. Some FPF publications may reference sensitive topics (e.g., police surveillance, law enforcement data sharing) that require careful context.

**Files:** `FPF Plugin Proposal.md` (lines 86-120)

**Impact:**
- Plugin could be misused to develop privacy-invasive technologies (e.g., surveillance tools using FPF's biometrics research)
- No mechanism to prevent adversarial use
- "Better context for privacy research" could help bad actors as easily as good actors

**Fix approach:**
- This is an inherent risk for public content — acknowledge it in project decisions
- Add prominent notices to high-risk topics (biometrics, surveillance, location data) reminding users to use knowledge responsibly
- Consider licensing: FPF's CC license allows commercial use, but plugin terms of service could impose additional restrictions

---

## Known Gaps & Missing Requirements

### 9. Regulatory Landscape Scope Undefined

**Issue:** Plugin claims to cover "50+ state comprehensive privacy laws," "GDPR, LGPD, POPIA, PIPL," and "27 laws across 14 states" for AI, but comprehensive coverage is not feasible.

**Files:** `FPF Plugin Proposal.md` (lines 106-108)

**Impact:**
- Users may expect complete jurisdiction coverage and receive incomplete guidance
- No clear priority order for which jurisdictions to cover first
- Risk of omitting emerging laws (e.g., new state AI law passed after plugin release)

**Fix approach:**
- Define MVP jurisdiction scope explicitly: which 3-5 states/countries are priority for Phase 1?
- Document coverage gaps clearly in skill output: "This assessment covers U.S. federal law and California law; verify compliance with your jurisdiction"
- Prioritize based on FPF's published focus areas and member distribution

---

### 10. Research Synthesis Agent Methodology Undefined

**Issue:** Phase 2 adds "Research Synthesis" agent that "conducts structured analysis following FPF methodology," but FPF methodology is encoded implicitly, not explicitly.

**Files:** `FPF Plugin Proposal.md` (lines 135-137)

**Impact:**
- Unclear what "FPF methodology" means: what steps does it follow? What frameworks?
- Agent output quality depends on how well the methodology is encoded — no validation plan
- Difficult to audit or improve agent behavior without explicit methodology specification

**Fix approach:**
- Before Phase 2, document FPF's research methodology explicitly:
  - What are the standard steps (e.g., problem identification → stakeholder mapping → regulatory analysis → synthesis)?
  - What sources does FPF prioritize (academic research, regulatory documents, stakeholder positions)?
  - What is FPF's position on conflicting viewpoints (pragmatic, rights-first, etc.)?
- Encode methodology in "Privacy Research Methodology" skill with concrete examples
- Create research synthesis agent template showing methodology flow before implementation

---

### 11. Stakeholder Map Agent Scope Unclear

**Issue:** `/fpf:stakeholder-map` identifies "industry, regulator, civil society, and academic positions," but no data source is specified.

**Files:** `FPF Plugin Proposal.md` (line 130)

**Impact:**
- Does the agent rely on FPF source catalog (static), web search (current but unvetted), or both?
- Potential for bias if stakeholder positions are not systematically sourced
- Unclear if "academic positions" means cited in FPF publications or all academic sources

**Fix approach:**
- Define stakeholder mapping methodology:
  - Primary sources: FPF publications, member discussions (for Tier 2)
  - Secondary sources: regulatory filings, published statements
  - Web search as fallback only
- Document known limitations (e.g., "industry positions are weighted toward organizations active in FPF communities")

---

## Operational & Sustainability Concerns

### 12. Phase Sequencing & Delivery Risk

**Issue:** Phase 1 requires building 18 skills + 2 commands, Phase 2 requires 4 more commands + 3 agents, Phase 3 requires MCP server for member portal. Scope is large.

**Files:** `FPF Plugin Proposal.md` (lines 174-189)

**Impact:**
- Phase 1 is high-risk: building 18 skills in parallel without shared patterns increases quality variance
- No explicit acceptance criteria or validation plan for Phase 1 completion
- Phase 2 depends on agents, which depend on solid skill foundations — delays cascade
- Phase 3 depends on unresolved member portal feasibility — could block entire Tier 2

**Fix approach:**
- Reorder phases: Phase 0 (feasibility & design) before Phase 1 implementation
  - Phase 0: Validate member portal API, draft skill design patterns, write legal disclaimers
  - Phase 1: Build 3 cross-cutting skills first, then 2-3 domain skills as patterns emerge
  - Phase 2: Expand skills and add commands
  - Phase 3: MCP server + members-only features (only if Phase 0 validates feasibility)
- Define Phase 1 completion criteria: all skills reviewed by SMEs, commands tested with 10+ sample inputs, output consistency validated

---

### 13. Distribution & Maintenance Ownership Not Assigned

**Issue:** Plugin requires ongoing maintenance, versioning, and distribution, but ownership is unclear.

**Files:** `FPF Plugin Proposal.md` (line 198)

**Impact:**
- Who owns the Claude Marketplace listing? Who updates it?
- Who monitors for bug reports or user feedback?
- Who decides when to cut a new version?
- Members-only distribution (if different from public) requires separate infrastructure

**Fix approach:**
- Assign plugin maintainer role (likely one of the staff members who approved skills)
- Define maintenance SLA: response time for bug reports, versioning cadence
- Create feedback loop: how do users report inaccurate guidance? How is it fixed?
- For members-only plugin, define distribution (hosted by FPF internally, Claude Marketplace, both?)

---

## Risk Summary Table

| Concern | Severity | Impact | Timing |
|---------|----------|--------|--------|
| Content freshness & decay | High | Plugin becomes inaccurate within 6 months | Pre-Phase 1 |
| Member portal feasibility | High | Phase 3 scope/timeline unknown | Pre-Phase 1 |
| Legal disclaimers missing | High | Liability exposure for FPF | Pre-Phase 1 |
| Skill validation unassigned | High | Inaccurate regulatory guidance | Pre-Phase 1 |
| Skill proliferation risk | Medium | High maintenance surface area | Phase 1 |
| Command consistency | Medium | Unpredictable UX | Phase 1 |
| Token management (Tier 2) | Medium | Auth failures, potential token leaks | Phase 3 |
| Research methodology undefined | Medium | Agent quality degradation | Phase 2 |
| Regulatory scope undefined | Medium | Unmet user expectations | Phase 1 |
| Phase sequencing risk | Medium | Delays cascade, quality variance | Pre-Phase 1 |
| Maintenance ownership unassigned | Low | Operational drift post-launch | Pre-Phase 1 |

---

*Concerns audit: 2026-03-12*
