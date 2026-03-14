# CPPA Navigation Guide

## Site Overview

The California Privacy Protection Agency (CPPA) website at cppa.ca.gov serves as the official portal for California's dedicated privacy enforcement body. The site provides access to CCPA/CPRA regulations, rulemaking proceedings, the Data Broker Registry, enforcement information, and consumer resources. The primary audience includes businesses seeking compliance guidance, consumers exercising their privacy rights, and privacy professionals tracking California's regulatory developments. The site is structured around the CPPA's core functions: rulemaking, enforcement, data broker oversight, and public engagement.

## URL Patterns

| Content Type | URL Pattern | Example |
|---|---|---|
| Regulations | `cppa.ca.gov/regulations/` | `cppa.ca.gov/regulations/` |
| Statute text | `cppa.ca.gov/regulations/{statute_name}.html` | `cppa.ca.gov/regulations/consumer_privacy_act.html` |
| Data broker registry | `cppa.ca.gov/data_broker_registry` | Redirects to registry landing page |
| Announcements | `cppa.ca.gov/announcements/` | `cppa.ca.gov/announcements/` |
| Board meetings | `cppa.ca.gov/meetings/` | `cppa.ca.gov/meetings/` |
| Consumer resources | `cppa.ca.gov/{resource_name}` | `cppa.ca.gov/consumer-resources/` |

**Note:** CPPA uses a flat URL structure for most pages rather than deeply nested paths. Major sections are accessible directly from the root domain.

## Key URLs

- **Regulations page:** https://cppa.ca.gov/regulations/ -- Central hub for CCPA/CPRA regulatory text, proposed regulations, and formal rulemaking documents. Start here for current and proposed rule language.
- **CCPA statute text:** https://cppa.ca.gov/regulations/consumer_privacy_act.html -- Full text of the California Consumer Privacy Act as currently amended by CPRA. The authoritative source for statutory language.
- **Data Broker Registry:** https://cppa.ca.gov/data_broker_registry -- Searchable registry of data brokers registered under the DELETE Act (SB 362). Includes broker names, contact information, and registration status. Over 500 brokers registered as of 2025.
- **Announcements:** https://cppa.ca.gov/announcements/ -- Press releases, enforcement advisories, rulemaking updates, and agency news. Primary source for CPPA enforcement actions and regulatory developments.
- **Board meetings:** https://cppa.ca.gov/meetings/ -- Schedule and materials for CPPA board meetings, including agendas, meeting packets, and recorded proceedings. Rulemaking discussions and enforcement policy decisions occur at these meetings.

## Key Sections

### Regulations
The regulations section is the most substantively important part of the site for privacy practitioners. It contains:
- Current CCPA/CPRA text (as amended)
- CPPA's adopted regulations (Title 11, Division 6, California Code of Regulations)
- Proposed rulemaking packages (cybersecurity audits, risk assessments, ADMT)
- Initial, modified, and final statements of reasons for adopted rules
- Public comment submissions on proposed rules

### Data Broker Registry
Established by the DELETE Act (SB 362, 2023), this section provides:
- Searchable database of registered data brokers
- Data broker registration requirements and annual renewal deadlines
- Information about the DELETE Request Opt-Out Platform (DROP) for centralized deletion requests
- Enforcement information for non-compliant data brokers ($200/day penalty)

### Consumer Resources
Consumer-facing materials including:
- How to exercise privacy rights under CCPA/CPRA
- How to file a complaint with the CPPA
- Information about opt-out rights and Global Privacy Control (GPC)
- Plain-language explanations of consumer privacy rights

### Enforcement
Enforcement information including:
- Enforcement advisories and compliance guidance
- Investigative priorities and enforcement philosophy
- Complaint filing portal for consumers
- Information about the CPPA's enforcement authority and penalty structure
- Details on penalty amounts: $2,500 per unintentional violation, $7,500 per intentional violation or violations involving minors

### Board and Agency
Information about the CPPA as an institution:
- Board member biographies and appointment information
- Board meeting schedule and archived meeting materials
- Agency strategic plan and enforcement priorities
- Public participation opportunities (public comment periods, board meeting testimony)
- Agency contact information and media inquiries

## Content Types

| Type | Description | Location |
|---|---|---|
| Regulatory text | Full statute and regulation text | Regulations section |
| Rulemaking documents | Proposed rules, statements of reasons, public comments | Regulations section |
| Press releases | Enforcement actions, agency updates, policy announcements | Announcements |
| Meeting materials | Board agendas, meeting packets, recorded proceedings | Meetings |
| Consumer guides | Plain-language privacy rights information | Consumer resources |
| Registry data | Data broker registration records | Data Broker Registry |

## Search Strategy

1. **For current regulation text:** Go directly to `cppa.ca.gov/regulations/consumer_privacy_act.html` for the statute or `cppa.ca.gov/regulations/` for CPPA-adopted regulations.
2. **For rulemaking status:** Check `cppa.ca.gov/regulations/` for active rulemaking packages. Proposed regulations on cybersecurity audits, risk assessments, and ADMT are the most actively tracked items.
3. **For enforcement actions:** Check `cppa.ca.gov/announcements/` for enforcement advisories and press releases. The CPPA does not maintain a separate enforcement database -- actions are published as announcements.
4. **For data broker information:** Use `cppa.ca.gov/data_broker_registry` to search registered data brokers by name.
5. **For board decisions:** Check `cppa.ca.gov/meetings/` for upcoming and past board meeting agendas. Significant regulatory and enforcement policy decisions are made at board meetings.
6. **For consumer complaint filing:** Navigate through the consumer resources section to the complaint submission portal.

## Tips

- The CPPA's rulemaking documents are the most valuable resource for understanding how CCPA/CPRA provisions will be interpreted. Statements of reasons explain the agency's reasoning behind specific regulatory requirements.
- Board meeting materials (meeting packets) often contain draft regulatory language and enforcement policy discussions before formal rulemaking begins. Monitor meetings for early signals of regulatory direction.
- The Data Broker Registry is updated as new registrations are processed. Use it to verify whether a specific company has registered as required under the DELETE Act.
- The CPPA site is separate from the California Attorney General's website (oag.ca.gov), which also has CCPA enforcement information. Both agencies share enforcement authority, but the CPPA is the rulemaking authority.
- Announcements are posted in reverse chronological order. For a comprehensive view of CPPA enforcement activity, review announcements filtered by enforcement-related topics.
- When tracking active rulemaking, the CPPA publishes both "initial statement of reasons" (explaining the rationale for proposed rules) and "final statement of reasons" (responding to public comments). Both are essential for understanding regulatory intent.
- The DELETE Act's Data Broker Registry and the DROP mechanism are distinct -- the registry is a transparency database (who is a data broker), while DROP is the consumer-facing deletion tool. The CPPA administers both.
- For Global Privacy Control (GPC) compliance questions, check the CPPA announcements for enforcement advisories. GPC enforcement has been a stated priority since the CPPA began enforcement operations.

## WebFetch Notes

**Accessibility:** CPPA's website renders server-side and is fully accessible via WebFetch. All tested pages return clean HTML content without JavaScript rendering requirements.

**Tested URLs (March 2026):**

| URL | Status | Notes |
|---|---|---|
| `cppa.ca.gov/` | 200 OK | Homepage loads cleanly |
| `cppa.ca.gov/regulations/` | 200 OK | Full regulations page content |
| `cppa.ca.gov/regulations/consumer_privacy_act.html` | 200 OK | Complete statute text |
| `cppa.ca.gov/data_broker_registry` | 301 -> 200 | Redirects to registry page, loads successfully |
| `cppa.ca.gov/announcements/` | 200 OK | Announcements page loads |
| `cppa.ca.gov/meetings/` | 200 OK | Meetings page loads |

**Reliability:** High. All major pages are accessible and return structured HTML. No Cloudflare protection, no User-Agent blocking, no rate limiting observed during testing.

**Phase 4 integration:** CPPA is an excellent candidate for live WebFetch queries. Regulation text, announcements, and data broker registry data can all be fetched programmatically. The server-side rendering means content is available in the initial HTML response without requiring JavaScript execution.

**Content freshness considerations:** The CPPA site is updated frequently during active rulemaking periods. Board meeting materials are typically posted 10 days before meetings. Announcements are published as events occur. For time-sensitive research (e.g., checking rulemaking status or recent enforcement actions), live WebFetch is preferred over cached knowledge to ensure current information.

---

*This navigation guide is loaded when queries involve CPPA site navigation, California privacy enforcement resources, CCPA/CPRA regulatory text, or data broker registry lookups. For CCPA/CPRA provisions, see [ccpa-reference.md](ccpa-reference.md). For CPPA enforcement profile, see [gov-regulators.md](gov-regulators.md).*
