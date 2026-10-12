---
ID: P70
Title: Healthcare Quality & Safety Improvement Engine
Registry: CLAI-OS (P-series, open tier)
License: AGPL-3.0
Version: 2.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-10-12
Variant-Family: base · P70-G (Global Equity) · P70-AM (Advanced Markets)
---

# P70: Healthcare Quality & Safety Improvement Engine

Abstract: P70 designs healthcare quality and patient safety improvement systems across three operating contexts. The base specification (high-reliability organization methods) identifies quality gaps (mortality, morbidity, readmissions, infections, errors), analyzes root causes (Ishikawa, 5 Whys, FMEA, Swiss cheese), designs interventions through PDSA cycles with standardized protocols and checklists, measures outcomes with statistical process control (not before/after comparisons), and hardwires sustainability — illustrated by a complete CLABSI reduction program from fishbone to culture change. The P70-G Global Equity variant targets the harms that actually kill in zero-ICU, zero-running-water facilities: counterfeit medication detection from packaging photographs, WHO Surgical Safety Checklist enforcement for ketamine/spinal settings, no-blood-bank hemorrhage protocols, maternal death surveillance with three-delays analysis and stockout-linked pattern recognition, WASH infrastructure gating (no water, no safe surgery), and respectful maternity care monitoring via SMS feedback. The P70-AM Advanced Markets variant adapts to Asia-Pacific: counterfeit and look-alike/sound-alike drug prevention (including character-similarity errors), overcrowding safety, healthcare-worker burnout (karoshi) monitoring, kaizen/5S integration, and migrant-worker safety. In every variant: analysis targets system failure rather than individual blame, measurement uses statistical process control, and every finding routes to an accountable owner.

## The Prompt (Base Specification)

Provenance: verbatim from the author's base specification (*CLAI OS P51-P70.txt*); no edits beyond whitespace.

ROLE: You are a Patient Safety Officer who designs continuous quality improvement systems. You understand Lean methodology, Six Sigma, root cause analysis, and high-reliability organizations.
ACTION: Design a quality improvement prompt that:
1.  Identifies quality gaps (mortality, morbidity, readmissions, infections, errors)
2.  Analyzes root causes (Ishikawa, 5 Whys, FMEA, Swiss cheese model)
3.  Designs interventions (PDSA cycles, standardized protocols, checklists)
4.  Measures outcomes (SPC charts, run charts, control charts)
5.  Sustains improvement (hardwire into workflow, culture change, governance)
SCOPE:
•  Gaps: clinical, operational, patient experience, financial
•  Analysis: data-driven, multidisciplinary, systems thinking (not blame)
•  Interventions: evidence-based, piloted, refined, scaled
•  Measurement: statistical process control, not before/after comparisons
•  Sustainability: leadership commitment, frontline engagement, continuous monitoring
CONTEXT:
[INSERT: Healthcare setting, quality priorities, baseline performance, regulatory requirements, culture]
EXAMPLES:
Central Line-Associated Bloodstream Infection (CLABSI) Reduction:
QUALITY GAP:
•  Baseline CLABSI rate: 3.2 per 1000 line-days (national benchmark: 1.0)
•  Excess infections: 15/year → 2 deaths, $450K excess cost
•  Variation: ICU A 4.5, ICU B 2.1, ICU C 3.8 (opportunity for standardization)
ROOT CAUSE ANALYSIS:
Fishbone Diagram:
•  People: Staffing turnover 40%, inconsistent training
•  Process: No standardized insertion checklist, line maintenance variable
•  Equipment: Dressing kits not standardized, CHG availability inconsistent
•  Environment: ICU A has older beds, poor line visualization
•  Culture: "It's just a line" attitude, near-misses not reported
5 Whys (representative case):
1.  Why CLABSI? → Line colonized
2.  Why colonized? → Dressing dislodged
3.  Why dislodged? → Not secured properly
4.  Why not secured? → Nurse rushed, no checklist
5.  Why no checklist? → Not required, not audited, not habit
INTERVENTION (PDSA Cycles):
PDSA 1: Standardized Insertion Bundle
•  Plan: Implement CDC central line insertion practices checklist
•  Do: Pilot in ICU B (lowest baseline, most engaged)
•  Study: CLABSI rate 2.1 → 0.8 in 3 months
•  Act: Refine checklist, scale to all ICUs
PDSA 2: Maintenance Bundle
•  Plan: Daily line necessity review, dressing change protocol, CHG bathing
•  Do: All ICUs simultaneously
•  Study: Rate 1.5 → 0.9 in 6 months
•  Act: Hardwire into EHR (automatic line day count, dressing change alerts)
PDSA 3: Culture Change
•  Plan: Non-punitive reporting, celebrate successes, frontline ownership
•  Do: Unit-based safety teams, huddle boards
•  Study: Near-miss reporting increased 300%, CLABSI 0.9 → 0.3
•  Act: Annual refresher, new staff onboarding, leadership

## Architecture

P70 is measurement-and-intervention infrastructure whose outputs trigger procurement, restriction, and personnel-adjacent findings, so its architecture makes measurement deterministic, findings attributable, and escalation governed.

**Deterministic-first safety pathways.** Quality metrics (rates per line-days, readmission proportions, checklist completion) execute as deterministic statistical process control — control charts, run charts, special-cause rules — over structured event data; FMEA risk priority numbers and -G WASH scores are deterministic computations over rubric inputs; hard gates are deterministic: the -G rule that surgery is flagged restricted when the water criterion fails cannot be waived by the model, and counterfeit suspicion scoring emits flag-and-quarantine actions, never exoneration. The model's role is root-cause hypothesis generation, Ishikawa/5-Whys facilitation, intervention design drafting, SMS feedback coding (sentiment and keyword extraction, -G), and narrative for governance review.

**FHIR R4 mapping.** Quality measures and their stratified results map to Measure and MeasureReport; safety events to AdverseEvent; checklist instruments and completions to Questionnaire/QuestionnaireResponse; maternal death review artifacts (-G) to DocumentReference with restricted-access security labels and Composition-structured three-delays analysis; counterfeit evidence packages (-G) to DocumentReference with chain-of-custody Provenance and Device linkage where batch data exists; SMS feedback to Communication with coded Observation categories; improvement interventions to PlanDefinition with PDSA-cycle versioning.

**Interposition contract.** P70 executes behind the CLAI-OS interposition layer: no metric, flag, review finding, or feedback-coded category reaches governance dashboards without deterministic validation (denominator integrity, rubric completeness, de-identification rules for staff- and patient-implicating content). Every finding travels in a Clinical Assertion Wrapper with per-claim epistemic labels — measured, coded-from-text, model-hypothesized — so governance never mistakes a root-cause hypothesis for an established cause.

**Audit and provenance stack.** Metric series, gate firings, quarantine actions, review proceedings access, and escalation dispositions are written to an immutable Merkle-anchored audit trail with access logging for confidential review materials; recursive self-audit monitors for metric gaming and suppression patterns; prompt mortality expires stale benchmarks and rubric versions.

**C0 classification.** This artifact is C0 informational: it confers no clinical, legal, financial, or safety authority. Regulatory action on counterfeit products, personnel consequences, and clinical accountability remain with designated authorities under due process.

## Variations

### P70-G — Global Equity Variant

Author's variant abstract (*CLAI-OS Global Equity Extension*):

> We present P70-G, a quality and safety engine for zero-ICU, zero-running-water environments. Counterfeit medicine detection uses AI reading medication packaging photos: batch number verification against manufacturer databases, visual anomaly detection (poor printing, wrong color, misspelled labels). WHO Surgical Safety Checklist is enforced for all settings including no-anesthesia-machine surgery (ketamine + spinal checklist) and no-blood-bank hemorrhage protocols (tranexamic acid, pressure, balloon tamponade). Maternal death surveillance requires verbal autopsy + facility review for every death, with "three delays" analysis (seeking care, reaching care, receiving care). AI identifies patterns: "3 maternal deaths this month from postpartum hemorrhage → oxytocin stockout → emergency procurement triggered." WASH quality is integrated: no running water = no safe surgery; AI monitors clinic WASH infrastructure and prioritizes rainwater harvesting + solar purification upgrades. Respectful maternity care (RMC) tracks disrespect and abuse (physical, verbal, detention for non-payment, lack of privacy) via SMS patient feedback surveys post-discharge.

Variant prompt compiled from the author's Global Equity Extension specification.

ROLE: You are a patient safety systems architect for facilities without ICUs, running water, reliable power, or incident reporting culture. You target system failures — stockouts, water absence, one nurse per dozens of patients — rather than individual blame, and you build detection and feedback loops that work with SMS, paper, and photographs.

ACTION: Design a complete quality and patient safety system for the facility context below. Deliver:
1. A counterfeit medicine detection module: packaging photograph capture protocol, batch number verification workflow against manufacturer databases, and visual anomaly detection criteria (poor printing, wrong color, misspelled labels), with quarantine and reporting actions for suspect products
2. A WHO Surgical Safety Checklist enforcement module adapted to setting: ketamine and spinal variant for no-anesthesia-machine surgery, and a no-blood-bank hemorrhage protocol (tranexamic acid, pressure, balloon tamponade) with stepwise escalation
3. A maternal death surveillance protocol: verbal autopsy plus facility review for every maternal death, structured "three delays" analysis (seeking care, reaching care, receiving care), and pattern recognition that links recurrent causes to system failures (e.g., postpartum hemorrhage cluster → oxytocin stockout → emergency procurement trigger)
4. An injection and medication safety audit: unsafe injection practice checklist, ketamine administration safety gate (airway management capability confirmation), and patient identification workflow for settings without wristbands
5. A WASH infrastructure scoring module: water, soap, and sanitation assessment with the explicit rule that no running water means no safe surgery, plus a prioritized upgrade ladder (rainwater harvesting, solar purification)
6. A respectful maternity care (RMC) feedback system: post-discharge SMS survey instrument detecting disrespect and abuse categories (physical, verbal, detention for non-payment, lack of privacy), with sentiment and keyword analysis and a protected escalation channel
7. An incident reporting culture starter kit: blame-free reporting taxonomy, paper-to-digital capture flow, and feedback loop showing reporters what changed

SCOPE:
• Every module must function with SMS, paper, and photographs; no module may require EHR integration or continuous power
• Root cause analysis targets system failure; individual-blame framing is a defect
• The surgical checklist and hemorrhage protocol are enforced pathways, not reference documents
• The engine detects, scores, and escalates; regulatory action on counterfeit products and clinical accountability decisions rest with the responsible authorities

CONTEXT:
[INSERT: facility type and staffing ratios; water and power status; medication supply chain and procurement authority; maternal services volume; surgical case mix; SMS penetration among patients; existing reporting culture and governance structure]

FORMAT:
• Detection modules as protocol cards: capture | check | threshold | action | escalation
• Checklist variants as timed sections with per-item verification lines
• Maternal surveillance as a case review template plus a pattern table: signal | linked system failure | triggered action
• WASH scoring as a rubric with the surgery-permission gate explicit
• RMC survey as an SMS script with category coding and escalation routing
• "Do Not" list: proceeding with surgery absent water; ketamine administration without airway capability confirmation; publishing RMC findings that identify individual patients or staff without due process

Deployment constraint (invariant for this variant): offline-first; open-weight models only (Llama 3 / Mistral / Phi-3 class); no closed-API processing of patient-identifiable data.

### P70-AM — Advanced Markets Variant

From the author's *CLAI-OS Advanced Markets Extension (P51-AM – P70-AM)*. No AM prompt body exists in the source; the variant is specified as deltas against the base prompt.

**What Changes**
| Dimension | US-Centric (P70) | Asia-Pacific (P70-AM) |
|-----------|------------------|----------------------|
| Quality Gaps | CLABSI, CAUTI, VAP | **Asia-specific**: Counterfeit medications (China/India/SE Asia 10-30% in some markets), medication errors due to look-alike/sound-alike drugs (Chinese character similarity), nosocomial infections from overcrowding (India/China), surgical site infection in humid tropics, anesthesia complications in high-volume settings |
| Root Cause | Process failure | **System failure**: Overcrowding (India: 1 nurse per 50 patients), doctor burnout (Japan karoshi, Korea 100+ hour weeks), fragmented care (Japan by-department silos), rural-urban quality gap (China/India), language barrier errors (migrant workers in Singapore/Japan) |
| Interventions | PDSA cycles | **Asia-adapted**: Japan kaizen (continuous improvement) culture integration. 5S methodology (Sort, Set, Shine, Standardize, Sustain) for ward organization. Checklist culture (WHO Surgical Safety Checklist high adoption Japan/Korea/Singapore). |
| Measurement | SPC charts | **Asia-specific**: Japan DPC quality indicators (surgical site infection rate, readmission rate). Korea HIRA quality assessment. Singapore MOH Clinical Quality Indicators. China's hospital tier (3A) quality standards. India's NQAS. |
| Sustainability | Leadership commitment | **Frontline ownership + hierarchy**: Japan = nurse-led quality circles (QC). Korea = physician champion model. Singapore = MOH top-down quality mandates. China = hospital director responsibility system. |

**Extended Actions**
```
P70-AM EXTENDED ACTIONS:
6. Build counterfeit medicine detection: 
   AI reads medication packaging 
   photos, checks batch numbers 
   against manufacturer database, 
   identifies visual anomalies. 
   Critical in China/India/SE 
   Asia where counterfeit 
   antibiotics and oncology 
   drugs kill.

7. Implement look-alike/sound-alike 
   drug prevention: Chinese 
   character similarity causes 
   medication errors (e.g., 
   similar-looking drug names 
   in kanji/hanzi). AI flags 
   high-risk pairs and suggests 
   storage separation + barcode 
   verification.

8. Support overcrowding safety: 
   India/China hospitals with 
   200%+ bed occupancy. AI 
   predicts infection outbreak 
   risk from overcrowding 
   metrics (bed spacing, 
   hand hygiene compliance, 
   ventilation). Triggers 
   cohorting and enhanced 
   cleaning.

9. Build burnout prevention for 
   healthcare workers (East 
   Asia): Japan karoshi and 
   Korea 100+ hour resident 
   weeks. AI monitors shift 
   patterns, sleep deprivation 
   indicators, and error rates. 
   Flags high-risk providers 
   for mandatory rest.

10. Design for migrant worker 
    safety (Singapore, Japan, 
    Korea, Taiwan): Foreign 
    workers face language 
    barriers, different disease 
    epidemiology (dengue, TB), 
    and limited health literacy 
    in host country language. 
    AI provides native-language 
    safety instructions and 
    culturally adapted 
    informed consent.
```

---

#### Implementation Architecture: The Advanced Markets CLAI-OS Node (from the source extension)

```
┌─────────────────────────────────────────────────────────────────────────┐
│              ADVANCED MARKETS CLAI-OS NODE — TIERED DEPLOYMENT         │
│                                                                          │
│  TIER 1: NATIONAL REFERENCE CENTER (Tokyo, Seoul, Singapore, Shanghai)  │
│  ├─ Full cloud compute + sovereign cloud backup (local jurisdiction)     │
│  ├─ All 20 prompts active (P51-AM through P70-AM)                      │
│  ├─ Genomic sequencing (Illumina, BGI, local lab)                        │
│  ├─ PACS + AI-assisted endoscopy + LDCT screening integration            │
│  ├─ National health exchange (NEHR, SS-MIX, ABHA, HIRA)                   │
│  └─ Training center for Tier 2/3 staff                                 │
│                                                                          │
│  TIER 2: REGIONAL HOSPITAL (Prefectural/District, 300-800 beds)          │
│  ├─ Edge server (GPU for imaging AI, 10TB storage)                       │
│  ├─ Core prompts: P52-AM (clinical), P53-AM (imaging), P55-AM (drug),   │
│  │   P57-AM (communication), P61-AM (mental health), P62-AM (surgery)    │
│  ├─ Diagnostics: Endoscopy + ultrasound + LDCT + lab (CBC, chemistry,    │
│  │   tumor markers, HBV/HCV serology)                                    │
│  ├─ EHR integration (hospital-specific + regional exchange)              │
│  └─ Teleconsult link to Tier 1                                         │
│                                                                          │
│  TIER 3: COMMUNITY HOSPITAL/CLINIC (Local, 50-200 beds)                 │
│  ├─ $500 tablet + messaging app integration (Line, WeChat, KakaoTalk)     │
│  ├─ Limited prompts: P52-AM (triage), P55-AM (essential meds),         │
│  │   P57-AM (patient education), P60-AM (telehealth), P69-AM (nutrition)│
│  ├─ Diagnostics: Rapid tests (HBV, HCV, HIV, H. pylori),                 │
│  │   point-of-care ultrasound, home BP/glucose monitoring                 │
│  ├─ Messaging app care plans and medication reminders                   │
│  └─ Daily sync to Tier 2                                               │
│                                                                          │
│  TIER 4: HOME / ELDERLY CARE (Aging-in-place, Japan/Korea super-aging)    │
│  ├─ Smartphone + wearable (BP monitor, glucose, fall detection)         │
│  ├─ Voice-based AI interface (Japanese/Korean/Mandarin)                   │
│  ├─ Family proxy portal (adult child manages elderly parent care)        │
│  ├─ Home visit nursing (kaigo) integration                              │
│  └─ Emergency alert: fall detection → auto-dial 119/120/999            │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## GOVERNANCE MODEL: ADVANCED MARKETS HEALTH INFRASTRUCTURE

```
┌─────────────────────────────────────────────────────────────────────────┐
│              CLAI-OS ADVANCED MARKETS GOVERNANCE                        │
│              (Regulatory-Harmonized, Market-Sustainable)                  │
│                                                                          │
│  OWNERSHIP STRUCTURE:                                                    │
│  ├─ Savant Framework LLC (Nigeria) holds global IP and architecture      │
│  ├─ Local operating entities in target markets (Japan, Singapore,       │
│  │   Korea, India) for regulatory compliance and data residency         │
│  ├─ Dual license: Commercial (for-profit hospitals, insurers, pharma)    │
│  │   + Mission (non-profit, academic, public hospital)                  │
│  ├─ Patent defense: Provisional patents filed defensively to prevent      │
│  │   proprietary capture by Northern vendors                            │
│  └─ Data trust: Patient data governed by local jurisdiction law          │
│     (APPI, PIPL, PDPA, HIPAA as applicable)                             │
│                                                                          │
│  FUNDING MODEL:                                                          │
│  ├─ Commercial: For-profit hospitals, insurers, device makers             │
│  │   [Commercial licensing terms — inquiries via the GitHub organization] │
│  ├─ Academic: Free for peer-reviewed research with data sharing           │
│  ├─ Public: Discounted for public hospitals and national health systems   │
│  └─ Innovation: Prize-based funding for breakthrough improvements        │
│                                                                          │
│  VALUE CREATION:                                                         │
│  ├─ Commercial revenue reinvested in:                                     │
│  │   1. R&D for next-tier prompts (P71-P90)                            │
│  │   2. Local team salaries (above-market to retain talent)            │
│  │   3. Advanced market deployment infrastructure                       │
│  │   4. Cross-subsidy to Global South deployment (30% of net revenue)   │
│  └─ Transparent quarterly reporting: Revenue, deployment metrics,         │
│     equity audits, carbon footprint                                      │
│                                                                          │
│  ACCOUNTABILITY:                                                         │
│  ├─ Local regulatory compliance: PMDA, NMPA, MFDS, HSA, CDSCO, FDA       │
│  ├─ Annual algorithmic bias audit by independent Asian academic body       │
│  ├─ Patient right to data portability across CLAI-OS nodes              │
│  └─ Right to fork: Any jurisdiction can self-host under AGPL             │
└─────────────────────────────────────────────────────────────────────────┘
```

---

#### Summary: The Advanced Markets Prompt Architecture (from the source extension)

| Prompt | Original Focus | Advanced Markets Extension |
|--------|---------------|---------------------------|
| P51 | HIPAA compliance | **Multi-jurisdictional: HIPAA + APPI + PIPL + PDPA + My Number + ABHA + sovereign cloud** |
| P52 | ACS/PE differential | **Bimodal: ACS/PE + HBV-HCC + gastric cancer + NPC + dengue DHF + HFMD** |
| P53 | CT/MRI/PET | **LDCT screening + AI endoscopy + HCC ultrasound + thyroid K-TIRADS + GGN management** |
| P54 | BRCA/ACMG | **EGFR NSCLC + HBV-HCC polygenic + CYP2C19 clopidogrel + HLA-B*15:02 SJS + thalassemia** |
| P55 | Warfarin/statins | **Clopidogrel + allopurinol SJS + TCM/Kampo/Ayurveda + ethnic dosing + HBV reactivation** |
| P56 | Pharma Phase III | **Asia-Pacific multi-registry + EGFR basket trials + bridging studies + TCM RCTs** |
| P57 | English literacy | **40+ languages + multi-script + family conference + TCM/Kampo/Ayurveda explanatory models** |
| P58 | Epic/Cerner | **SS-MIX + NEHR + ABHA + WeChat/Line/KakaoTalk + hospital-specific connectors** |
| P59 | HEDIS/CMS | **NDB + HIRA + MOH CDMP + Healthy China 2030 + super-aging analytics + air quality** |
| P60 | Video visits | **Messaging-app-first + family-mediated elderly + store-and-forward + pharmacy integration** |
| P61 | PHQ-9/988 | **PHQ-9 Asia-validated + hikikomori + exam stress + karoshi + family-mediated distress** |
| P62 | ACS NSQIP | **Japan ERAS + gastric cancer surgery + robotic optimization + HBV prophylaxis + same-day** |
| P63 | Rett/Angelman | **Kawasaki + IgA nephropathy + Takayasu + MPS + Wilson + HBV-PAN + consanguinity** |
| P64 | Algorithmic bias | **Asian BMI 23 + eGFR race-free + spirometry GLI-Asian + acral melanoma + angle-closure** |
| P65 | FDA trials | **Multi-regulatory simultaneous submission + basket trials + bridging + elderly-inclusive** |
| P66 | Class II/III FDA | **PMDA/NMPA/MFDS/HSA/CDSCO + Fitzpatrick III-V + Asian eye anatomy + local manufacturing** |
| P67 | Influenza/ESSENCE | **HFMD + dengue + avian flu + Nipah + JE + melioidosis + One Health poultry/bat** |
| P68 | FIM/6-minute walk | **Super-aging frailty + taichi/yoga/qigong + robotic rehab + hip fracture cascade** |
| P69 | SGA/MNA | **Sarcopenia AWGS + TCM food therapy + Ayurvedic dosha + NAFLD + kodokushi prevention** |
| P70 | CLABSI/PDSA | **Counterfeit detection + look-alike drug prevention + overcrowding safety + migrant worker** |

---

*End of Advanced Markets Extension — CLAI-OS v1.0-AM*
*"The best medical AI is not the most Western. It is the most precise for the population it serves."*

Named jurisdiction examples (from the source): Japan (kaizen and 5S integration, nurse-led quality circles, DPC quality indicators, karoshi burnout monitoring); Korea (HIRA quality assessment, physician-champion model, 100+ hour resident weeks); Singapore (MOH clinical quality indicators, migrant-worker language safety); China (3A hospital tier standards, character-similarity drug errors); India (NQAS, overcrowding safety at 200%+ bed occupancy).

### Regional Adapters

Regional adapters set the harm profile, measurement standards, and escalation owners. -AF (Africa): the -G variant is primary — counterfeit detection, no-water surgical safety, maternal death surveillance with stockout pattern recognition, WASH gating, respectful maternity care via SMS feedback. -AR (Arab region): -G modules for conflict-affected facilities; supply-chain integrity for humanitarian procurement; maternal safety in displacement settings. -US: the base specification as written — CLABSI/CAUTI/VAP-class hospital-acquired infection reduction, PDSA discipline, SPC measurement, high-reliability culture change. APAC: the -AM variant — counterfeit and look-alike/sound-alike prevention (character-similarity drug names), overcrowding infection risk, karoshi burnout monitoring, kaizen/5S integration, migrant-worker language safety. Adapters are configuration packs (harm taxonomy, benchmark sets, checklist language packs, escalation directory); none permits individual-blame framing or suppression of the water/counterfeit hard gates where they apply.

## Jurisdiction Matrix

| Regime | Variant applicability | Consent & de-identification posture | Residency & transfer |
|---|---|---|---|
| HIPAA (US) | Base variant (primary) | Quality records may attract patient-safety work-product protection under PSQIA-class frameworks — confirm privilege posture before assuming confidentiality or discoverability; incident reports with reporter protection | US-hosted; BAAs; PSO participation where elected |
| GDPR (EU/EEA) | Base-EU; -AM partnerships | Art. 9 health data; death review records engage family confidentiality expectations; DPIA; SMS feedback with transparency notice and lawful basis | EU/EEA residency; SCCs for transfer |
| NDPR (Nigeria) | -G variant (primary; MDSR contexts) | Maternal death review and incident data sensitive; staff-identifiable findings are staff personal data with fair-process duties; reporter identity protected | In-country under facility/ministry governance; aggregates for cross-border |
| Kenya DPA 2019 | -G variant (Kenya) | Sensitive data; registration; MPDSR program alignment | Transfer with safeguards |
| India DPDP Act | -G/-AM (India; NQAS contexts) | Consent plus notice; state quality-assurance programs under public functions; counterfeit reporting to national regulator per drugs law | Sectoral rules may apply |
| Brazil LGPD | -G variant (Latin America) | Sensitive data; ANVISA reporting duties for counterfeit/adverse events; ANPD oversight | ANPD mechanisms |
| Saudi PDPL | -G/-AM (Arab region) | Sensitive data; strict transfer controls; SFDA counterfeit reporting | In-Kingdom hosting default |
| China PIPL | -AM variant (China) | Sensitive personal information; separate consent; hospital tier (3A) quality reporting through official systems; counterfeit evidence to NMPA channels | Localization default; export approvals |
| Japan APPI | -AM variant (Japan) | Special-care-required personal information; opt-in consent; DPC quality indicator reporting per national rules; burnout monitoring of staff requires labor-law-aware consent | Transfer with consent or equivalent protections |
| Tribal / community consent | -G variant (community feedback; RMC) | SMS feedback with informed opt-in; community-level disrespect/abuse patterns reported without identifying individuals; death review involvement honors family and cultural norms | Community-governed feedback channels; fair process before personnel use |

## Methodology

Base: quality gap identification (mortality, morbidity, readmissions, infections, errors); root cause analysis (Ishikawa, 5 Whys, FMEA, Swiss cheese); PDSA cycle design with pilot-refine-scale discipline; statistical process control measurement (control charts, run charts, special-cause rules); sustainability hardwiring (workflow integration, culture change, governance).

Global Equity (P70-G): counterfeit detection model (packaging image classification, batch verification, visual anomaly criteria); WHO checklist digitization with ketamine/spinal variants and no-blood-bank hemorrhage protocols (tranexamic acid, pressure, balloon tamponade); maternal death surveillance with verbal autopsy, three-delays analysis, and association-rule pattern recognition (death clusters to stockouts to emergency procurement triggers); WASH infrastructure scoring with surgery-permission gating; RMC SMS feedback analysis (sentiment, keyword extraction, protected escalation).

Advanced Markets (P70-AM): look-alike/sound-alike drug-error prevention (character-similarity flagging, storage separation, barcode verification); overcrowding infection-risk prediction (bed spacing, hygiene compliance, ventilation); healthcare-worker burnout monitoring (shift patterns, sleep deprivation, error rates) with mandatory-rest flags; kaizen/5S methodology integration; migrant-worker native-language safety and consent.

## Merits

• Reduces hospital-acquired infection through bundle discipline measured by SPC, not anecdote (base)
• Prevents deaths from counterfeit antimalarials, antibiotics, and oncology drugs through photo-based detection and quarantine escalation (-G, -AM)
• Converts maternal deaths from uncounted tragedies into system-fix triggers via structured surveillance and stockout linkage (-G)
• Enforces the uncompromising floor: no running water, no safe surgery (-G)
• Surfaces disrespect and abuse in childbirth through systematic, protected patient feedback (-G) and staff burnout before it kills patients (-AM)

## Guidance for Use

**Base deployments.** Baseline data integrity first — denominators before dashboards; PDSA pilots on engaged units; measurement plans reviewed with statistical expertise; governance owns sustainment.

**Global Equity deployments (-G).** Offline-first on facility-controlled infrastructure; open-weight models only (Llama 3, Mistral, Phi-3 class); no closed-API processing of identifiable patient, staff, or report data. Counterfeit detection provides suspicion flags, not legal determinations — quarantine and report to the national medicines regulator; do not destroy suspect stock before regulator guidance. Maternal death reviews are configured as confidential, blame-free quality processes under the national MDSR framework; three-delays analysis informs system fixes and is not repurposed for discipline without due process. RMC surveys require informed opt-in; findings identifying individuals get fair process before any personnel consequence. WASH gates are binary: facilities failing the water criterion are flagged surgery-restricted until remediation.

**Advanced Markets deployments (-AM).** Burnout monitoring deployed under labor-law-aware consent with worker representation; look-alike/sound-alike pairs validated against the local formulary.

**Prerequisites (all variants).** Event data capture with denominator integrity; confidential review governance; escalation directory with named owners; regulator reporting channel; audit storage.

**Misuse.** Do not use quality data for individual blame; do not publish findings identifying patients or staff without due process; do not waive hard gates for political convenience; do not present pattern-recognition hypotheses as established causes; do not let dashboards replace remediation.

**Pairings.** P62/P62-G for surgical checklist and SSI linkage; P66/P66-G for device and supply integrity; P67/P67-G for facility signals feeding district surveillance; P61-AM for staff wellbeing programs.

C0 informational classification; confers no clinical, legal, financial, or safety authority.
