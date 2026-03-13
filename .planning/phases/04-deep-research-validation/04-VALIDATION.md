---
phase: 04
slug: deep-research-validation
status: draft
nyquist_compliant: false
wave_0_complete: false
created: 2026-03-13
---

# Phase 04 — Validation Strategy

> Per-phase validation contract for feedback sampling during execution.

---

## Test Infrastructure

| Property | Value |
|----------|-------|
| **Framework** | Manual end-to-end testing via `/privacy` command invocation |
| **Config file** | None — skill is markdown-based, no automated test runner |
| **Quick run command** | `/privacy [test query]` in Claude Code session |
| **Full suite command** | Run all validation queries listed below sequentially |
| **Estimated runtime** | ~5 minutes (manual interactive testing) |

---

## Sampling Rate

- **After every task commit:** Run 2-3 representative `/privacy` test queries
- **After every plan wave:** Run full validation suite (all 6 test queries)
- **Before `/gsd:verify-work`:** Full suite must produce correct behavior
- **Max feedback latency:** ~30 seconds per query

---

## Per-Task Verification Map

| Task ID | Plan | Wave | Requirement | Test Type | Validation Command | File Exists | Status |
|---------|------|------|-------------|-----------|-------------------|-------------|--------|
| 04-01-01 | 01 | 1 | ARCH-04 | manual e2e | `/privacy What is the current state of children's privacy law?` — verify live-fetched content alongside static COPPA/FERPA knowledge | ❌ W0 | ⬜ pending |
| 04-01-02 | 01 | 1 | ARCH-04 | manual e2e | `/privacy What has FPF published about AI governance recently?` — verify response cites specific recent FPF blog posts with dates | ❌ W0 | ⬜ pending |
| 04-01-03 | 01 | 1 | ARCH-05 | manual e2e | Verify degradation header appears when specific sources are unavailable (FTC, EPIC, CDT queries naturally trigger this) | ❌ W0 | ⬜ pending |
| 04-01-04 | 01 | 1 | ARCH-05 | manual e2e | Test in offline/restricted mode — verify response uses static knowledge with total failure note | ❌ W0 | ⬜ pending |
| 04-01-05 | 01 | 1 | DEPTH-02 | manual e2e | `/privacy Current state of AI regulation globally` — verify response weaves 3+ sources in theme-based structure | ❌ W0 | ⬜ pending |
| 04-01-06 | 01 | 1 | DEPTH-02 | manual e2e | Verify different query topics select different source combinations (regulation vs. org vs. cross-cutting) | ❌ W0 | ⬜ pending |

*Status: ⬜ pending · ✅ green · ❌ red · ⚠️ flaky*

---

## Wave 0 Requirements

- [ ] Validation query set designed as part of plan execution (manual interactive tests, not file stubs)
- [ ] No automated test framework needed — all validation is manual skill invocation

*Existing infrastructure covers test execution: Claude Code session with `/privacy` skill.*

---

## Manual-Only Verifications

| Behavior | Requirement | Why Manual | Test Instructions |
|----------|-------------|------------|-------------------|
| Live WebFetch augments static knowledge | ARCH-04 | Skill is markdown instructions — no code to unit test | Run `/privacy` with research query, verify live content in response |
| Graceful degradation on partial failure | ARCH-05 | Requires real network conditions | Run queries targeting blocked sources (FTC, EPIC), verify degradation header |
| Graceful degradation on total failure | ARCH-05 | Requires network restriction | Test in offline mode, verify static-only response with limitation note |
| Multi-source synthesis | DEPTH-02 | Output quality is subjective | Run cross-cutting query, verify theme-based interleaving from 3+ sources |
| Source routing accuracy | DEPTH-02 | Depends on query interpretation | Run diverse queries, verify different source selections |

*All phase behaviors require manual verification — this is a markdown-based skill with no executable code.*

---

## Validation Sign-Off

- [ ] All tasks have manual verification instructions
- [ ] Sampling continuity: test queries run after each file modification
- [ ] Wave 0 covers all validation scenarios
- [ ] No watch-mode flags
- [ ] Feedback latency < 30s per query
- [ ] `nyquist_compliant: true` set in frontmatter

**Approval:** pending
