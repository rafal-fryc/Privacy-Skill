---
phase: 01
slug: skill-foundation-fpf-primary-source
status: draft
nyquist_compliant: false
wave_0_complete: false
created: 2026-03-13
---

# Phase 01 — Validation Strategy

> Per-phase validation contract for feedback sampling during execution.

---

## Test Infrastructure

| Property | Value |
|----------|-------|
| **Framework** | Manual validation (markdown skill, no runtime code) |
| **Config file** | None — skill is pure markdown, no test runner |
| **Quick run command** | Invoke `/privacy [test query]` in Claude Code session |
| **Full suite command** | Run all 12 requirement validation queries sequentially |
| **Estimated runtime** | ~5 minutes (manual queries) |

---

## Sampling Rate

- **After every task commit:** Review file for structural correctness (line counts, file references, frontmatter format)
- **After every plan wave:** Run 3-5 representative queries from example set in a Claude Code session
- **Before `/gsd:verify-work`:** Full suite of 12 requirement validation queries must pass
- **Max feedback latency:** ~30 seconds per query

---

## Per-Task Verification Map

| Task ID | Plan | Wave | Requirement | Test Type | Validation Method | File Exists | Status |
|---------|------|------|-------------|-----------|-------------------|-------------|--------|
| 01-01-01 | 01 | 1 | ARCH-01 | manual | Type `/privacy what is GDPR?` and verify skill activates | ❌ W0 | ⬜ pending |
| 01-01-02 | 01 | 1 | ARCH-02 | manual | `wc -l SKILL.md` < 500, verify reference file dispatching | ❌ W0 | ⬜ pending |
| 01-01-03 | 01 | 1 | ARCH-03 | manual | Ask FPF-specific vs general query, verify different reference files loaded | ❌ W0 | ⬜ pending |
| 01-02-01 | 02 | 1 | FPF-01 | manual | Ask "What types of publications does FPF produce?" — verify all 6 types | ❌ W0 | ⬜ pending |
| 01-02-02 | 02 | 1 | FPF-02 | manual | Ask "What issue areas does FPF cover?" — verify 20+ areas | ❌ W0 | ⬜ pending |
| 01-02-03 | 02 | 1 | FPF-03 | manual | Review fpf-reference.md URL patterns, spot-check 3-5 URLs | ❌ W0 | ⬜ pending |
| 01-02-04 | 02 | 1 | FPF-04 | manual | Ask about FPF-covered topic, verify FPF cited first | ❌ W0 | ⬜ pending |
| 01-02-05 | 02 | 1 | FPF-05 | manual | Ask "What are FPF's major programs?" — verify list | ❌ W0 | ⬜ pending |
| 01-03-01 | 03 | 2 | ARCH-06 | manual | Review responses for professional-grade language | ❌ W0 | ⬜ pending |
| 01-03-02 | 03 | 2 | ARCH-07 | manual | Ask specific fact, verify answer cites reference not training data | ❌ W0 | ⬜ pending |
| 01-03-03 | 03 | 2 | ARCH-08 | manual | Run 5+ queries, verify all have disclaimer footer | ❌ W0 | ⬜ pending |
| 01-03-04 | 03 | 2 | ORG-04 | manual | Run 5+ queries, verify inline citations with org names and URLs | ❌ W0 | ⬜ pending |

*Status: ⬜ pending · ✅ green · ❌ red · ⚠️ flaky*

---

## Wave 0 Requirements

- [ ] No test infrastructure needed — this is a pure markdown skill with no runtime code
- [ ] Prepare 12 test queries (one per requirement) with expected behavior descriptions
- [ ] URL spot-check script: simple bash script that `curl -sI` a set of fpf.org URLs and reports HTTP status codes

*Existing infrastructure covers runtime requirements. Validation is manual by nature of the skill type.*

---

## Manual-Only Verifications

| Behavior | Requirement | Why Manual | Test Instructions |
|----------|-------------|------------|-------------------|
| `/privacy` triggers skill | ARCH-01 | Requires Claude Code session | Type `/privacy what is GDPR?` and verify skill activates |
| SKILL.md dispatches to reference files | ARCH-03 | Requires observing Claude behavior | Ask FPF-specific vs general query, verify different files loaded |
| Professional-grade language | ARCH-06 | Subjective quality check | Review 3+ responses for precise terminology |
| Anti-hallucination from references | ARCH-07 | Requires content review | Ask specific regulatory fact, verify sourced from reference files |
| Disclaimer on every response | ARCH-08 | Requires Claude Code session | Run 5+ varied queries, verify all have disclaimer |
| FPF cited first when relevant | FPF-04 | Requires content review | Ask about FPF-covered topic, verify FPF primary in attribution |
| Source attribution in every answer | ORG-04 | Requires content review | Run 5+ queries, verify inline citations with org names and URLs |

---

## Validation Sign-Off

- [ ] All tasks have manual verify or Wave 0 dependencies
- [ ] Sampling continuity: no 3 consecutive tasks without automated verify
- [ ] Wave 0 covers all MISSING references
- [ ] No watch-mode flags
- [ ] Feedback latency < 30s
- [ ] `nyquist_compliant: true` set in frontmatter

**Approval:** pending
