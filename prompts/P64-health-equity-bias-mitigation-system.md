---
ID: P64
Title: Health Equity & Bias Mitigation System
Registry: CLAI-OS (P-series, open tier)
License: AGPL-3.0
Version: 2.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-10-12
Variant-Family: base · P64-G (Global Equity) · P64-AM (Advanced Markets)
---

# P64: Health Equity & Bias Mitigation System

Abstract: P64 designs health equity and bias mitigation systems across three operating contexts. The base specification audits algorithms for demographic bias (race, ethnicity, gender, age, socioeconomic status), adjusts for structural determinants (access, insurance, transportation, language), enforces representative training data, implements fairness metrics (equalized odds, calibration across groups), and generates culturally adapted recommendations — illustrated by the kidney-transplant waitlist audit that removes the race coefficient from eGFR and separates medical urgency from access barriers. The P64-G Global Equity variant hardens the same position into reparative engineering: race removed from all clinical equations (CKD-EPI 2021 race-free eGFR, GLI-2012 spirometry, ancestry-appropriate references), training data deliberately oversampled for underrepresented populations with a 3x misclassification penalty, mandatory local validation (minimum N=1000 per site), helicopter-research detection, climate-justice analysis, and carbon-minimized AI training. The P64-AM Advanced Markets variant applies the audit to Asia-Pacific calibration: Asian BMI cutoffs, race-free eGFR, GLI-Asian spirometry references, acral melanoma awareness, and angle-closure glaucoma risk. In every variant the standard is the same: equal accuracy across groups, gap-closing rather than status quo, and equity adjustments that are explicit, audited, and reversible under governance.

## The Prompt (Base Specification)

Provenance: verbatim from the author's base specification (*CLAI OS P51-P70.txt*); no edits beyond whitespace.

ROLE: You are a Health Equity Researcher who designs AI systems that reduce, not amplify, healthcare disparities. You understand algorithmic bias, social determinants of health, and culturally competent care.
ACTION: Design an equity-focused prompt that:
1.  Audits for demographic bias (race, ethnicity, gender, age, socioeconomic status)
2.  Adjusts for structural determinants (access, insurance, transportation, language)
3.  Ensures representative training data (diversity in examples, case studies)
4.  Implements fairness metrics (equalized odds, calibration across groups)
5.  Generates culturally adapted recommendations (not one-size-fits-all)
SCOPE:
•  Bias detection: pre-deployment, in-deployment, post-deployment
•  Adjustment: risk scores, resource allocation, treatment recommendations
•  Representation: diverse patient examples, not stereotyped
•  Fairness: equal accuracy across groups, not equal treatment
•  Equity: closing gaps, not maintaining status quo
CONTEXT:
[INSERT: Patient population demographics, known disparities, health system equity goals, community partnerships]
EXAMPLES:
Bias Audit:
ALGORITHM: Kidney transplant waitlist priority score
AUDIT FINDINGS:
•  Race adjustment: eGFR calculation includes race coefficient
•  Effect: Black patients have higher eGFR → lower disease severity → lower priority
•  Bias: Systematic underestimation of kidney disease in Black patients
•  Action: Remove race coefficient, use cystatin C-based eGFR
•  Socioeconomic bias: Priority given to patients with private insurance
•  Effect: Uninsured patients wait longer
•  Bias: Structural barrier, not biological
•  Action: Separate medical urgency from access barriers; provide navigation support
•  Geographic bias: Transplant centers concentrated in urban areas
•  Effect: Rural patients face travel burden
•  Bias: Access inequity
•  Action: Telehealth evaluation, travel assistance, satellite clinics
EQUITY-ADJUSTED RECOMMENDATION:
Original score: 72 (moderate priority)
Equity adjustments:
•  Remove race coefficient: +8 points (true disease severity)
•  Add social risk score (housing instability, food insecurity): +5 points
•  Add access barrier (distance >100 miles, no insurance): +3 points
Adjusted score: 88 (high priority)
Rationale: Medical need + structural barriers = higher priority to achieve equity
FORMAT:
•  Bias detection checklist (pre-, in-, post-deployment)
•  Demographic stratification framework
•  Fairness metric calculation
•  Equity adjustment algorithms
•  Community engagement protocol
•  Continuous monitoring dashboard

## Architecture

P64 is a meta-system: it audits and adjusts other clinical algorithms, so its architecture emphasizes measurement integrity, governance gating, and evidence-grade provenance over interaction.

**Deterministic-first safety pathways.** Bias detection executes as deterministic statistical computation — subgroup performance stratification, calibration curves, equalized-odds measurement — over labeled evaluation datasets; the model's role is hypothesis generation about bias sources, audit narrative, and recommendation drafting. Equation substitution (-G: CKD-EPI 2021 race-free, GLI-2012; -AM: Asian BMI thresholds, GLI-Asian references) is a deterministic replacement executed against a versioned equation library; the system blocks deprecated race-adjusted forms from being served. Local validation gates (-G: minimum N=1000 per deployment site) are deterministic pass/fail checks that prevent a model version from entering clinical service until the gate clears.

**FHIR R4 mapping.** Equity audit outputs attach to the audited artifacts rather than patients: audit reports map to MeasureReport with stratifier dimensions (demographic strata, calibration results); fairness thresholds and scoring rules to Measure; monitored risk scores remain Observation on the patient but carry extensions flagging the equity-audited version; structural-determinant findings map to Observation (SDOH categories) and ServiceRequest for navigation support; community engagement and governance approvals to Consent and DocumentReference. All audit artifacts carry signed Provenance.

**Interposition contract.** P64 executes behind the CLAI-OS interposition layer with elevated authority: its deprecation register feeds the Safety Kernel's blocked-content rules, so a race-adjusted equation flagged for retirement cannot be served by any co-deployed prompt. Every adjustment (score modification, reference-equation swap, sampling weight) is emitted in a Clinical Assertion Wrapper with per-claim epistemic labels — measured, configured, or model-proposed — and equity adjustments are never silent: each carries rationale, evidence reference, and reversibility record.

**Audit and provenance stack.** Stratified performance measurements, gate firings, deprecation events, and authorship-equity flags are written to an immutable Merkle-anchored audit trail suitable for regulator and community review; recursive self-audit watches for re-introduction of retired adjustments (bias regression); prompt mortality expires stale equation libraries and fairness thresholds.

**C0 classification.** This artifact is C0 informational: it confers no clinical, legal, financial, or safety authority. Clinical adoption of any equation replacement proceeds through the host institution's clinical governance.

## Variations

### P64-G — Global Equity Variant

Author's variant abstract (*CLAI-OS Global Equity Extension*):

> We present P64-G, a reparative equity engine that removes race from ALL clinical equations. eGFR uses cystatin C-based or CKD-EPI 2021 race-free equations. Spirometry uses GLI-2012 reference equations by ethnicity, not correction factors. VBAC calculators, uterine fibroid risk, and bone density Z-scores use ancestry-specific references, not European T-scores for all. Training data is deliberately oversampled for African, South Asian, Southeast Asian, Latin American, and indigenous populations; the loss function applies 3x penalty for misclassification of underrepresented groups. Local validation is mandatory: every deployed model must be validated on the local population before use. Medical colonialism is addressed through "helicopter research" detection—flagging publications where Northern researchers use local data without local first/senior authorship. Climate justice integration predicts health harms from Northern-caused emissions and advocates for mitigation resources. The carbon footprint of AI itself is minimized by training in renewable-energy regions and avoiding Northern data center shipping.

Variant prompt compiled from the author's Global Equity Extension specification.

ROLE: You are a reparative health-equity systems architect. Your position is technical, not rhetorical: race is a social category, and its use as a biological coefficient in clinical software produces measurable harm. You replace race-adjusted instruments with validated race-free alternatives, you engineer training pipelines that correct sampling injustice, and you audit research and compute practices for extractive patterns.

ACTION: Design a complete reparative equity implementation for the deployment context below. Deliver:
1. A race-free clinical equation library specifying, per instrument, the replacement: eGFR via cystatin C-based or CKD-EPI 2021 race-free equations; spirometry via GLI-2012 reference equations; VBAC calculators, uterine fibroid risk, and bone density Z-scores via ancestry-appropriate references — each with the deprecated race-adjusted form named and blocked
2. A reparative training data plan: deliberate oversampling of African, South Asian, Southeast Asian, Latin American, and indigenous populations, with a loss function applying a 3x misclassification penalty for underrepresented groups, and documentation of sampling provenance
3. A local validation protocol: every deployed model validated on the local population before clinical use, with a minimum sample of N=1000 per deployment site and defined subgroup performance reporting
4. A helicopter research detection module: publication audit logic flagging work where Northern researchers use local data without local first or senior authorship, with an authorship equity report format
5. A climate-justice integration: regression-based prediction of health harms from Northern-caused emissions borne by the deployment population, with an advocacy output framing mitigation resource claims
6. An AI carbon minimization plan: training sited in renewable-energy regions, avoidance of data shipping to Northern data centers, and reporting of compute energy provenance
7. A deprecation register: every race-adjusted instrument found in the host system, its replacement, and its retirement date

SCOPE:
• Race removal is total: "debiasing" a race coefficient is not an acceptable deliverable; replacement is
• Every equation substitution must cite its validated source class (CKD-EPI 2021, GLI-2012, ancestry-appropriate reference); do not invent coefficients
• Local validation is a hard gate: no model enters clinical use without local-population validation at the stated minimum sample
• The engine audits and replaces; clinical interpretation remains with the responsible clinician

CONTEXT:
[INSERT: host health system and instrument inventory; population composition; available local datasets and their provenance; model inventory requiring validation; research partnerships and publication pipelines; compute infrastructure and energy sourcing options]

FORMAT:
• Equation library as a table: instrument | deprecated form | race-free replacement | validation source class | status
• Training plan as a pipeline specification: sampling | weighting | loss penalty | subgroup metrics
• Validation protocol as a numbered gate checklist with pass/fail criteria and subgroup reporting template
• Helicopter research audit as a report template: publication | data origin | authorship positions | flag | recommended action
• Climate and carbon sections as short analytical briefs with stated assumptions and data sources
• "Do Not" list: re-introducing race coefficients "for calibration"; deploying unvalidated models pending data; extracting local data to external compute without local governance approval

Deployment constraint (invariant for this variant): offline-first; open-weight models only (Llama 3 / Mistral / Phi-3 class); no closed-API processing of patient-identifiable data.

### P64-AM — Advanced Markets Variant

From the author's *CLAI-OS Advanced Markets Extension (P51-AM – P70-AM)*. No AM prompt body exists in the source; the variant is specified as deltas against the base prompt.

**What Changes**
| Dimension | US-Centric (P64) | Asia-Pacific (P64-AM) |
|-----------|------------------|----------------------|
| Bias Focus | Race adjustment in algorithms | **Asia-specific bias**: eGFR race coefficient harms Asians (underestimates true GFR). Spirometry "correction" for "smaller lungs" in Asians is biological racism. Asian BMI cutoff (23 vs 25) ignored by US algorithms. Asian diabetes risk at lower BMI. Asian osteoporosis risk at lower BMD T-scores. |
| Adjustment | Risk score tweaking | **Fundamental redesign**: Remove race from ALL equations. Use ancestry-specific reference ranges derived from Asian populations (Japan NDB, Korea NHIS, China CDC, India ICMR). Asian-specific BMI thresholds (WHO Western Pacific: overweight ≥23, obese ≥25). |
| Social Determinants | Insurance, zip code | **Asia-specific**: Urban-rural divide (China/India), hukou system (China internal migration barrier), caste/scheduled tribe (India), burakumin (Japan historical discrimination), foreign worker status (Singapore, Japan), academic credentialism (Korea). |
| Fairness | Equal accuracy across groups | **Reparative accuracy for Asia**: Oversample East Asian, South Asian, Southeast Asian populations in training data. Weight loss function: 3x penalty for misclassification of underrepresented Asian subgroups (e.g., indigenous Taiwan, Ainu Japan, tribal India). |
| Community | Advisory boards | **Asia governance**: Patient data governance in Japan (community-based long-term care councils), India (village health committees), China (resident health committees). AI health systems co-owned by Asian communities, not parachuted by Western vendors. |

**Extended Actions**
```
P64-AM EXTENDED ACTIONS:
6. Remove race from all clinical equations 
   and replace with Asian-specific references:
   - eGFR: Use CKD-EPI 2021 (race-free) 
     or Japanese eGFR equation (adjusted 
     for Japanese body composition)
   - Spirometry: Use GLI-2012 Asian 
     reference equations (not "correction 
     factors" for "smaller lungs")
   - BMI: Apply WHO Western Pacific 
     criteria (overweight ≥23, obese ≥25) 
     for all Asian patients
   - Diabetes screening: FPG ≥100 or 
     HbA1c ≥5.7% for Asians (lower than 
     Western thresholds due to higher 
     visceral fat at lower BMI)
   - Osteoporosis: Use Asian-specific 
     BMD reference populations (Japan, 
     Korea, China have different norms)

7. Build Asian-specific training data:
   - Deliberately oversample East Asian 
     (Japanese, Korean, Han Chinese), 
     South Asian (Indian subcontinent), 
     Southeast Asian populations
   - Weight loss function: Misclassification 
     of underrepresented Asian subgroup = 
     3x penalty vs majority group
   - Local validation: Every deployed 
     model validated on local Asian 
     population before use

8. Address algorithmic racism in Asian 
   healthcare:
   - Western AI trained on Caucasian 
     skin fails on Asian Fitzpatrick 
     III-IV (pigmentary differences, 
     melanoma presentation differences)
   - Western dermatology AI misses 
     acral lentiginous melanoma (higher 
     in Asians, different site distribution)
   - Western ophthalmology AI fails on 
     angle-closure glaucoma (higher in 
     Asians, different optic disc anatomy)

9. Integrate urban-rural equity (China/
   India): AI identifies rural patients 
   with delayed diagnosis (longer travel 
   time, fewer specialists) and prioritizes 
   them for telehealth and mobile clinic 
   outreach.

10. Support indigenous Asian data sovereignty:
    - Ainu (Japan), indigenous Taiwanese, 
      hill tribes (Thailand), Adivasi 
      (India) own their health data
    - AI models trained on indigenous 
      Asian data require community council 
      approval
    - Benefit-sharing if commercial product 
      emerges
```

---

Named jurisdiction examples (from the source): Japan (GLI-Asian spirometry references, super-aging stratifiers); China and East Asia (Asian BMI 23/25 cutoffs (WHO Western Pacific), angle-closure glaucoma risk); Southeast Asia and South Asia (acral melanoma awareness); multi-jurisdiction fairness accountability across PMDA, MFDS, NMPA, and HSA contexts as stated in the source's governance framework.

### Regional Adapters

Regional adapters set the audit targets and reference standards. -AF (Africa): the -G variant is primary — race-free equation library, oversampling and 3x loss penalty for underrepresented populations, local validation gates, helicopter-research detection, renewable-region training siting. -AR (Arab region): equation calibration for regional populations; community governance for dataset construction; conflict-affected population inclusion in sampling frames. -US: the base specification as written — waitlist and risk-score audits, SDOH adjustment, fairness metrics, navigation support; tribal sovereignty modules for datasets involving Native populations. APAC: the -AM variant — Asian BMI 23/25 cutoffs (WHO Western Pacific), race-free eGFR, GLI-Asian spirometry, acral melanoma and angle-closure glaucoma risk calibration, super-aging population stratifiers. Adapters are configuration packs (stratifier sets, reference-equation versions, validation sample minimums, governance contacts); none permits re-introducing group coefficients that the variant family has retired.

## Jurisdiction Matrix

| Regime | Variant applicability | Consent & de-identification posture | Residency & transfer |
|---|---|---|---|
| HIPAA (US) | Base variant (primary) | Audit datasets containing PHI under authorization or de-identification; equity measurement using race/ethnicity data is permitted for health-care operations and civil-rights compliance — document purpose limitation; tribal data under tribal sovereignty agreements | US-hosted; BAAs; de-identified or limited data sets for shared audits |
| GDPR (EU/EEA) | Base-EU; -AM partnerships | Art. 9 covers racial/ethnic origin and health data — equity measurement requires an explicit Art. 9(2) condition (substantial public interest with safeguards); DPIA and necessity/minimization analysis mandatory | EU/EEA residency; transfer of audit aggregates only under SCCs |
| NDPR (Nigeria) | -G variant (primary) | Ethnicity-linked health data is sensitive; reparative oversampling does not exempt lawful basis and consent; community data partnerships documented | In-country training/validation; no export to Northern data centers without community-approved governance |
| Kenya DPA 2019 | -G variant (Kenya) | Sensitive data; registration; community engagement norms for dataset construction | Transfer with safeguards; local validation data retained in-country |
| India DPDP Act | -G/-AM (India) | Consent plus notice; caste/ethnicity-linked stratifiers handled with explicit purpose limitation and legal review | Sectoral program residency rules may apply |
| Brazil LGPD | -G variant (Latin America; oversampled populations) | Sensitive data (racial/ethnic origin, health); explicit consent or public-interest research condition; ANPD guidance on equity measurement | ANPD transfer mechanisms; local processing preferred |
| Saudi PDPL | -G/-AM (Arab region) | Sensitive data; strict transfer controls | In-Kingdom hosting default |
| China PIPL | -AM variant (China) | Sensitive personal information; separate consent for ethnicity-linked processing; PIPIA; algorithmic fairness duties under PIPL automated-decision provisions | Localization default; CAC assessment for export |
| Japan APPI | -AM variant (Japan) | Special-care-required personal information; opt-in consent; note Japan's narrow ethnicity categories — stratifier design requires local legal review | Transfer with consent or equivalent protections |
| Tribal / community consent | -G variant (indigenous populations; core) | CARE principles, OCAP where applicable, community advisory board approval; community consent precedes individual consent for training data; withdrawal rights and benefit-sharing recorded | Community-governed storage; no cross-border transfer without governance approval |

## Methodology

Base: bias detection across the lifecycle (pre-deployment, in-deployment, post-deployment); demographic stratification framework; fairness metric computation (equalized odds, calibration across groups); equity adjustment algorithms separating medical urgency from access barriers; community engagement protocol; continuous monitoring dashboard.

Global Equity (P64-G): race-free clinical equation library (eGFR, spirometry, VBAC, bone density); reparative training data augmentation with 3x loss penalty for underrepresented groups; local validation protocol (minimum N=1000 per deployment site); authorship equity audit algorithm; climate-health impact regression; renewable-energy training site selection.

Advanced Markets (P64-AM): Asia-Pacific calibration audit — Asian BMI thresholds, race-free eGFR validation, GLI-Asian spirometry references, acral-site melanoma screening awareness, angle-closure glaucoma risk stratification; multi-jurisdiction fairness reporting (PMDA/MFDS/NMPA/HSA contexts).

## Merits

• Detects and documents algorithmic bias with regulator-grade stratified measurement rather than anecdote (base)
• Eliminates race coefficients from clinical equations outright and enforces local validation before deployment (-G)
• Corrects sampling injustice structurally: deliberate oversampling plus loss-function penalty, with community governance (-G)
• Extends calibration audit to Asia-Pacific populations whose reference standards differ from Northern defaults (-AM)
• Makes every equity adjustment explicit, evidenced, and reversible — equity by governance, not by assertion

## Guidance for Use

**Base deployments.** Begin with an inventory of algorithms in production and their input features; run the bias audit before any adjustment; publish stratified results to clinical governance; adjustments require sign-off and a rollback plan.

**Global Equity deployments (-G).** Offline-first on locally governed infrastructure; open-weight models only (Llama 3, Mistral, Phi-3 class); no closed-API processing of identifiable data and no shipping of local training data to external data centers without community-approved governance. Equation replacements (CKD-EPI 2021, GLI-2012) are confirmed against current published guidance by clinical governance before cutover; the local validation gate (N=1000 minimum per site) is non-overridable in default configuration. Oversampling requires local data partnership agreements — extraction without governance reproduces the harm this variant exists to end.

**Advanced Markets deployments (-AM).** Confirm population reference standards (Asian BMI, GLI-Asian) against national society guidance; run stratifier design past local legal review where ethnicity categories are legally constrained.

**Prerequisites (all variants).** Labeled evaluation datasets with documented provenance; governance body with authority to gate deployment; versioned equation library; audit storage.

**Misuse.** Do not reintroduce group coefficients 'for calibration'; do not deploy unvalidated models pending data; do not use stratified data for any purpose beyond the documented equity measurement; do not present audit outputs as regulatory certification.

**Pairings.** Audits every clinical prompt in the family (P52, P53, P61, P62, P63 and their variants); P65/P65-G for research authorship equity; P105-class data sovereignty governance for dataset custody; P51 for compliance plumbing.

C0 informational classification; confers no clinical, legal, financial, or safety authority.
