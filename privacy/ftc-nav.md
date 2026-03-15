# FTC Navigation Guide

## Site Overview

The Federal Trade Commission (FTC) website at ftc.gov is the official portal for the United States' primary consumer protection and privacy enforcement agency. The site provides access to enforcement actions, business guidance, legal library resources, consumer complaint filing, and policy documents. For privacy professionals, the most valuable sections are the business guidance hub (privacy and security resources), the legal library (cases and proceedings), and the enforcement action archive. The FTC site is large and comprehensive, organized by audience (business, consumer, legal professional) with privacy and data security content distributed across multiple sections.

**Important: ftc.gov blocks automated access (WebFetch returns 403 on all tested pages).** This guide provides navigation patterns for manual access and reference. See WebFetch Notes for details and alternative data sources.

## URL Patterns

| Content Type | URL Pattern | Example |
|---|---|---|
| Business guidance | `ftc.gov/business-guidance/{topic}` | `ftc.gov/business-guidance/privacy-security` |
| Legal library | `ftc.gov/legal-library/browse/{type}` | `ftc.gov/legal-library/browse/cases-proceedings` |
| News and events | `ftc.gov/news-events/topics/{topic-path}` | `ftc.gov/news-events/topics/protecting-consumer-privacy-security` |
| Blog posts | `ftc.gov/business-guidance/blog/` | `ftc.gov/business-guidance/blog/` |
| Consumer info | `ftc.gov/consumer-protection/{topic}` | `ftc.gov/consumer-protection/privacy-identity` |
| Reports | `ftc.gov/reports/{report-slug}` | Varies by report |
| Complaint filing | `ftc.gov/complaint` | Direct consumer complaint portal |
| Commissioner statements | `ftc.gov/legal-library/browse/public-statements/` | Commissioner opinions on enforcement |

**Note:** FTC URLs are hierarchical and generally stable. Section-level URLs (e.g., `/business-guidance/privacy-security`) are more stable than individual document URLs, which may change during site restructuring. The FTC restructured its website in 2022, which changed many historical URLs. Current URL patterns have been stable since that restructuring.

**URL verification note:** All URL patterns documented here were verified via WebSearch (not WebFetch, which is blocked). URLs are confirmed to exist and resolve correctly when accessed through a standard web browser.

## Key URLs

- **Privacy and Security Business Guidance:** https://www.ftc.gov/business-guidance/privacy-security -- Central hub for all FTC privacy and data security guidance directed at businesses. Includes compliance resources, best practices, and regulatory expectations. Start here for understanding FTC's privacy compliance expectations.
- **Cases and Proceedings:** https://www.ftc.gov/legal-library/browse/cases-proceedings -- Searchable database of FTC enforcement actions including complaints, consent decrees, and administrative orders. Filter by topic (privacy, data security, COPPA) to find relevant cases.
- **Privacy and Security Enforcement:** https://www.ftc.gov/news-events/topics/protecting-consumer-privacy-security/privacy-security-enforcement -- News and updates on FTC privacy enforcement actions, including press releases, blog posts, and commissioner statements about recent cases.
- **COPPA Rule Page:** https://www.ftc.gov/legal-library/browse/rules/childrens-online-privacy-protection-rule-coppa -- Official COPPA Rule text, FAQs, and compliance guidance. The authoritative source for COPPA regulatory requirements.
- **Consumer Complaint Portal:** https://www.ftc.gov/complaint -- Submit consumer complaints to the FTC's Consumer Sentinel Network. Complaint data informs enforcement priorities and may trigger investigations.

## Key Sections

### Business Guidance -- Privacy and Security
The most relevant section for privacy practitioners, containing:
- Start with Security guide (practical security guidance for businesses)
- Protecting Personal Information guide
- Children's Privacy guidance (COPPA compliance)
- Health Privacy guidance (Health Breach Notification Rule)
- Mobile and IoT privacy guidance
- Data security after a breach response guidance
- Industry-specific privacy compliance guides (financial, health, education)

### Legal Library
The FTC's comprehensive legal document repository:
- **Cases and proceedings:** Searchable enforcement action database. Each case entry includes the complaint, consent order, analysis to aid public comment, and related press releases.
- **Federal Register notices:** Proposed and final rules, including COPPA Rule amendments and the Health Breach Notification Rule.
- **Public statements:** Commissioner speeches and statements providing enforcement policy context.
- **Rules:** FTC Rules text including COPPA Rule, Gramm-Leach-Bliley Safeguards Rule, and Health Breach Notification Rule.
- **Advisory opinions and guidance documents:** Staff opinions and guidance on specific compliance questions.

### News and Events
Organized by topic area:
- Privacy and security enforcement news
- Data security enforcement news
- COPPA enforcement news
- Technology news and analysis
- Commissioner blog posts and policy commentary
- Congressional testimony transcripts

### Consumer Protection
Consumer-facing resources organized by privacy topic:
- Identity theft recovery guidance (IdentityTheft.gov integration)
- Privacy and identity protection resources
- Online security guides
- Scam and fraud alerts with privacy dimensions
- Do Not Call Registry management

### Reports and Research
The FTC publishes substantive reports on privacy and technology topics:
- Annual privacy and data security enforcement reports
- Commercial surveillance and data security reports
- Industry-specific studies (data brokers, facial recognition, mobile apps)
- Workshop reports from FTC-hosted privacy and technology events
- Congressional testimony transcripts on privacy policy issues

## Content Types

| Type | Description | Location |
|---|---|---|
| Enforcement actions | Complaints, consent decrees, administrative orders | Legal Library > Cases and Proceedings |
| Business guidance | Compliance guides, best practices, FAQs | Business Guidance > Privacy and Security |
| Rule text | COPPA Rule, HBNR, Safeguards Rule | Legal Library > Rules |
| Press releases | Enforcement announcements, policy statements | News and Events |
| Blog posts | Policy analysis, compliance tips, enforcement context | Business Guidance Blog |
| Reports | Annual privacy and data security reports, technology reports | Reports section |
| Commissioner statements | Individual commissioner positions on enforcement actions | Legal Library > Public Statements |
| Federal Register notices | Proposed rules, final rules, advance notices | Legal Library > Federal Register |

## Search Strategy

1. **For specific enforcement actions:** Start at the Cases and Proceedings page (`ftc.gov/legal-library/browse/cases-proceedings`). Filter by topic ("Privacy and Security" or "Children's Privacy") and date range to find relevant cases.
2. **For COPPA compliance:** Go directly to the COPPA Rule page (`ftc.gov/legal-library/browse/rules/childrens-online-privacy-protection-rule-coppa`) for rule text and FAQs. The Business Guidance section has additional children's privacy compliance resources.
3. **For data security guidance:** The "Start with Security" guide under Business Guidance is the FTC's most comprehensive data security resource. It distills lessons from 60+ enforcement actions into practical guidance.
4. **For recent enforcement:** Check the Privacy and Security Enforcement news page for chronological enforcement action announcements.
5. **For policy context:** Commissioner statements and blog posts provide interpretive context that is not available in formal enforcement documents. These are especially valuable for understanding enforcement priorities and how the FTC views emerging technologies.
6. **For Health Breach Notification Rule:** Search the Legal Library for HBNR-related cases and the rule text under Federal Register notices.

**Alternative search approach:** Because ftc.gov blocks automated access, IAPP's Global Privacy and Data Protection Enforcement Database (see [iapp.org](https://iapp.org)) catalogs FTC enforcement actions with structured metadata and is accessible via WebFetch. For automated enforcement action lookups, IAPP is the recommended alternative data source.

## Tips

- The FTC's enforcement approach evolves through case-by-case precedent rather than prescriptive rules. Reading consent decrees (not just press releases) reveals the specific practices the FTC considers problematic and the remedial measures it requires.
- Commissioner statements on enforcement actions often signal future enforcement direction. When commissioners dissent, the dissenting statements explain what additional enforcement they would pursue.
- The FTC Blog (under Business Guidance) is more actionable than formal guidance documents for understanding current enforcement expectations. Blog posts often explain how recent enforcement actions apply to common business practices.
- The FTC's "Start with Security" guide is built from enforcement action lessons and represents the FTC's de facto minimum security expectations. Deviating from its recommendations increases enforcement risk.
- The COPPA Safe Harbor Programs page lists FTC-approved self-regulatory programs that provide alternative compliance frameworks for COPPA requirements.
- FTC enforcement actions often include 20-year monitoring provisions. Checking the terms of consent decrees for companies in your industry reveals what the FTC considers baseline privacy requirements for that sector.
- For enforcement data in automated workflows, use IAPP's enforcement database rather than ftc.gov directly (see WebFetch Notes).
- The FTC's Annual Highlights report summarizes the year's major enforcement actions and policy initiatives. It is a useful starting point for understanding the agency's current priorities and enforcement volume.
- When researching a specific company's FTC history, search the Cases and Proceedings database by company name. Multiple actions against the same company (e.g., successive COPPA violations) indicate systemic compliance failures that inform risk assessment.
- The FTC's Gramm-Leach-Bliley Safeguards Rule (revised 2023) imposes specific technical security requirements on financial institutions. It represents the FTC's most prescriptive security mandate and is found under the Legal Library Rules section.
- For information about the FTC's rulemaking authority and limitations (particularly after AMG Capital Management v. FTC, 2021), review commissioner statements and the agency's Section 18 rulemaking initiatives on commercial surveillance and data security.

## WebFetch Notes

**Accessibility:** ftc.gov blocks automated access. All tested URLs return HTTP 403 (Forbidden), indicating server-side User-Agent or bot detection that rejects non-browser requests.

**Tested URLs (March 2026):**

| URL | Status | Notes |
|---|---|---|
| `ftc.gov/` | 403 Forbidden | Root page blocked |
| `ftc.gov/business-guidance/privacy-security` | 403 Forbidden | Business guidance blocked |
| `ftc.gov/legal-library/browse/cases-proceedings` | 403 Forbidden | Legal library blocked |
| `ftc.gov/complaint` | 403 Forbidden | Complaint portal blocked |
| `ftc.gov/news-events` | 403 Forbidden | News section blocked |

**Block scope:** Universal -- the 403 response applies to all tested URL paths, not just specific sections. This is likely a server-wide configuration blocking non-browser User-Agents.

**Impact on Phase 4:** FTC content cannot be fetched via WebFetch in automated research workflows. This is a significant limitation because the FTC is the primary U.S. privacy enforcement agency.

**Alternative data sources for automated access:**
- **IAPP Global Enforcement Database** (iapp.org) -- Catalogs FTC enforcement actions with structured metadata. Accessible via WebFetch. Recommended primary alternative for FTC enforcement data.
- **Law firm analysis sites** -- Many law firms publish FTC enforcement action summaries that are WebFetch-accessible.
- **Federal Register** (federalregister.gov) -- FTC rulemakings and Federal Register notices may be accessible for regulatory text.

**Workaround strategies for Phase 4:**
- Route enforcement action queries through IAPP's Global Enforcement Database (WebFetch-accessible, structured metadata)
- Route regulatory text queries through the Federal Register (federalregister.gov) for proposed and final rules
- Use WebSearch as a fallback to find FTC content indexed by search engines, then provide direct URLs for manual access
- Cache known FTC guidance documents (e.g., "Start with Security" principles) in skill knowledge for static fallback

**Recommendation:** For Phase 4 automated research, route FTC enforcement queries through IAPP's enforcement database rather than ftc.gov. For regulatory text, try the Federal Register. This guide still provides value for manual navigation reference and understanding FTC site structure when providing users with specific navigation guidance.

---

*This navigation guide is loaded when queries involve FTC site navigation, FTC enforcement resources, COPPA compliance guidance, or FTC business guidance on privacy and data security. For COPPA provisions, see [coppa-reference.md](coppa-reference.md). For FTC enforcement profile, see [gov-regulators.md](gov-regulators.md).*
