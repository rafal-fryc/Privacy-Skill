---
phase: 03
slug: organization-catalog-government-sources
status: draft
nyquist_compliant: false
wave_0_complete: false
created: 2026-03-13
---

# Phase 03 — Validation Strategy

> Per-phase validation contract for feedback sampling during execution.

---

## Test Infrastructure

| Property | Value |
|----------|-------|
| **Framework** | Manual validation (content-only phase, no executable code) |
| **Config file** | None — no automated test infrastructure applicable |
| **Quick run command** | Manual review of file structure and SKILL.md routing |
| **Full suite command** | End-to-end test: invoke `/privacy` with org-related queries |
| **Estimated runtime** | ~2 minutes (manual review) |

---

## Sampling Rate

- **After every task commit:** Verify new files created, count catalog entries, check nav guide sections
- **After every plan wave:** Full SKILL.md routing review, verify all cross-references resolve
- **Before `/gsd:verify-work`:** Invoke `/privacy` with test queries from each routing intent category
- **Max feedback latency:** N/A (manual review)

---

## Per-Task Verification Map

| Task ID | Plan | Wave | Requirement | Test Type | Automated Command | File Exists | Status |
|---------|------|------|-------------|-----------|-------------------|-------------|--------|
| 03-XX-01 | XX | 1 | ORG-01 | manual-only | Count entries in advocacy-orgs.md + gov-regulators.md + academic-centers.md | ❌ W0 | ⬜ pending |
| 03-XX-02 | XX | 1 | ORG-02 | manual-only | Verify 7 new nav guide files created + fpf-reference.md exists | ❌ W0 | ⬜ pending |
| 03-XX-03 | XX | 1 | ORG-03 | manual-only | Check each nav guide has all template sections | ❌ W0 | ⬜ pending |
| 03-XX-04 | XX | 1 | ORG-05 | manual-only | Verify gov-regulators.md has all 5 regulator entries + state AG section | ❌ W0 | ⬜ pending |
| 03-XX-05 | XX | 1 | ORG-06 | manual-only | Verify academic-centers.md has required entries | ❌ W0 | ⬜ pending |

*Status: ⬜ pending · ✅ green · ❌ red · ⚠️ flaky*

---

## Wave 0 Requirements

*Existing infrastructure covers all phase requirements. No test infrastructure needed for content-only deliverables. Validation is structural review during implementation.*

---

## Manual-Only Verifications

| Behavior | Requirement | Why Manual | Test Instructions |
|----------|-------------|------------|-------------------|
| 15-20 orgs cataloged with required fields | ORG-01 | Content authoring — no executable code | Count org entries across 3 catalog files, verify each has name/focus/website/resources |
| 8 nav guides exist with URL patterns | ORG-02, ORG-03 | File structure + content quality | List nav guide files, verify each contains all template sections |
| Gov regulator directory complete | ORG-05 | Content accuracy | Verify FTC, EDPB, ICO, CPPA, CNIL entries + state AG overview |
| Academic centers cataloged | ORG-06 | Content accuracy | Verify Georgetown, Berkman Klein, Stanford HAI, Brookings entries |
| SKILL.md routing works for org queries | ORG-02 | Requires live skill invocation | Test `/privacy` with org-focused queries |

---

## Validation Sign-Off

- [ ] All tasks have manual verification criteria defined
- [ ] Sampling continuity: structural review after each commit
- [ ] Wave 0 covers all MISSING references
- [ ] No watch-mode flags
- [ ] Feedback latency: immediate (manual review)
- [ ] `nyquist_compliant: true` set in frontmatter

**Approval:** pending
