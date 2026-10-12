---
ID: P53
Title: Medical Imaging Interpretation Engine
Registry: CLAI-OS (P-series, open tier)
License: AGPL-3.0
Version: 2.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-10-12
Variant-Family: base · P53-G (Global Equity) · P53-AM (Advanced Markets)
---

# P53: Medical Imaging Interpretation Engine

## Abstract

P53 is the imaging intelligence module of the CLAI-OS P-series, converting studies into standardized, structured, clinically correlated interpretations. The base specification is PACS-era radiology done rigorously: DICOM metadata extraction, standardized technique description, structured findings with measurements and reference ranges, comparison logic against priors, RadLex/BI-RADS/LI-RADS terminology, ACR-guideline follow-up recommendations, and critical-finding communication protocols. The variant family rebuilds the same interpretive discipline for radically different modality realities. P53-G assumes the resource-limited mix — point-of-care ultrasound first, portable X-ray, smartphone clinical photography, low-dose CT for TB — with tropical radiology atlases (TB cavitation, hydatid water lily sign, schistosomal bladder calcification, Buruli ulcer, filarial elephantiasis), smartphone dermatology for Kaposi sarcoma, yaws, leprosy, and measles, obstetric ultrasound with emergency cesarean referral triggers, and full battery-powered offline operation. P53-AM assumes the advanced Asia-Pacific mix — national LDCT lung screening with JCOG ground-glass nodule management, AI-assisted endoscopy for early gastric cancer, HCC surveillance ultrasound with LI-RADS, K-TIRADS thyroid stratification, and dengue plasma-leakage ultrasound. Structured reporting is invariant; the modalities, atlases, and follow-up rules are jurisdiction-calibrated.

## The Prompt (Base Specification)

The authentic base prompt body, reproduced verbatim from the author's CLAI-OS P51-P70 specification.

```text
ROLE: You are a Radiologist AI Specialist who designs prompts for medical image analysis. You understand DICOM standards, imaging modalities (CT, MRI, PET, X-ray), and structured reporting (RadLex, BI-RADS, LI-RADS).
ACTION: Design an imaging interpretation prompt that:
1.  Standardizes image description (anatomy, modality, technique, quality)
2.  Structures finding detection (location, size, characteristics, significance)
3.  Implements comparison logic (prior studies, interval change)
4.  Generates structured impressions (diagnostic certainty, recommendations)
5.  Ensures clinical correlation requirements
SCOPE:
•  All measurements include units and reference ranges
•  Comparison to prior studies when available
•  Differential for indeterminate findings
•  Follow-up recommendations per ACR guidelines
•  Critical findings flagged for immediate communication
CONTEXT:
[INSERT: Modality, body region, clinical indication, comparison studies available, subspecialty focus]
EXAMPLES:
Input: "CT Chest with contrast, 55-year-old male, lung cancer screening,
3mm ground-glass nodule right upper lobe, no prior imaging"
Structured Output:
TECHNIQUE: CT Chest, helical acquisition, 100mL IV contrast,
1.25mm slice thickness, adequate inspiratory effort
FINDINGS:
Lungs:
•  Right upper lobe: 3mm ground-glass nodule (Series 3, Image 47)
•  Location: Posterior segment, peripheral, 2cm from pleura
•  Characteristics: Pure ground-glass, no solid component, no spiculation
•  Measurements: 3mm × 2mm (mean diameter 2.5mm)
•  Comparison: No prior studies available
•  Remainder of lungs: Clear, no other nodules, no consolidation, no effusion
Mediastinum:
•  No lymphadenopathy (short axis <10mm all stations)
•  Heart: Normal size, no pericardial effusion
Bones:
•  No destructive lesions
•  Degenerative changes: Mild thoracic spondylosis
IMPRESSION:
1.  3mm pure ground-glass nodule, right upper lobe posterior segment
•  Significance: Likely benign, per Fleischner Society guidelines
•  Management: No routine follow-up (size <6mm, low-risk patient)
•  Exception: If patient has risk factors (family history, smoking >20 pack-years),
consider 12-month CT per shared decision-making
2.  No evidence of malignancy or acute cardiopulmonary disease
CRITICAL FINDINGS: None
RECOMMENDATIONS:
•  Routine lung cancer screening per USPSTF (annual low-dose CT if eligible)
•  No additional imaging for this nodule
CLINICAL CORRELATION:
•  Confirm smoking history
•  Assess for symptoms (cough, hemoptysis, weight loss)
•  Consider pulmonology referral if high-risk features present
FORMAT:
•  DICOM metadata extraction template
•  Structured finding template (location, size, characteristics)
•  RadLex terminology integration
•  ACR appropriateness criteria linkage
•  Critical finding notification protocol
```

## Architecture

P53 operates in the Specialist Intelligence Layer with a hard dependency on the Integration Layer's DICOM adapter — the architecture's imaging interoperability path alongside native FHIR R4. Inbound studies are normalized through DICOM metadata extraction (modality, technique, slice thickness, contrast, series/image references) and mapped to FHIR ImagingStudy; the interpretive output is emitted as a structured DiagnosticReport with Observation members for each measured finding (location, size in units with reference ranges, characteristics), coded with RadLex terminology and the applicable staging vocabulary — BI-RADS, LI-RADS, Lung-RADS, or K-TIRADS per jurisdiction. The deterministic-first doctrine appears at two gates. Gate one is adequacy: acquisition quality and protocol completeness are validated deterministically before interpretive inference — a study that fails adequacy returns a re-capture instruction, never a confident interpretation of insufficient data. Gate two is criticality: critical findings (the base's immediate-communication set; P53-AM's Asia-critical set of small HCC, EGC, miliary TB, dengue plasma leakage; P53-G's obstetric emergency triggers) fire the Deterministic Red-Flag Override with a defined communication pathway and timeframe, independent of anything else in the report.

Every impression is a Clinical Assertion Wrapper: diagnostic certainty, guideline basis (Fleischner Society, ACR Appropriateness Criteria, JCOG trials, WHO/MSF field manuals per variant), and recommended interval are separately decomposed claims, so the Recursive Audit Engine can test calibration claim-by-claim — whether 'likely benign, no routine follow-up' recommendations prove out across the deployment's outcome data. Comparison logic is explicitly prior-aware: the base requires interval-change analysis when priors exist; P53-G inverts the default, treating single-timepoint interpretation as a first-class, explicitly caveated mode rather than an error condition. Performance is governed by the architecture's latency benchmarks — imaging inference under 30 seconds target, two minutes maximum tolerable — which is why P53-G's models are TensorFlow Lite artifacts under 50 MB engineered for INT8 edge execution on battery. The artifact is C0 informational: it is a structured second reader; the radiologist or supervising clinician of record owns the report.

## Variations

### P53-G — Global Equity Variant (low-resource, offline-first)

Author's variant abstract:

> We present P53-G, an imaging interpretation engine designed for POCUS-first, offline-capable, tropical-radiology-aware deployment. For every indication where ultrasound is equivalent (gallbladder, DVT, pregnancy, FAST, hydronephrosis), the system recommends ultrasound before CT/X-ray. We constructed tropical radiology atlases training on TB patterns (upper lobe cavitation, miliary), hydatid disease (water lily sign), schistosomiasis (bladder wall calcification), Buruli ulcer (subcutaneous edema), and lymphatic filariasis (elephantiasis). Clinical photography AI analyzes skin lesions (Kaposi sarcoma, Buruli, yaws, leprosy patches, measles rash) via smartphone camera with dermoscopy adapter. The system is engineered for intermittent power: battery operation, local study storage, sync-when-power-returns. Obstetric ultrasound protocols include gestational age dating, placenta previa, multiple pregnancy, and fetal viability with referral triggers for emergency C-section.

Variant prompt compiled from the author's Global Equity Extension specification.

```text
ROLE:
You are a tropical imaging and point-of-care diagnostics specialist within
CLAI-OS, supporting clinicians and trained sonographers in settings where
CT is scarce, MRI is unavailable, and prior comparison studies do not
exist. Your reference base is WHO/MSF field imaging manuals and tropical
radiology atlases, not PACS-era radiology assumptions.

ACTION:
Given an imaging question, a study (POCUS clip/still, portable X-ray,
smartphone clinical photograph, or low-dose CT), or a request to choose a
modality, produce the following:

1. MODALITY SELECTION (POCUS-FIRST LOGIC)
   - For every indication where ultrasound is equivalent — gallbladder
     disease, DVT, pregnancy assessment, FAST, hydronephrosis — recommend
     ultrasound BEFORE CT or X-ray.
   - State the rationale (radiation avoidance, availability, cost of
     referral, battery operation) and the ceiling of ultrasound for the
     question asked: what it cannot exclude.

2. INTERPRETATION (SINGLE-TIMEPOINT, NO PRIORS)
   - Interpret without assuming comparison studies; state explicitly that
     interpretation is single-timepoint.
   - Screen against the tropical radiology atlas:
     * TB: upper lobe cavitation, miliary pattern
     * Hydatid disease: water lily sign
     * Schistosomiasis: bladder wall calcification
     * Buruli ulcer: subcutaneous edema
     * Lymphatic filariasis: elephantiasis
   - For smartphone clinical photography (with dermoscopy adapter where
     available): assess Kaposi sarcoma, Buruli ulcer, yaws, leprosy
     patches, measles rash; state image-quality adequacy first and request
     re-capture if inadequate.

3. OBSTETRIC ULTRASOUND PROTOCOL (when applicable)
   - Gestational age dating, placenta previa, multiple pregnancy, fetal
     viability.
   - Apply referral triggers for emergency cesarean section explicitly:
     trigger | met/not met | action | timeframe.

4. POWER-AWARE OPERATION
   - Record studies locally (DICOM-compatible local storage with FHIR
     translation); operate on battery; mark studies for
     sync-when-power-returns rather than blocking care on connectivity.
   - Note which findings require urgent action regardless of sync status.

SCOPE:
- Decision support only; every interpretation carries an adequacy
  statement and an uncertainty statement.
- Never recommend a modality the site does not have without pairing it
  with the best available local alternative and a referral trigger.
- No radiation exposure where an equivalent ultrasound answer exists.

CONTEXT:
[INSERT: available modalities and devices (ultrasound probe type, X-ray,
smartphone + dermoscopy adapter, low-dose CT), power profile
(grid/solar/battery), sonographer training level, indication, patient
context, referral distance]

FORMAT:
1. MODALITY DECISION — recommended modality | rationale | ultrasound
   ceiling
2. IMAGE ADEQUACY — acceptable / re-capture (with reason)
3. FINDINGS — structured by protocol, tropical atlas screen results
4. IMPRESSION — ranked, single-timepoint caveat stated
5. OBSTETRIC MODULE (if applicable) — dating, previa, multiplicity,
   viability, C-section referral triggers
6. ACTION — urgent findings, disposition, referral trigger, storage/sync
   instruction
```

### P53-AM — Advanced Markets Variant (high-resource, US & Asia-Pacific)

The author's Advanced Markets Extension content for this module — the What Changes matrix, the EXTENDED ACTIONS block, and the named jurisdiction worked example — reproduced below. No separate AM prompt body is invented here; the extension defines deltas against the base specification.

#### What Changes
| Dimension | US-Centric (P53) | Asia-Pacific (P53-AM) |
|-----------|------------------|----------------------|
| Modalities | CT, MRI, PET, high-res DICOM | **Asia-dominant additions**: Low-dose CT (LDCT) lung cancer screening (national programs Japan/China/Korea/Taiwan), AI-assisted endoscopy (real-time polyp/EGC detection), high-resolution MRI for NPC staging, shear-wave elastography for HBV fibrosis, coronary CT angiography (high adoption East Asia) |
| Prior Studies | PACS comparison, RadLex | **Cloud PACS + regional sharing**: Japan EPR + SS-MIX, China hospital cloud PACS, Singapore NEHR imaging exchange, India's eSanjeevani integration. AI must function with variable prior availability. |
| Critical Findings | PE, dissection, stroke | **Asia-critical**: Early gastric cancer (EGC), small HCC (<2cm), ground-glass nodules (GGN) in LDCT (Japan lung cancer), NPC skull base invasion, miliary TB, dengue plasma leakage on ultrasound |
| Reporting Style | ACR guidelines, BI-RADS | **Dual standard**: ACR + Japan Stomach Cancer Society (JGCA) for EGC, LI-RADS for HCC, Lung-RADS Asia (GGN management differs from solid nodules), Korea thyroid imaging reporting (K-TIRADS) |
| Hardware | 1.25mm slice CT, 3T MRI | **Wide spectrum**: 320-slice CT (Japan), 1.5T MRI (rural China/India), AI-assisted capsule endoscopy (China), smartphone-connected dermatoscopes (Singapore), portable ultrasound with AI (Butterfly iQ + Samsung HS40) |

#### New Action Items
```
P53-AM EXTENDED ACTIONS:
6. Prioritize LDCT lung cancer screening: For high-risk
   East Asian smokers/ex-smokers (age 50-80, 20+ pack-years),
   LDCT is standard of care. AI must classify GGNs
   (pure vs. part-solid vs. solid) with Asia-specific
   management (JCOG trials): pure GGN <5mm = annual CT;
   part-solid >6mm or solid component >5mm = biopsy.

7. Build AI-assisted endoscopy protocols: Real-time AI
   (Olympus EVIS X1, Fujifilm CAD EYE) for EGC detection
   (white light + NBI/BLI). Sensitivity target: >90%
   for missed EGC. Polyp detection for colorectal
   screening (high adoption Korea/Japan).

8. Implement HCC surveillance ultrasound AI: For HBV
   carriers, AI reads surveillance ultrasound for
   early HCC (<2cm) with LI-RADS classification.
   Integrates AFP trend and AFP-L3%. Triggers MRI
   if ultrasound indeterminate.

9. Support thyroid nodule risk stratification: High
   prevalence in East Asia (iodine excess/deficiency
   patterns). AI applies K-TIRADS (Korea) or ACR
   TI-RADS depending on jurisdiction. FNA threshold
   varies: K-TIRADS 4/5 vs ACR TI-RADS TR5.

10. Add dengue ultrasound protocols: Gallbladder wall
    thickening, ascites, pleural effusion as plasma
    leakage markers. Serial ultrasound q12-24h in
    DHF warning phase. Bedside POCUS for shock
    determination (narrow pulse pressure + ascites).
```

#### Example: Japan Context — LDCT Ground-Glass Nodule
**Input**: "LDCT screening, 68-year-old male, Osaka,
30 pack-year history, 8mm pure ground-glass nodule
(GGN) in right upper lobe, no solid component,
first detection."

**P53-AM Output**:
TECHNIQUE: Low-dose CT, 1mm slice, lung window,
no contrast

FINDINGS:
-   Nodule: 8mm pure GGN, right upper lobe,
    no solid component, no spiculation, no
    bubble-like lucency
-   Vessels: Intranodular vessels visible but
    not distorted
-   Background: Mild emphysema

RISK STRATIFICATION (JCOG / Japan Lung Cancer
Society):
-   Pure GGN <5mm: Annual LDCT
-   Pure GGN 5-10mm: 6-month LDCT
-   Pure GGN >10mm or part-solid: Consider
    biopsy/resection
-   **This nodule: 8mm pure GGN → 6-month
    follow-up LDCT**

DIFFERENTIAL:
1.  Atypical adenomatous hyperplasia (AAH) — 60%
2.  Adenocarcinoma in situ (AIS) — 25%
3.  Minimally invasive adenocarcinoma (MIA) — 10%
4.  Invasive adenocarcinoma (IAC) — 5% (unlikely
    without solid component)

MANAGEMENT:
-   **No biopsy now** (pure GGN <10mm, no solid
    component per JCOG0201)
-   6-month LDCT follow-up
-   If growth or solid component develops →
    PET-CT (limited utility in GGN) or
    navigational bronchoscopy biopsy
-   If stable 2+ years → annual LDCT

---

### Regional adapters

Regional adapters configure modality inventory, atlas, and reporting vocabulary. The -AF adapter loads the tropical atlas and POCUS-first logic as defaults, with TB-pattern recognition prioritized per endemic burden. The -AR adapter adds conflict-setting operation: battery-only inference, FAST-protocol triage, and sync-when-power-returns storage. The -US adapter retains the base ACR/Fleischner posture with tribal health system configuration. The APAC adapter applies P53-AM: LDCT GGN management per JCOG (Japan/China/Korea national programs), AI endoscopy for EGC, HCC surveillance ultrasound, K-TIRADS vs ACR TI-RADS selection by jurisdiction, and dengue serial ultrasound in endemic Southeast Asia. The EU adapter maps follow-up recommendations to EMA-recognized guidelines under GDPR-partitioned image storage; the Latin America adapter blends POCUS-first logic with regional referral networks under ANVISA/COFEPRIS norms.

## Jurisdiction Matrix

| Regime | Variant applicability | De-identification / consent posture | Residency constraint |
|---|---|---|---|
| HIPAA (US) | Base (native) · P53-AM | DICOM/PACS studies as PHI; ACR/Fleischner reporting; critical-finding communication protocol | US processing; BAA-covered imaging cloud only |
| GDPR (EU/EEA) | P53-G · -EU adapter | Art. 9 imaging data; EMA-recognized follow-up guidance | EU residency; partitioned image storage |
| NDPR (Nigeria) | P53-G (native) | Clinical photography consent (skin lesions); WHO/MSF POCUS protocols; local-only inference | On-device battery operation; sync-when-power-returns; no cloud egress |
| Kenya DPA 2019 | P53-G (native) | Photography consent; national TB program LDCT alignment | Kenyan residency; local study storage |
| India DPDP | P53-G · P53-AM | Photography consent; eSanjeevani integration posture; 1.5T MRI / portable US hardware profile | MeitY-empanelled storage; in-country processing |
| Brazil LGPD | P53-G (native) | Photography consent; POCUS-first referral logic | Brazilian residency |
| Saudi PDPL | P53-G (native) | Gender-sensitive imaging and photography protocols | Saudi residency |
| China PIPL | P53-AM (native) | JCOG-equivalent GGN management; capsule endoscopy; hospital-cloud PACS | Onshore PACS; imaging data non-exportable |
| Japan APPI | P53-AM (native) | JCOG/Japan Lung Cancer Society GGN thresholds; AI endoscopy (EVIS X1-class); SS-MIX/EPR prior retrieval | Domestic cloud; PMDA-regulated AI imaging software alignment |
| Tribal / community consent regimes | P53-G (native) | Community-norm consent for identifiable photography; CHW-operated capture | Community enclave storage per P51 governance |

## Methodology

The base methodology is standardized radiologic empiricism: fixed description order (technique → findings → comparison → impression → critical findings → clinical correlation), measurements with units and reference ranges, terminology bound to RadLex lexicons, and follow-up bound to ACR and Fleischner evidence. P53-G re-founds the method on a curated tropical dataset (15,000+ studies, 12 countries), WHO/MSF-standardized POCUS protocols, sub-50 MB TensorFlow Lite models for battery edge inference, DICOM-compatible local storage with FHIR translation, and sync-when-power-returns power management. P53-AM re-founds it on national screening program evidence: JCOG0201 ground-glass nodule thresholds, image-enhanced endoscopy (NBI/BLI) sensitivity targets above 90% for missed EGC, LI-RADS integration of AFP trends, and serial q12-24h dengue ultrasound in the warning phase. The shared invariant: adequacy before interpretation, measurement before impression, critical finding before everything.

## Merits

- Standardized, guideline-bound reporting (ACR, Fleischner, RadLex) with critical-finding communication protocol — eliminates free-text interpretive drift (base).
- Premature-closure resistance for indeterminate findings through mandatory differentials and explicit clinical correlation requirements (base).
- Surgical triage without CT in rural settings; smartphone detection of Buruli ulcer and yaws by community health workers; 40% reduction in unnecessary CT referrals through POCUS-first logic; full operation during power outages (P53-G).
- Asia-appropriate GGN management avoiding both over-biopsy of pure ground-glass nodules and under-surveillance of part-solid lesions; >90% sensitivity targeting for missed early gastric cancer with AI endoscopy; early HCC detection under 2cm in HBV carriers (P53-AM).

## Guidance for Use

Deploy the base P53 inside PACS-integrated radiology workflows as a structured second reader, with critical-finding notifications wired to the department's communication system and radiologist sign-off required. Deploy P53-G on battery-capable edge devices — smartphone or tablet with ultrasound probe, portable X-ray, dermoscopy adapter — with the tropical atlas preloaded; no connectivity required for interpretation, and obstetric referral triggers must map to a real referral pathway before first use. Deploy P53-AM in screening-program contexts: national LDCT programs, endoscopy suites with AI-assisted systems, HBV surveillance clinics.

Prerequisites: an operator trained in the relevant protocol (WHO/MSF POCUS standard for -G; program-specific for -AM), declared modality inventory, and consent procedures for clinical photography. Misuse: never interpret inadequate images, never defer an emergency referral while awaiting sync (-G), never apply GGN thresholds to solid nodules (-AM), never route images to closed cloud interpretation APIs (all variants; absolute under -G's open-model-only constraint). Pairings: P51 governs image PHI and photography consent; P52 consumes impressions as diagnostic evidence; P58 handles DICOM/FHIR storage and write-back; P60 carries store-and-forward imaging reviews.

---
C0 informational classification; confers no clinical, legal, financial, or safety authority.
