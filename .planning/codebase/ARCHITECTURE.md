# Architecture

**Analysis Date:** 2026-03-12

## Pattern Overview

**Overall:** Modular Plugin Architecture (Anthropic Claude Cowork Plugin Pattern)

**Key Characteristics:**
- Layered skill-based context injection (auto-activated domain knowledge)
- Command-driven user workflows (slash commands for explicit user actions)
- Specialized agent sub-systems for complex reasoning tasks
- MCP (Model Context Protocol) server integration for external data access (members-only tier)
- Two-tier deployment (public and members-only)
- Methodology-first approach (FPF frameworks encoded in skills)

---

## Layers

**Skills Layer:**
- Purpose: Auto-invoked contextual knowledge that Claude uses automatically when a topic is mentioned. Encodes domain expertise, regulatory frameworks, FPF methodology, and curated resource catalogs.
- Location: `.claude/fpf.skills/` (proposed)
- Contains: 18 skill definitions (3 cross-cutting + 15 domain-specific)
- Depends on: FPF content universe, curated resource catalog
- Used by: Claude foundation model (auto-activated), commands, agents

**Commands Layer:**
- Purpose: Explicit user-invoked workflows that guide Claude through structured analysis processes. Maps user intent to multi-step reasoning patterns.
- Location: `.claude/fpf.commands/` (proposed)
- Contains: Slash command handlers (`/fpf:brief`, `/fpf:landscape`, `/fpf:assess`, `/fpf:checklist`, `/fpf:compare`, `/fpf:stakeholder-map`)
- Depends on: Skills layer for context, agent layer for complex workflows
- Used by: End users and applications

**Agents Layer:**
- Purpose: Specialized sub-agents that encapsulate multi-step analytical workflows for complex tasks (policy research, privacy assessments, compliance analysis).
- Location: `.claude/fpf.agents/` (proposed)
- Contains:
  - `PrivacyPolicyAnalyst` — Reviews policies and ToS against FPF best practices
  - `ResearchSynthesis` — Structured multi-step privacy research following FPF methodology
  - `AIGovernanceAdvisor` — EU AI Act and U.S. AI law assessment specialist
  - `ComplianceAdvisor` — (Members-only) PIA and compliance roadmap generation
- Depends on: Skills layer (domain knowledge), commands (workflow structure)
- Used by: Commands and direct user requests

**Connectors Layer (Members-Only):**
- Purpose: External service integrations that provide Claude access to FPF member portal and exclusive content.
- Location: `.claude/fpf.connectors/` (proposed)
- Contains: MCP server configuration, member portal API client
- Depends on: Member portal APIs (requires feasibility assessment)
- Used by: Members-only skills and commands

**Configuration Layer:**
- Purpose: Plugin metadata, version management, and plugin.json manifest.
- Location: `.claude-plugin/plugin.json`, `.mcp.json`, `.claude/settings.local.json`
- Contains: Plugin name, version, description, author, permission declarations
- Depends on: None (foundational)
- Used by: Claude Cowork plugin registry and runtime

---

## Data Flow

**Public Plugin — User Question to Answer:**

1. User asks Claude a question about privacy/policy (e.g., "What are CCPA requirements?")
2. Claude's background processing auto-activates relevant skills:
   - Privacy Research Methodology (cross-cutting)
   - FPF Source Catalog (cross-cutting)
   - Risk Assessment Framework (cross-cutting)
   - U.S. Privacy Legislation skill (domain-specific)
3. Skill context primes Claude with:
   - FPF's analytical framework and methodology
   - Curated index of 407+ FPF resources
   - Applicable regulations and enforcement dates
   - Severity classification matrix
4. Claude generates answer using injected context
5. Answer references FPF publications and frameworks

**Public Plugin — Explicit Command Flow (e.g., `/fpf:brief`):**

1. User invokes `/fpf:brief [topic]` command
2. Command handler extracts topic parameter
3. Command invokes appropriate agent based on topic:
   - Policy briefing → Research Synthesis agent
   - AI topic → AI Governance Advisor agent
   - General → Privacy Policy Analyst agent
4. Agent receives:
   - User input (topic, mode: Daily/Topic/Incident)
   - Auto-activated skill context
   - Step-by-step methodology from agent template
5. Agent executes structured workflow:
   - Background research (using FPF catalog skill)
   - Stakeholder position analysis
   - Risk assessment (using Risk Assessment Framework skill)
   - Recommendation generation
6. Command handler formats output and returns to user

**Members-Only Plugin — Member Portal Access:**

1. User invokes member-only command (e.g., `/fpf-members:search [query]`)
2. Member authentication validated via `.claude-plugin/plugin.json` permissions
3. MCP server processes request:
   - Encodes query
   - Calls member portal API
   - Returns structured results
4. Member Resource Navigator skill provides context about portal structure
5. Claude generates response with exclusive content

**State Management:**
- Skills are stateless — they inject context at runtime; Claude's context window manages conversation history
- Commands are stateless — each invocation is independent
- Agents are stateless — multi-step reasoning is managed within a single Claude context window
- MCP server maintains connection state for member portal access

---

## Key Abstractions

**Skill:**
- Purpose: A bundle of encoded domain knowledge, methodology, and resource catalogs that auto-activates when relevant.
- Examples:
  - `SkillUsingPrivacyLegislation` (`src/.claude/fpf.skills/us-privacy-legislation.md`)
  - `SkillAIGovernance` (`src/.claude/fpf.skills/ai-governance.md`)
  - `SkillFPFSourceCatalog` (`src/.claude/fpf.skills/fpf-source-catalog.md`)
- Pattern: Markdown file containing:
  - Topic definition and scope
  - Key regulatory landscape
  - FPF methodology and frameworks
  - Curated resource index (with links)
  - Severity/risk classification guidance
  - Escalation triggers
  - Related skills and cross-references

**Command:**
- Purpose: User-invoked workflow that structures a multi-step Claude analysis process.
- Examples:
  - `/fpf:brief` — Policy briefing generation
  - `/fpf:assess` — Privacy impact assessment
  - `/fpf:landscape` — Regulatory landscape overview
- Pattern: Markdown/JSON file containing:
  - Command signature and parameters
  - Workflow steps (numbered, multi-turn reasoning)
  - Input schema (what user provides)
  - Output schema (what Claude returns)
  - Associated agent or skill references
  - Example invocations

**Agent:**
- Purpose: Specialized sub-system that encapsulates a multi-step analytical workflow for a specific domain.
- Examples:
  - `PrivacyPolicyAnalyst` — Green/Yellow/Red classification of policy risks
  - `AIGovernanceAdvisor` — EU AI Act conformity assessment
  - `ResearchSynthesis` — Multi-stakeholder privacy research
- Pattern: Definition containing:
  - System prompt (role, methodology, constraints)
  - Step-by-step workflow template
  - Input/output schemas
  - Related skills required
  - Escalation criteria and warnings

**MCP Server:**
- Purpose: Gateway for Claude to access external services (member portal, FPF APIs).
- Examples:
  - `member-portal-mcp` — Member portal data gateway
- Pattern: Configuration + implementation containing:
  - Authentication mechanism (API key, session token)
  - Resource definitions (tools, prompts)
  - Error handling and rate limits
  - Response transformation to Claude-readable format

---

## Entry Points

**Claude UI Entry Point:**
- Location: Anthropic Claude Cowork web interface
- Triggers: User asks question or invokes slash command
- Responsibilities:
  - Accept user input (natural language question or slash command)
  - Route to appropriate skill(s) based on content
  - Route slash commands to command handler
  - Return Claude's response to user

**Plugin Installation Entry Point:**
- Location: `.claude-plugin/plugin.json`
- Triggers: User downloads and installs plugin in Cowork
- Responsibilities:
  - Declare plugin metadata (name, version, author)
  - Register all skills, commands, agents available in plugin
  - Declare required permissions (web fetch, member portal access, etc.)
  - Define plugin icon and description

**API Entry Point (Members-Only):**
- Location: MCP server in `.claude/fpf.connectors/member-portal-mcp/`
- Triggers: User invokes `/fpf-members:*` command
- Responsibilities:
  - Authenticate user against member portal
  - Translate command parameters to API calls
  - Handle member portal API responses
  - Return data to Claude in structured format

---

## Error Handling

**Strategy:** Graceful degradation with escalation guidance.

**Patterns:**

**Regulation Not Found:**
- Skill detects unknown regulation/law
- Returns: "This regulation is not covered in FPF's current scope. Consider consulting..."
- Suggests: Alternative regulations, external resources, escalation to FPF experts
- No failure — provides next steps instead

**Skill Context Insufficient:**
- Agent detects question outside its domain
- Returns: Risk assessment with HIGH severity, recommends human expert review
- Suggests: Which FPF expert community is relevant
- For members: Provides MCP server call to member portal expert directory

**MCP Server Failure (Members-Only):**
- Authentication fails: Returns "Member portal access denied. Verify your account."
- API timeout: Returns partial results from cache if available, notes data may be stale
- Connection error: Falls back to public plugin knowledge, notes "member content unavailable"
- Never blocks user — provides context about failure and next steps

**Validation Error (Command Parameters):**
- User invokes command with invalid parameters (e.g., `/fpf:compare ccpa unknown-law`)
- Command handler validates against known regulations list
- Returns: "Regulation 'unknown-law' not recognized. Valid options: GDPR, CCPA, LGPD, ..."
- Suggests: Closest match (fuzzy matching on regulation name)

**Severity Classification Conflict:**
- Agent assigns risk/severity level, user disputes it
- Agent includes reasoning chain in output
- User can ask "why was this marked ORANGE?" — Claude re-explains classification
- For critical disagreements: Escalates to FPF compliance expert recommendation

---

## Cross-Cutting Concerns

**Logging:**
- Plugin invocations logged to `.claude-plugin/logs/` (proposed)
- Commands logged with: timestamp, command name, parameters, execution time, user_id (if available)
- Error cases logged with: error type, context, recovery action
- Members-only command invocations logged separately for audit

**Validation:**
- All user inputs validated at command handler layer
- Regulation/law names validated against curated registry before skill activation
- MCP server validates authentication tokens on every request
- Agent outputs validated against schema before returning to user

**Authentication (Members-Only):**
- OAuth 2.0 or API key authentication (requires member portal assessment)
- Tokens cached in Claude Cowork session (not persisted to disk)
- Commands check user role before allowing member-only operations
- Graceful fallback to public plugin if auth fails

**Authorization (Members-Only):**
- Members-only skills and commands not available to non-members
- MCP server checks membership status before returning portal content
- Commands decorated with membership requirement (e.g., `@requires_member`)
- UI hides member-only commands from non-members

---

*Architecture analysis: 2026-03-12*
