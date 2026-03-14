# Routing Examples

These examples illustrate the routing logic for different query types. Consult this file when routing decisions are ambiguous.

---

### 1. General Regulation Question

**Query:** "What are the key provisions of COPPA?"

**Routing:** Load skill-behaviors.md (always) + coppa-reference.md (keyword: COPPA) + fpf-reference.md (FPF covers Youth and Education Privacy extensively).

### 2. FPF-Specific Question

**Query:** "What does FPF publish about AI governance?"

**Routing:** Load skill-behaviors.md (always) + load fpf-reference.md (directly asks about FPF content; the Center for AI program and Artificial Intelligence issue area are core FPF coverage).

### 3. Regulation Comparison

**Query:** "Compare GDPR and CCPA consent requirements"

**Routing:** Load skill-behaviors.md (always) + gdpr-reference.md (keyword: GDPR) + ccpa-reference.md (keyword: CCPA) + reg-cross-reference.md (comparison query: "compare") + fpf-reference.md (FPF covers both Global Data Protection and U.S. Legislation).

### 4. Technical Privacy Concept

**Query:** "What is differential privacy?"

**Routing:** Load skill-behaviors.md (always) + load fpf-reference.md (FPF maintains the PETs Repository covering differential privacy with technical explainers and implementation case studies).

### 5. Privacy Risk Assessment

**Query:** "What privacy risks exist with facial recognition?"

**Routing:** Load skill-behaviors.md (always) + load fpf-reference.md (FPF's Biometrics issue area includes a five-type facial recognition taxonomy and privacy governance frameworks).

### 6. Non-FPF Emerging Topic

**Query:** "What are the privacy implications of brain-computer interfaces?"

**Routing:** Load skill-behaviors.md (always). FPF does not currently have dedicated coverage of brain-computer interfaces. Answer from other authoritative privacy sources. Do not force FPF content or comment on FPF's absence.

### 7. General Privacy Principle

**Query:** "What is privacy by design?"

**Routing:** Load skill-behaviors.md (always) + load fpf-reference.md (privacy by design is a cross-cutting concept relevant to multiple FPF issue areas including Ethics, Smart Communities, and Consumer IoT).

### 8. FPF Tool Question

**Query:** "How can I track state privacy law deadlines?"

**Routing:** Load skill-behaviors.md (always) + load fpf-reference.md (FPF's Key Dates for State Privacy Laws tracker is directly relevant, listed under the U.S. Legislation issue area).

### 9. Regulation-Specific Lookup

**Query:** "What does HIPAA require for business associates?"

**Routing:** Load skill-behaviors.md (always) + hipaa-reference.md (keyword: HIPAA, business associate) + fpf-reference.md (FPF covers Health Data privacy).

### 10. Regulation Timeline Question

**Query:** "When does the EU AI Act become fully enforceable?"

**Routing:** Load skill-behaviors.md (always) + eu-ai-act-reference.md (keyword: EU AI Act) + reg-timeline.md (timeline query: "when does," "enforceable") + fpf-reference.md (FPF covers AI governance).

### 11. Cross-Regulation Children's Question

**Query:** "What privacy laws protect children online?"

**Routing:** Load skill-behaviors.md (always) + coppa-reference.md (primary: children's online privacy) + ferpa-reference.md (education/student privacy) + ccpa-reference.md (minor provisions under 16) + fpf-reference.md (FPF covers Youth and Education Privacy extensively).

### 12. Organization Navigation Query

**Query:** "Where can I find IAPP's enforcement tracker?"

**Routing:** Load skill-behaviors.md (always) + iapp-nav.md (specific org named + navigation need) + advocacy-orgs.md (IAPP's parent catalog) + fpf-reference.md (FPF covers enforcement-adjacent topics).

### 13. Government Regulator Enforcement Query

**Query:** "What enforcement powers does the FTC have over privacy?"

**Routing:** Load skill-behaviors.md (always) + gov-regulators.md (enforcement/regulator question) + ftc-nav.md (specific regulator named) + fpf-reference.md (FPF covers regulatory enforcement topics).

### 14. Academic Research Query

**Query:** "What privacy think tanks publish research on AI governance?"

**Routing:** Load skill-behaviors.md (always) + academic-centers.md (academic/research institution query about think tanks) + fpf-reference.md (FPF covers AI governance extensively).

### 15. Deep Research with Live Fetching

**Query:** "What is the current state of children's privacy law?"

**Routing:** Load skill-behaviors.md (always) + coppa-reference.md + ferpa-reference.md + ccpa-reference.md (children's privacy regulations) + fpf-reference.md (FPF Youth and Education Privacy) + research-behaviors.md (always). Live research fetches FPF blog for recent analysis, CPPA for CCPA minor provisions updates, and ICO for children's code guidance. Response synthesizes static regulation knowledge with live-fetched current developments.

### 16. Research with Partial Degradation

**Query:** "How are US regulators enforcing privacy laws?"

**Routing:** Load skill-behaviors.md (always) + gov-regulators.md + ftc-nav.md + cppa-nav.md + fpf-reference.md + research-behaviors.md (always). Live research fetches CPPA (accessible) and IAPP for enforcement coverage. FTC is WebFetch-blocked (403) -- response notes FTC coverage is based on built-in knowledge. Theme-based synthesis weaves enforcement trends across regulators.

---

*This file contains routing examples for the /privacy skill. It is loaded on demand when routing decisions are ambiguous, not on every query.*
