# Feature Research

**Domain:** Data Privacy Research Skill (Claude Code Skill for Privacy Professionals)
**Researched:** 2026-03-12
**Confidence:** MEDIUM-HIGH

## Context: What Privacy Professionals Actually Need

Privacy professionals (lawyers, compliance officers, policy analysts) face a fragmented research landscape. Their pain points, validated by ISACA's 2025 survey showing 63% find their jobs more stressful than five years ago, center on:

1. **Regulatory velocity:** 8 new U.S. state privacy laws took effect in 2025 alone, plus the EU AI Act (August 2026). Keeping up requires monitoring dozens of sources daily.
2. **Source fragmentation:** Research is scattered across FPF, IAPP, EPIC, CalPrivacy, DPA websites, law firm blogs, government regulators, think tanks, and academic centers. No single tool covers them all.
3. **Context switching:** Moving between Westlaw/LexisNexis (legal text), IAPP (trackers and analysis), FPF (policy research), and government sites (enforcement actions) wastes significant time.
4. **Precision requirements:** Privacy professionals need exact regulatory language, specific provisions, and authoritative citations -- not summaries or paraphrases.

### Existing Tool Landscape

| Tool | What It Does | Gap This Skill Fills |
|------|-------------|---------------------|
| **Westlaw** | Full legal text, case law, 50-state surveys, Data Privacy Practice Center | Expensive ($$$), no org-level research (FPF papers, IAPP analysis), no navigation guidance |
| **LexisNexis Practical Guidance** | Practice notes, checklists, state law comparison (14+ topics), regulatory trackers (FTC, SEC, OCR, GDPR) | Enterprise pricing, compliance-workflow focused, not research-discovery focused |
| **IAPP Resource Center** | Trackers (state legislation, global AI, enforcement database), glossary, research reports, global privacy directory | Membership-gated, siloed from other orgs, no cross-source synthesis |
| **OneTrust** | Compliance automation across 300+ jurisdictions, consent management, AI governance | Operational tool, not research tool; enterprise SaaS, not knowledge access |
| **Bloomberg Law** | Comparison charts (US state vs EU), analysis | Legal-text focused, not policy-research focused |

**Key insight:** No existing tool acts as a **unified research navigator** that knows where to look across the entire privacy ecosystem and how to extract information from each source. This is the core value proposition.

## Feature Landscape

### Table Stakes (Users Expect These)

Features users assume exist. Missing these = skill feels incomplete and not worth using.

| Feature | Why Expected | Complexity | Notes |
|---------|--------------|------------|-------|
| **FPF content index** (publications, programs, issue areas) | Primary source per project requirements; users expect deep FPF knowledge | MEDIUM | Must cover all 6 publication types (Reports, White Papers, Filings, Infographics, Events, Videos) and 20+ issue areas. Static index baked into SKILL.md |
| **Major privacy org catalog** | A research skill that only knows FPF is too narrow to be useful | MEDIUM | Must include at minimum: IAPP, EPIC, CalPrivacy (CPPA), CDT, EFF, Georgetown Privacy Center, Brookings, noyb, Access Now, Privacy Rights Clearinghouse. Plus government bodies: FTC, EDPB, ICO, CNIL |
| **Per-source navigation guides** | The skill's core differentiator vs generic LLM; users expect the skill to know HOW to search each site | HIGH | URL patterns, key sections, content organization, search strategies for each indexed source. This is the most labor-intensive feature but defines the skill's value |
| **Quick reference for major regulations** | COPPA, CCPA/CPRA, GDPR, HIPAA, FERPA, GLBA, EU AI Act -- professionals ask about these constantly | MEDIUM | Key provisions, applicability, rights granted, enforcement body, penalties. Static knowledge base covers the 80% case |
| **Hybrid static/live architecture** | Static-only misses current developments; live-only is slow for common queries | MEDIUM | Static for: org catalogs, regulation summaries, navigation guides. Live for: recent enforcement actions, new legislation, current policy debates |
| **Professional-grade language** | Target audience knows the field; dumbed-down explanations waste their time | LOW | Prompt engineering in SKILL.md: use precise legal/regulatory terminology, assume domain knowledge, cite specific statutory sections |
| **Source attribution** | Privacy professionals need to verify claims; "the law says X" without a source is useless | LOW | Every answer cites the organization, document, and ideally URL. FPF cited first when relevant per project requirements |
| **Regulation cross-reference** | "How does CCPA compare to GDPR on consent?" is a daily question | MEDIUM | Key provision comparison across major frameworks. Static knowledge covers common comparisons; live fetching for emerging state laws |

### Differentiators (Competitive Advantage)

Features that set this skill apart from generic LLM privacy knowledge and existing tools.

| Feature | Value Proposition | Complexity | Notes |
|---------|-------------------|------------|-------|
| **FPF-first citation priority** | No other tool prioritizes FPF publications; this serves the specific user base (FPF-affiliated professionals) | LOW | Routing logic: check FPF coverage first, supplement with other sources. Simple prompt-level instruction |
| **Site-specific search strategies** | Teaching the LLM how each site organizes content (URL patterns, filter parameters, API endpoints) so it can construct precise fetch URLs | HIGH | This is the hardest feature to build well but creates the deepest moat. IAPP uses `/resources/article/`, FPF uses `/issue/` and `/publication-type/`, EPIC uses `/our-work/`, CalPrivacy uses `privacy.ca.gov` |
| **Tiered research depth** | Quick lookup ("What does COPPA require?") vs. deep research ("Current state of children's privacy law across all U.S. states") with different behaviors | MEDIUM | Quick: static knowledge base only, fast response. Deep: multi-source live fetching, synthesis across organizations, longer response |
| **Government regulator directory** | DPA/enforcement body lookup with jurisdiction, powers, key contact pages, recent enforcement actions | MEDIUM | U.S.: FTC, state AGs, CalPrivacy. EU: EDPB, national DPAs (ICO, CNIL, BfDI, AEPD, Garante). Plus: PIPEDA Commissioner, APAC DPAs |
| **FPF program and initiative awareness** | Knowledge of FPF's Center for AI, Youth Privacy work, training programs, Privacy Papers for Policymakers, working groups | MEDIUM | Static index of major programs with descriptions, key contacts, publication streams. Enables "What has FPF published on AI governance?" queries |
| **Regulatory timeline awareness** | Key dates: when laws take effect, comment periods, enforcement deadlines | MEDIUM | IAPP maintains a key dates tracker; static knowledge for major dates (EU AI Act August 2026), live fetching for current legislative calendar |
| **Think tank and academic center catalog** | Georgetown Privacy Center, Berkman Klein (Harvard), Stanford HAI, Brookings AI Initiative, R Street, Cato, Information Technology & Innovation Foundation | LOW | Often overlooked but these produce significant policy research that informs legislation |
| **Graceful degradation** | Skill remains useful without web access (static knowledge) but becomes more powerful with it | LOW | Architecture decision already made; implementation is about clear fallback messaging |

### Anti-Features (Commonly Requested, Often Problematic)

Features that seem good but create problems in this context.

| Feature | Why Requested | Why Problematic | Alternative |
|---------|---------------|-----------------|-------------|
| **Legal advice / compliance determinations** | Users naturally ask "Am I compliant?" or "What should we do?" | Liability risk, unauthorized practice of law, skill cannot assess specific business contexts | Provide regulatory requirements and point to relevant provisions; explicitly state the skill assists research, not legal review |
| **Exhaustive regulation text reproduction** | Users want full statutory text inline | Bloats responses, often exceeds context limits, text changes with amendments | Provide key provisions with citations and links to authoritative full text (e.g., official government sources) |
| **Real-time regulatory alert monitoring** | Privacy teams want push notifications on new developments | A Claude Code skill cannot run persistently; it only responds when invoked | Support "What's new in [jurisdiction]?" queries with live fetching. Recommend IAPP/OneTrust for actual monitoring |
| **Internal/proprietary FPF content** | Users affiliated with FPF may expect member-only content | Skill can only access public content; promising more creates disappointment | Clearly scope to public FPF content; provide navigation guide to member portal for users who have access |
| **Case management / workflow automation** | Compliance officers want DSR tracking, DPIA checklists, audit trails | Wrong tool category: this is a research skill, not a compliance platform | Recommend OneTrust, TrustArc, or BigID for operational compliance; this skill helps with the research that feeds those workflows |
| **All-jurisdiction depth** | Covering every country's privacy law in detail | Diminishing returns; 160+ jurisdictions is impossible to maintain accurately in static knowledge | Deep coverage of major frameworks (GDPR, CCPA/CPRA, COPPA, HIPAA, EU AI Act, UK DPA 2018) + pointers to DLA Piper Data Protection Laws of the World for exhaustive global coverage |
| **Enforcement action database** | Users want to search past enforcement decisions | Data changes constantly, volume is massive, IAPP already maintains this authoritatively | Provide navigation guide to IAPP Enforcement Database and key DPA enforcement pages; use live fetching for recent notable actions |
| **Multi-language support** | Global privacy professionals work in multiple languages | Massive complexity for marginal gain in a Claude Code skill; most privacy professionals working with these English-language sources read English | English only; note that many EU DPA sites have English sections and the navigation guides should include those |

## Feature Dependencies

```
[Per-source navigation guides]
    |-- requires --> [Major privacy org catalog] (must know what orgs exist before writing guides)
    |-- requires --> [FPF content index] (FPF guide is the most detailed)

[Tiered research depth]
    |-- requires --> [Quick reference for major regulations] (static layer)
    |-- requires --> [Per-source navigation guides] (live layer uses these to fetch)
    |-- requires --> [Hybrid static/live architecture]

[Regulation cross-reference]
    |-- requires --> [Quick reference for major regulations] (must know each regulation first)

[FPF-first citation priority]
    |-- requires --> [FPF content index]
    |-- requires --> [Source attribution]

[FPF program awareness]
    |-- requires --> [FPF content index]

[Government regulator directory]
    |-- enhances --> [Per-source navigation guides] (regulator sites are key sources)
    |-- enhances --> [Regulation cross-reference] (enforcement body maps to jurisdiction)

[Regulatory timeline awareness]
    |-- enhances --> [Quick reference for major regulations]
    |-- enhances --> [Tiered research depth] (time-sensitive queries need this)

[Site-specific search strategies]
    |-- requires --> [Per-source navigation guides] (strategies are embedded in guides)
    |-- enhances --> [Hybrid static/live architecture] (strategies make live fetching effective)
```

### Dependency Notes

- **Per-source navigation guides require org catalog:** You cannot write a navigation guide for a source you have not cataloged. The catalog defines scope; the guides provide depth.
- **Tiered research depth requires both static and live layers:** Quick mode uses static knowledge; deep mode adds live fetching using navigation guides. Both must exist.
- **Regulation cross-reference requires individual regulation knowledge:** Cannot compare regulations without first indexing their key provisions.
- **Site-specific search strategies are embedded in navigation guides:** These are not separate features but the most critical component of each guide. Separated here because the quality of search strategies determines the skill's effectiveness at live fetching.

## MVP Definition

### Launch With (v1)

Minimum viable product -- what is needed to validate the concept.

- [x] **FPF content index** -- Core identity; without deep FPF knowledge the skill has no reason to exist vs. generic LLM
- [x] **Major privacy org catalog** (15-20 organizations minimum) -- Establishes breadth; users need to see this covers their research landscape
- [x] **Per-source navigation guides** (FPF + 5-8 top sources) -- Core differentiator; start with FPF, IAPP, EPIC, CalPrivacy, CDT, FTC, EDPB
- [x] **Quick reference for major regulations** (CCPA/CPRA, GDPR, COPPA, HIPAA, FERPA, EU AI Act) -- Handles the most common queries without live fetching
- [x] **Professional-grade language** -- Prompt-level; trivial to implement, critical to user experience
- [x] **Source attribution with FPF-first priority** -- Defines the skill's identity and trustworthiness
- [x] **Hybrid static/live architecture** -- Architecture decision already made; v1 implements both layers

### Add After Validation (v1.x)

Features to add once core is working and user feedback confirms direction.

- [ ] **Expanded navigation guides** (remaining orgs from catalog) -- Trigger: users request specific sources not yet covered in depth
- [ ] **Regulation cross-reference** -- Trigger: users frequently ask comparison questions
- [ ] **Government regulator directory** -- Trigger: users need enforcement body information beyond what quick reference covers
- [ ] **Regulatory timeline awareness** -- Trigger: users ask "when does X take effect?" frequently
- [ ] **FPF program deep-dive** (Center for AI, Youth Privacy, working groups) -- Trigger: FPF-affiliated users want program-specific queries

### Future Consideration (v2+)

Features to defer until product-market fit is established.

- [ ] **Think tank / academic center catalog** -- Lower priority; most research queries hit the major orgs first
- [ ] **International DPA coverage** (beyond EDPB/ICO/CNIL) -- Defer until demand from users working in APAC, Latin America, or Africa jurisdictions
- [ ] **Sector-specific privacy guides** (health, fintech, edtech, adtech) -- Significant complexity; defer until vertical demand is clear
- [ ] **State-by-state U.S. privacy law navigator** -- IAPP does this well; only build if live-fetching IAPP proves insufficient

## Feature Prioritization Matrix

| Feature | User Value | Implementation Cost | Priority |
|---------|------------|---------------------|----------|
| FPF content index | HIGH | MEDIUM | P1 |
| Major privacy org catalog | HIGH | MEDIUM | P1 |
| Per-source navigation guides (top 8) | HIGH | HIGH | P1 |
| Quick reference for major regulations | HIGH | MEDIUM | P1 |
| Professional-grade language | HIGH | LOW | P1 |
| Source attribution + FPF-first | HIGH | LOW | P1 |
| Hybrid static/live architecture | HIGH | MEDIUM | P1 |
| Tiered research depth (quick vs deep) | MEDIUM | MEDIUM | P1 |
| Regulation cross-reference | MEDIUM | MEDIUM | P2 |
| Government regulator directory | MEDIUM | MEDIUM | P2 |
| FPF program awareness | MEDIUM | MEDIUM | P2 |
| Regulatory timeline awareness | MEDIUM | LOW | P2 |
| Site-specific search strategies (advanced) | MEDIUM | HIGH | P2 |
| Think tank / academic catalog | LOW | LOW | P3 |
| International DPA coverage | LOW | MEDIUM | P3 |
| Sector-specific privacy guides | MEDIUM | HIGH | P3 |

**Priority key:**
- P1: Must have for launch -- defines the skill's identity and basic utility
- P2: Should have, add when possible -- expands capability based on user feedback
- P3: Nice to have, future consideration -- only if demand emerges

## Competitor Feature Analysis

| Feature | Westlaw / LexisNexis | IAPP Resource Center | OneTrust Research | This Skill (Our Approach) |
|---------|---------------------|---------------------|-------------------|--------------------------|
| **Full legal text** | Complete statutory and case law coverage | Links to legislation, not full text | Regulatory summaries | Key provisions + links to authoritative full text. Do not try to reproduce Westlaw |
| **Legislation tracking** | 50-state surveys, regulatory trackers | US State Privacy Tracker (14 provisions), Global AI Tracker | 300+ jurisdiction coverage | Static knowledge of major laws + live-fetch IAPP/FPF for current tracking |
| **Cross-regulation comparison** | State law comparison tool (14+ topics) | Side-by-side provision charts | Automated gap analysis | Static comparison of major frameworks; point to IAPP/Bloomberg for detailed charts |
| **Policy research and analysis** | Secondary sources (treatises) | In-depth web articles, research papers | Limited; compliance-focused | FPF publications first, then IAPP/EPIC/CDT analysis. This is our strongest area |
| **Organization/source navigation** | N/A (self-contained) | N/A (self-contained) | N/A (self-contained) | Per-source navigation guides -- unique to this skill. No competitor does this |
| **Enforcement actions** | Case law database | Enforcement Database (searchable) | Enforcement tracking | Navigation guide to IAPP Enforcement DB + live fetch for recent notable actions |
| **Pricing** | $$$$ (enterprise subscription) | $$$ (membership required for most content) | $$$$ (enterprise SaaS) | Free (Claude Code skill using public sources) |
| **AI-powered research** | Westlaw CoCounsel, LexisNexis Protege AI | Limited | AI governance features | Native AI -- the entire skill is an AI-powered research assistant |
| **Speed of access** | Fast (indexed database) | Fast (web-based) | Fast (SaaS platform) | Instant for static lookups; seconds for live fetching |

## FPF-Specific Feature Depth

Because FPF is the primary source, the FPF index deserves special attention on what to cover.

### FPF Publication Types to Index
1. **Reports** (123 items) -- Flagship research outputs; most cited in policy discussions
2. **White Papers** (88 items) -- Technical and policy deep-dives
3. **Filings** (64 items) -- Regulatory comments, amicus briefs
4. **Infographics** (31 items) -- Visual guides on complex topics (COPPA, health privacy, AI)
5. **Events** (100 items) -- DC Privacy Forum, training sessions, webinars
6. **Videos** (24 items) -- Presentations, panel discussions

### FPF Issue Areas to Index (20+ topics)
**High-priority (high volume):**
- U.S. Legislation (82 resources)
- Global (65 resources)
- Artificial Intelligence (48 resources)
- Youth Privacy (42 resources)

**Medium-priority:**
- Health, Smart Communities, Mobility & Location, Research & Ethics, Immersive Technologies, De-Identification, International Data Transfers, Privacy Enhancing Technologies

**Lower-priority (specialized):**
- Open Banking, Ad Tech, Cybersecurity, Biometrics, Africa, Latin America, India

### FPF Programs to Know
- Center for Artificial Intelligence (headed by Anne J. Flanagan)
- Youth & Education Privacy program
- Privacy Papers for Policymakers (annual competition)
- FPF Training Program (member benefit)
- DC Privacy Forum (annual event)
- Working Groups (Ad and Location Practices, etc.)

## Sources

- [IAPP Tools and Trackers](https://iapp.org/resources/article/iapp-tools-and-trackers/)
- [IAPP US State Privacy Legislation Tracker](https://iapp.org/resources/article/us-state-privacy-legislation-tracker)
- [FPF Resources Page](https://fpf.org/resources/)
- [FPF Year in Review 2025](https://fpf.org/blog/fpf-year-in-review-2025/)
- [FPF Center for Artificial Intelligence](https://fpf.org/center-for-artificial-intelligence/)
- [LexisNexis Practical Guidance Data Privacy](https://www.lexisnexis.com/en-us/products/practical-guidance/data-privacy-and-security.page)
- [Georgetown Privacy Law Research Guide](https://guides.ll.georgetown.edu/privacy)
- [EPIC Publications](https://epic.org/our-work/publications/)
- [CalPrivacy (CPPA)](https://cppa.ca.gov/)
- [ISACA 2025 Survey: Privacy Professional Stress](https://www.isaca.org/about-us/newsroom/press-releases/2025/63-percent-of-privacy-professionals-find-their-jobs--more-stressful-now-than-five-years-ago)
- [OneTrust IDC MarketScape 2025](https://www.onetrust.com/news/onetrust-named-a-leader-in-idc-marketscape-2025-worldwide-data-privacy-compliance-software-report/)
- [DLA Piper Data Protection Laws of the World](https://www.dlapiperdataprotection.com/)
- [IAPP Global AI Law and Policy Tracker](https://iapp.org/resources/article/global-ai-legislation-tracker)
- [IAPP Global Privacy Directory](https://iapp.org/resources/global-privacy-directory)
- [Georgetown NGOs/Think Tanks Privacy Guide](https://guides.ll.georgetown.edu/c.php?g=468955&p=3962183)
- [18 Privacy Organizations You Should Know](https://identityreview.com/18-privacy-organizations-you-should-know/)

---
*Feature research for: Data Privacy Research Skill*
*Researched: 2026-03-12*
