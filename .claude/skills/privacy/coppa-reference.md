# COPPA -- Quick Reference

> **Last verified:** March 2026. Consult the [FTC COPPA page](https://www.ftc.gov/legal-library/browse/rules/childrens-online-privacy-protection-rule-coppa) for current rule text and enforcement guidance.

## Overview

The Children's Online Privacy Protection Act (COPPA) was enacted in 1998 and implemented through the FTC's COPPA Rule, which took effect in April 2000. The Rule was significantly amended in 2013 to address mobile apps, social networking, and behavioral advertising, and again in January 2025 with amendments that expand the definition of personal information, impose data retention limits, and require separate consent for third-party disclosures.

COPPA protects the online privacy of children under 13 by requiring operators of commercial websites, online services (including mobile apps and connected devices), and third-party plug-in operators to obtain verifiable parental consent before collecting, using, or disclosing children's personal information. The statute is enforced exclusively by the FTC; there is no private right of action.

**Key dates:**

| Event | Date |
|-------|------|
| COPPA enacted | October 21, 1998 |
| Original COPPA Rule effective | April 21, 2000 |
| First major Rule amendment (FTC) | July 1, 2013 |
| 2025 Rule amendments finalized | January 16, 2025 |
| 2025 amendments effective | June 23, 2025 |
| Compliance deadline (existing operators) | April 22, 2026 |

## Key Provisions

### Scope and Applicability

COPPA applies to:

- **Operators of commercial websites or online services directed to children under 13.** A site or service is "directed to children" based on its subject matter, visual content, use of animated characters, child-oriented activities, music, age of models, advertising presence, and other indicators. A site need not be exclusively for children -- mixed-audience sites that target children as one segment are covered.
- **Operators of general audience websites or online services with actual knowledge that they are collecting personal information from children under 13.** Actual knowledge includes information provided by the user (e.g., date of birth indicating age under 13) or notification from a parent or other credible source.
- **Third-party plug-in operators** (e.g., advertising networks, analytics providers) that collect personal information through child-directed sites, where the plug-in operator knows or has reason to know the site is directed to children.

COPPA does not apply to nonprofit organizations (unless they operate for commercial purposes) or to entities outside FTC jurisdiction (common carriers, banks, insurance companies, airlines regulated by other federal agencies).

### Mixed-Audience Sites

Sites and services that are not directed primarily to children but that have a separate children's section or area are treated as child-directed with respect to that section. General audience sites that age-gate and block collection from users who indicate they are under 13 are not subject to COPPA for users who pass the age gate -- but the age gate must not encourage users to falsify their age. The FTC has taken the position that age gates asking only "Are you over 13? [Yes/No]" may be insufficient if the design encourages false responses.

### Personal Information Definition

Personal information under COPPA includes:

- Full name, home address, email address, telephone number
- Social Security number
- Screen name or user name that functions as online contact information
- Persistent identifiers (cookies, device IDs, IP addresses) when used to recognize a user over time and across sites -- except when used solely for internal operations
- Photograph, video, or audio file containing a child's image or voice
- Geolocation information sufficient to identify a street name and city
- **Biometric identifiers** (added January 2025): fingerprints, retinal or iris scans, facial geometry, voiceprints, and other data generated from measurements of biological characteristics used to identify an individual
- **Government-issued identification numbers** (added January 2025)

The definition is intentionally broad. Operators should assess all data elements collected against this list, including data collected passively through SDKs, cookies, and device sensors.

### Verifiable Parental Consent (VPC)

Operators must obtain verifiable parental consent before collecting, using, or disclosing a child's personal information. Approved VPC methods include:

- Signed paper consent form returned by mail, fax, or electronic scan
- Credit card, debit card, or other online payment transaction (with notification that the card was charged)
- Toll-free telephone call or video conference staffed by trained personnel
- Government-issued ID checked against a database, provided the ID is deleted promptly after verification
- Knowledge-based authentication challenge (questions only likely answered by the parent)
- Face-matching technology comparing a parent's photo ID to a live image (added 2013)

The FTC may approve additional consent methods through applications from operators or industry groups.

**Consent exceptions (limited):**

- **Internal operations exception:** Operators may collect persistent identifiers without parental consent when used solely for support of internal operations (maintaining/analyzing site function, performing network communications, protecting security/integrity, serving contextual advertising). The operator must not contact the child or enable third-party contact.
- **One-time contact exception:** Operators may collect a child's email address without parental consent for the sole purpose of responding directly to a one-time request from the child. The email must be deleted after responding.
- **Multiple contact exception (with parental notification):** Operators may collect a child's email for ongoing contact (e.g., newsletter) if they notify a parent and provide an opt-out mechanism. The parent must be given the opportunity to stop the contact before the second communication.

### 2025 Rule Amendments

The FTC finalized major COPPA Rule amendments on January 16, 2025. Key changes:

- **Separate consent for third-party disclosures:** Operators can no longer bundle consent for their own collection with consent for disclosing children's PI to third parties. Parents must provide separate, affirmative consent specifically for third-party disclosures.
- **Data retention limits:** Operators must retain children's personal information only for as long as reasonably necessary to fulfill the purpose for which it was collected. When the information is no longer needed, operators must delete it.
- **Expanded personal information definition:** Biometric identifiers and government-issued identification numbers are now covered (see above).
- **Safe harbor program transparency:** FTC-approved self-regulatory programs must publicly disclose their membership lists. Programs must also submit revised guidelines to the FTC for review.
- **Effective date:** June 23, 2025.
- **Compliance deadline for existing operators:** April 22, 2026.

## Operator Obligations

### Notice Requirements

- **Online notice (posted on website/service):** Must include a description of what personal information is collected, how it is used, and the operator's disclosure practices. Must link to a complete privacy policy.
- **Direct notice to parents:** Before collecting a child's personal information, operators must provide direct notice to the parent that includes: what information will be collected, how it will be used, a description of parental rights, and a means for the parent to provide or refuse consent.
- **Privacy policy content requirements:** The operator's privacy policy must include: a list of all operators collecting or maintaining children's PI through the site/service, a description of what information is collected, how information is used and whether it is disclosed to third parties, a description of parental rights, and the name and contact information of a designated operator to handle inquiries.

### Data Collection and Use

- **Data minimization:** Operators may not condition a child's participation in an activity on the disclosure of more personal information than is reasonably necessary for participation.
- **Data security:** Operators must establish and maintain reasonable procedures to protect the confidentiality, security, and integrity of children's personal information.
- **Data retention limits (2025):** Personal information must be retained only as long as reasonably necessary to fulfill the purpose for which it was collected. Operators must delete information when it is no longer needed.
- **Internal operations exception:** Persistent identifiers used solely for support of internal operations (e.g., contextualizing content, frequency capping, legal compliance, site analysis) do not require parental consent, but the operator must not contact the child or enable contact.

### Parental Rights

- Parents may review personal information collected from their child
- Parents may request deletion of their child's personal information
- Parents may refuse to permit further collection or use
- Parents may revoke consent at any time
- Operators must respond to parental requests within a reasonable time

### Record-Keeping Obligations

Operators must maintain records of:
- Each individual consent provided by a parent (or documentation of consent method used)
- All notices sent to parents
- For at least 3 years: date, content, and recipients of direct notices; each parental consent and its scope; responses to parental access/deletion requests

Operators must also make these records available to the FTC upon request.

## Safe Harbor Programs

The FTC approves industry self-regulatory programs ("safe harbor programs") that implement protective guidelines meeting or exceeding COPPA Rule requirements. Operators participating in an approved safe harbor program are subject to the program's disciplinary procedures in lieu of direct FTC enforcement -- provided the operator complies with the program's guidelines.

**Currently approved safe harbor programs include:**
- CARU (Children's Advertising Review Unit) Safe Harbor Program
- ESRB Privacy Certified (Entertainment Software Rating Board)
- kidSAFE Seal Program
- Aristotle/PRIVO

**2025 transparency requirements:**
- Programs must publicly disclose their complete membership lists
- Programs must submit revised self-regulatory guidelines to the FTC (deadline: October 2025)
- Programs must report enforcement actions to the FTC
- Programs face revocation if they fail to enforce their guidelines effectively

**Benefits of safe harbor participation:**
- Regulatory shelter: compliance with the safe harbor program's guidelines serves as a complete defense against FTC enforcement of the COPPA Rule
- Guidance and updates: programs provide compliance guidance and interpretive support
- Consumer trust signal: membership may serve as a trust indicator for parents
- Pre-review: some programs pre-review operators' practices, catching issues before FTC scrutiny

## Enforcement and Penalties

### Enforcement Authority

COPPA is enforced exclusively by the Federal Trade Commission under Section 5 of the FTC Act. State attorneys general may also bring enforcement actions for violations occurring within their states.

There is **no private right of action** under COPPA. Individual consumers cannot sue operators directly for COPPA violations.

### Penalty Structure

- Civil penalties of up to **$53,088 per violation** (2024 inflation-adjusted amount; adjusted annually). Each instance of collecting personal information from a child without compliant consent may constitute a separate violation.
- The FTC may seek **injunctive relief** requiring operators to change practices, implement compliance programs, or delete improperly collected information.
- The FTC may refer matters to the Department of Justice for civil litigation.
- **State AG enforcement:** State attorneys general have independent authority to enforce COPPA on behalf of their residents. Several states have pursued COPPA actions alongside or independently from FTC enforcement.
- **Consent order provisions:** FTC consent orders frequently require operators to implement comprehensive privacy programs, submit to independent audits for 20 years, and delete improperly collected data.

## Key Enforcement Milestones

1. **Epic Games / Fortnite -- $275M (2022).** Largest COPPA penalty in history. FTC alleged Epic collected personal information from children under 13 without parental consent, used manipulative dark patterns, and failed to provide required COPPA notices. Consent order also required Epic to adopt strong privacy protections and default settings for young users.

2. **Google/YouTube -- $170M (2019).** FTC and New York AG jointly alleged YouTube illegally collected persistent identifiers (cookies) from viewers of child-directed channels to deliver targeted advertising. YouTube settled and implemented a system requiring channel operators to designate content as child-directed.

3. **Disney -- $10M (2025).** Disney subsidiary agreed to pay $10M to settle FTC allegations of collecting children's personal information through advertising on YouTube child-directed content without verifiable parental consent.

4. **Musical.ly (TikTok) -- $5.7M (2019).** FTC alleged Musical.ly collected names, email addresses, and other personal information from children under 13 without parental consent. At the time, this was the largest COPPA civil penalty.

5. **Apitor Technology -- $500K suspended (2024).** FTC alleged Apitor, through a Chinese third-party service provider, collected geolocation data from children without parental consent via a robot-building app. The case highlighted supply chain liability and third-party service provider responsibilities.

## Recent Developments

- **January 16, 2025:** FTC finalized comprehensive COPPA Rule amendments (see 2025 Rule Amendments section above).
- **June 23, 2025:** Amended COPPA Rule takes effect.
- **April 22, 2026:** Compliance deadline for existing operators to conform to the 2025 amendments.
- **Expanded enforcement posture:** The FTC has increasingly pursued large COPPA penalties, with the Epic Games settlement signaling willingness to impose nine-figure fines for egregious violations involving dark patterns.
- **Ed-tech scrutiny:** Growing FTC attention to education technology platforms collecting children's information, particularly where parental consent mechanisms are unclear.
- **Connected devices and IoT:** Smart toys and connected children's devices remain an enforcement priority, with the FTC monitoring compliance across product categories that interact with children.
- **State-level children's privacy legislation:** Multiple states have enacted or proposed children's privacy laws that go beyond COPPA, including California's Age-Appropriate Design Code Act (AADC), which applies age-appropriate data protections for users under 18, and other state-level age verification and design code requirements. These complement but do not preempt COPPA.
- **Interaction with proposed federal legislation:** Various federal proposals (e.g., COPPA 2.0, Kids Online Safety Act) have sought to raise the COPPA age threshold to 16 or 17 and impose additional requirements on platforms. As of March 2026, COPPA's age-13 threshold remains in effect.

## Common Compliance Challenges

Practitioners frequently encounter these COPPA-specific compliance challenges:

- **Determining "directed to children" status:** The multi-factor test for whether a site or service is directed to children involves subjective judgment. Operators of content platforms, gaming services, and educational apps must evaluate their audience composition carefully. The FTC considers totality of circumstances, not any single factor.
- **Third-party SDK and plug-in liability:** Operators are responsible for the data collection practices of third-party code (SDKs, plug-ins, analytics tools) embedded in their child-directed sites or services. The 2025 amendments heighten this obligation by requiring separate consent for third-party disclosures, meaning operators must audit all third-party data flows.
- **Age verification versus age-gating:** COPPA does not require operators to verify age proactively. Operators of general audience sites can use a neutral age gate to screen users, but the mechanism must not be designed to encourage false age declarations. Age verification for VPC is a separate requirement that applies only after a child is identified.
- **School-context COPPA compliance:** When ed-tech platforms serve both school and home contexts, COPPA compliance overlaps with FERPA. Schools may consent on behalf of parents for educational purposes, but the scope is limited to the educational context. Home use of the same platform reverts to standard COPPA consent requirements.
- **International application:** COPPA applies to foreign-based operators who operate sites or services directed to children in the United States or who have actual knowledge of collecting personal information from U.S. children. The FTC has pursued enforcement against non-U.S. companies.
- **Persistent identifier management:** Determining when a persistent identifier is used for "internal operations" (exempt from consent) versus "recognizing a user over time" (requires consent) requires careful technical and legal analysis of actual data flows and purposes.

## Compliance Essentials

A practitioner checklist for COPPA compliance:

1. **Age gate or actual knowledge mechanism operational.** Determine whether your service is child-directed or whether you have actual knowledge of child users, and implement appropriate screening.
2. **Verifiable parental consent obtained before ANY collection.** Use an FTC-approved VPC method before collecting, using, or disclosing personal information from children under 13.
3. **Direct notice to parents includes all required disclosures.** Provide clear, complete direct notice describing what information is collected, how it is used, and the parent's rights -- before seeking consent.
4. **Separate consent for third-party disclosures (2025 requirement).** Do not bundle consent for your own data use with consent for sharing children's personal information with third parties. Obtain distinct, affirmative consent for each.
5. **Data retention limited to reasonable necessity.** Retain children's personal information only as long as reasonably necessary for the purpose collected. Implement deletion procedures for information no longer needed (2025 requirement).
6. **Data security measures reasonable and appropriate.** Establish and maintain reasonable procedures to protect the confidentiality, security, and integrity of children's personal information.
7. **Safe harbor program membership current and publicly disclosed (if participating).** If your organization participates in an FTC-approved safe harbor program, ensure membership is current, guidelines are followed, and membership is publicly disclosed per 2025 transparency requirements.

---

*This reference file is part of the /privacy skill knowledge base. It provides practitioner-level COPPA coverage and is loaded when queries mention COPPA, children's online privacy, parental consent requirements, or child-directed services.*
