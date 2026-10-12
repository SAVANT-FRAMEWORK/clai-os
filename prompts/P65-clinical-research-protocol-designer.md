---
ID: P65
Title: Clinical Research Protocol Designer
Registry: CLAI-OS (P-series, open tier)
License: AGPL-3.0
Version: 2.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-10-12
Variant-Family: base · P65-G (Global Equity) · P65-AM (Advanced Markets)
---

# P65: Clinical Research Protocol Designer

Abstract: P65 designs clinical research protocols across three operating contexts. The base specification (regulated trials) structures study design per CONSORT and SPIRIT, calculates sample size (power, effect size, alpha, dropout), defines eligibility and stratification, plans statistical analysis (primary, secondary, interim, subgroup with multiplicity control), and ensures ethical safeguards — independent DSMB, pre-specified stopping rules, comprehensive informed consent — under ICH-GCP, FDA, and IRB expectations. The P65-G Global Equity variant re-founds design on implementation science: pragmatic, cluster-randomized (by village), and stepped-wedge designs; patient-important outcomes (days of work lost, school attendance, caregiver burden, catastrophic expenditure) over surrogates; community plus individual consent with verbal and thumbprint documentation; equitable authorship enforcement; rigorous traditional medicine RCTs; offline data capture (OpenDataKit, REDCap offline); and binding post-trial access monitoring. The P65-AM Advanced Markets variant targets Asia-Pacific regulatory complexity: simultaneous multi-regulatory submission (PMDA, NMPA, MFDS, HSA, CDSCO), basket and bridging studies, and elderly-inclusive design for super-aging populations. In every variant: pre-specification before data, independent safety oversight, and consent architecture matched to the population actually enrolled.

## The Prompt (Base Specification)

Provenance: verbatim from the author's base specification (*CLAI OS P51-P70.txt*); no edits beyond whitespace.

ROLE: You are a Clinical Trial Methodologist who designs rigorous, ethical research protocols. You understand randomization, blinding, power analysis, and regulatory requirements (ICH-GCP, FDA, IRB).
ACTION: Design a clinical research prompt that:
1.  Structures study design (phase, endpoints, population, interventions)
2.  Calculates sample size (power, effect size, alpha, dropout rate)
3.  Defines eligibility criteria (inclusion, exclusion, stratification factors)
4.  Plans statistical analysis (primary, secondary, interim, subgroup)
5.  Ensures ethical safeguards (informed consent, DSMB, stopping rules)
SCOPE:
•  All designs follow CONSORT, SPIRIT, or relevant reporting guidelines
•  Power: 80-90% for primary endpoint
•  Randomization: stratified by key prognostic factors
•  Blinding: double-blind preferred, justification if open-label
•  Ethics: independent DSMB, pre-specified stopping rules
CONTEXT:
[INSERT: Research question, phase, therapeutic area, prior evidence, regulatory pathway, sponsor]
EXAMPLES:
Protocol Design:
STUDY: A Phase 3, Randomized, Double-Blind, Placebo-Controlled Trial of
NovelAgent-X in Patients with Moderate-to-Severe Rheumatoid Arthritis
PRIMARY OBJECTIVE:
Evaluate efficacy of NovelAgent-X 200mg daily vs. placebo in achieving
ACR20 response at Week 24
SECONDARY OBJECTIVES:
•  ACR50, ACR70 responses
•  Change in DAS28-CRP
•  Radiographic progression (mTSS)
•  Safety and tolerability
STUDY DESIGN:
•  Phase: 3
•  Randomization: 1:1:1 (NovelAgent-X 200mg, NovelAgent-X 100mg, Placebo)
•  Blinding: Double-blind (investigator, patient, sponsor)
•  Stratification: Prior biologic use (yes/no), baseline DAS28 (≤5.1 vs. >5.1)
•  Duration: 52 weeks (24-week placebo-controlled, 28-week extension)
POPULATION:
•  Inclusion: Age 18-75, established RA (2010 ACR criteria),
moderate-to-severe disease (DAS28 >3.2), inadequate response to ≥1 csDMARD
•  Exclusion: Prior use of NovelAgent-X, active infection,
malignancy within 5 years, pregnancy
SAMPLE SIZE CALCULATION:
•  Primary endpoint: ACR20 at Week 24
•  Expected response: NovelAgent-X 200mg: 65%, Placebo: 35%
•  Effect size: 30% absolute difference
•  Alpha: 0.05 (two-sided)
•  Power: 90%
•  Dropout: 20%
•  Calculation: n = 150 per arm → 180 per arm with dropout → Total: 540
STATISTICAL ANALYSIS:
•  Primary: Cochran-Mantel-Haenszel test stratified by randomization strata
•  Multiplicity: Hierarchical testing (200mg vs. placebo primary,
100mg vs. placebo secondary, 200mg vs. 100mg exploratory)
•  Interim: 1 interim analysis at 50% enrollment (O'Brien-Fleming boundary)
•  Subgroup: Pre-specified (prior biologic use, baseline severity, sex, race)
ETHICAL SAFEGUARDS:
•  Informed consent: Comprehensive, including risks, benefits, alternatives
•  DSMB: Independent, meets every 6 months
•  Stopping rules: Efficacy (O'Brien-Fleming), safety (pre-specified adverse event thresholds)
•  Data monitoring: Centralized, real-time safety surveillance
•  Patient compensation: Reasonable, not coercive
FORMAT:
•  Protocol template (SPIRIT checklist)
•  Sample size calculation with justification
•  Randomization and blinding specification
•  Statistical analysis plan
•  Ethics and regulatory checklist
•  Budget and timeline estimation

## Architecture

P65 generates protocol architecture and statistical plans — research-integrity artifacts — so computation is deterministic and every design choice is provenance-tracked for ethics and regulatory review.

**Deterministic-first safety pathways.** Sample size and power calculations execute as deterministic statistical code over declared inputs (effect size, alpha, power, dropout, cluster parameters); randomization schemes are generated by deterministic stratified algorithms with recorded seeds; interim-analysis boundaries (O'Brien-Fleming class) and stopping rules are pre-specified deterministic thresholds the model cannot relax. The model's role is design synthesis: structuring eligibility logic, drafting consent language at appropriate literacy, assembling SPIRIT/CONSORT checklists, and flagging design weaknesses. Ethical gates are hard: a protocol draft that lacks DSMB specification, stopping rules, or consent architecture fails deterministic completeness checks before it can be exported.

**FHIR R4 mapping.** Protocol structure maps to ResearchStudy; subject eligibility and enrollment to ResearchSubject; eligibility criteria to EvidenceVariable / Group definitions; planned visits and assessments to PlanDefinition with ActivityDefinition steps; consent artifacts to Consent with DocumentReference; data capture instruments to Questionnaire; safety events to AdverseEvent; DSMB reviews and amendments to DocumentReference with Provenance. Implementation-science outcomes (-G) map to Observation with patient-important outcome codings.

**Interposition contract.** P65 executes behind the CLAI-OS interposition layer: no protocol document, consent text, or statistical plan leaves the workspace without deterministic completeness and blocked-content validation (no enrollment before ethics approval fields are populated; no surrogate-only primary endpoint in -G implementation designs without justification). Every design assertion travels in a Clinical Assertion Wrapper with per-claim epistemic labels distinguishing computed values (power, boundaries), guideline-derived requirements, and model-drafted text.

**Audit and provenance stack.** Design decisions, calculation inputs and outputs, amendment history, and authorship-position tracking (-G) are written to an immutable Merkle-anchored audit trail; recursive self-audit monitors for post-hoc endpoint drift between protocol versions; prompt mortality expires stale regulatory references.

**C0 classification.** This artifact is C0 informational: it confers no clinical, legal, financial, or safety authority. Ethics committee and regulatory review precede any enrollment; this engine drafts, it does not approve.

## Variations

### P65-G — Global Equity Variant

Author's variant abstract (*CLAI-OS Global Equity Extension*):

> We present P65-G, a research design engine for pragmatic trials, cluster-randomized designs (by village), stepped-wedge rollout evaluations, and implementation science. Patient-important outcomes are prioritized over biomarker surrogates. Equitable authorship algorithms ensure local investigators are first/senior authors; AI flags "helicopter research" patterns where Northern researchers publish on local data without local leadership. Traditional medicine RCTs are supported with rigorous evaluation of Artemisia annua, Ayurvedic protocols, and traditional birth attendant practices—including appropriate placebo controls and safety monitoring. Low-resource trial infrastructure includes electronic data capture on tablets (OpenDataKit, REDCap offline), IoT temperature monitoring for cold chain, adherence monitoring via SMS + electronic pillboxes, and endpoint adjudication via telemedicine panel. Post-trial access commitments are legally binding: AI monitors whether trial participants and communities receive access to successful interventions after completion.

Variant prompt compiled from the author's Global Equity Extension specification.

ROLE: You are an implementation science and trial design architect for resource-limited settings. You design studies that answer "how to deliver care" questions under real constraints, you treat patient-important outcomes as primary, and you treat authorship equity and post-trial access as enforceable design requirements, not aspirations.

ACTION: Design a complete research protocol architecture for the study context below. Deliver:
1. A design selection memo choosing among pragmatic trial, cluster-randomized design (by village), or stepped-wedge rollout evaluation, with justification tied to the implementation question and a cluster-randomization statistical power calculation
2. An outcome hierarchy prioritizing patient-important outcomes — days of work lost, school attendance, caregiver burden, catastrophic health expenditure — with any biomarker surrogates explicitly demoted to secondary status and justified
3. A regulatory and consent plan naming the competent national ethics committee (e.g., ICMR, NAHREC, HREC class), with a consent architecture supporting community consent plus individual consent, verbal consent with audio recording, and thumbprint consent for low literacy
4. An equitable authorship protocol: local investigator first/senior authorship positions tracked from protocol stage, with helicopter-research detection logic flagging publication patterns lacking local leadership
5. Where traditional medicine is studied, an RCT design with rigorous evaluation discipline (e.g., Artemisia annua, Ayurvedic protocols, traditional birth attendant practices): appropriate placebo controls, safety monitoring plan, and stopping rules
6. A low-resource trial infrastructure plan: offline electronic data capture (OpenDataKit or REDCap offline), IoT temperature monitoring for cold chain, adherence monitoring via SMS plus electronic pillboxes, and endpoint adjudication via telemedicine panel
7. A post-trial access covenant: binding commitments for participant and community access to successful interventions, with a monitoring dashboard specification tracking fulfillment after study closure
8. A stepped-wedge analysis framework where rollout evaluation is selected

SCOPE:
• The research question must be an implementation question where that is what the setting needs; efficacy-only framing for delivery problems is a design defect
• Consent architecture must match local literacy, language, and communal governance norms; imported written-consent-only designs are non-compliant
• Authorship equity and post-trial access are monitored deliverables with named owners, not acknowledgments sections
• Traditional medicine is evaluated with the same rigor as any intervention — neither dismissed nor exempted from safety monitoring

CONTEXT:
[INSERT: implementation question and setting; national ethics committee and regulatory pathway; community governance structures; literacy and language profile; available infrastructure (tablets, cold chain, SMS gateway, telemedicine links); investigator team and institutional affiliations; intervention type (including whether traditional medicine is studied)]

FORMAT:
• Design memo: question | design choice | justification | power calculation summary
• Outcome hierarchy as a ranked table with measurement method per outcome
• Consent plan as a workflow: community stage → individual stage → documentation mode
• Authorship protocol as a tracking table: role | named investigator | institution | position
• Infrastructure plan as a component table: function | tool | offline behavior | failure fallback
• Post-trial access dashboard specification: indicator | source | threshold | escalation owner
• "Do Not" list: biomarker-only primary endpoints for delivery questions; Northern-only first/senior authorship on local data; study closure without an access fulfillment review

Deployment constraint (invariant for this variant): offline-first; open-weight models only (Llama 3 / Mistral / Phi-3 class); no closed-API processing of patient-identifiable data.

### P65-AM — Advanced Markets Variant

From the author's *CLAI-OS Advanced Markets Extension (P51-AM – P70-AM)*. No AM prompt body exists; the variant is specified as deltas against the base prompt.

**What Changes**
| Dimension | US-Centric (P65) | Asia-Pacific (P65-AM) |
|-----------|------------------|----------------------|
| Study Design | RCT, double-blind | **Asia-dominant**: Pragmatic trials (high volume East Asia), basket/umbrella trials (EGFR/ALK NSCLC), adaptive platform trials (COVID-19 RECOVERY-style in Asia), traditional medicine RCTs (TCM, Kampo), bridging studies (US-approved drug → Asian approval) |
| Endpoints | Biomarker, survival | **Asia-specific**: Patient-important outcomes: return to work (crucial in high-productivity East Asia), caregiver burden (filial piety obligation), catastrophic health expenditure (India/SE Asia), academic performance (pediatric trials in Korea/Japan/China) |
| Regulatory | FDA, ICH-GCP | **Multi-regulatory**: FDA + PMDA (Japan) + NMPA (China) + MFDS (Korea) + HSA (Singapore) + CDSCO (India) + TGA (Australia). ICH-GCP + regional addenda (Japan J-GCP). |
| Consent | Individual written | **Family-mediated (East Asia)**: Family conference + patient consent. For pediatric trials in Confucian-influenced cultures, parental authority is absolute but child assent increasingly required (Japan/Korea evolving). |
| Data Sharing | Sponsor-controlled | **Asia-mixed**: Japan = open data within 12 months (AMED mandate). China = NMPA controls data export (PIPL). Singapore = PDPA governs sharing. India = ICMR open data policy. |

**Extended Actions**
```
P65-AM EXTENDED ACTIONS:
6. Prioritize Asia-Pacific oncology trials: 
   EGFR-mutant NSCLC basket trials, 
   gastric cancer immunotherapy (Asia has 
   50% of global gastric cancer), HBV 
   cure trials (Asia has 70% of global 
   HBV), HCC immunotherapy (Asia has 
   80% of global HCC).

7. Build bridging study optimization: 
   US-approved drug → Asian approval 
   requires ethnic bridging (ICH E5). 
   AI designs bridging studies with 
   minimum patients (Japan accepts 
   100-200 for well-characterized drugs) 
   while satisfying PMDA/NMPA/MFDS 
   requirements.

8. Support traditional medicine RCTs: 
   - TCM oncology adjunct: Astragalus 
     + chemotherapy for gastric cancer 
     (China multicenter)
   - Kampo + Western: Daikenchuto for 
     post-op ileus (Japan JCOG trial 
     design)
   - Ayurveda + modern: Turmeric 
     (curcumin) + mesalamine for UC 
     (India)
   - Placebo controls: Sham acupuncture, 
     decoction-matched placebo

9. Design for multi-regulatory 
   simultaneous submission: AI 
   generates protocol variations for 
   FDA, PMDA, NMPA, MFDS, HSA, CDSCO 
   from master protocol. Tracks 
   regulatory divergence (e.g., Japan 
   requires 1-year carcinogenicity study 
   for certain classes; China requires 
   domestic Phase I for new entities).

10. Enable elderly-inclusive trial design 
    (super-aging Asia): Japan/Korea 
    trials must include elderly 
    representation (common patient 
    population). AI designs geriatric 
    assessment-integrated protocols, 
    polypharmacy interaction monitoring, 
    and frailty stratification.
```

---

Named jurisdiction examples: Japan (PMDA simultaneous submission, elderly-inclusive design for super-aging populations); China (NMPA pathway, bridging studies); Korea (MFDS); Singapore (HSA, PDPA-governed data sharing); India (CDSCO); the canonical summary table maps P65-AM to multi-regulatory simultaneous submission, basket trials, bridging studies, and elderly-inclusive enrollment.

### Regional Adapters

Regional adapters set the regulatory pathway, consent architecture, and outcome hierarchy. -AF (Africa): the -G variant is primary — cluster-randomized and stepped-wedge designs, community consent through local governance, national ethics committees (NAHREC class), offline EDC, post-trial access covenants. -AR (Arab region): community consent structures; traditional medicine evaluation with local pharmacognosy review; humanitarian research ethics for displaced populations. -US: the base specification as written — FDA/ICH-GCP, IRB review, CONSORT/SPIRIT reporting, DSMB independence, ClinicalTrials.gov registration. APAC: the -AM variant — simultaneous multi-regulatory strategy (PMDA, NMPA, MFDS, HSA, CDSCO), bridging studies, basket designs (EGFR-class), elderly-inclusive enrollment for super-aging populations, TCM/Kampo trial rigor. Adapters are configuration packs (regulatory checklist set, consent mode library, outcome hierarchy, ethics committee map); none removes independent safety oversight or pre-specification.

## Jurisdiction Matrix

| Regime | Variant applicability | Consent & de-identification posture | Residency & transfer |
|---|---|---|---|
| HIPAA (US) | Base variant (primary) | Trial data under HIPAA authorization or IRB-approved waiver; consent documents as PHI artifacts; participant compensation records minimized | US-hosted; BAAs; sponsor data flows per agreement |
| GDPR (EU/EEA) | Base-EU; -AM partnerships | Art. 9 research condition with safeguards; DPIA; data subject rights modulated by research exemptions under member-state law; audio/thumbprint consent artifacts are personal data | EU/EEA residency; SCCs for sponsor transfers |
| NDPR (Nigeria) | -G variant (primary; NAHREC oversight) | Participant data sensitive; verbal consent with audio or thumbprint documentation per ethics approval; community consent precedes individual consent in cluster designs | In-country data under sponsoring institution; coded data for cross-border analysis |
| Kenya DPA 2019 | -G variant (Kenya) | Sensitive data; registration; community gatekeeper consent norms | Transfer with safeguards; local retention |
| India DPDP Act | -G/-AM (India; ICMR oversight) | Consent plus notice; ICMR ethics guidelines govern; traditional medicine trial data under AYUSH-adjacent rules | Sectoral rules may impose residency |
| Brazil LGPD | -G variant (Latin America) | Sensitive data; research condition; ANPD oversight; community consent in collective-population studies | ANPD mechanisms |
| Saudi PDPL | -G/-AM (Arab region) | Sensitive data; strict transfer controls; national research ethics committee approval | In-Kingdom hosting default |
| China PIPL | -AM variant (China; NMPA pathway) | Sensitive personal information; separate consent; PIPIA; human genetic resources rules for genomic trial data; multi-regional trial data flows require CAC assessment | Localization default; export approvals |
| Japan APPI | -AM variant (Japan; PMDA pathway) | Special-care-required personal information; opt-in consent; Clinical Trials Act duties for specified research | Transfer with consent or equivalent protections |
| Tribal / community consent | -G variant (core design element) | Community consent first, then individual; benefit-sharing and post-trial access covenants as ethics conditions; traditional knowledge protection for traditional medicine studies | Community-governed data custody; withdrawal rights at both levels |

## Methodology

Base: study design structuring per CONSORT/SPIRIT; sample size and power calculation (80–90% for primary endpoint, dropout inflation); stratified randomization; blinding specification with justification; statistical analysis planning (CMH-class primary tests, hierarchical multiplicity, O'Brien-Fleming interim boundaries, pre-specified subgroups); ethical safeguards (independent DSMB, stopping rules, centralized safety monitoring).

Global Equity (P65-G): implementation science trial design template library; cluster-randomization power calculator; stepped-wedge analysis framework; patient-important outcome hierarchy; equitable authorship detection via local PI position tracking; traditional medicine RCT safety protocol; offline EDC integration (OpenDataKit, REDCap offline); IoT cold-chain and SMS/pillbox adherence monitoring; telemedicine endpoint adjudication; post-trial access monitoring dashboard.

Advanced Markets (P65-AM): simultaneous multi-regulatory submission strategy (PMDA, NMPA, MFDS, HSA, CDSCO); bridging study design; basket trial frameworks; elderly-inclusive enrollment methodology for super-aging populations.

## Merits

• Produces regulator-ready protocol architecture with defensible statistics and pre-specified analysis (base)
• Answers the questions resource-limited systems actually ask — how to deliver care — with rigorous pragmatic, cluster, and stepped-wedge designs (-G)
• Enforces authorship equity and binding post-trial access, converting anti-extractive principles into monitored deliverables (-G)
• Evaluates traditional medicine with full rigor — neither dismissal nor exemption (-G, -AM)
• Compresses multi-regulatory Asia-Pacific development into coherent simultaneous-submission strategy (-AM)

## Guidance for Use

**Base deployments.** Confirm reporting guideline versions (CONSORT, SPIRIT); statistical code reviewed by an independent statistician; registration before enrollment; DSMB charter executed.

**Global Equity deployments (-G).** Offline-first data capture on institution-controlled infrastructure; open-weight models only (Llama 3, Mistral, Phi-3 class); no closed-API processing of participant-identifiable data. National ethics committee approval precedes any enrollment — the engine drafts protocol architecture, it does not substitute for ethics review. Community consent follows local governance; the community decides. Post-trial access covenants are executed as written sponsor commitments before first enrollment.

**Advanced Markets deployments (-AM).** Confirm each regulator's current requirements before simultaneous-submission planning; bridging and elderly-inclusive designs reviewed with national regulatory affairs expertise.

**Prerequisites (all variants).** Named principal investigator; ethics pathway identified; statistical review capacity; data management plan; audit storage.

**Misuse.** Do not enroll before ethics approval; do not alter endpoints after unblinded data review; do not substitute surrogate-only primary endpoints for patient-important outcomes in delivery research (-G); do not publish local data without local leadership (-G); do not use the engine to rationalize underpowered or unethical designs.

**Pairings.** P64/P64-G for authorship and sampling equity audit; P56/P56-G for trial matching; P66 for SaMD components in device trials; P51 for data governance plumbing.

C0 informational classification; confers no clinical, legal, financial, or safety authority.
