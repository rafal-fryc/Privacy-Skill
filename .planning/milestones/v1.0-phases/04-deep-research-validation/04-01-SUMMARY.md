---
phase: 04-deep-research-validation
plan: 01
subsystem: skill-behaviors
tags: [webfetch, live-research, degradation, source-selection, url-construction]

# Dependency graph
requires:
  - phase: 03-org-catalog-gov-sources
    provides: "7 navigation guides with URL patterns and WebFetch compatibility notes"
  - phase: 01-skill-foundation
    provides: "skill-behaviors.md behavioral instruction pattern"
provides:
  - "research-behaviors.md: live WebFetch research workflow instructions"
  - "WebFetch source compatibility matrix (5 accessible, 3 blocked)"
  - "Source selection logic with FPF-first priority and 3-4 cap"
  - "URL construction patterns from nav guide site maps"
  - "Three-tier degradation handling (partial, total, timeout)"
affects: [04-02, validation, SKILL.md-routing]

# Tech tracking
tech-stack:
  added: []
  patterns: ["Behavioral instruction file for research workflow", "WebFetch compatibility matrix", "Three-tier degradation communication"]

key-files:
  created: [".claude/skills/privacy/research-behaviors.md"]
  modified: []

key-decisions:
  - "FPF blog two-step approach: scan index then fetch specific post (counts within source cap)"
  - "Sequential WebFetch execution (simplest approach, revisit if latency is an issue)"
  - "400-800 word ceiling for multi-source synthesis (not a floor)"

patterns-established:
  - "Research behavioral instruction file: teaches HOW to research, parallel to skill-behaviors.md which teaches HOW to format"
  - "Source compatibility matrix embedded in instruction file for fast lookup"
  - "Degradation notes placed before topic heading, not at bottom"

requirements-completed: [ARCH-04, ARCH-05, DEPTH-02]

# Metrics
duration: 2min
completed: 2026-03-13
---

# Phase 4 Plan 01: Research Behaviors Summary

**Live WebFetch research workflow with source selection, URL construction from nav guides, theme-based synthesis, and three-tier degradation handling**

## Performance

- **Duration:** 2 min
- **Started:** 2026-03-13T22:51:26Z
- **Completed:** 2026-03-13T22:53:18Z
- **Tasks:** 1
- **Files modified:** 1

## Accomplishments
- Created research-behaviors.md (161 lines) as a complete behavioral instruction file for live web research
- Embedded verified WebFetch compatibility matrix covering all 8 sources (5 accessible, 3 blocked)
- Encoded all locked decisions from CONTEXT.md: every-query live fetch, FPF-first priority, 3-4 source cap, theme-based synthesis, inline citations only, three-tier degradation, contradiction handling with dates

## Task Commits

Each task was committed atomically:

1. **Task 1: Create research-behaviors.md behavioral instruction file** - `b9635c5` (feat)

## Files Created/Modified
- `.claude/skills/privacy/research-behaviors.md` - Live research behavioral instructions covering source selection, URL construction, WebFetch execution, content integration, and degradation handling (7 sections, 161 lines)

## Decisions Made
- FPF blog two-step approach: fetch blog index first to scan titles, then fetch specific relevant post URL. Both fetches count within the 3-4 source cap since they target the same organization.
- Sequential WebFetch execution assumed (simplest approach). Can be revisited if response latency becomes an issue.
- 400-800 words treated as ceiling not floor for multi-source synthesis. Shorter responses appropriate when live content merely confirms static knowledge.

## Deviations from Plan

None - plan executed exactly as written.

## Issues Encountered

None.

## User Setup Required

None - no external service configuration required.

## Next Phase Readiness
- research-behaviors.md is ready to be loaded by SKILL.md routing
- Plan 04-02 should add a new routing step in SKILL.md to load research-behaviors.md and trigger live fetching on every query
- File is 161 lines, well within the context budget for every-query loading

## Self-Check: PASSED

- [x] `.claude/skills/privacy/research-behaviors.md` exists (161 lines)
- [x] Commit `b9635c5` exists in git history
- [x] File contains all 7 sections (Purpose, Compatibility, Source Selection, URL Construction, WebFetch Execution, Content Integration, Degradation Handling)
- [x] Compatibility matrix includes all 8 sources with correct ACCESSIBLE/BLOCKED status

---
*Phase: 04-deep-research-validation*
*Completed: 2026-03-13*
