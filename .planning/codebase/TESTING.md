# Testing Patterns

**Analysis Date:** 2026-03-12

## Project Status

This is a planning-stage project with no implementation code. Testing framework and patterns should be established before development begins. This document provides recommendations based on the plugin architecture design.

## Test Framework (Recommended)

**Runner:**
- **Recommendation:** `jest` or `vitest` (for TypeScript/Node.js-based MCP servers)
- Alternative: `pytest` (if Python implementation is chosen)
- Config location: `jest.config.js` or `vitest.config.ts` (TBD in project setup)

**Assertion Library:**
- Built-in Jest/Vitest assertions for core behavior
- Consider `@testing-library/jest-dom` for validation helpers

**Run Commands:**
```bash
npm test                    # Run all tests
npm run test:watch         # Watch mode for development
npm run test:coverage      # Generate coverage report
npm run test:ci            # CI/CD pipeline testing
```

## Test File Organization

**Location:**
- **Recommended pattern:** Co-located alongside source
- Structure mirrors source layout:

```
src/
  skills/
    ai-governance/
      skill.ts
      skill.test.ts         # Tests for skill definitions
      handlers.ts
      handlers.test.ts      # Tests for skill logic
    legislation/
      ...
  commands/
    brief/
      command.ts
      command.test.ts
      handlers.ts
      handlers.test.ts
  agents/
    policy-analyst/
      agent.ts
      agent.test.ts
  utilities/
    risk-assessment/
      risk-assessment.ts
      risk-assessment.test.ts
  __tests__/
    integration/            # Cross-skill tests
      ai-governance-vs-legislation.test.ts
    fixtures/               # Test data
      regulations.fixture.ts
      stakeholder-positions.fixture.ts
```

**Naming:**
- Unit tests: `[module].test.ts`
- Integration tests: `[scenario].integration.test.ts`
- Snapshot tests: `[component].snapshot.test.ts`

## Test Structure

**Suite Organization:**
```typescript
describe('Skill: AI Governance', () => {
  describe('EU AI Act Conformity Assessment', () => {
    it('should classify prohibited practices as RED risk', () => {
      // Test
    })

    it('should return assessment results with step-by-step guidance', () => {
      // Test
    })

    it('should escalate critical findings for human review', () => {
      // Test
    })
  })

  describe('Risk Severity Classification', () => {
    it('should correctly map risk factors to GREEN/YELLOW/ORANGE/RED', () => {
      // Test
    })
  })
})
```

**Patterns:**
- Setup: Arrange test data, mock external APIs
- Teardown: Reset mocks, clear test fixtures
- Assertion: Verify output shape, severity classification, escalation triggers

**Sample Test Structure:**
```typescript
describe('Command: /fpf:brief', () => {
  let mockFetcher: jest.Mock
  let commandHandler: BriefCommandHandler

  beforeEach(() => {
    mockFetcher = jest.fn()
    commandHandler = new BriefCommandHandler({
      dataFetcher: mockFetcher
    })
  })

  afterEach(() => {
    jest.clearAllMocks()
  })

  describe('Daily briefing mode', () => {
    it('should return recent FPF publications within 7 days', async () => {
      mockFetcher.mockResolvedValue([
        { publishedDate: new Date(), title: 'AI Governance Update' }
      ])

      const result = await commandHandler.execute({
        mode: 'daily',
        topic: 'AI governance'
      })

      expect(result.briefings).toHaveLength(1)
      expect(result.briefings[0].publicationDays).toBeLessThan(7)
    })

    it('should structure briefing with Background/Issues/Recommendations', async () => {
      const result = await commandHandler.execute({
        mode: 'daily',
        topic: 'privacy legislation'
      })

      expect(result).toHaveProperty('background')
      expect(result).toHaveProperty('keyIssues')
      expect(result).toHaveProperty('recommendations')
    })
  })
})
```

## Mocking

**Framework:** `jest.mock()` or `vitest.mock()`

**Patterns:**

1. **Mock external API calls:**
```typescript
jest.mock('@/utilities/api-client', () => ({
  fetchRegulations: jest.fn(),
  fetchFPFContent: jest.fn()
}))
```

2. **Mock MCP Server responses:**
```typescript
const mockMCPServer = {
  listResources: jest.fn().mockResolvedValue([
    { name: 'ai-governance', uri: 'fpf://skills/ai-governance' }
  ]),
  readResource: jest.fn().mockResolvedValue({
    contents: [{ mimeType: 'text/plain', text: 'skill definition' }]
  })
}
```

3. **Mock risk assessment utility:**
```typescript
jest.mock('@/utilities/risk-assessment', () => ({
  assessRisk: jest.fn((factors) => ({
    severity: 'YELLOW',
    score: 65,
    mitigations: []
  }))
}))
```

**What to Mock:**
- External API calls (FPF content API, regulatory data sources)
- MCP server communication
- Database queries (if applicable)
- Filesystem operations (for local fixtures)

**What NOT to Mock:**
- Risk assessment logic (test the real implementation)
- Regulatory framework comparisons (business logic)
- Data transformation utilities (should be deterministic)
- Severity classification (core business rule)

## Fixtures and Factories

**Test Data:**
```typescript
// fixtures/regulations.fixture.ts
export const createRegulation = (overrides = {}) => ({
  id: 'ccpa',
  name: 'California Consumer Privacy Act',
  jurisdiction: 'US-CA',
  enforcementDate: new Date('2023-01-01'),
  riskCategory: 'comprehensive',
  ...overrides
})

export const mockRegulations = {
  ccpa: createRegulation({ id: 'ccpa', name: 'CCPA' }),
  gdpr: createRegulation({ id: 'gdpr', name: 'GDPR', jurisdiction: 'EU' }),
  lgpd: createRegulation({ id: 'lgpd', name: 'LGPD', jurisdiction: 'BR' })
}
```

**Location:**
- Test fixtures: `src/__tests__/fixtures/`
- Factory functions for common test data objects
- Domain-specific fixtures: `src/__tests__/fixtures/regulations.fixture.ts`, `src/__tests__/fixtures/risks.fixture.ts`

## Coverage

**Requirements:**
- **Recommended:** Minimum 70% statement coverage
- Critical paths (skill activation, command execution, risk assessment): 100% coverage
- External integrations (API calls, MCP): 90%+ coverage

**View Coverage:**
```bash
npm run test:coverage
# Generates coverage report in coverage/
# View HTML report: open coverage/lcov-report/index.html
```

**Coverage reporting:**
- GitHub Actions CI should fail if coverage drops below target
- Coverage thresholds enforced per file type:
  - Skills: 85%+
  - Commands: 85%+
  - Utilities: 75%+
  - Integration: 70%+

## Test Types

### Unit Tests

**Scope:** Individual skill/command handler functions

**Approach:**
- Isolated function testing with mocked dependencies
- Test happy path and error conditions
- Verify return object structure and field values

**Example:**
```typescript
describe('Risk Assessment: Privacy Impact Assessment', () => {
  it('should calculate YELLOW severity for missing data retention policy', () => {
    const assessment = assessRisk({
      practiceDescription: 'App collects health data with no deletion timeline',
      regulation: 'HIPAA',
      jurisdiction: 'US'
    })
    expect(assessment.severity).toBe('YELLOW')
    expect(assessment.recommendations).toContain('Define data retention policy')
  })
})
```

### Integration Tests

**Scope:** Skill-to-skill interactions, command-to-utility chains

**Approach:**
- Test real skill composition (no mocking skills)
- Verify data flows between components
- Test command handlers with actual utility functions

**Location:** `src/__tests__/integration/`

**Example:**
```typescript
describe('Integration: /fpf:assess command with Risk Framework', () => {
  it('should classify AI system assessment through full pipeline', async () => {
    const command = new AssessCommand({
      riskFramework: realRiskFrameworkSkill,
      aiGovernanceSkill: realAIGovernanceSkill
    })

    const result = await command.execute({
      practiceDescription: 'ML-based hiring system using demographic data',
      focusArea: 'AI Governance'
    })

    expect(result.riskAssessment.severity).toBe('ORANGE')
    expect(result.recommendedActions).toContain('EU AI Act prohibited practice review')
  })
})
```

### E2E Tests

**Status:** Not required for Phase 1

**When applicable:** Once MCP server and external integrations are implemented

**Framework:** TBD - Consider `playwright` or `cypress` for CLI/API testing

## Common Patterns

### Async Testing

```typescript
it('should fetch and process FPF content', async () => {
  const result = await skillHandler.fetchAndProcessContent('ai-governance')
  expect(result.resourceCount).toBeGreaterThan(0)
})

// With timeout for slow operations
it('should fetch large dataset within 5 seconds', async () => {
  const result = await skillHandler.fetchLargeDataset()
  expect(result).toBeDefined()
}, 5000) // Jest timeout in ms
```

### Error Testing

```typescript
describe('Error Handling', () => {
  it('should return RED severity when regulation data is missing', async () => {
    mockFetcher.mockRejectedValue(new Error('API unavailable'))

    const result = await skillHandler.assessCompliance('CCPA')

    expect(result.error.severity).toBe('HIGH')
    expect(result.error.code).toBe('REGULATION_DATA_UNAVAILABLE')
    expect(result.escalateToHuman).toBe(true)
  })

  it('should gracefully handle malformed regulatory data', async () => {
    mockFetcher.mockResolvedValue({ malformed: 'data' })

    expect(() => parseRegulation(mockFetcher.result))
      .toThrow('Invalid regulation format')
  })
})
```

### Snapshot Testing

Use for comparing assessment outputs when format changes are intentional:

```typescript
it('should generate briefing with consistent structure', () => {
  const briefing = commandHandler.generateBriefing('daily', 'privacy legislation')
  expect(briefing).toMatchSnapshot()
})
```

Update snapshots with caution - review all changes:
```bash
npm test -- -u
```

## Test Naming Convention

Follow: `should [expected behavior] when [condition]`

**Examples:**
```typescript
should return GREEN risk when all GDPR requirements met
should return YELLOW severity when data retention policy missing
should throw ValidationError when regulation code invalid
should activate AI Governance skill when topic mentions "EU AI Act"
should escalate to human review when risk score exceeds threshold
should retry API call three times before failing
```

---

*Testing analysis: 2026-03-12*

Note: This is a pre-implementation analysis. Testing framework and coverage targets should be finalized in DECISIONS.md before development begins. Recommended approach:
1. Start with Jest/Vitest + co-located test files
2. Establish coverage thresholds per component type
3. Create fixture library for regulatory data
4. Build integration test suite for command pipelines
