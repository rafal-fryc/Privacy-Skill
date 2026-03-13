---
phase: 2
slug: regulation-knowledge-base
status: draft
nyquist_compliant: false
wave_0_complete: false
created: 2026-03-13
---

# Phase 2 — Validation Strategy

> Per-phase validation contract for feedback sampling during execution.

---

## Test Infrastructure

| Property | Value |
|----------|-------|
| **Framework** | Manual testing via `/privacy` command invocation |
| **Config file** | None — Claude Code skills are tested by invocation |
| **Quick run command** | `/privacy What does GDPR require?` (manual) |
| **Full suite command** | Run all 9 test queries below in sequence (manual) |
| **Estimated runtime** | ~5 minutes (manual invocation) |

---

## Sampling Rate

- **After every task commit:** Invoke `/privacy` with a regulation-specific query and verify the response uses the regulation file content
- **After every plan wave:** Run all 9 test queries and verify correct file routing
- **Before `/gsd:verify-work`:** All 9 test queries produce structured, accurate answers from static knowledge
- **Max feedback latency:** ~30 seconds per query (manual)

---

## Per-Task Verification Map

| Task ID | Plan | Wave | Requirement | Test Type | Test Query | File Exists | Status |
|---------|------|------|-------------|-----------|-----------|-------------|--------|
| TBD | 01 | 1 | REG-01 | manual | `/privacy What are the GDPR lawful bases for processing?` | N/A — regulation file must exist | ⬜ pending |
| TBD | 01 | 1 | REG-02 | manual | `/privacy What consumer rights does the CCPA provide?` | N/A — regulation file must exist | ⬜ pending |
| TBD | 01 | 1 | REG-03 | manual | `/privacy What does COPPA require for parental consent?` | N/A — regulation file must exist | ⬜ pending |
| TBD | 01 | 1 | REG-04 | manual | `/privacy What entities are covered by HIPAA?` | N/A — regulation file must exist | ⬜ pending |
| TBD | 01 | 1 | REG-05 | manual | `/privacy What are education records under FERPA?` | N/A — regulation file must exist | ⬜ pending |
| TBD | 01 | 1 | REG-06 | manual | `/privacy What AI practices does the EU AI Act prohibit?` | N/A — regulation file must exist | ⬜ pending |
| TBD | 02 | 2 | REG-07 | manual | `/privacy Compare GDPR and CCPA consent requirements` | N/A — cross-reference file must exist | ⬜ pending |
| TBD | 02 | 2 | REG-08 | manual | `/privacy When does the COPPA rule update take effect?` | N/A — timeline file must exist | ⬜ pending |
| TBD | 02 | 2 | DEPTH-01 | manual | `/privacy What are GDPR breach notification requirements?` (verify no web fetch triggered) | N/A — routing + files must exist | ⬜ pending |

*Status: ⬜ pending · ✅ green · ❌ red · ⚠️ flaky*

---

## Wave 0 Requirements

*Existing infrastructure covers all phase requirements — no test framework setup needed. Claude Code skills are validated by manual invocation.*

---

## Manual-Only Verifications

| Behavior | Requirement | Why Manual | Test Instructions |
|----------|-------------|------------|-------------------|
| GDPR quick reference | REG-01 | Claude Code skills have no automated test harness | Invoke `/privacy What are the GDPR lawful bases?` — verify structured answer from static knowledge |
| CCPA/CPRA quick reference | REG-02 | Claude Code skills have no automated test harness | Invoke `/privacy What consumer rights does CCPA provide?` — verify structured answer |
| COPPA quick reference | REG-03 | Claude Code skills have no automated test harness | Invoke `/privacy What does COPPA require?` — verify structured answer |
| HIPAA quick reference | REG-04 | Claude Code skills have no automated test harness | Invoke `/privacy What entities are covered by HIPAA?` — verify structured answer |
| FERPA quick reference | REG-05 | Claude Code skills have no automated test harness | Invoke `/privacy What are education records under FERPA?` — verify structured answer |
| EU AI Act quick reference | REG-06 | Claude Code skills have no automated test harness | Invoke `/privacy What does the EU AI Act prohibit?` — verify privacy-focused answer |
| Cross-regulation comparison | REG-07 | Claude Code skills have no automated test harness | Invoke `/privacy Compare GDPR and CCPA on consent` — verify dimension-based comparison |
| Regulatory timeline | REG-08 | Claude Code skills have no automated test harness | Invoke `/privacy When does COPPA rule update take effect?` — verify date-stamped answer |
| Quick lookup mode | DEPTH-01 | Cannot programmatically verify no web fetch occurred | Invoke regulation query — verify response uses reference file content without web fetch |

---

## Validation Sign-Off

- [ ] All tasks have manual verification instructions
- [ ] Sampling continuity: every regulation file verified after creation
- [ ] Wave 0 covers all MISSING references
- [ ] No watch-mode flags
- [ ] Feedback latency < 30s per query
- [ ] `nyquist_compliant: true` set in frontmatter

**Approval:** pending
