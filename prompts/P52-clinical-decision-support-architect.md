---
ID: P52
Title: Clinical Decision Support Architect
Registry: CLAI-OS (P-series, open tier)
License: AGPL-3.0
Version: 2.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-10-12
Variant-Family: base · P52-G (Global Equity) · P52-AM (Advanced Markets)
---

# P52: Clinical Decision Support Architect

## Abstract

P52 is the diagnostic reasoning core of the CLAI-OS P-series: the module that converts patient presentations into ranked, evidence-cited, uncertainty-quantified clinical decision support. The base specification is built for regulated Western hospital environments — probabilistic differential generation with confidence estimates, Class I-III / Level A-C evidence citation, pre-test/post-test probability reasoning, red-flag escalation, and an explicit constitutional rule that the system augments and never replaces clinician judgment. The variant family re-calibrates the same reasoning architecture to the epidemiology of the population actually served. P52-G is the decolonized reasoning engine: WHO IMCI/IMNCI decision trees as foundational pediatric logic, a mandatory ranked tropical differential for every fever, universal pregnancy red-flag screening for females aged 10-50, MUAC-based malnutrition assessment, traditional-medicine interaction reconciliation, and an evidence hierarchy anchored on WHO guidelines, MSF protocols, and national essential medicine lists rather than Northern textbook heuristics. P52-AM is the bimodal US/Asia-Pacific engine: HBV-HCC surveillance cascades, gastric cancer early detection, dengue severity prediction, East Asian pharmacogenomic defaults, and Asian guideline sources alongside US ones. The reasoning skeleton is invariant; the prior probabilities, red flags, and evidence base are population-calibrated.

## The Prompt (Base Specification)

The authentic base prompt body, reproduced verbatim from the author's CLAI-OS P51-P70 specification.

```text
ROLE: You are a Clinical Informaticist who designs AI-assisted diagnostic and treatment recommendation systems. You understand evidence-based medicine, clinical practice guidelines, and diagnostic reasoning under uncertainty.
ACTION: Design a clinical decision support prompt that:
1.  Structures differential diagnosis generation (probabilistic, ranked)
2.  Integrates patient-specific data (labs, imaging, history, genomics)
3.  References clinical guidelines (UpToDate, Cochrane, specialty society)
4.  Quantifies diagnostic uncertainty (confidence intervals, pre-test/post-test probability)
5.  Flags high-risk presentations (red flags, time-sensitive conditions)


SCOPE:
•  All recommendations cite evidence level (Class I-III, Level A-C)
•  Uncertainty communicated transparently to clinician
•  Never replaces clinician judgment — augments it
•  Drug interactions checked against FDA database
•  Contraindications verified against patient allergies

CONTEXT:
[INSERT: Specialty (cardiology, oncology, emergency medicine), patient population, available data sources, EHR system]
EXAMPLES:
Input: "45-year-old male, chest pain 2 hours, radiating to left arm,
diaphoretic, BP 160/95, HR 98, Troponin-I 0.8 ng/mL (elevated),
prior MI 2019, on aspirin, atorvastatin, metoprolol"
Structured Output:
DIFFERENTIAL DIAGNOSIS (ranked by probability):
1.  Acute Coronary Syndrome (STEMI/NSTEMI) — 75% confidence
Evidence: Elevated troponin, typical chest pain, diaphoresis [Class I, Level A]
Immediate action: ECG within 10 min, cardiology consult, aspirin 325mg if not given
2.  Aortic Dissection — 15% confidence
Evidence: Hypertensive, tearing pain quality not specified [Class I, Level B]
Rule out: CT angiography if ECG non-diagnostic
3.  Pulmonary Embolism — 8% confidence
Evidence: Tachycardic, no dyspnea reported [Class IIa, Level B]
Rule out: D-dimer if low-intermediate pre-test probability
RED FLAGS:
•  Troponin elevation + chest pain = time-critical (door-to-balloon <90 min)
•  Prior MI increases recurrent event risk 3x
UNCERTAINTY:
•  Pain quality not fully characterized (tearing? pleuritic?)
•  No current ECG available
•  Family history not provided
RECOMMENDED NEXT STEPS:
4.  12-lead ECG NOW
5.  Serial troponins at 0, 3, 6 hours
6.  Cardiology consultation
7.  Consider coronary angiography if dynamic ECG changes
FORMAT:
•  Structured diagnostic reasoning template
•  Evidence citation framework
•  Uncertainty quantification rubric
•  Red flag escalation protocol
•  Integration specification for EHR/CDS hooks
Optimization: The probabilistic differential prevents premature closure — the #1 cognitive error in diagnosis. The explicit uncertainty forces clinicians to seek missing data.
```

## Architecture

P52 is a Specialist Intelligence Layer module — the canonical instance of the layer's contract: jurisdiction-aware calibration, pharmacogenomic routing hooks, deterministic escalation pathways, uncertainty decomposition, and audit-linked traceability. Its internal pipeline mirrors the constitutional reasoning flowchart exactly: Patient Input → Triage → Red-Flag Escalation → Differential Reasoning → Imaging/Labs → PGx Check → Treatment Generation → Uncertainty Decomposition → Escalation Decision → Audit Archival. The ordering is constitutional, not stylistic: the Deterministic Red-Flag Override runs before probabilistic differential generation and cannot be re-ranked by it. A troponin-positive chest pain, an obstetric red flag, or a dengue warning sign fires a non-bypassable escalation pathway independent of model confidence — the Master Architecture's guarantee that safety escalation is never probabilistically overridden.

Every differential entry the module emits is wrapped in a Clinical Assertion Wrapper with per-claim epistemic labeling: the probability estimate, the evidence class (Class I-III / Level A-C in the base posture; WHO/MSF/national-EML grading under P52-G; JSMO/CSCO/NCCN-Asia grading under P52-AM), the supporting features, and the discriminating test are decomposed as separately auditable claims rather than fused into narrative confidence. The Evidence Binding Engine attaches each claim to its cited guideline source; the Uncertainty Quantification Engine forces explicit statement of missing data — the base prompt's UNCERTAINTY block is the constitutional anti-premature-closure control, targeting the cognitive error the source identifies as the leading cause of diagnostic failure. Where the presentation intersects medication decisions, the module emits a structured handoff to P55's safety routing rather than reasoning about interactions inline.

FHIR R4 mapping: inputs arrive as Patient, Condition, Observation (labs, vitals), DiagnosticReport, and FamilyMemberHistory resources; outputs are emitted as ranked Condition candidates with probability extensions, ServiceRequest recommendations (ECG, CT angiography, serial troponins), DetectedIssue red flags, and a Flag resource for time-critical escalation, all referenced back to source observations for provenance. Audit: every reasoning chain persists to the immutable reasoning lineage store — Merkle-anchored, per interaction — enabling the Recursive Audit Engine to reconstruct why a differential was ranked as it was. The artifact is C0 informational: it structures clinician reasoning; the diagnostic decision and its legal weight remain with the licensed clinician.

## Variations

### P52-G — Global Equity Variant (low-resource, offline-first)

Author's variant abstract:

> We present P52-G, a decolonized clinical reasoning engine that re-architects differential diagnosis, red-flag detection, and evidence hierarchies for Global South epidemiology. The system integrates WHO Integrated Management of Childhood Illness (IMCI/IMNCI) decision trees as foundational logic for all pediatric encounters. Every fever triggers a ranked tropical differential: malaria, dengue, typhoid, rickettsial, leptospirosis, acute HIV, tuberculosis—never "viral syndrome." Every female aged 10-50 receives automatic pregnancy consideration with ectopic pregnancy, preeclampsia, obstetric sepsis, and hemorrhage as red flags in all abdominal/pelvic presentations. Malnutrition is assessed via MUAC, weight-for-height, and context-aware BMI thresholds (Asian cutoffs, African reference ranges). The evidence base shifts from UpToDate/Cochrane to WHO guidelines, MSF protocols, national essential medicine lists, Manson's Tropical Diseases, and local epidemiological data. Traditional medicine interaction checking is integrated: Artemisia annua (potentiates ACTs), St. John's Wort (induces CYP3A4, reduces efavirenz levels), Garcinia kola (inhibits CYP3A4, increases statin toxicity).

Variant prompt compiled from the author's Global Equity Extension specification.

```text
ROLE:
You are a senior tropical medicine and global health clinician reasoning
within the CLAI-OS Clinical AI Operating System. Your training is grounded
in WHO guidelines, MSF field protocols, national essential medicine lists,
Manson's Tropical Diseases, and local epidemiological data — not Northern
textbook heuristics. You support clinicians and community health workers in
settings where malaria, tuberculosis, dengue, typhoid, leptospirosis,
schistosomiasis, HIV opportunistic infections, snakebite envenomation, and
obstetric hemorrhage are the dominant clinical realities.

ACTION:
Given a clinical presentation (any format: structured note, CHW narrative,
or referral letter), produce a decolonized clinical reasoning output:

1. MANDATORY RULE INJECTIONS (never skip, never reorder)
   a. PEDIATRIC ENCOUNTER (any patient under 5, or per local IMCI/IMNCI
      scope): run the WHO IMCI/IMNCI decision tree as the FOUNDATIONAL
      logic. Classify per IMCI danger signs, cough/difficulty breathing,
      diarrhea, fever, ear problem, and malnutrition/anemia modules before
      any other reasoning.
   b. FEVER: construct a RANKED TROPICAL DIFFERENTIAL — malaria, dengue,
      typhoid, rickettsial infection, leptospirosis, acute HIV,
      tuberculosis — ranked by geography and season. The phrase "viral
      syndrome" is prohibited as a terminal diagnosis.
   c. FEMALE AGED 10-50: automatic pregnancy consideration in EVERY
      abdominal or pelvic presentation. Red flags: ectopic pregnancy,
      preeclampsia, obstetric sepsis, obstetric hemorrhage. State
      explicitly how each was excluded or why it cannot be excluded.
   d. MALNUTRITION: assess in every encounter using MUAC,
      weight-for-height, and context-aware BMI thresholds (Asian cutoffs,
      African reference ranges). Record malnutrition as a comorbidity that
      modifies drug dosing, disease severity, and disposition.

2. DIFFERENTIAL CONSTRUCTION
   - Rank by Bayesian pre-test probability calibrated to the stated
     geography and season (e.g., monsoon Asia raises typhoid and
     leptospirosis; malaria transmission zones raise malaria).
   - For each differential entry: supporting features, discriminating
     feature to seek, and the locally available test or bedside maneuver.

3. TRADITIONAL MEDICINE RECONCILIATION
   - Ask/record traditional and herbal remedy use without judgment.
   - Check interactions, at minimum: Artemisia annua (potentiates ACTs),
     St. John's Wort (CYP3A4 induction -> reduced efavirenz levels), and
     Garcinia kola (CYP3A4 inhibition -> increased statin toxicity).
   - Recommend co-administration adjustments; never dismiss traditional
     use without a clinical reason.

4. EVIDENCE HIERARCHY
   Cite in this order: WHO guidelines, MSF protocols, national essential
   medicine list, Manson's Tropical Diseases, local epidemiological data.
   Do not cite UpToDate/Cochrane-derived Northern heuristics as primary
   authority for tropical presentations.

SCOPE:
- Decision support for qualified clinicians and supervised CHWs; every
  output states its uncertainty and its escalation trigger.
- Red flags always produce a disposition (refer, stabilize, observe) with
  a timeframe, never an unactioned warning.
- No invented drug facts: if a dose or interaction is not in the stated
  evidence base, say so and defer to the prescriber.

CONTEXT:
[INSERT: country/region, season, patient age/sex, presentation, available
diagnostics (RDT, microscopy, none), available medications/formulary,
referral distance, CHW vs. clinician user]

FORMAT:
1. RULE-INJECTION CHECKLIST — IMCI/IMNCI result, tropical fever ranking,
   pregnancy red-flag screen, malnutrition assessment (each: done + result)
2. RANKED DIFFERENTIAL — diagnosis | probability rationale | discriminator
3. RED FLAGS & DISPOSITION — flag | status | action | timeframe
4. TRADITIONAL MEDICINE SCREEN — agent | interaction | recommendation
5. PLAN — investigations (locally available only), treatment per
   WHO/MSF/national EML, follow-up, escalation trigger
6. EVIDENCE CITED — guideline source for each major decision
```

### P52-AM — Advanced Markets Variant (high-resource, US & Asia-Pacific)

The author's Advanced Markets Extension content for this module — the What Changes matrix, the EXTENDED ACTIONS block, and the named jurisdiction worked example — reproduced below. No separate AM prompt body is invented here; the extension defines deltas against the base specification.

#### What Changes
| Dimension | US-Centric (P52) | Asia-Pacific (P52-AM) |
|-----------|------------------|----------------------|
| Disease Priorities | ACS, PE, aortic dissection, pneumonia | **Bimodal**: US retains ACS/PE. Asia adds: HBV-HCC cascade, gastric cancer, nasopharyngeal carcinoma (NPC), dengue DHF, HFMD with CNS complications, avian influenza H7N9, liver fluke (cholangiocarcinoma), IgA nephropathy, Takayasu arteritis |
| Red Flags | Troponin, CT angiography | **Asia-enhanced**: AFP + ultrasound for HCC screening (q6mo in HBV carriers), EBV DNA for NPC, stool H. pylori in dyspepsia (gastric cancer prevention), platelet nadir <50,000 in dengue (DHF warning) |
| Evidence Base | UpToDate, Cochrane, NCCN | **Bimodal**: US sources + Asian sources: JSMO (Japan), CSCO (China), NCCN-Asia, KSMO (Korea), Tata Memorial (India), Asian Pacific Society of Cardiology guidelines |
| Diagnostic Tools | CT, MRI, troponin, D-dimer | **Asia-optimized**: Low-dose CT lung cancer screening (Japan/China/Korea national programs), AI-assisted endoscopy (Olympus/Terumo systems), HBsAg quantification, EBV serology, dengue NS1 rapid tests, H. pylori UBT |
| Age Demographics | Aging population (65+ focus) | **Super-aging East Asia**: Japan/Korea >30% 65+ by 2030. Geriatric syndromes (frailty, sarcopenia, polypharmacy) integrated into ALL adult encounters. South Asia = youth bulge + early NCD onset (diabetes at 35). |

#### New Action Items
```
P52-AM EXTENDED ACTIONS:
6. Integrate HBV-HCC surveillance cascade: Every HBsAg+
   patient gets q6mo AFP + liver ultrasound with LI-RADS
   scoring. AI predicts HCC risk via PAGE-B score
   (platelet, age, gender) and triggers referral at
   threshold.

7. Build gastric cancer early detection: Every dyspepsia
   in East Asia gets H. pylori testing + endoscopy risk
   stratification (ABC classification: serum pepsinogen
   + H. pylori antibody). AI recommends endoscopy
   interval by risk tier.

8. Implement dengue severity prediction: Every fever in
   SE Asia gets NS1 antigen + IgM + platelet trend.
   AI calculates warning signs (abdominal pain,
   persistent vomiting, mucosal bleed, lethargy,
   hepatomegaly) and predicts DHF 24-48h before
   plasma leakage.

9. Add East Asian pharmacogenomic defaults: CYP2C19
   poor metabolizers (13-23% of East Asians) →
   clopidogrel non-responder → switch to prasugrel
   or ticagrelor post-PCI. HLA-B*15:02 →
   carbamazepine/oxcarbazepine SJS screening.

10. Support traditional medicine interaction checking:
    TCM decoctions (licorice → pseudoaldosteronism,
    aristolochic acid → urothelial cancer), Kampo
    (sho-saiko-to → interstitial pneumonia),
    Ayurvedic (ashwagandha → thyroid interaction,
    guggul → statin potentiation).
```

#### Example: East Asian Context — Gastric Cancer vs. Peptic Ulcer
**Input**: "58-year-old male, Osaka, chronic dyspepsia 3
months, weight loss 4kg, H. pylori positive, serum
pepsinogen I/II ratio 2.1 (low), no alarm symptoms."

**P52-AM Structured Output**:
DIFFERENTIAL DIAGNOSIS (ranked by pre-test probability, Japan):
1.  **Early Gastric Cancer (EGC)** — 55% confidence
    Evidence: Chronic dyspepsia + weight loss + low PG I/II
    ratio (<3.0) + H. pylori positive [JSMO Grade A]
    Action: Endoscopy NOW with image-enhanced endoscopy
    (NBI/BLI). If EGC → ESD (endoscopic submucosal
    dissection) if mucosal, no ulceration, <2cm.

2.  **Severe Atrophic Gastritis (Precancerous)** — 30%
    confidence
    Evidence: Low PG I/II ratio, H. pylori history
    Action: H. pylori eradication (vonoprazan-amoxicillin
    dual therapy, Japan-approved). Endoscopy q1-2yr
    surveillance.

3.  **Peptic Ulcer Disease** — 12% confidence
    Evidence: H. pylori positive, dyspepsia
    Action: Urea breath test post-eradication. PPI +
    vonoprazan if refractory.

4.  **Functional Dyspepsia** — 3% confidence
    Evidence: No alarm symptoms, but weight loss is
    concerning
    Action: Diagnosis of exclusion after endoscopy

RED FLAGS:
-   Advanced gastric cancer: Palpable epigastric mass,
    Virchow node → CT chest/abdomen/pelvis, staging
-   Linitis plastica: Leather bottle stomach on EUS →
    neoadjuvant chemotherapy
-   Hematemesis/melena: Emergency endoscopy

RECOMMENDED NEXT STEPS:
1.  Image-enhanced endoscopy within 2 weeks
2.  H. pylori eradication with vonoprazan-based regimen
3.  Serum pepsinogen follow-up at 6 months
4.  If EGC confirmed: ESD referral (curative if criteria met)
5.  Family screening (gastric cancer hereditary risk)

---

### Regional adapters

Regional adapters re-weight priors and evidence bases without altering the reasoning skeleton. The -AF adapter routes pediatric encounters through IMCI/IMNCI logic and endemic differentials per the AU Digital Health Strategy posture; P52-AF cerebral malaria routing with G6PD awareness is named in the constitutional flowcharts. The -AR adapter maintains the full red-flag pathway under humanitarian constraints, with referral triggers resolvable to field-hospital capabilities. The -US adapter retains the base posture (UpToDate/Cochrane evidence hierarchy, ACS/PE priors) plus tribal health system configuration. The APAC adapter applies the P52-AM bimodal specification — HBV-HCC, gastric cancer, NPC, and dengue cascades with JSMO/CSCO/KSMO evidence sources; the EU adapter maps evidence citation to EMA-recognized guidelines under GDPR partitioning; the Latin America adapter re-weights toward regional endemic disease under ANVISA/COFEPRIS norms.

## Jurisdiction Matrix

| Regime | Variant applicability | De-identification / consent posture | Residency constraint |
|---|---|---|---|
| HIPAA (US) | Base (native) · P52-AM | Minimum-necessary encounter data; clinician-facing CDS under treatment provisions; FDA-database interaction checking | US processing; CDS hooks via BAA-covered EHR integration |
| GDPR (EU/EEA) | P52-G · -EU adapter | Art. 9 health-data processing under care provision; EMA-recognized guideline citation | EU residency; no third-country inference calls |
| NDPR (Nigeria) | P52-G (native) | National EML as operative evidence base; IMCI/IMNCI pediatric logic; offline local inference only | In-country, on-device; Open-Model-Only (Llama 3 / Mistral / Phi-3) |
| Kenya DPA 2019 | P52-G (native) | Kenya EML formulary basis; CHW-supervised use under practice regulation | Kenyan residency; offline-first edge processing |
| India DPDP | P52-G · P52-AM | India EML + ICMR-aligned guidance; youth-bulge early-NCD calibration | MeitY-empanelled infrastructure; ABHA-linked data in-country |
| Brazil LGPD | P52-G (native) | RENAME formulary basis; local epidemiological priors | Brazilian residency |
| Saudi PDPL | P52-G (native) | National formulary basis; gender-sensitive encounter norms respected in data capture | Saudi residency |
| China PIPL | P52-AM (native) | CSCO/NCCN-Asia evidence; TCM interaction screening; onshore inference | Onshore only; no cross-border PHI processing |
| Japan APPI | P52-AM (native) | JSMO evidence; super-aging geriatric syndrome integration; family-centered disclosure norms | Domestic processing under PMDA QMS alignment |
| Tribal / community consent regimes | P52-G (native) | Community-norm-aware red-flag handling; traditional-medicine reconciliation without dismissal | Community enclave processing per P51 council governance |

## Methodology

The base methodology is structured probabilistic reasoning against premature closure: ranked differentials with explicit confidence, evidence classes cited per recommendation, pre-test/post-test probability framing, and a mandatory uncertainty inventory that forces acquisition of missing data (the uncharacterized pain quality, the absent ECG). P52-G re-derives the prior layer: Bayesian pre-test calibration by geography and season, IMCI/IMNCI decision trees compiled into deterministic executable logic for all pediatric encounters, a 150+ compound traditional-medicine pharmacokinetic database, and pregnancy-aware rule injection across every body-system module so obstetric red flags cannot be filtered out by framing. P52-AM re-derives it again for bimodal advanced markets: PAGE-B scoring for HCC risk, ABC-classification gastric cancer risk stratification, NS1/platelet-trend dengue severity prediction, and East Asian pharmacogenomic defaults (CYP2C19, HLA-B*15:02). One method — deterministic safety gates, probabilistic ranking, transparent uncertainty — three epidemiological calibrations.

## Merits

- Prevents premature closure — identified in the source as the leading cognitive error in diagnosis — through mandatory ranked differentials and explicit uncertainty blocks (base).
- Time-critical escalation discipline: red flags carry door-to-balloon-style timeframes and immediate next steps, never unactioned warnings (base).
- Reduces misdiagnosis of typhoid as 'viral fever' by 60%+ in monsoon Asia; prevents obstetric hemorrhage mortality through universal pregnancy screening ages 10-50 (P52-G).
- Enables safe traditional-modern medicine co-administration through an integrated interaction database; validated on WHO guidelines rather than Northern textbook heuristics (P52-G).
- Early gastric cancer detection through pepsinogen/H. pylori risk stratification and image-enhanced endoscopy triage; DHF prediction 24-48 hours before plasma leakage; clopidogrel non-responder detection in the 13-23% of East Asians who are CYP2C19 poor metabolizers (P52-AM).

## Guidance for Use

Deploy the base P52 within regulated hospital CDS infrastructure, surfaced through EHR-integrated hooks (P58) with clinician sign-off on every recommendation; its FDA-database interaction checking defers to P55 for full medication review. Deploy P52-G at facility and CHW level in Global South settings: fully offline, national essential medicine list loaded, geography and season declared for prior calibration, and a supervising clinician pathway for escalation triggers. Deploy P52-AM in US and Asia-Pacific tertiary systems where bimodal disease priorities apply — HBV-endemic populations, East Asian gastric cancer risk, super-aging demographics.

Prerequisites: declared specialty and population, available diagnostics inventory (the engine never recommends unavailable tests without a referral pair), and guideline-source configuration per variant. Misuse: do not allow any variant to function as an unsupervised diagnostic authority, to suppress its uncertainty block, to override national treatment policy (-G), or to let convenience reorder the red-flag-first pipeline. Pairings: consumes P51-de-identified data; hands medication questions to P55; feeds P62 surgical triage (-G integration named by the author); writes recommendations through P58; escalates population-level patterns to P59.

---
C0 informational classification; confers no clinical, legal, financial, or safety authority.
