# CDT Navigation Guide

## Site Overview

The Center for Democracy and Technology (CDT) is a nonpartisan nonprofit working to advance civil rights and civil liberties in the digital age. Founded in 1994, CDT operates from Washington, D.C., Brussels, and San Francisco, spanning both U.S. and European policy. The site serves as a hub for CDT's policy research, advocacy positions, and analysis across privacy, free expression, government surveillance, and AI governance.

CDT is distinctive for its nonpartisan approach and its presence in both U.S. and EU policy processes. The organization produces substantial policy research and formal regulatory comments while maintaining a lighter advocacy tone compared to more litigation-focused organizations. The primary audience is policymakers, privacy practitioners, technology companies, and civil society organizations.

---

## URL Patterns

| Content Type | URL Pattern | Example |
|---|---|---|
| Areas of focus index | `cdt.org/areas-of-focus/` | All focus areas |
| Specific focus area | `cdt.org/area-of-focus/{slug}/` | Individual area page |
| Insights (blog/analysis) | `cdt.org/insights/` | All insights |
| Specific insight | `cdt.org/insights/{post-slug}/` | Individual post |
| Press releases | `cdt.org/press/` | Press section |
| About | `cdt.org/about/` | Organization info |
| Policy comments | Part of insights | Filtered by content type |

**Note:** CDT uses `area-of-focus` (singular) for individual area pages but `areas-of-focus` (plural) for the index. This inconsistency is important for URL construction.

---

## Key URLs

- **Areas of Focus Index:** https://cdt.org/areas-of-focus/ -- Central navigation page listing all CDT areas of focus. Start here to understand CDT's organizational structure and find topic-specific content.
- **Privacy and Data:** https://cdt.org/area-of-focus/privacy-data/ -- CDT's privacy work covering consumer privacy, data protection legislation, privacy-enhancing technologies, and data broker regulation.
- **Free Expression:** https://cdt.org/area-of-focus/free-expression/ -- CDT's work on online speech, content moderation, platform governance, and intermediary liability.
- **Government Surveillance:** https://cdt.org/area-of-focus/government-surveillance/ -- CDT's work on surveillance reform, law enforcement access to data, national security authorities, and warrant requirements.
- **Insights:** https://cdt.org/insights/ -- CDT's primary publication feed including policy analysis, research reports, blog posts, and formal regulatory comments.

---

## Key Sections

### Areas of Focus
CDT organizes its work into thematic areas, each with a dedicated page containing background, current projects, and related publications:
- **Privacy and Data:** Consumer data protection, comprehensive privacy legislation, data broker regulation, privacy-enhancing technologies (PETs), health data privacy, biometric data
- **Free Expression:** Content moderation policy, platform governance, intermediary liability, online speech protections, government censorship
- **Government Surveillance:** FISA reform, law enforcement data access, Section 702, surveillance technology policy, encryption policy
- **Security and Surveillance:** Cybersecurity policy, vulnerability disclosure, security research protections, IoT security
- **Artificial Intelligence:** AI governance, algorithmic accountability, automated decision-making, AI impact assessments, EU AI Act analysis
- **Elections and Democracy:** Election security, voting technology, disinformation policy, political advertising transparency
- **Open Internet:** Net neutrality, broadband access, internet governance, competition policy

### Insights
CDT's primary content stream. Insights include policy analysis, research reports, regulatory comments, blog posts, and position papers. This is the most frequently updated section and contains CDT's substantive analytical output.

### European Office
CDT maintains a Brussels office focused on EU policy. European-focused work covers GDPR implementation, EU AI Act, Digital Services Act, and other EU regulatory frameworks. European policy content appears within the relevant area-of-focus pages rather than a separate European section.

### Press
Press releases and media statements covering CDT's positions on current privacy and technology policy developments. Useful for tracking CDT's public advocacy positions.

---

## Content Types

- **Policy analysis:** Detailed analysis of proposed and enacted privacy legislation, regulatory actions, and technology policy developments
- **Research reports:** Multi-page research documents on specific policy topics, often with recommendations
- **Regulatory comments:** Formal comments on proposed rules, ANPR responses, and legislative testimony
- **Blog posts/insights:** Shorter-form analysis and commentary on current developments
- **Position statements:** CDT's official positions on policy questions
- **Press releases:** Announcements of new publications, advocacy positions, and organizational news
- **Testimony:** Congressional testimony and regulatory hearing statements
- **Amicus briefs:** Legal filings in cases involving civil liberties and technology (less frequent than EPIC's litigation program)

---

## Search Strategy

1. **For CDT's coverage of a specific privacy topic:** Start at the Areas of Focus Index. Navigate to the relevant area page for background, current projects, and links to related insights and publications.
2. **For CDT's most recent analysis:** Check the Insights feed, which is the primary publication stream. Insights are published regularly and cover current developments across all CDT focus areas.
3. **For formal regulatory comments:** CDT's regulatory comments are published as insights. Search within Insights for comments on specific agencies (FTC, FCC) or regulatory proposals.
4. **For EU-specific analysis:** CDT's European work is integrated into the relevant focus areas. Check Privacy and Data and the AI focus area for EU regulatory content (GDPR, AI Act, DSA).
5. **For CDT's position on a specific policy question:** Check the Press section for public statements and the relevant area-of-focus page for detailed analysis.

---

## Tips

- CDT's nonpartisan positioning means its analysis is frequently cited by both industry and civil society. It provides a useful middle-ground perspective compared to more advocacy-oriented organizations.
- CDT's Brussels office makes it one of the few U.S.-based privacy organizations with direct engagement in EU policy. Its EU AI Act and GDPR analysis reflects firsthand policy engagement.
- The Insights feed is CDT's most valuable single resource -- it contains the substantive analytical output across all areas. Bookmark it for current privacy policy analysis.
- CDT's regulatory comments are well-structured and provide clear policy recommendations, making them useful reference documents for understanding stakeholder positions on proposed regulations.
- CDT covers both privacy and free expression, which gives it a distinctive perspective on questions where these rights intersect (e.g., content moderation, surveillance, data access for law enforcement).
- For AI governance analysis, CDT provides a civil liberties lens that complements FPF's governance-focused approach and EPIC's enforcement-focused approach.
- CDT's work on government surveillance reform (Section 702, FISA) provides detailed analysis not covered by most privacy-focused organizations.
- The singular/plural URL inconsistency (`areas-of-focus` for index, `area-of-focus` for individual pages) is a known pattern -- use the correct form when constructing URLs.
- CDT frequently collaborates with other organizations on joint policy statements and coalition letters. These collaborative outputs often appear in the Insights feed.
- For health data privacy, CDT provides analysis on consumer health data outside HIPAA scope, complementing FPF's health data coverage.

---

## WebFetch Notes

**Status: Not Accessible (Cloudflare Block)**

CDT's website is protected by Cloudflare and is not accessible via WebFetch. Automated requests receive a Cloudflare security challenge rather than page content.

**Test Results (March 2026):**
- `cdt.org/areas-of-focus/` -- Cloudflare challenge page returned. No site content accessible.
- `cdt.org/area-of-focus/privacy-data/` -- Cloudflare challenge page returned. No site content accessible.

**Likely Cause:** Cloudflare's bot protection blocks non-browser HTTP requests. The challenge page requires JavaScript execution and potentially browser fingerprinting to pass, which WebFetch does not support.

**Workarounds for Phase 4:**
- **WebSearch:** Use web search to find specific CDT content. CDT insights and publications are well-indexed. Queries like `site:cdt.org [topic]` return relevant results with titles and descriptions.
- **IAPP coverage:** IAPP frequently covers CDT's publications and policy positions in its news articles and resource summaries.
- **Direct citation:** When CDT content is referenced by other sources, cite the CDT URL for attribution. The URL patterns documented above are stable for human navigation.
- **RSS/feeds:** CDT may offer RSS feeds that bypass Cloudflare protection -- worth testing in Phase 4 as an alternative access method.

**Impact on skill:** CDT's nav guide remains valuable as a navigation reference and for query routing. When a user asks about CDT's work, the skill can direct them to the relevant area-of-focus page and provide context about CDT's coverage, even without live fetching.

---

*This file provides navigation guidance for the CDT website. For CDT as an organization, see [advocacy-orgs.md](advocacy-orgs.md).*
