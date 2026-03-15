# EPIC Navigation Guide

## Site Overview

The Electronic Privacy Information Center (EPIC) is a public interest research center focused on privacy and civil liberties. Founded in 1994, EPIC is based in Washington, D.C. and operates at the intersection of privacy advocacy, litigation, and policy research. The site serves as a repository for EPIC's issue-area research, litigation filings, Freedom of Information Act (FOIA) work, and policy advocacy.

EPIC is distinctive among privacy organizations for its extensive litigation activity (EPIC v. [Agency] cases), its FOIA program obtaining government documents related to surveillance and privacy, and its focus on consumer privacy, algorithmic transparency, and open government. The primary audience is privacy researchers, policy advocates, journalists, and legal practitioners.

---

## URL Patterns

| Content Type | URL Pattern | Example |
|---|---|---|
| Issue areas | `epic.org/issues/` | Issues index |
| Specific issue | `epic.org/issues/{issue-slug}/` | Individual issue page |
| Projects | `epic.org/projects/` | Project listings |
| About | `epic.org/about/` | Organization info |
| FOIA work | `epic.org/foia/` | FOIA documents |
| Press/news | `epic.org/press/` | Press releases |

**Note:** EPIC restructured its website in recent years. Current URL patterns use `/issues/` and `/projects/` as primary navigation paths. Some older resources may use legacy URL patterns.

---

## Key URLs

- **Issues Index:** https://epic.org/issues/ -- Central navigation page listing all EPIC issue areas with descriptions and links to detailed pages. Start here when looking for EPIC's coverage of a specific privacy topic.
- **Consumer Privacy:** https://epic.org/issues/consumer-privacy/ -- EPIC's consumer privacy work covering data brokers, online tracking, privacy policies, and consumer rights advocacy.
- **Algorithmic Transparency:** https://epic.org/issues/algorithmic-transparency/ -- EPIC's work on AI accountability, algorithmic decision-making, and automated systems transparency requirements.
- **Open Government:** https://epic.org/issues/open-government/ -- EPIC's FOIA litigation and open government advocacy, including published government documents obtained through FOIA requests.
- **Student Privacy:** https://epic.org/issues/student-privacy/ -- EPIC's work on FERPA, student data collection, and edtech privacy concerns.

---

## Key Sections

### Issue Areas
EPIC organizes its work into thematic issue areas. Each issue page contains background, current advocacy efforts, related litigation, and relevant documents. Key issue areas include:
- **Consumer Privacy:** Data brokers, online tracking, privacy policies, consumer rights
- **Algorithmic Transparency:** AI accountability, automated decision-making, algorithmic auditing
- **Surveillance:** Government surveillance programs, facial recognition, location tracking
- **Open Government:** FOIA advocacy, government transparency, access to public records
- **Student Privacy:** Educational records, edtech privacy, classroom surveillance
- **Data Protection:** Comprehensive privacy legislation advocacy, international data protection
- **Cyber Security:** Data breaches, cybersecurity policy, encryption policy
- **Health Privacy:** Health data beyond HIPAA, genetic privacy, reproductive data

### Projects
EPIC operates several ongoing projects and initiatives beyond its issue-area work, including research programs, educational initiatives, and collaborative advocacy efforts.

### Litigation
EPIC maintains an active litigation program, frequently filing amicus curiae briefs in privacy cases and bringing original actions. EPIC v. [Agency] cases have shaped privacy law in areas including:
- Government surveillance authorities
- Privacy impact assessments for federal agencies
- Consumer data protection enforcement
- Facial recognition deployment by government agencies

### FOIA Work
EPIC's Freedom of Information Act program is one of the most active among privacy organizations. EPIC obtains and publishes government documents related to surveillance programs, privacy policies, and data collection practices. FOIA-obtained documents are published on the site and frequently cited in policy debates.

---

## Content Types

- **Issue area pages:** Background research and analysis on privacy topics with current advocacy positions
- **Litigation filings:** Amicus briefs, complaints, court filings, and case summaries from EPIC's legal program
- **FOIA documents:** Government documents obtained through FOIA requests, often with EPIC's analysis
- **Policy comments:** Formal comments on proposed regulations, FTC proceedings, and legislative proposals
- **Press releases:** Announcements of new litigation, FOIA releases, and policy positions
- **Reports and publications:** Research reports on specific privacy topics (less frequent than other output types)
- **Blog posts:** Commentary on privacy developments and EPIC's ongoing work
- **Testimony:** Congressional testimony and regulatory hearing statements

---

## Search Strategy

1. **For EPIC's coverage of a specific privacy topic:** Start at the Issues Index page. Each issue area page provides comprehensive coverage of EPIC's research, advocacy, and litigation on that topic.
2. **For litigation and legal filings:** Navigate to the relevant issue area page, which typically includes links to related litigation. EPIC's amicus briefs and case filings are organized by issue.
3. **For government documents obtained via FOIA:** Check the Open Government issue area and the FOIA section. Published documents are organized by agency and topic.
4. **For EPIC's position on pending legislation or regulation:** Check Press Releases and the relevant issue area page for policy comments and formal submissions.
5. **For current EPIC priorities:** Check the front page and Press section for recent activity. EPIC's current priority areas include AI accountability, data broker regulation, and surveillance reform.

---

## Tips

- EPIC's litigation filings (especially amicus briefs) are valuable primary sources for understanding privacy law arguments beyond EPIC's own advocacy positions. They synthesize case law and statutory analysis.
- EPIC's FOIA-obtained documents are primary sources that appear nowhere else publicly -- they are particularly valuable for research on government surveillance and data collection programs.
- EPIC focuses on U.S. federal privacy issues more than state-level. For state privacy law coverage, IAPP and FPF are better sources.
- EPIC is an advocacy organization -- its analysis reflects its public-interest perspective. For balanced multi-stakeholder analysis, cross-reference with FPF or academic sources.
- The Issues Index page is the best starting point for most research questions about EPIC's work. It provides a comprehensive map of the site's content.
- EPIC's Congressional testimony is a good source for concise, well-structured arguments on privacy policy questions.
- For EPIC's coverage of FTC enforcement, check the Consumer Privacy issue area, which tracks FTC actions relevant to consumer data protection.

---

## WebFetch Notes

**Status: Not Accessible (Timeout)**

EPIC's website is not reliably accessible via WebFetch. Attempted connections time out before returning content.

**Test Results (March 2026):**
- `epic.org/issues/` -- Connection timeout. No content returned.
- `epic.org/` -- Connection timeout. No content returned.

**Likely Cause:** The site may use aggressive rate limiting, JavaScript-heavy rendering, or WAF (Web Application Firewall) rules that block automated access. The timeout behavior (rather than an explicit block message) suggests network-level filtering or server-side timeout on non-browser requests.

**Workarounds for Phase 4:**
- **WebSearch:** Use web search to find specific EPIC content. EPIC pages are well-indexed by search engines. Queries like `site:epic.org [topic]` return relevant results.
- **IAPP coverage:** IAPP's news and resource articles frequently cover EPIC's filings, litigation, and policy positions.
- **Direct citation:** When EPIC content is referenced in other sources (FPF blog, IAPP news, law firm analyses), cite the EPIC URL for attribution even if WebFetch cannot retrieve it directly.
- **Manual navigation:** The URL patterns documented above remain valid for human navigation and manual reference.

**Impact on skill:** EPIC's nav guide remains valuable as a manual navigation reference and for query routing. When a user asks about EPIC's work, the skill can provide the relevant URL patterns and issue area structure even without live fetching.

---

*This file provides navigation guidance for the EPIC website. For EPIC as an organization, see [advocacy-orgs.md](advocacy-orgs.md).*
