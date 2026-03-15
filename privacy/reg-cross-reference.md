# Regulation Cross-Reference

> **Last verified:** March 2026. This file is loaded for comparison queries only. For detailed coverage of any individual regulation, load the corresponding regulation reference file.

This file provides side-by-side comparison of 6 major privacy regulations across common compliance dimensions. Each dimension is a separate table for readability. For detailed coverage of any individual regulation, load the corresponding regulation reference file.

**Regulations covered:** GDPR, CCPA/CPRA, COPPA, HIPAA, FERPA, EU AI Act.

**How to use:** Each dimension splits the 6 regulations into two tables of 3 for readability. Tables are designed for scanning -- cells are concise (1-3 sentences). When a regulation has no provision for a dimension, entries are marked "N/A" with a brief reason.

---

## Scope and Applicability

Regulations differ fundamentally in who they regulate and protect. GDPR and the EU AI Act have extraterritorial reach; HIPAA and FERPA are sector-specific; COPPA is age-specific.

| Aspect | GDPR | CCPA/CPRA | COPPA |
|--------|------|-----------|-------|
| Who is regulated | Any controller/processor handling personal data of EU/EEA individuals, regardless of establishment | For-profit businesses in California meeting revenue ($25M+), data volume (100K+), or revenue-source (50%+ from selling/sharing PI) thresholds | Operators of commercial websites, online services, and apps directed to children under 13 or with actual knowledge of collecting from children under 13 |
| Who is protected | Data subjects: any identified or identifiable natural person in the EU/EEA | California consumers: natural persons who are California residents | Children under 13 years of age |
| Territorial reach | Extraterritorial: applies worldwide if offering goods/services to or monitoring behavior of EU/EEA individuals | California-focused but applies to any business worldwide that collects PI from California consumers and meets thresholds | U.S. federal: applies to operators under FTC jurisdiction regardless of location, if directed at U.S. children under 13 |
| Sector scope | Cross-sector (all industries) | Cross-sector (all for-profit businesses meeting thresholds) | Cross-sector but age-specific (under 13 only) |

| Aspect | HIPAA | FERPA | EU AI Act |
|--------|-------|-------|-----------|
| Who is regulated | Covered entities (health plans, clearinghouses, providers conducting standard electronic transactions) and their business associates | Educational agencies/institutions receiving federal DOE funding (virtually all public K-12 and most colleges/universities) | Providers, deployers, importers, and distributors of AI systems placed on the EU market or used in the EU |
| Who is protected | Individuals whose PHI is held by covered entities or business associates | Students (and parents of minor students) at covered institutions | Natural persons affected by AI systems within the EU |
| Territorial reach | U.S. federal: applies within the U.S. healthcare system | U.S. federal: applies to institutions receiving DOE funding, primarily domestic | Extraterritorial: applies regardless of establishment, if AI output is used in the EU |
| Sector scope | Sector-specific: healthcare only | Sector-specific: education only | Cross-sector but risk-based: scope determined by AI risk classification, not industry |

## Consent and Legal Basis

The fundamental distinction: GDPR requires opt-in with 6 lawful bases; CCPA uses opt-out with business purpose exceptions; COPPA requires verifiable parental consent; HIPAA uses authorization with 12 exception categories; FERPA requires written consent with 11 exceptions. The EU AI Act defers consent to GDPR.

| Aspect | GDPR | CCPA/CPRA | COPPA |
|--------|------|-----------|-------|
| Consent model | Opt-in: requires affirmative lawful basis before processing begins. Consent must be freely given, specific, informed, unambiguous | Opt-out: businesses may collect/use PI without prior consent, but consumers can opt out of sale/sharing. Minors under 16 must opt in | Opt-in: verifiable parental consent (VPC) required before collecting, using, or disclosing children's PI. 2025 amendments require separate consent for third-party disclosures |
| Other lawful bases | 6 lawful bases: consent, contract, legal obligation, vital interests, public interest, legitimate interest | Business purpose exceptions for specified operational needs (security, debugging, short-term transient use) | Limited VPC exceptions: internal operations without third-party disclosure; responses to specific child requests; school-authorized educational purposes |
| Special categories | Explicit consent for special category data (health, biometrics, racial/ethnic origin, political opinions, religious beliefs, sexual orientation, genetic data, union membership) | Sensitive PI has additional restrictions: consumers can limit use/disclosure. Includes geolocation, racial/ethnic origin, health, genetics, biometrics, union membership, sexual orientation, SSN, financial accounts, credentials | 2025 amendments: separate VPC required for third-party disclosures. Biometric data added to personal information definition |

| Aspect | HIPAA | FERPA | EU AI Act |
|--------|-------|-------|-----------|
| Consent model | Authorization-based: uses/disclosures of PHI require individual authorization unless a specific exception applies (treatment, payment, healthcare operations, public health, etc.) | Consent-based: prior written consent required for disclosure of education records, unless a specific exception applies (11 enumerated exceptions) | N/A -- no standalone consent framework. Defers to GDPR for personal data processing consent |
| Other lawful bases | 12 categories of permitted uses/disclosures without authorization (treatment, payment, healthcare operations, public health, research with IRB/Privacy Board waiver, etc.) | 11 consent exceptions: school officials with legitimate interest, transfer to other schools, audit/evaluation, financial aid, health/safety emergency, directory information, etc. | N/A -- AI Act obligations (risk assessments, conformity assessments, transparency) are regulatory requirements, not consent-based |
| Special categories | Psychotherapy notes require separate authorization beyond general PHI authorization. Marketing and sale of PHI require specific authorization | Directory information: institutions may designate certain info as directory information and disclose without consent, but must allow opt-out | Prohibited practices (Art. 5) create categories where no consent can authorize use: real-time biometric ID in public spaces, social scoring, emotion recognition in workplace/education |

## Individual Rights

Rights frameworks vary significantly. GDPR provides the most comprehensive set; CCPA/CPRA approaches GDPR-level rights post-CPRA amendments; COPPA centers on parental control; HIPAA provides access and amendment but not deletion; FERPA provides access and amendment but not deletion; the EU AI Act defers most data rights to GDPR.

| Aspect | GDPR | CCPA/CPRA | COPPA |
|--------|------|-----------|-------|
| Access | Right to confirmation and copy of personal data (Art. 15). Response within 1 month | Right to know PI collected, sources, purposes, and third parties. Response within 45 days (extendable to 90) | Parents can request review of child's PI collected by operator |
| Deletion | Right to erasure ("right to be forgotten") with exceptions for legal obligations, public interest (Art. 17) | Right to delete PI with exceptions for legal obligations, security, free speech | Parents can request deletion of child's PI at any time |
| Correction | Right to rectification of inaccurate data without undue delay (Art. 16) | Right to correct inaccurate PI (added by CPRA) | N/A -- parents can request changes but no formal correction right |
| Portability | Right to receive data in structured, machine-readable format and transmit to another controller (Art. 20) | Right to data portability in readily useable format (enhanced by CPRA) | N/A -- no portability right |
| Opt-out / Object | Right to object to processing based on legitimate interest or public interest (Art. 21). Absolute right to object to direct marketing | Right to opt out of sale/sharing. Right to limit use of sensitive PI. Must honor GPC signals | Parents can revoke consent prospectively at any time |
| Additional rights | Restriction of processing (Art. 18). No solely automated decision-making (Art. 22). Complaint to DPA | Non-discrimination for exercising rights. ADMT opt-out effective 2027 | N/A -- focuses on parental control, not individual child rights |

| Aspect | HIPAA | FERPA | EU AI Act |
|--------|-------|-------|-----------|
| Access | Right to access and copy PHI. Response within 30 days (extendable to 60) | Parents (or eligible students 18+) can inspect and review education records. Response within 45 days | Right to explanation of individual AI decisions (Art. 86) |
| Deletion | N/A -- no general deletion right. Covered entities must maintain records for 6 years. Can request amendment of inaccurate records | N/A -- no deletion right. Can request amendment of inaccurate records but not deletion | N/A -- defers to GDPR erasure rights for personal data in AI systems |
| Correction | Right to request amendment of inaccurate/incomplete PHI. Entity may deny; must provide written explanation | Right to request amendment of inaccurate/misleading records. If denied, parent/student may place statement in record | N/A -- defers to GDPR |
| Portability | N/A -- no portability right (21st Century Cures Act promotes health data interoperability separately) | N/A -- no portability right | N/A -- defers to GDPR |
| Opt-out / Object | N/A -- no general opt-out. Can request restrictions but entity not required to agree (limited exceptions) | N/A -- no opt-out beyond consent/exception framework | N/A -- Art. 26 requires human oversight for high-risk AI |
| Additional rights | Accounting of disclosures (non-routine disclosures over 6 years). Confidential communications | Hearing on denied amendment requests. Consent to disclosure (with 11 exceptions) | Complaint to national authority. Fundamental rights impact assessment required for high-risk AI (Art. 27) |

## Enforcement Authority

| Aspect | GDPR | CCPA/CPRA | COPPA |
|--------|------|-----------|-------|
| Primary enforcer | National DPAs in each EU/EEA member state. Lead supervisory authority for cross-border cases | California Privacy Protection Agency (CPPA) -- first dedicated U.S. state privacy agency | Federal Trade Commission (FTC) -- exclusive enforcement authority |
| Secondary enforcement | EDPB coordinates cross-border enforcement, issues binding decisions, consistency opinions | California Attorney General retains concurrent enforcement authority | State AGs may enforce under state UDAP statutes but not directly under COPPA |
| Private right of action | No general private right; member states may provide civil remedies. Data subjects can lodge DPA complaints and seek judicial remedies (Arts. 77-79) | Limited: only for data breaches from failure to implement reasonable security. Statutory damages $100-$750 per consumer per incident | No private right of action. FTC-only enforcement |
| Cross-border coordination | EDPB consistency mechanism, mutual assistance, joint operations, one-stop-shop for cross-border processing | N/A -- California-specific enforcement | N/A -- FTC-only; international cooperation via bilateral agreements |

| Aspect | HIPAA | FERPA | EU AI Act |
|--------|-------|-------|-----------|
| Primary enforcer | Office for Civil Rights (OCR) within HHS | Family Policy Compliance Office (FPCO) within DOE | National competent authorities per member state; EU AI Office for GPAI models |
| Secondary enforcement | State AGs can bring HIPAA actions under HITECH Act. DOJ handles criminal violations | N/A -- FPCO is the sole enforcement body | European AI Board provides guidance. Market surveillance authorities for product-safety aspects |
| Private right of action | No private right for Privacy Rule violations. Limited state-law remedies for wrongful disclosure | No private right of action (Gonzaga v. Doe, 2002). FPCO complaints only | No private right specified. Complaints to national authorities; member states may establish additional remedies |
| Cross-border coordination | N/A -- domestic enforcement only | N/A -- domestic enforcement only | EU AI Board coordinates across member states. AI Office handles cross-border GPAI issues |

## Penalties

| Aspect | GDPR | CCPA/CPRA | COPPA |
|--------|------|-----------|-------|
| Maximum monetary | EUR 20M or 4% of global turnover (Art. 83(5)). Lower tier: EUR 10M or 2% | $7,500 per intentional violation; $2,500 per unintentional. No per-violation cap | $50,120 per violation (inflation-adjusted). No statutory cap; total based on violation count |
| Per-violation basis | Per violation/per data subject. DPAs consider nature, gravity, duration, intent, mitigation, history | $2,500-$7,500 per violation. Children's data carries $7,500 max | Per-violation; FTC aggregates across affected children. Notable: Epic Games $275M (2022), YouTube $170M (2019) |
| Non-monetary | Processing bans, data erasure orders, reprimands, suspension of data flows | Injunctive relief, cease processing orders, consent decrees | Consent decrees, injunctions, 20-year compliance monitoring, independent assessments |

| Aspect | HIPAA | FERPA | EU AI Act |
|--------|-------|-------|-----------|
| Maximum monetary | Tiered: $100-$50K per violation depending on culpability. $1.5M per year per violation category | N/A -- no monetary penalties. Enforcement via federal funding withdrawal | EUR 35M or 7% global turnover for prohibited practices. EUR 15M or 3% for other violations. EUR 7.5M or 1% for incorrect info |
| Per-violation basis | 4 tiers: did not know ($100-$50K), reasonable cause ($1K-$50K), willful neglect corrected ($10K-$50K), willful neglect uncorrected ($50K). Criminal: up to $250K and 10 years | N/A -- funding withdrawal is sole mechanism. In practice, FPCO uses compliance letters; funding has never been withdrawn | Per-violation; scaled by company size with reduced caps for SMEs/startups |
| Non-monetary | Corrective action plans, compliance agreements, exclusion from federal healthcare programs | Compliance letters, corrective action, technical assistance | Market withdrawal orders, recalls, restrictions on placing AI systems on market |

## Breach Notification

GDPR and HIPAA have the most developed breach notification frameworks. CCPA defers to California's separate breach statute. COPPA, FERPA, and the EU AI Act lack standalone breach notification requirements.

| Aspect | GDPR | CCPA/CPRA | COPPA |
|--------|------|-----------|-------|
| To authority | Mandatory within 72 hours of awareness unless unlikely to result in risk (Art. 33) | No CCPA-specific notification. California breach statute (Civ. Code 1798.82) requires AG notification if 500+ residents affected | N/A -- no breach notification requirement. FTC Act Section 5 may apply to inadequate security |
| To individuals | Required when likely high risk to rights/freedoms (Art. 34). Must describe breach, consequences, mitigation | Required under California breach statute for unencrypted PI breaches | N/A |
| Timeline | 72 hours to DPA; without undue delay to individuals when high risk | "Most expedient time possible" under breach statute; no specific hour/day deadline | N/A |
| Threshold | Any personal data breach unless unlikely to cause risk. Risk assessment determines obligation | Breach of unencrypted/unredacted PI (name + SSN, license, financial account, medical info, health insurance, credentials) | N/A |

| Aspect | HIPAA | FERPA | EU AI Act |
|--------|-------|-------|-----------|
| To authority | Mandatory within 60 days to HHS. Breaches affecting 500+ reported immediately; smaller breaches reported annually | N/A -- no breach notification requirement | N/A -- defers to GDPR when personal data involved |
| To individuals | Required within 60 days for breaches involving 500+ individuals in a state | N/A | N/A -- defers to GDPR |
| Timeline | 60 days from discovery. Media notification if 500+ in single state | N/A | N/A |
| Threshold | Breach of "unsecured PHI" -- PHI not rendered unusable/unreadable via encryption or destruction per HHS guidance | N/A | N/A |

## International Transfers

GDPR has the most developed international transfer framework. Most other regulations either lack transfer provisions (sector/age-specific scope) or use market access rules (EU AI Act).

| Aspect | GDPR | CCPA/CPRA | COPPA |
|--------|------|-----------|-------|
| Transfer mechanism | Chapter V: adequacy decisions, SCCs, BCRs, derogations (Art. 49) | N/A -- no international transfer restrictions. Contracts apply regardless of location | N/A -- applies regardless of operator location but does not regulate cross-border flows |
| Key frameworks | EU-U.S. DPF (2023), SCCs (2021), adequacy decisions, BCRs | N/A | N/A |
| Restrictions | Non-adequate countries require safeguards. Schrems II invalidated Privacy Shield; DPF replaced it. Transfer impact assessments recommended | N/A | N/A |

| Aspect | HIPAA | FERPA | EU AI Act |
|--------|-------|-------|-----------|
| Transfer mechanism | N/A -- sector-specific with no cross-border mechanism. BAAs apply regardless of BA location | N/A -- applies to DOE-funded institutions, primarily domestic | Market access rules: compliance required if AI output used in EU, regardless of provider location |
| Key frameworks | N/A | N/A | Mutual recognition for AI standards. International cooperation for GPAI governance |
| Restrictions | N/A | N/A | Non-EU providers must appoint authorized EU representative for high-risk systems |

## Children's Provisions

COPPA provides the most comprehensive children's protection. GDPR establishes age-based consent thresholds. CCPA/CPRA requires opt-in for minors under 16. HIPAA and FERPA address children through their sector-specific frameworks (health and education respectively). The EU AI Act prohibits exploitation of children's vulnerabilities.

| Aspect | GDPR | CCPA/CPRA | COPPA |
|--------|------|-----------|-------|
| Age threshold | Art. 8: member states set 13-16 for information society services. Default: 16 (UK/Ireland: 13, Germany: 16, France: 15) | Under 16 must opt in before sale/sharing. Under 13 require parental consent for opt-in | Under 13: comprehensive protection with age verification and parental consent framework |
| Consent mechanism | Parental consent for children below threshold when processing based on consent. Reasonable efforts to verify | Opt-in authorization before sale/sharing. No specific mechanism. Must not sell/share under-16 PI without authorization | VPC via FTC-approved methods: signed form, credit card, video call, government ID, knowledge-based questions. 2025: biometric methods added |
| Specific protections | Data protection by design must consider children. DPIA for large-scale children's data processing. Erasure right particularly for childhood data | Delete functionality for children's accounts. Dark pattern prohibitions protect minors. ADMT opt-out (2027) covers minor profiling | Notice, data minimization, retention limits, security, safe harbor programs, prohibition on conditioning participation on unnecessary collection. 2025: biometric protections, retention caps |

| Aspect | HIPAA | FERPA | EU AI Act |
|--------|-------|-------|-----------|
| Age threshold | N/A -- no age-based protections. State laws govern minor consent for healthcare, affecting PHI access | Rights transfer at 18 or postsecondary enrollment. Parents hold rights for minor students | Prohibited: AI exploiting age-based vulnerabilities (Art. 5(1)(b)). Emotion recognition banned in educational settings |
| Consent mechanism | N/A -- defers to state law on minor consent for treatment | Written parental consent for disclosure. Transfers to eligible student at 18 | N/A -- defers to GDPR for children's data consent in AI |
| Specific protections | N/A -- no child-specific provisions beyond general PHI protections | Transfer disclosures, health/safety emergency disclosures. Directory information opt-out exercised by parents | FRIAs (Art. 27) must assess impact on children when high-risk AI deployed in education/childcare |

---

*This file provides cross-regulation comparison tables. For individual regulation details, load the corresponding regulation reference file (e.g., gdpr-reference.md, ccpa-reference.md). For timeline and date information, load reg-timeline.md.*
