# HIPAA -- Quick Reference

> **Last verified:** March 2026. Consult the [HHS HIPAA page](https://www.hhs.gov/hipaa/index.html) for current regulations, guidance, and enforcement actions.

## Overview

The Health Insurance Portability and Accountability Act (HIPAA) was enacted in 1996. The HIPAA Privacy Rule, issued by the Department of Health and Human Services (HHS), took effect on April 14, 2003. HIPAA protects individually identifiable health information -- known as Protected Health Information (PHI) -- held by covered entities and their business associates.

HIPAA is a **sector-specific** regulation: it applies to healthcare, not to all industries. It governs health plans, healthcare clearinghouses, and healthcare providers who conduct standard electronic transactions, as well as their business associates. Consumer health apps, wearable fitness devices, and direct-to-consumer genetic testing services that do not involve covered entities are generally outside HIPAA's scope -- a significant gap in the current health data privacy landscape.

The HIPAA framework includes multiple rules: the Privacy Rule (governs uses and disclosures of PHI), the Security Rule (technical/administrative/physical safeguards for electronic PHI), the Breach Notification Rule (notification requirements after a breach of unsecured PHI), and the Enforcement Rule (investigation and penalty procedures). This reference focuses on the **Privacy Rule** while noting other rules where relevant.

**Key dates:**

| Event | Date |
|-------|------|
| HIPAA enacted | August 21, 1996 |
| Privacy Rule effective | April 14, 2003 |
| Security Rule effective | April 20, 2005 |
| HITECH Act enacted (expanded enforcement) | February 17, 2009 |
| Omnibus Rule effective (BA direct liability) | September 23, 2013 |
| Reproductive health privacy amendments finalized | April 26, 2024 |
| Reproductive health amendments partially vacated | June 2025 |
| Security Rule modernization NPRM published | December 27, 2024 |

## Key Provisions

### Protected Health Information (PHI)

PHI is individually identifiable health information that is:

- Created or received by a healthcare provider, health plan, employer, or healthcare clearinghouse
- Relates to the past, present, or future physical or mental health condition of an individual; the provision of healthcare to an individual; or the past, present, or future payment for provision of healthcare to an individual
- Identifies the individual or provides a reasonable basis to identify the individual
- Transmitted or maintained in any form or medium -- electronic, paper, or oral

PHI excludes: employment records held by a covered entity in its capacity as employer, education records covered by FERPA, and records of persons deceased for more than 50 years.

### Covered Entities

HIPAA applies to three categories of covered entities:

1. **Health plans:** Individual and group health insurance plans, HMOs, Medicare, Medicaid, long-term care insurance, employer-sponsored group health plans, church-sponsored health plans, and multi-employer health plans. Health plans with fewer than 50 participants administered solely by the employer are exempt.

2. **Healthcare clearinghouses:** Entities that process nonstandard health information received from another entity into a standard format (or vice versa). Clearinghouses include billing services, repricing companies, community health management information systems, and value-added networks.

3. **Healthcare providers:** Any provider of medical or health services (as defined in 42 USC 1395x(s)) and any person or organization that furnishes, bills, or is paid for healthcare in the normal course of business -- **if** they transmit health information in electronic form in connection with a standard transaction (claims, eligibility inquiries, referral authorizations, etc.).

### Business Associates

A business associate is a person or entity (other than a member of the covered entity's workforce) that:

- Performs or assists in performing a function or activity on behalf of a covered entity involving the use or disclosure of PHI, or
- Provides certain services to or for a covered entity involving PHI access (legal, actuarial, accounting, consulting, data aggregation, management, accreditation, financial services)

Since the HITECH Act and the 2013 Omnibus Rule, business associates are **directly liable** under HIPAA for compliance with applicable Privacy Rule and Security Rule provisions. Subcontractors of business associates that access PHI are also considered business associates.

### Minimum Necessary Standard

Covered entities must make reasonable efforts to limit PHI uses, disclosures, and requests to the **minimum necessary** to accomplish the intended purpose. This applies to:

- Internal uses of PHI by the covered entity's workforce
- Disclosures to and requests from other covered entities and business associates
- Requests by the covered entity to other covered entities

**Exceptions to minimum necessary:** Disclosures to or requests by a healthcare provider for treatment purposes, disclosures to the individual who is the subject of the information, disclosures authorized by the individual, disclosures to HHS for enforcement, uses or disclosures required by law, and uses or disclosures required for HIPAA compliance.

### Treatment, Payment, and Operations (TPO)

PHI may be used and disclosed for Treatment, Payment, and Healthcare Operations (TPO) **without individual authorization.** This is the primary operational exception and covers the vast majority of routine healthcare data flows:

- **Treatment:** Provision, coordination, or management of healthcare and related services
- **Payment:** Healthcare billing, claims management, medical data processing, utilization review, coverage determinations
- **Operations:** Quality assessment, competency assurance, performance evaluation, protocol development, business planning, customer service, resolution of grievances, legal compliance

### De-identification

HIPAA provides two methods for de-identifying PHI, after which the data is no longer PHI and no longer subject to HIPAA:

1. **Safe Harbor method:** Remove all 18 specified identifiers (names, geographic data smaller than state, dates more specific than year for ages over 89, phone/fax numbers, email, SSN, medical record numbers, health plan beneficiary numbers, account numbers, certificate/license numbers, vehicle identifiers, device identifiers, URLs, IP addresses, biometric identifiers, full-face photos, and any other unique identifying number) and the covered entity has no actual knowledge that the remaining information can identify an individual.

2. **Expert Determination method:** A qualified statistical or scientific expert determines that the risk of identifying an individual from the information is very small, applying generally accepted statistical and scientific principles and methods. The expert must document methods and results.

## Patient Rights

The HIPAA Privacy Rule grants individuals the following rights regarding their PHI:

1. **Right of access:** Individuals may request access to their PHI maintained in a designated record set. Covered entities must provide access within **30 days** of the request (one 30-day extension permitted with written explanation). Access may be provided in the format requested if readily producible. Reasonable cost-based fees may be charged.

2. **Right to amendment:** Individuals may request amendment of PHI they believe is inaccurate or incomplete. Covered entities must act on the request within **60 days** (one 30-day extension permitted). If the request is denied, the covered entity must provide a written denial with the basis for denial.

3. **Right to an accounting of disclosures:** Individuals may request an accounting of disclosures of their PHI made in the 6 years prior to the request. Excludes disclosures for TPO, to the individual, pursuant to authorization, for national security/intelligence, to correctional institutions, and incident to permitted disclosures.

4. **Right to request restrictions:** Individuals may request restrictions on uses and disclosures of their PHI for treatment, payment, or operations. Covered entities are **not required to agree** to requested restrictions -- with one exception: a covered entity **must** agree to restrict disclosure to a health plan if the PHI pertains to a healthcare item/service paid for in full out of pocket.

5. **Right to confidential communications:** Individuals may request that communications of PHI be made by alternative means or at alternative locations (e.g., send correspondence to a work address rather than home address). Health plans must accommodate reasonable requests; providers must accommodate requests if reasonable.

6. **Right to notice of privacy practices:** Covered entities must provide a Notice of Privacy Practices (NPP) describing how PHI is used and disclosed, the individual's rights, and the entity's legal duties. Providers with direct treatment relationships must make a good-faith effort to obtain written acknowledgment of receipt.

7. **Right to file a complaint:** Individuals may file complaints about Privacy Rule violations with the covered entity or directly with the HHS Office for Civil Rights (OCR).

## Business Associate Requirements

### Business Associate Agreements (BAAs)

A covered entity must enter into a BAA with each business associate before sharing PHI. The BAA must:

- Specify the permitted and required uses and disclosures of PHI
- Require the business associate to use appropriate safeguards (including implementing Security Rule requirements for electronic PHI)
- Require the business associate to report breaches of unsecured PHI
- Require the business associate to ensure any subcontractors that create or receive PHI agree to the same restrictions
- Authorize termination of the contract if the business associate violates a material term

### Direct Liability

Since the HITECH Act (2009) and the 2013 Omnibus Rule, business associates are directly liable for:

- Impermissible uses and disclosures of PHI
- Failure to provide breach notification to the covered entity
- Failure to provide access to PHI to the covered entity, individual, or HHS
- Failure to disclose PHI to HHS during investigations
- Failure to comply with applicable Security Rule requirements

Business associates face the same civil and criminal penalty tiers as covered entities.

## Enforcement and Penalties

### Enforcement Authority

HIPAA is enforced by the **HHS Office for Civil Rights (OCR)**. OCR investigates complaints, conducts compliance reviews, and resolves violations through voluntary corrective action or civil monetary penalties.

State attorneys general may also bring civil actions on behalf of state residents for HIPAA violations (authority granted by HITECH Act). The DOJ handles criminal prosecutions for knowing violations.

### Penalty Structure (2026 Inflation-Adjusted)

HIPAA penalties follow a four-tier structure:

| Tier | Culpability Level | Per Violation | Annual Cap |
|------|------------------|---------------|------------|
| 1 | Did not know (and would not have known with reasonable diligence) | $141 -- $71,162 | $35,581 |
| 2 | Reasonable cause (not willful neglect) | $1,424 -- $71,162 | $142,355 |
| 3 | Willful neglect, corrected within 30 days | $14,232 -- $71,162 | $355,808 |
| 4 | Willful neglect, not corrected | $71,162 minimum | $2,134,483 |

**Criminal penalties** for knowing violations:

| Level | Penalty |
|-------|---------|
| Knowing violation | Fine up to $50,000 and/or up to 1 year imprisonment |
| Under false pretenses | Fine up to $100,000 and/or up to 5 years imprisonment |
| Intent to sell/use for personal gain | Fine up to $250,000 and/or up to 10 years imprisonment |

### Resolution Mechanisms

OCR may resolve cases through:

- **Technical assistance:** For minor or inadvertent violations
- **Voluntary corrective action plans:** Entity agrees to remediate without monetary penalty
- **Resolution agreements:** Settlement with monetary payment and corrective action plan
- **Civil monetary penalties:** Imposed after formal hearing process (appealable)
- **Referral to DOJ:** For potential criminal violations

## Key Enforcement Milestones

1. **Anthem Inc. -- $16M (2018).** Largest HIPAA settlement in history. Data breach compromised electronic PHI of approximately 78.8 million individuals. OCR found Anthem failed to conduct an enterprise-wide risk analysis, had insufficient procedures to regularly review information system activity, and failed to identify and respond to security incidents.

2. **Montefiore Medical Center -- $4.75M (2024).** OCR settlement for insider threat case where an employee stole PHI of approximately 12,500 patients over six months. OCR found the hospital failed to analyze risks to electronic PHI, implement appropriate access controls, and review information system activity records.

3. **Solara Medical Supplies -- $3M (2025).** OCR settlement for phishing attack that compromised PHI of more than 114,000 individuals. OCR found Solara failed to conduct an adequate risk analysis, implement security measures sufficient to reduce risks, and failed to provide timely breach notification.

4. **Banner Health -- $1.25M (2023).** OCR settlement for 2016 cyberattack affecting approximately 2.81 million individuals. OCR found Banner Health failed to conduct an enterprise-wide risk analysis as required by the Security Rule.

5. **OCR Right of Access Initiative (2019-ongoing).** OCR has settled over 45 cases enforcing individuals' right to access their PHI in a timely manner. Settlements range from $3,500 to $240,000, establishing that delays in providing records are an enforcement priority.

## Recent Developments

- **Reproductive health privacy amendments (uncertain status):** HHS finalized amendments in April 2024 prohibiting the use or disclosure of PHI to investigate or impose liability for lawful reproductive healthcare. A federal court partially vacated these amendments in June 2025. The status remains uncertain pending further litigation or rulemaking.

- **Security Rule modernization (proposed December 27, 2024):** HHS proposed comprehensive updates to the Security Rule. Key proposals include mandatory encryption of electronic PHI at rest and in transit, multi-factor authentication, network segmentation, vulnerability scanning every 6 months, penetration testing annually, and a 72-hour restoration requirement for critical systems. If finalized (expected ~May 2026), these would represent the most significant Security Rule update since 2013.

- **OCR Risk Analysis Initiative (launched fall 2024):** OCR announced a targeted enforcement initiative focused on covered entities and business associates that have never conducted an enterprise-wide risk analysis -- the most commonly cited HIPAA violation. The initiative uses proactive outreach and complaint-driven investigations.

- **Right of access enforcement continues:** OCR continues active enforcement of the patient right of access, with multiple settlements per year and increasing penalty amounts for repeat or egregious access violations.

- **State health privacy laws:** Several states have enacted comprehensive health data privacy laws that go beyond HIPAA, covering consumer health data outside the covered entity framework (e.g., Washington's My Health My Data Act, Connecticut health data provisions). These create overlapping obligations for entities handling health-related data.

## Compliance Essentials

A practitioner checklist for HIPAA Privacy Rule compliance:

1. **Risk analysis conducted and documented (enterprise-wide, not just IT).** The most commonly cited HIPAA violation. Must cover all electronic PHI in all systems across the organization, assess threats and vulnerabilities, and document the analysis.

2. **Notice of Privacy Practices current and available.** NPP must describe uses/disclosures of PHI, patient rights, and entity's duties. Must be provided at first service delivery and posted prominently.

3. **BAAs in place with every business associate before PHI sharing.** Verify that BAAs are executed with all vendors, contractors, and subcontractors that access PHI. Review and update BAAs periodically.

4. **Minimum necessary standard applied to all uses and disclosures.** Implement policies defining who in the workforce needs access to what categories of PHI, and role-based access controls. Review access levels regularly.

5. **Workforce training on PHI handling completed and documented.** Train all workforce members (employees, volunteers, trainees) on HIPAA policies and procedures. Document training completion and provide periodic refresher training.

6. **Breach notification procedures operational.** Individual notification within **60 days** of discovery. HHS notification: annually for breaches affecting fewer than 500 individuals, within 60 days for breaches affecting 500 or more. Media notification required for breaches affecting 500+ individuals in a state/jurisdiction.

7. **Patient rights processes operational.** Procedures for access requests (30-day response), amendment requests (60-day response), accounting of disclosures, restriction requests, and confidential communications. Track and document all requests and responses.

8. **Policies and procedures documented and retained for 6 years.** HIPAA requires covered entities and business associates to maintain all required policies, procedures, and documentation for 6 years from the date of creation or the date last in effect, whichever is later.

---

*This reference file is part of the /privacy skill knowledge base. It provides practitioner-level HIPAA privacy provisions coverage and is loaded when queries mention HIPAA, PHI, protected health information, covered entities, business associates, or health privacy.*
