# EU AI Act -- Quick Reference (Privacy Lens)

> **Last verified:** March 2026. Consult the [EU AI Act Service Desk](https://digital-strategy.ec.europa.eu/en/policies/european-approach-artificial-intelligence), [EDPB guidance](https://www.edpb.europa.eu/), and individual Member State competent authority publications for current implementation details and national transposition measures.

> **Scope note:** This file covers the EU AI Act from a privacy and data protection perspective. It focuses on provisions that intersect with personal data processing, biometrics, and data protection. For the full scope of AI safety, liability, general-purpose AI model evaluation, product safety, and regulatory sandbox provisions, consult the full regulation text (Regulation (EU) 2024/1689).

---

## Overview

The **EU AI Act** (Regulation (EU) 2024/1689) is the world's first comprehensive legal framework for artificial intelligence. Adopted in June 2024 and entered into force on **August 1, 2024**, it establishes a horizontal, risk-based regulatory framework for AI systems placed on the market, put into service, or used within the EU. The regulation applies regardless of where the AI provider is established, provided the AI system's output is used within the EU (extraterritorial scope similar to GDPR).

For privacy practitioners, the AI Act matters because many AI systems process personal data, and the regulation creates new obligations that run in parallel with -- and complement -- existing GDPR requirements. The Act introduces prohibited practices targeting biometric surveillance, emotion recognition, and social scoring; imposes data governance requirements on training datasets; requires fundamental rights impact assessments for high-risk AI; and designates data protection authorities as potential enforcement bodies. Understanding the AI Act's privacy-relevant provisions is essential for any organization deploying AI systems that touch personal data in the EU.

---

## Prohibited Practices (Privacy-Relevant)

**Effective: February 2, 2025** -- these prohibitions are already enforceable.

The following AI practices are banned under Article 5 of the AI Act. All listed prohibitions have direct privacy and data protection implications:

### Biometric Prohibitions

- **Real-time remote biometric identification in publicly accessible spaces:** Prohibited for law enforcement purposes except under narrow exceptions requiring prior judicial authorization (imminent threat of terrorist attack, search for specific victims of crime, prosecution of serious criminal offences listed in Annex II). Non-law-enforcement real-time remote biometric identification in public spaces is prohibited without exception.
- **Untargeted facial image scraping:** Building or expanding facial recognition databases through untargeted scraping of facial images from the internet or CCTV footage is prohibited outright, with no exceptions.
- **Biometric categorization using sensitive characteristics:** AI systems that categorize natural persons based on biometric data to deduce or infer race, political opinions, trade union membership, religious or philosophical beliefs, sex life, or sexual orientation are prohibited. Exception: labeling or filtering of lawfully acquired biometric datasets in the context of law enforcement.

### Behavioral and Surveillance Prohibitions

- **Emotion recognition in workplace and educational settings:** AI systems that infer emotions of natural persons in the workplace or educational institutions are prohibited. Exception: systems deployed for medical or safety purposes (e.g., monitoring a pilot's fatigue level).
- **Social scoring by public authorities:** AI systems used by public authorities (or on their behalf) to evaluate or classify natural persons based on social behavior or personal characteristics, leading to detrimental or unfavorable treatment, are prohibited.
- **Subliminal, manipulative, or exploitative techniques:** AI systems deploying subliminal techniques beyond a person's consciousness, or exploiting vulnerabilities related to age, disability, or socioeconomic situation, to materially distort behavior in a way that causes significant harm.

> **Practitioner note:** The biometric prohibitions (facial image scraping, biometric categorization, real-time remote biometric ID) are the most directly relevant to data protection work. Organizations processing biometric data through AI systems should conduct an immediate audit against Article 5 prohibitions.

---

## Risk Classification (Privacy-Relevant Categories)

The AI Act classifies AI systems into risk tiers. The following high-risk categories under **Annex III** are most relevant to privacy practitioners because they involve systematic processing of personal data:

### High-Risk AI Systems (Annex III) -- Privacy-Relevant

**Effective: August 2, 2026** for Annex III systems.

| Category | Examples | Privacy Relevance |
|----------|----------|-------------------|
| **Biometric identification and categorization** | Facial recognition, fingerprint matching, voice recognition, gait analysis | Direct processing of biometric personal data (GDPR Article 9 special category) |
| **Critical infrastructure management** | AI managing energy, water, transport, digital networks | Personal data processed in service delivery and safety monitoring |
| **Education and vocational training** | Student assessment, admissions scoring, learning analytics, proctoring | Education records, student profiling, automated grading decisions |
| **Employment and workforce management** | CV screening, recruitment ranking, performance evaluation, task allocation, termination decisions | Employee personal data, automated employment decisions, workplace profiling |
| **Access to essential services** | Credit scoring, insurance pricing and underwriting, social benefit eligibility, emergency service dispatching | Financial data, health data, profiling for service access decisions |
| **Law enforcement** | Individual risk assessment, polygraph and similar tools, evidence evaluation, profiling, crime analytics | Criminal records, surveillance data, predictive profiling of individuals |
| **Migration, asylum, and border control** | Visa application processing, risk assessment at borders, document authenticity verification | Immigration records, biometric data, automated risk profiling |

### High-Risk System Requirements (Privacy-Relevant)

Providers and deployers of high-risk AI systems must comply with the following requirements, each of which has data protection implications:

1. **Risk management system** (Article 9): Continuous, iterative process identifying and mitigating risks, including risks to fundamental rights and personal data.
2. **Data governance** (Article 10): Quality, relevance, representativeness, and bias assessment requirements for training, validation, and testing data. See dedicated section below.
3. **Technical documentation** (Article 11): Detailed documentation of system design, data processing, and decision-making logic -- overlaps with GDPR transparency and accountability obligations.
4. **Record-keeping** (Article 12): Automatic logging of system operations to enable traceability -- relates to GDPR Article 30 records of processing activities.
5. **Transparency and information to deployers** (Article 13): Deployers must receive clear information about system capabilities and limitations, including the nature and extent of personal data processing.
6. **Human oversight** (Article 14): Measures enabling human oversight of AI system operation, including ability to override or reverse automated decisions -- directly relevant to GDPR Article 22 (automated decision-making).
7. **Accuracy, robustness, and cybersecurity** (Article 15): Technical standards for system reliability -- cybersecurity requirements complement GDPR Article 32 (security of processing).

---

## Data Governance Requirements

**Article 10** establishes specific data governance obligations for high-risk AI systems that directly intersect with data protection law:

### Training Data Quality (Article 10(2)-(3))

- Training, validation, and testing datasets must be subject to appropriate **data governance and management practices**.
- Datasets must be **relevant, sufficiently representative, and free of errors** to the extent possible given the intended purpose.
- Datasets must have **appropriate statistical properties**, including with regard to the persons or groups of persons on whom the high-risk AI system is intended to be used.

### Bias Detection and Correction (Article 10(5))

- Providers must **examine datasets for possible biases** that are likely to affect the health and safety of persons, have an adverse impact on fundamental rights, or lead to discrimination prohibited under EU law.
- **Special categories of personal data** (as defined by GDPR Article 9: racial or ethnic origin, political opinions, religious beliefs, trade union membership, genetic data, biometric data, health data, sex life, sexual orientation) **may be processed** for the purpose of bias detection, correction, and monitoring -- but only where:
  - Strictly necessary for those purposes
  - Subject to appropriate safeguards for fundamental rights and freedoms
  - Including technical limitations on re-use, time limits, and access controls
  - GDPR-compliant legal basis and safeguards are in place

> **Practitioner note:** Article 10(5) is significant because it creates a specific legal pathway for processing special category data in the context of AI bias detection -- something that has been uncertain under GDPR alone. However, this does not override GDPR requirements; both frameworks must be satisfied simultaneously.

### Data Governance Documentation

- Data governance practices, design choices, and dataset characteristics must be **documented** as part of the technical documentation required under Article 11.
- Documentation must include information about data collection processes, data preparation operations (annotation, labeling, cleaning, enrichment), and relevant data gaps or shortcomings.

---

## GDPR Interplay

The AI Act and GDPR operate as complementary frameworks. Neither replaces the other. Key interaction points for privacy practitioners:

### Fundamental Rights Impact Assessment (FRIA) and DPIA

- **Article 27** requires deployers of high-risk AI systems to conduct a **fundamental rights impact assessment (FRIA)** before putting the system into use.
- The FRIA complements -- but does not replace -- GDPR **Data Protection Impact Assessments (DPIAs)** under Article 35 GDPR.
- Where both apply to the same AI system processing personal data, organizations should coordinate FRIA and DPIA processes to avoid duplication while satisfying both requirements.
- The FRIA must describe the intended purpose, geographic and temporal scope, categories of affected persons, specific risks to fundamental rights, human oversight measures, and governance measures.

### Enforcement Authority Overlap

- Member States may designate their **Data Protection Authorities (DPAs)** as national competent authorities (or market surveillance authorities) for AI Act enforcement.
- Several Member States are likely to assign AI Act responsibilities to existing DPAs, creating unified oversight for both data protection and AI regulation.
- The **EDPB** (European Data Protection Board) and the **AI Office** coordinate on matters involving both AI and personal data, including guidance on the intersection of the two frameworks.

### Parallel Legal Obligations

| GDPR Obligation | AI Act Parallel | Interaction |
|-----------------|-----------------|-------------|
| Lawful basis for processing (Art. 6) | Data governance for training data (Art. 10) | Training data processing requires a GDPR lawful basis AND must meet AI Act quality/governance standards |
| Purpose limitation (Art. 5(1)(b)) | Intended purpose documentation (Art. 13) | AI system's intended purpose constrains both GDPR processing purposes and AI Act deployment scope |
| Data minimization (Art. 5(1)(c)) | Dataset representativeness (Art. 10(3)) | Tension: GDPR minimization vs. AI Act representativeness requirements; both must be balanced |
| Transparency (Art. 13-14) | Transparency to deployers and users (Art. 13, 50) | GDPR data subject information rights apply alongside AI Act transparency obligations |
| Automated decision-making (Art. 22) | Human oversight (Art. 14) | GDPR right not to be subject to solely automated decisions is reinforced by AI Act human oversight requirements |
| DPIA (Art. 35) | FRIA (Art. 27) | Complementary assessments; should be coordinated, not duplicated |
| Security of processing (Art. 32) | Cybersecurity requirements (Art. 15) | Both require appropriate technical and organizational measures |
| DPO (Art. 37-39) | No direct equivalent | DPO role may expand to cover AI Act compliance in organizations where DPA is also AI competent authority |

### AI-Generated Personal Data

- Personal data generated by AI systems -- including **inferences, profiling results, predictions, and risk scores** -- constitutes personal data under GDPR when it relates to an identifiable natural person.
- All GDPR data subject rights (access, rectification, erasure, restriction, portability, objection) apply to AI-generated personal data.
- This is particularly relevant for high-risk AI systems in employment, credit scoring, and law enforcement contexts, where AI-generated assessments directly affect individuals.

---

## Transparency Requirements (Privacy-Relevant)

**Effective: August 2, 2026** for most transparency obligations.

Transparency obligations under the AI Act that directly affect data protection practice:

- **Emotion recognition and biometric categorization deployers** (Article 50(3)): Must inform natural persons that they are being exposed to an emotion recognition or biometric categorization system. Information must be provided before the system's use.
- **Deepfakes and AI-generated content** (Article 50(4)): AI-generated or manipulated image, audio, or video content (deepfakes) must be disclosed and labeled as artificially generated or manipulated, in a machine-readable format where technically feasible.
- **AI interaction disclosure** (Article 50(1)): Persons interacting with an AI system (chatbots, virtual assistants) must be informed that they are interacting with an AI system, unless this is obvious from the circumstances.
- **Interaction with GDPR transparency:** These obligations operate alongside GDPR Articles 13-14 (information to data subjects). Organizations must satisfy both AI Act disclosure requirements and GDPR transparency obligations for the same system.

---

## Enforcement and Penalties

### Enforcement Structure

- **National competent authorities** in each EU Member State supervise and enforce AI Act obligations within their territory. Member States had until August 2, 2025 to designate these authorities.
- **EU AI Office** (established within the European Commission): Coordinates cross-border enforcement, supervises general-purpose AI models, and develops guidelines and standards.
- **European Artificial Intelligence Board:** Advisory body composed of Member State representatives, facilitating consistent implementation.
- National **market surveillance authorities** handle conformity assessments and market monitoring for high-risk AI systems.

### Penalty Structure

Three-tier penalty system based on the severity of the infringement:

| Violation Category | Maximum Penalty | Scope |
|--------------------|-----------------|-------|
| Prohibited practices (Article 5) | EUR 35 million or **7%** of total worldwide annual turnover (whichever is higher) | Deploying banned AI systems: biometric scraping, social scoring, prohibited emotion recognition, etc. |
| High-risk system obligations and other key provisions | EUR 15 million or **3%** of total worldwide annual turnover | Non-compliance with data governance, risk management, transparency, human oversight, FRIA requirements |
| Supplying misleading information to authorities | EUR 7.5 million or **1%** of total worldwide annual turnover | Providing incorrect, incomplete, or misleading information to competent authorities or notified bodies |

- **Reduced caps for SMEs and startups:** Penalties are proportionate; lower of the two amounts (fixed or percentage) applies to SMEs and startups for each tier.
- **Public sector:** Administrative fines apply to public authorities and bodies deploying AI systems.

### Key Enforcement Milestones

The AI Act is newly in force, with enforcement infrastructure still being established. Significant milestones to date:

1. **February 2, 2025 -- Prohibited practices enforcement begins:** First tier of AI Act obligations becomes enforceable. Biometric prohibitions and social scoring bans now carry penalties.
2. **August 2, 2025 -- GPAI rules apply:** General-purpose AI model providers must comply with transparency obligations and, for systemic risk models, with additional evaluation and incident reporting requirements. Training data governance requirements begin.
3. **Member State competent authority designations (2025):** Several Member States have designated or are designating their DPAs as AI Act competent authorities, signaling unified data protection and AI oversight.
4. **EDPB-AI Office coordination (2025-2026):** Joint guidance on GDPR-AI Act intersection expected, particularly on FRIA/DPIA coordination and special category data processing for bias detection.

> **Practitioner note:** Unlike GDPR, which had landmark enforcement cases years before significant fines were issued, the AI Act is in its earliest enforcement phase. No significant enforcement actions have been taken under the AI Act as of March 2026. Practitioners should monitor the EU AI Act Service Desk and national competent authority websites for emerging enforcement priorities.

---

## Implementation Timeline

The AI Act uses **phased enforcement** to allow organizations time to adapt. Key dates with privacy relevance:

| Date | Milestone | Privacy Relevance |
|------|-----------|-------------------|
| **August 1, 2024** | AI Act enters into force | Regulation published and legally binding; preparation period begins |
| **February 2, 2025** | Prohibited practices enforceable | Biometric prohibitions (facial scraping, emotion recognition, biometric categorization) in effect. Immediate compliance required. |
| **August 2, 2025** | GPAI rules apply; AI literacy; competent authority designation | Training data governance requirements for general-purpose AI; Member States must designate competent authorities (some designating DPAs) |
| **August 2, 2026** | High-risk Annex III obligations apply; transparency obligations effective | Biometric ID systems, employment AI, education AI, credit scoring AI rules enforceable. FRIA required. Emotion recognition/deepfake disclosure obligations begin. |
| **August 2, 2027** | High-risk obligations for regulated products (Annex I) | AI systems embedded in products regulated by EU harmonization legislation (medical devices, machinery, vehicles) must comply |

### Immediate Action Items (Already Enforceable)

As of March 2026, organizations should have already:
- Audited AI systems against Article 5 prohibited practices (enforceable since February 2025)
- Ensured no real-time remote biometric identification in public spaces (unless narrow law enforcement exception applies)
- Confirmed no untargeted facial image scraping for database building
- Verified no emotion recognition in workplace or educational AI deployments (unless medical/safety exception applies)

### Upcoming Deadlines

By **August 2, 2026**, organizations deploying high-risk AI systems must:
- Complete fundamental rights impact assessments (FRIAs)
- Implement data governance and documentation requirements
- Establish transparency and human oversight mechanisms
- Coordinate AI Act compliance with existing GDPR compliance programs

---

## Compliance Essentials

For privacy practitioners managing AI Act compliance alongside existing data protection obligations:

1. **Inventory AI systems processing personal data and classify by risk tier.** Map each AI system against the Annex III high-risk categories. Systems processing biometric data, making employment or credit decisions, or used in education are almost certainly high-risk.

2. **Prohibited practice audit.** Confirm no deployed systems fall under Article 5 prohibitions -- particularly biometric scraping, emotion recognition in workplace or educational settings, biometric categorization using sensitive characteristics, and social scoring. This is already enforceable.

3. **Fundamental rights impact assessment for high-risk AI systems.** Conduct FRIAs for Annex III systems, coordinating with GDPR DPIAs where both frameworks apply to the same AI system processing personal data. Build a unified assessment process to avoid duplication.

4. **Data governance documentation for training datasets.** Document quality criteria, representativeness assessment, bias detection methodology, and any special category data processing with GDPR-compliant safeguards (Article 10(5) pathway).

5. **Transparency mechanisms.** Implement AI interaction disclosure (chatbots), deepfake labeling, and biometric system notification requirements. Align with GDPR Articles 13-14 transparency obligations for a unified disclosure approach.

6. **Coordinate with competent authority designation.** Identify whether your Member State DPA is also the AI Act competent authority. If so, prepare for unified oversight and expect enforcement priorities that bridge data protection and AI regulation.

7. **Human oversight mechanisms for high-risk AI systems.** Ensure meaningful human oversight of AI systems making decisions that affect individuals' personal data -- reinforcing GDPR Article 22 rights against solely automated decision-making.

8. **Monitor implementing acts and harmonized standards.** The European Commission is developing implementing acts, delegated acts, and harmonized standards that will specify detailed technical requirements for high-risk AI systems. These are in active development as of March 2026 and will shape specific compliance obligations.

---

*This reference file covers the EU AI Act from a privacy practitioner's perspective. It does not address general-purpose AI model evaluation requirements, product safety provisions, AI regulatory sandboxes, codes of practice, or AI liability frameworks unless they directly involve personal data processing.*
