# Project Retrospective

*A living document updated after each milestone. Lessons feed forward into future planning.*

## Milestone: v1.0 — FPF Privacy Research Skill

**Shipped:** 2026-03-13
**Phases:** 4 | **Plans:** 12 | **Commits:** 63

### What Was Built
- Complete `/privacy` Claude Code skill with 22 markdown files (3,882 lines)
- FPF-prioritized routing with 319-line reference file covering publications, programs, and issue areas
- 6 regulation quick-reference files with cross-reference comparison and regulatory timeline
- Organization ecosystem: 9 advocacy orgs, 13 government regulators, 8 academic centers
- 7 site-specific navigation guides with WebFetch-tested URLs
- Live research pipeline with multi-source synthesis and three-tier graceful degradation
- 6-step routing SKILL.md orchestrating all components

### What Worked
- Progressive file loading architecture kept SKILL.md lean (304/500 lines) while supporting 22 reference files
- Phase 3 navigation guides (with WebFetch compatibility notes) directly enabled Phase 4's live research pipeline — good dependency planning
- Additive routing steps (FPF → Regulation → Organization → Live Research) each independent — no complex coupling
- Plan execution velocity was fast: 12 plans in ~39 minutes total execution time
- The discuss-phase workflow captured good design decisions that prevented rework (especially "every query attempts live fetch" simplification)

### What Was Inefficient
- Summary one-liners were not consistently populated by executors, making milestone accomplishment extraction manual
- Some executor agents found work already partially done by prior sessions, causing verification-only runs
- WebFetch compatibility testing happened during research but could have been done earlier as a spike

### Patterns Established
- Three-tier anti-hallucination (strict/high/standard) for different content confidence levels
- Nav guide template: 8-section structure (Overview, URL Patterns, Content Organization, Key Sections, Search Tips, WebFetch Notes, Quick Reference, Limitations)
- Practitioner blockquote notes pattern for editorial guidance within reference files
- Intent-detection routing over keyword matching for query classification

### Key Lessons
1. Navigation guides are the key infrastructure for live research — investing in them during Phase 3 made Phase 4 straightforward
2. "Always attempt live fetch" is simpler than mode-switching and works better in practice — static knowledge as foundation means live failures are graceful, not catastrophic
3. For markdown-only skills, all validation is manual — accept this constraint early rather than fighting it
4. WebFetch uses Haiku 3.5 for content processing — prompts sent to WebFetch need to be specific and focused

### Cost Observations
- Model mix: Primarily opus (orchestrator + executor), sonnet (plan checker + verifier)
- Sessions: ~6 sessions across 2 days
- Notable: Plans averaged 3.25 minutes execution — markdown file creation is fast; the bottleneck is research and planning, not execution

---

## Cross-Milestone Trends

### Process Evolution

| Milestone | Commits | Phases | Key Change |
|-----------|---------|--------|------------|
| v1.0 | 63 | 4 | Initial milestone — established progressive loading architecture |

### Cumulative Quality

| Milestone | Skill Files | Total LOC | Routing Steps |
|-----------|-------------|-----------|---------------|
| v1.0 | 22 | 3,882 | 6 |

### Top Lessons (Verified Across Milestones)

1. Navigation guides as infrastructure for live research — invest upfront, reap downstream
2. Additive independent routing steps scale better than monolithic query classification
