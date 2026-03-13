# Technology Stack

**Analysis Date:** 2026-03-12

## Project Overview

This is an **FPF (Future of Privacy Forum) Plugin for Anthropic's Claude Cowork** — a bundle of skills, commands, and agents designed to provide contextualized privacy research and policy analysis. Currently in planning/architecture phase with no production code yet.

## Languages

**Markdown:**
- `.md` files - Skills, commands, and documentation
- Format: YAML frontmatter + markdown content for Cowork plugin definitions

**JSON:**
- `plugin.json` - Plugin metadata (name, version, description, author)
- `.mcp.json` - MCP server configurations (if members-only plugin implemented)

**No runtime language yet** — Plugin will be platform-agnostic YAML/Markdown definitions and structured data. Execution happens within Claude Cowork environment.

## Platform

**Target Platform:**
- Anthropic Claude Cowork (AI Agent Platform)

**Access:**
- Public variant: Available to users with Anthropic accounts
- Members-only variant: FPF member portal access required (Phase 3)

## Frameworks & Architecture

**Claude Cowork Plugin Components:**

1. **Skills** (18 total, auto-invoked context)
   - 3 cross-cutting skills (methodology, source catalog, risk assessment)
   - 15 domain-specific skills (organized by FPF focus areas)
   - Format: Markdown with YAML metadata

2. **Commands** (6 total, user-invoked slash commands)
   - `/fpf:brief [topic]` - Policy briefings (Phase 1)
   - `/fpf:landscape [topic]` - Regulatory landscape (Phase 1)
   - `/fpf:compare [law1] vs [law2]` - Legislation comparison (Phase 2)
   - `/fpf:assess [description]` - Privacy impact assessment (Phase 2)
   - `/fpf:checklist [regulation]` - Compliance checklists (Phase 2)
   - `/fpf:stakeholder-map [issue]` - Stakeholder mapping (Phase 2)

3. **Agents** (3 total, specialized sub-agents)
   - Privacy Policy Analyst (Phase 2)
   - Research Synthesis (Phase 2)
   - AI Governance Advisor (Phase 2)

4. **MCP Servers** (Phase 3, members-only)
   - Member Portal MCP Server - Gateway for accessing member-exclusive resources

## Key Dependencies & Reference Materials

**Content Sources (No Runtime Dependency):**
- FPF's 407+ public resources (reports, white papers, filings, infographics)
- 20+ issue area frameworks
- Specialized tools: Key Dates Tracker, Data Sharing for Research Tracker, Mobility Data Sharing Assessment Tool, PETs Repository, Student Privacy Compass

**Reference Plugin:**
- Anthropic's `legal` plugin architecture (5 MCP servers, 5 commands, 6 skills)
- Design patterns: Severity classification (GREEN/YELLOW/RED), tool-agnostic connectors, methodology-first skills

**Member Resources (Phase 3 Integration):**
- FPF Member Portal API (to be determined during Phase 3 feasibility study)
- 8+ expert communities
- Privacy Executives Network (PEN) — 230+ senior leaders
- Training materials and staff briefings

## Configuration

**Plugin Package Structure:**
```
fpf-plugin/
├── .claude-plugin/
│   └── plugin.json          # Plugin metadata
├── .mcp.json                # MCP server configurations (Phase 3)
├── skills/                  # 18 skill definitions
│   ├── methodology/
│   │   └── privacy-research-methodology.md
│   ├── catalog/
│   │   └── fpf-source-catalog.md
│   ├── risk-assessment/
│   │   └── risk-assessment-framework.md
│   ├── domains/
│   │   ├── ai-governance.md
│   │   ├── ai-legislation.md
│   │   ├── us-privacy-legislation.md
│   │   ├── global-data-protection.md
│   │   ├── youth-education-privacy.md
│   │   ├── health-data-privacy.md
│   │   ├── ad-tech.md
│   │   ├── biometrics.md
│   │   ├── privacy-enhancing-tech.md
│   │   ├── immersive-tech.md
│   │   ├── mobility-location.md
│   │   ├── smart-communities.md
│   │   ├── cybersecurity.md
│   │   ├── open-banking.md
│   │   └── research-ethics.md
├── commands/                # 6 command definitions
│   ├── brief.md
│   ├── landscape.md
│   ├── compare.md
│   ├── assess.md
│   ├── checklist.md
│   └── stakeholder-map.md
├── agents/                  # 3 agent definitions
│   ├── privacy-policy-analyst.md
│   ├── research-synthesis.md
│   └── ai-governance-advisor.md
└── CONNECTORS.md            # Tool-agnostic connector placeholders
```

**Environment Configuration:**
- No environment variables required for Phase 1 (public plugin)
- Phase 3 requires member portal credentials (to be determined)

## Build & Deployment

**Package Management:**
- Plugin packaged as `.zip` or `.tar.gz` distribution
- Versioned using semantic versioning (e.g., v1.0.0)
- Distributed via FPF website or Anthropic's Claude Cowork plugin marketplace

**Deployment Target:**
- Anthropic Claude Cowork platform
- Potential future compatibility: Other LLM platforms (GPT, etc.) following similar plugin standards

## Development Requirements

**Content Authoring:**
- Markdown editor
- Understanding of FPF's 407+ existing resources
- Validation against FPF's established methodologies (from `FPF Plugin Proposal.md`)

**Validation Process (Not Yet Automated):**
- FPF staff review of analytical frameworks encoded in skills (open question in proposal)
- Legal review for compliance disclaimers (open question)
- Portal feasibility study for Phase 3 MCP integration

## Phase Timeline

| Phase | Deliverables | Status |
|-------|-------------|--------|
| Phase 1 | 18 skills + 2 commands (brief, landscape) | Planned |
| Phase 2 | 4 additional commands + 3 agents | Planned |
| Phase 3 | Members-only plugin + MCP server gateway | Pending portal feasibility study |

## Open Technical Questions

1. **Member Portal API** — What authentication/API methods does FPF member portal expose?
2. **Content Update Strategy** — How should skill knowledge base be refreshed as FPF publishes ~50+ new resources annually?
3. **Content Encoding Format** — Exact YAML/Markdown structure for storing domain knowledge in skills
4. **Dynamic Content Fetching** — Should skills embed static knowledge or dynamically fetch latest FPF content?

---

*Stack analysis: 2026-03-12*
