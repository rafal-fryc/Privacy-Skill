# Codebase Structure

**Analysis Date:** 2026-03-12

## Directory Layout

This project is a plugin system for Anthropic's Claude Cowork platform. The structure is template-driven, with markdown and JSON files defining skills, commands, and agents.

## Directory Purposes

**.claude-plugin/:**
- Plugin manifest and metadata for Cowork registry
- Key file: plugin.json with name, version, author, permissions

**.claude/:**
- Claude-specific configuration
- settings.local.json: Local development permissions

**skills/:**
- 18 skill definitions (auto-invoked contextual knowledge)
- Organized into: methodology/, catalog/, risk-assessment/, domains/
- Each domain gets one skill file (kebab-case.md)

**commands/:**
- 6 user-invoked slash command workflows
- Files: brief.md, landscape.md, compare.md, assess.md, checklist.md, stakeholder-map.md

**agents/:**
- 3 specialized sub-agents for complex workflows
- Types: privacy-policy-analyst, research-synthesis, ai-governance-advisor

**connectors/:**
- External service integrations (MCP servers)
- member-portal-mcp/ subdirectory for Phase 3

**data/:**
- Static metadata: regulations-registry.json, fpf-resources-index.json, severity-classifications.json

**docs/:**
- Project planning and architecture diagrams

**.planning/codebase/:**
- GSD codebase analysis documents (not part of plugin distribution)

## Key File Locations

**Entry Points:**
- .claude-plugin/plugin.json: Plugin manifest
- skills/methodology/privacy-research-methodology.md: Core methodology skill
- skills/catalog/fpf-source-catalog.md: Resource index

**Configuration:**
- .claude/settings.local.json: Permissions
- data/regulations-registry.json: Regulation catalog

**Core Logic:**
- skills/domains/*.md: 15 domain-specific skills
- commands/*.md: 6 command workflows
- agents/*.md: 3 agent definitions

## Naming Conventions

**Skills:** {domain-name}.md (kebab-case)
**Commands:** {command-name}.md (matches /fpf:{name})
**Agents:** {agent-purpose}.md (kebab-case)
**Data:** {entity-type}-{sub-type}.json
**Directories:** Plural nouns, kebab-case subdirectories

## Where to Add New Code

**New Skill:**
1. Create: skills/domains/{skill-name}.md
2. Update: .claude-plugin/plugin.json to register
3. Update: data/fpf-resources-index.json with resources

**New Command:**
1. Create: commands/{command-name}.md
2. Update: .claude-plugin/plugin.json to register
3. Link: Associate with agent(s)

**New Agent:**
1. Create: agents/{agent-purpose}.md
2. Update: .claude-plugin/plugin.json to register
3. Create: Commands that invoke this agent

**Member-Only Feature (Phase 3):**
1. Create: connectors/member-portal-mcp/{feature-name}.js
2. Register: In .mcp.json with authentication
3. Update: .claude-plugin/plugin.json with permissions

## Phase Organization

**Phase 1 (MVP):**
- 18 skills (3 cross-cutting + 15 domain)
- 2 commands (/fpf:brief, /fpf:landscape)

**Phase 2:**
- 4 additional commands
- 3 agents (PrivacyPolicyAnalyst, ResearchSynthesis, AIGovernanceAdvisor)

**Phase 3 (Members-Only):**
- MCP server for member portal
- 3 member-only commands
- 2 additional skills
- 1 additional agent (ComplianceAdvisor)

---

*Structure analysis: 2026-03-12*
