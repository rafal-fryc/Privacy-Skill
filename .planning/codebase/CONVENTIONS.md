# Coding Conventions

**Analysis Date:** 2026-03-12

## Project Status

This is a planning-stage project with architecture and design documents but no implementation code present. The following conventions should be established before development begins.

## Recommended Conventions (Pre-Implementation)

### Naming Patterns

**Files:**
- Skill definitions: `skill-[skill-name].json` (e.g., `skill-ai-governance.json`)
- Commands: `command-[command-name].json` (e.g., `command-brief.json`)
- Agents: `agent-[agent-name].json` (e.g., `agent-policy-analyst.json`)
- Configuration: PascalCase for class/interface names, camelCase for properties
- Asset directories: lowercase, hyphen-separated (e.g., `ai-governance/`, `data-protection/`)

**Functions/Methods:**
- camelCase for function names and methods
- Verb-first naming: `fetchResources()`, `assessRisk()`, `generateBriefing()`
- Private/internal methods: prefix with underscore `_processContent()`

**Variables:**
- camelCase for constants and variables
- Descriptive names reflecting domain: `riskSeverityMatrix`, `regulationTimeline`, `stakeholderPositions`
- Boolean variables: prefix with `is` or `has` (e.g., `isCompliant`, `hasContent`)

**Types/Interfaces:**
- PascalCase for type/interface names: `PrivacyRisk`, `RegulationFramework`, `StakeholderMap`
- Enums for severity ratings: `RiskSeverity` with values `GREEN`, `YELLOW`, `ORANGE`, `RED`

### Code Style

**Formatting:**
- JSON: 2-space indentation for manifest files (`.claude-plugin/plugin.json`, `.mcp.json`)
- YAML: 2-space indentation for configuration files
- Markdown: consistent heading hierarchy, code fences with language specifiers

**Linting/Validation:**
- JSON Schema validation for all manifest files
- Markdown linting for skill/command documentation (consistent heading structure)
- No tool yet specified - should be determined at project start and documented in DECISIONS.md

**Plugin Manifest Structure:**
```json
{
  "name": "fpf-[tier]",
  "version": "0.1.0",
  "description": "...",
  "author": "FPF",
  "commands": [],
  "skills": [],
  "agents": []
}
```

### Import Organization

**Order:**
1. Plugin manifest imports
2. Skill/command definitions
3. Data utilities
4. External integrations (API clients, MCP servers)
5. Local utilities and helpers

**Path Aliases:**
- TBD - should be established in `DECISIONS.md` once framework is chosen
- Recommend: `@skills/`, `@commands/`, `@data/`, `@utils/`

### Error Handling

**Patterns:**
- Return structured error objects with `code`, `message`, `details` fields
- Severity-based error classification matching risk framework: `HIGH`, `MEDIUM`, `LOW`
- Errors from external sources (API, MCP) wrapped with context
- No swallowing exceptions - all errors explicitly handled or propagated

**Example pattern:**
```json
{
  "code": "REGULATION_FETCH_FAILED",
  "message": "Failed to fetch regulation data",
  "details": {
    "regulation": "CCPA",
    "source": "error from API",
    "severity": "HIGH"
  }
}
```

### Logging

**Framework:** TBD - should support JSON logging for structured data

**Patterns:**
- Log at entry point of each command/skill activation
- Log fetch operations and external API calls
- Log assessment/comparison operations with risk severity
- Do NOT log user queries containing sensitive information
- Structured logging: timestamp, level (info/warn/error), context, message

**Levels:**
- `info`: Skill activation, command execution start
- `warn`: API call failures (recovered), slow operations
- `error`: Command failures, data validation failures

### Comments

**When to Comment:**
- Complex risk assessment logic
- Non-obvious regulatory interpretations
- Integration with external data sources
- Workarounds for known issues

**JSDoc/Doc Format:**
```json
{
  "skill": "ai-governance",
  "description": "EU AI Act conformity assessment and U.S. AI legislation tracking",
  "activationTriggers": ["AI governance", "EU AI Act", "AI regulation"],
  "encodedContent": {
    "primaryRegulations": ["EU AI Act", "US AI Executive Order"],
    "methodologySteps": ["Prohibited practices assessment", "Risk categorization", "Conformity roadmap"]
  }
}
```

### Function Design

**Size:**
- Skill/command handlers should be decomposable into smaller utilities
- Each regulatory assessment should have its own function

**Parameters:**
- Command handlers: accept structured input object with required/optional fields
- Skill functions: pure data transformation functions where possible

**Return Values:**
- Structured responses with `success`, `data`, `error` fields
- Consistent shape across all commands/skills
- Clear error propagation

### Module Design

**Exports:**
- Each skill/command/agent is independently importable
- Barrel files for skill groups: `ai/index.json` exports all AI-related skills

**Barrel Files:**
```
skills/
  ai/
    index.json        # exports all AI governance skills
  legislation/
    index.json        # exports all legislation skills
```

## Domain Conventions (Privacy/Policy-Specific)

### Risk Severity Naming

Consistent across all assessments:
- `GREEN`: Low risk, compliant, best practice
- `YELLOW`: Medium risk, requires attention/mitigation
- `ORANGE`: High risk, significant gaps, urgent action needed
- `RED`: Critical risk, non-compliant, escalate immediately

### Regulatory Timeline Format

```json
{
  "regulation": "CCPA",
  "enforcementDate": "2023-01-01",
  "curePeriod": "30 days",
  "optOutDeadline": "2024-01-15",
  "notes": "Enhanced enforcement via AG cooperation"
}
```

### Stakeholder Position Mapping

```json
{
  "issue": "AI governance in EU",
  "stakeholders": {
    "industry": "...",
    "regulator": "...",
    "civilSociety": "...",
    "academic": "..."
  }
}
```

---

*Convention analysis: 2026-03-12*

Note: This is a pre-implementation analysis. Once development begins, these conventions should be formalized in the project's `.claude/` local rules and version controlled.
