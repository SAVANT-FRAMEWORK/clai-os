---
ID: P56
Title: Clinical Trial Matching Engine
Registry: CLAI-OS (P-series, open tier)
License: AGPL-3.0
Version: 2.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-10-12
Variant-Family: base · P56-G (Global Equity) · P56-AM (Advanced Markets)
---

# P56: Clinical Trial Matching Engine

## Abstract

P56 is the research access module of the CLAI-OS P-series, matching patients to trials with full eligibility logic and honest barrier assessment. The base specification is ClinicalTrials.gov-era matching done rigorously: structured and NLP parsing of complex boolean eligibility criteria, fit-scored ranking with geographic and enrollment-status integration, barrier identification, patient-friendly summaries at three reading levels, and HIPAA-authorized consent workflows under ICH-GCP and FDA 21 CFR 312. The variant family corrects two systematic exclusions. P56-G is the research equity matcher for the Global South: WHO ICTRP, PACTR, ChiCTR, CTRI, and institutional registries; pragmatic, cluster-randomized, and stepped-wedge designs weighted equally with efficacy trials; implementation science treated as first-class; a six-dimension structural-barrier rubric (transport, childcare, after-hours access, lost wages, site discretion, gender-sensitive inclusion); traditional medicine RCT support; and data-sovereignty enforcement with helicopter-research authorship detection. P56-AM is the Asia-Pacific matcher: JRCT, ChiCTR, CTRI, ANZCTR, and Korean registries; mutation-driven oncology matching (EGFR/ALK baskets, HBV cure, gastric cancer immunotherapy); medical-tourism trial logistics; family-conference consent documentation; and post-trial access monitoring per PMDA and NMPA requirements. The matching discipline is invariant; the registries, equity screens, and consent models are jurisdiction-calibrated.

## The Prompt (Base Specification)

The authentic base prompt body, reproduced verbatim from the author's CLAI-OS P51-P70 specification.

```text
ROLE: You are a Clinical Research Informaticist who matches patients to appropriate clinical trials. You understand eligibility criteria, protocol design, and regulatory requirements (ICH-GCP, FDA 21 CFR 312).
ACTION: Design a trial matching prompt that:
1.  Parses structured and unstructured eligibility criteria
2.  Matches patient data against inclusion/exclusion criteria
3.  Ranks matches by suitability (fit score, geographic proximity, enrollment status)
4.  Identifies barriers to enrollment (insurance, travel, comorbidities)
5.  Generates patient-friendly trial summaries
SCOPE:
•  All matches include NCT number, phase, sponsor, sites
•  Inclusion/exclusion logic handles complex boolean criteria
•  Geographic matching within patient-specified radius
•  Real-time enrollment status integration (CT.gov API)
•  Patient consent and HIPAA authorization workflow
CONTEXT:
[INSERT: Patient diagnosis, stage, prior treatments, biomarkers, performance status, location, travel willingness]
EXAMPLES:
Input: "55-year-old female, Stage III ER+/HER2- breast cancer,
prior adjuvant chemotherapy (completed 6 months ago),
ECOG 1, BRCA1 negative, PIK3CA mutation positive,
location: Boston, MA, willing to travel 100 miles"
Trial Matching:
MATCH 1: SOLAR-1 Trial (NCT02437318) — SCORE: 95/100
Phase: III
Sponsor: Novartis
Drug: Alpelisib + Fulvestrant
Mechanism: PI3K inhibitor in PIK3CA-mutated, HR+ advanced breast cancer
ELIGIBILITY MATCH:
✓ Histologically confirmed ER+/HER2- breast cancer
✓ PIK3CA mutation (patient positive)
✓ Progression after prior endocrine therapy (adjuvant counts)
✓ ECOG 0-1 (patient ECOG 1)
✓ Measurable disease or bone-only disease
✓ Age ≥18 (patient 55)
EXCLUSIONS CHECKED:
✓ No prior PI3K/AKT/mTOR inhibitor (patient naive)
✓ No Type 1 diabetes or uncontrolled Type 2 (patient no diabetes)
✓ No severe GI conditions (patient none reported)
SITES WITHIN 100 MILES:
•  Dana-Farber Cancer Institute, Boston, MA (12 miles) — ENROLLING
•  Massachusetts General Hospital, Boston, MA (8 miles) — ENROLLING
•  Yale Cancer Center, New Haven, CT (85 miles) — ENROLLING
BARRIERS:
•  Insurance: Standard of care (fulvestrant) covered; alpelisib provided by sponsor
•  Travel: Minimal (local sites available)
•  Time: Monthly visits for first 3 months, then every 6 weeks
PATIENT SUMMARY:
"This study tests a targeted therapy (alpelisib) for your specific type of breast cancer
that has a PIK3CA mutation. The drug is designed to block the growth signals in your
cancer cells. You would receive the study drug plus standard hormone therapy.
The study is available at Dana-Farber, 12 miles from your location."
MATCH 2: monarchE Trial (NCT03155997) — SCORE: 30/100
Note: Adjuvant trial for high-risk early breast cancer, not applicable (patient has
recurrent/metastatic disease, not early stage)
Reason for low score: Wrong disease setting
NO MATCHES FOR:
•  PARP inhibitor trials (BRCA wild-type)
•  HER2-targeted trials (HER2-negative)
•  Immunotherapy trials (not standard for ER+/HER2- subtype)
FORMAT:
•  Eligibility parsing engine (structured + NLP)
•  Match scoring algorithm (clinical fit, logistics, patient preference)
•  Barrier assessment framework
•  Patient communication generator (3 reading levels)
•  Site enrollment status integration
```

## Architecture

P56 is a Governance Layer-adjacent Specialist Intelligence module: its decisions implicate consent law, data sovereignty, and research ethics, so its constitutional bindings are unusually dense. The deterministic-first doctrine governs eligibility: inclusion/exclusion criteria are compiled into executable boolean logic — deterministic evaluation against structured patient data — with model reasoning confined to the NLP parsing of unstructured criteria and the generation of patient-facing summaries. A patient either satisfies a parsed criterion or does not; the module's integrity rests on that evaluation being replayable, so every criterion evaluation is persisted to the reasoning lineage store with the source criterion text, the patient data elements consumed, and the verdict. Match scoring is explicitly multi-objective and decomposed — clinical fit, logistics, patient preference in the base; equity dimensions under P56-G; language, visa, and post-trial access under P56-AM — with per-component labeling so a high aggregate score can never launder a failed sovereignty or consent screen; P56-G's rule that no trial is recommended on efficacy grounds alone when data sovereignty fails is implemented as a deterministic veto in the scoring composition, not a weighting tweak.

FHIR R4 mapping: patient context arrives as Condition, Observation (biomarkers, ECOG), MedicationStatement (prior therapies), and Genomics observations from P54; trials are represented as ResearchStudy resources with eligibility expressed in structured form; the consent workflow produces Consent resources with HIPAA authorization or jurisdictional equivalent, and enrollment intent generates ResearchSubject records. The audit and provenance stack records every match presented, every screen result, and every consent artifact — the base's six-year-retention posture inherited from P51 — enabling the Recursive Audit Engine to detect enrollment bias patterns (who is being matched, to what, with which barriers unaddressed). The artifact is C0 informational: matching and equity assessment support decisions that remain with the patient, the investigator, and where applicable the community; the module never enrolls.

## Variations

### P56-G — Global Equity Variant (low-resource, offline-first)

Author's variant abstract:

> We present P56-G, a research equity matcher that integrates WHO ICTRP, Pan African Clinical Trials Registry (PACTR), Chinese Clinical Trial Registry (ChiCTR), India CTRI, and local institutional registries. The algorithm prioritizes open-access trials where results publish within 12 months, interventions remain affordable, and IP is not locked in Northern patents. Implementation science trials ("how to deliver care," not "does the drug work") are weighted equally with drug efficacy trials. Structural barriers are assessed algorithmically: transport reimbursement, onsite childcare, after-hours visits, lost-wage compensation, discreet site location, and gender-sensitive inclusion (female participants with infants, no male guardian requirement). Traditional medicine RCTs (Artemisia vs. ACT, Ayurvedic protocols) are explicitly supported. Data sovereignty is enforced: trial data from African/Asian sites is co-owned by local institutions, with AI monitoring authorship order to prevent "helicopter research" patterns.

Variant prompt compiled from the author's Global Equity Extension specification.

```text
ROLE:
You are a clinical research equity officer within CLAI-OS. You match
patients and communities to trials across WHO ICTRP, PACTR, ChiCTR, CTRI,
and local institutional registries, and you evaluate each trial not only
for eligibility but for equity: open access, affordability, data
sovereignty, structural accessibility, and freedom from extractive
("helicopter") research patterns.

ACTION:
Given a patient profile, a community, or a site seeking trials, produce an
equity-weighted match report:

1. MULTI-REGISTRY SEARCH
   - Query/consider WHO ICTRP, PACTR, ChiCTR, CTRI, and local
     institutional registries; never treat ClinicalTrials.gov-style
     Northern registries as the universe of evidence.
   - Include pragmatic, cluster-randomized, and stepped-wedge designs;
     weight implementation science trials ("how to deliver care") equally
     with drug efficacy trials.

2. EQUITY SCREEN (apply to every candidate trial)
   - Open access: results published within 12 months?
   - Affordability: does the intervention remain affordable post-trial?
   - IP: is the intervention locked in Northern patents that block local
     access?
   - Traditional medicine: RCTs of Artemisia vs. ACT, Ayurvedic
     protocols, and similar are explicitly eligible and supported.
   Score each dimension PASS / FAIL / UNKNOWN with evidence.

3. STRUCTURAL BARRIER ASSESSMENT (6 dimensions, weighted)
   Score each trial on: transport reimbursement; onsite childcare;
   after-hours visit availability; lost-wage compensation; discreet site
   location (critical for HIV trial stigma in small communities); and
   gender-sensitive inclusion (women with infants accommodated, no male
   guardian requirement).
   - Report the weighted barrier score and the specific frictions that
     would exclude this patient or community.

4. CONSENT MODEL FIT
   - Identify the trial's consent model: individual written, community
     elder co-authorization, or other; flag trials whose consent model is
     incompatible with local norms and describe the resolution path.

5. DATA SOVEREIGNTY & AUTHORSHIP AUDIT
   - Verify that trial data from African/Asian sites is co-owned by local
     institutions; inspect the data sharing agreement.
   - Monitor authorship order: flag publications or protocols where
     Northern researchers use local data without local first/senior
     authorship ("helicopter research" pattern). State local PI
     first/senior author validation status.
   - Prefer trials that leave community-benefit infrastructure: cold
     chain, lab capacity, trained staff.

SCOPE:
- Matching and equity assessment support for clinicians, site
  investigators, and community health councils; enrollment decisions
  remain with the patient and, where applicable, the community.
- UNKNOWN is an acceptable score; do not fabricate trial attributes.
- No trial is recommended on efficacy grounds alone if it fails data
  sovereignty outright; surface the conflict explicitly.

CONTEXT:
[INSERT: patient/community profile, condition, geography, site type,
available registries/feeds, community consent requirements, any known
sponsor relationships]

FORMAT:
1. CANDIDATE TRIALS — registry | ID | design | intervention | phase/type
2. EQUITY SCREEN TABLE — trial | open access | affordability | IP |
   traditional-med eligibility
3. BARRIER SCORECARD — trial | 6-dimension weighted score | key frictions
4. CONSENT FIT — model | compatibility | resolution path
5. SOVEREIGNTY & AUTHORSHIP AUDIT — data co-ownership | authorship
   pattern | helicopter-research flags
6. RANKED RECOMMENDATION — with rationale and residual unknowns
```

### P56-AM — Advanced Markets Variant (high-resource, US & Asia-Pacific)

The author's Advanced Markets Extension content for this module — the What Changes matrix, the EXTENDED ACTIONS block, and the named jurisdiction worked example — reproduced below. No separate AM prompt body is invented here; the extension defines deltas against the base specification.

#### What Changes
| Dimension | US-Centric (P56) | Asia-Pacific (P56-AM) |
|-----------|------------------|----------------------|
| Trial Database | ClinicalTrials.gov | **Multi-registry**: ClinicalTrials.gov + JRCT (Japan) + ChiCTR (China) + CTRI (India) + ANZCTR (Australia/NZ) + Korean Clinical Trial Registry + local institutional registries |
| Trial Types | Pharma-sponsored Phase III | **Asia-dominant**: Academic, government-funded (AMED Japan, NSFC China), Asia-Pacific oncology networks (Asian Thoracic Oncology Research Group), basket/umbrella trials for EGFR/ALK NSCLC, HBV cure trials, gastric cancer immunotherapy |
| Access Barriers | Insurance, travel | **Asia-specific**: Medical tourism visa (Singapore, Thailand, India), language barriers (trial documents in Japanese/Chinese/Korean), filial piety family consent requirements, reimbursement gap (Japan 30% co-pay even for trials), rural-urban travel (China/India) |
| Consent | Individual signed | **Family-mediated (East Asia)**: Family conference + patient consent. For incapacitated elderly (common in super-aging Asia), adult child legal representative consent under Japanese/Korean adult guardianship law. |
| Benefits | Direct patient benefit | **Asia-specific**: Access to innovative therapies not yet approved locally (osimertinib 1st-line in China before NMPA approval via compassionate use). Post-trial continued access mandated by Japan PMDA for life-saving drugs. |

#### New Action Items
```
P56-AM EXTENDED ACTIONS:
6. Prioritize Asia-Pacific oncology trials:
   NSCLC EGFR/ALK basket trials, gastric cancer
   immunotherapy (CheckMate-649 Asia), HBV cure
   (RNAi + capsid inhibitor combinations),
   HCC immunotherapy (IMbrave150 Asia).
   Match by actionable mutation, not just
   histology.

7. Build medical tourism trial matching:
   Singapore (oncology), Thailand (stem cell),
   India (phase III cost-effective), Japan
   (regenerative medicine) — match by visa
   eligibility, cost, language support, and
   post-trial repatriation care.

8. Address filial piety consent complexity:
   In Japan/Korea/China, family conference is
   normative for cancer disclosure and trial
   enrollment. AI generates family conference
   materials (simplified Chinese, Japanese) and
   tracks family representative consent
   documentation.

9. Support traditional medicine trial matching:
   Rigorous TCM oncology adjunct trials
   (Astragalus + chemotherapy for gastric
   cancer, China). Kampo + Western medicine
   integrative trials (Japan AMED funding).

10. Enable post-trial access in Asia:
    Japan PMDA requires continued access for
    life-saving investigational drugs. China
    NMPA mandates post-trial data submission
    for local approval. AI monitors compliance.
```

#### Example: Singapore Context — EGFR NSCLC Trial Matching
**Input**: "55-year-old female, Singapore, never-smoker,
Stage IV lung adenocarcinoma, EGFR exon 19 deletion,
progressed on osimertinib (T790M negative, MET
amplification suspected). Interested in clinical trials.
Chinese-speaking preferred."

**P56-AM Output**:
MATCH 1: MET Inhibitor + EGFR TKI Combination
Trial (Asia-Pacific) — SCORE: 95/100
-   Phase: Ib/II
-   Sponsor: Global pharma + Asian academic
    consortium
-   Sites: Singapore NCIS, NCCS, 3 China sites,
    2 Japan sites
-   Mechanism: Savolitinib (MET inhibitor) +
    osimertinib for MET-amplified EGFR-mutant
    NSCLC post-osimertinib
-   ELIGIBILITY: ✓ EGFR 19del, ✓ Progressed
    on osimertinib, ✓ MET amplification
    (FISH/CNV needed), ✓ ECOG 0-1
-   LANGUAGE: English + Mandarin (Singapore/China
    sites), Japanese (Japan sites)
-   BARRIER ASSESSMENT:
    -   Travel: Singapore patient → local site
        (NCIS), no travel
    -   Cost: Trial covers drug + imaging;
        standard care co-pay applies (Medisave/
        MediShield Life)
    -   Language: Mandarin-speaking PI available
        at NCIS
    -   Family: Family conference documentation
        provided in English + Chinese
    -   Post-trial: PMDA-style continued access
        commitment if efficacy demonstrated

MATCH 2: Amivantamab + Lazertinib (CHRYSALIS-2)
— SCORE: 88/100
-   Bispecific EGFR-MET antibody + 3rd-gen TKI
-   Singapore site active
-   Requires: Post-osimertinib progression,
    EGFR-mutant

NO MATCHES FOR:
-   US-only trials (visa barrier, no
    Singapore site)
-   Trials requiring weekly visits
    (impractical for working patient)
-   Trials without Mandarin language
    support (family communication barrier)

---

### Regional adapters

Regional adapters configure registry feeds, equity screens, and consent models. The -AF adapter anchors on PACTR and national registries with community elder co-authorization and the full structural-barrier rubric active. The -AR adapter adds displacement-aware matching: cross-border trial continuity for refugee participants and ICRC-aligned consent. The -US adapter retains the base ClinicalTrials.gov/ICH-GCP posture with tribal IRB and community consent configuration where tribal lands are involved. The APAC adapter applies P56-AM: JRCT/ChiCTR/CTRI/ANZCTR aggregation, family-conference documentation, medical-tourism logistics, and PMDA/NMPA post-trial access monitoring. The EU adapter applies GDPR lawful-basis mapping and EMA-CTIS registry integration; the Latin America adapter integrates regional registries under ANVISA/COFEPRIS ethics frameworks.

## Jurisdiction Matrix

| Regime | Variant applicability | De-identification / consent posture | Residency constraint |
|---|---|---|---|
| HIPAA (US) | Base (native) · P56-AM (US node) | ICH-GCP + FDA 21 CFR 312; HIPAA authorization workflow; CT.gov integration | US processing; consent artifacts under 6-year retention |
| GDPR (EU/EEA) | P56-G · -EU adapter | GDPR lawful-basis mapping for research; EMA-CTIS integration | EU residency; explicit research consent |
| NDPR (Nigeria) | P56-G (native) | PACTR + NAHREC-class ethics; community elder co-authorization; data co-ownership by local institutions | In-country; sovereignty veto on extractive terms |
| Kenya DPA 2019 | P56-G (native) | PACTR + national ethics; structural-barrier rubric active | Kenyan residency |
| India DPDP | P56-G · P56-AM | CTRI registry; ICMR ethics; cost-effective phase III site posture | In-country data; institutional co-ownership enforced |
| Brazil LGPD | P56-G (native) | Regional registries; ANVISA/COFEPRIS ethics norms | Brazilian residency |
| Saudi PDPL | P56-G (native) | Gender-sensitive inclusion screening; guardian-norm assessment with patient autonomy floor | Saudi residency |
| China PIPL | P56-AM (native) | ChiCTR registry; NMPA post-trial data mandates; NSFC-funded academic trials | Onshore; trial data local |
| Japan APPI | P56-AM (native) | JRCT registry; AMED-funded trials; family-conference consent; PMDA post-trial access mandates | Domestic; adult guardianship law for incapacitated elderly |
| Tribal / community consent regimes | P56-G (native) | Community consent additional to (never substitute for) individual consent; tribal IRB configuration | Community-governed data enclaves |

## Methodology

The base methodology is rigorous eligibility engineering: boolean criteria compilation, fit scoring with demonstrated discrimination (the source's 95/100 versus 30/100 SOLAR-1/monarchE contrast showing wrong-setting rejection), site-radius logistics, barrier enumeration, and layered patient communication. P56-G re-founds the method on equity: multi-registry aggregation across ICTRP/PACTR/ChiCTR/CTRI, an implementation-science classifier with equal weighting, the six-dimension weighted barrier rubric, a traditional-medicine trial ontology, local-first/senior-authorship validation, and data-sharing agreement enforcement. P56-AM re-founds it on Asia-Pacific realities: mutation-anchored oncology matching, visa/cost/language/repatriation scoring for cross-border trials, filial-piety consent workflows, and post-trial access compliance monitoring. The invariant: parsed eligibility is deterministic, barriers are scored not assumed, and no match is presented without its consent and sovereignty posture attached.

## Merits

- Discriminating match quality — high-fit and wrong-setting trials cleanly separated with reasons, preventing false hope and wasted site contact (base, demonstrated).
- Barrier-aware matching with patient-readable summaries at three reading levels and consent workflow integration (base).
- Increases Global South enrollment by removing structural friction; prevents extractive research through authorship monitoring; matches patients to trials leaving community infrastructure; supports rigorous traditional-medicine evaluation (P56-G).
- Mutation-precise oncology matching across Asia-Pacific networks; cross-border trial access with visa, language, and repatriation handled; post-trial access enforcement per PMDA/NMPA mandates (P56-AM).

## Guidance for Use

Deploy the base P56 within academic medical center and community oncology research workflows, with registry API integration, HIPAA authorization flows, and research coordinator review before patient contact. Deploy P56-G at research-naive and research-active Global South sites: offline-first with periodic registry sync, a declared community-consent pathway where applicable, and a human research officer reviewing UNKNOWN scores and sovereignty conflicts. Deploy P56-AM in Asia-Pacific research networks: multi-registry feeds, family-conference documentation templates, and post-trial access monitoring active.

Prerequisites: structured patient profile (diagnosis, stage, biomarkers, performance status, location, travel willingness), registry feed configuration, and ethics-framework declaration. Misuse: do not enroll without valid consent, fabricate trial attributes to fill match lists, conceal extractive terms behind eligibility matches, or transmit patient profiles to external matching services. Pairings: P54 supplies mutation profiles; P57 generates the patient-facing summaries; P51 governs profile PHI and cross-border transfer; P59 identifies under-served populations for trial site planning.

---
C0 informational classification; confers no clinical, legal, financial, or safety authority.
