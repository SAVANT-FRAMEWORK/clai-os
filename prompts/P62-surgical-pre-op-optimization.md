---
ID: P62
Title: Surgical Pre-Op Optimization
Registry: CLAI-OS (P-series, open tier)
License: AGPL-3.0
Version: 2.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-10-12
Variant-Family: base · P62-G (Global Equity) · P62-AM (Advanced Markets)
---

# P62: Surgical Pre-Op Optimization

Abstract: P62 designs surgical pre-operative optimization across three operating contexts. The base specification (high-resource perioperative medicine) calculates surgical risk with ACS NSQIP, Revised Cardiac Risk Index, and Gupta-class calculators; identifies modifiable risk factors (anemia, malnutrition, diabetes control, smoking); generates time-boxed optimization protocols; coordinates anesthesia, surgery, medicine, and nutrition; and tracks readiness milestones across a 2–8 week window with ERAS and frailty assessment for special populations. The P62-G Global Equity variant re-founds preparation on the WHO Surgical Safety Checklist as mandatory logic where there is no anesthesia machine, blood bank, or ICU: cesarean decision support via partograph, ketamine and spinal anesthesia defaults, adapted START triage, traditional surgery collaboration boundaries, and SSI prevention without running water. The P62-AM Advanced Markets variant adapts to Asia-Pacific advanced systems: Japan-validated E-PASS and bleeding scores, Japan ERAS protocols, gastric cancer surgery decision support, robotic surgery optimization, and HBV reactivation prophylaxis. In every variant, risk must be computed by validated instruments, the checklist is non-skippable, and the final readiness decision belongs to the responsible surgical team.

## The Prompt (Base Specification)

Provenance: verbatim from the author's base specification (*CLAI OS P51-P70.txt*); no edits beyond whitespace.

ROLE: You are a Perioperative Medicine Specialist who optimizes patients for surgery. You understand ERAS protocols, frailty assessment, and surgical risk calculators (ACS NSQIP, POSSUM).
ACTION: Design a pre-op optimization prompt that:
1.  Calculates surgical risk (cardiac, pulmonary, renal, bleeding, mortality)
2.  Identifies modifiable risk factors (anemia, malnutrition, diabetes control, smoking)
3.  Generates optimization protocols (timeframe, interventions, targets)
4.  Coordinates multidisciplinary care (anesthesia, surgery, medicine, nutrition)
5.  Tracks optimization progress (metrics, milestones, readiness assessment)
SCOPE:
•  Risk calculators: ACS NSQIP, Revised Cardiac Risk Index, Gupta calculator
•  Optimization window: 2-8 weeks pre-op (modifiable), day-of (non-modifiable)
•  Special populations: elderly (frailty), obese (OSA), cardiac (stents, valves)
•  Shared decision-making: risk communication, goals of care, alternatives
CONTEXT:
[INSERT: Surgical procedure, patient demographics, comorbidities, functional status, urgency]
EXAMPLES:
Input: "68-year-old male, BMI 32, elective laparoscopic colectomy for colon cancer,
HbA1c 8.5%, hemoglobin 10.2, eGFR 48, former smoker (quit 2 years ago),
METs 4, walks 1 block before dyspnea"
Risk Assessment:
PROCEDURE RISK: Laparoscopic colectomy (intermediate risk)
ACS NSQIP RISK:
•  Serious complication: 12.4%
•  Mortality: 1.8%
•  Cardiac complication: 4.2%
•  Renal dysfunction: 3.1%
•  Surgical site infection: 8.7%
REVISED CARDIAC RISK INDEX:
•  History of ischemic heart disease: Yes (prior MI 2019)
•  History of heart failure: No
•  History of cerebrovascular disease: No
•  Diabetes on insulin: No (oral agents)
•  Chronic kidney disease: Yes (eGFR 48)
•  High-risk surgery: No (intermediate)
•  RCRI Score: 2 → Cardiac risk: 6.6%
FRAILTY ASSESSMENT:
•  Grip strength: Not measured
•  Walking speed: Slow (1 block dyspnea)
•  Weight loss: None reported
•  Exhaustion: Not assessed
•  Activity level: Low (METs 4)
•  Frailty score: Intermediate (2/5 criteria)
OPTIMIZATION PROTOCOL (6 weeks pre-op):
WEEK 1-2: Baseline + Initiation
•  Cardiology consultation: Stress test, optimize cardiac meds
•  Nutrition consult: Protein supplementation, target albumin >3.5
•  Diabetes optimization: Endocrinology, target HbA1c <7.0%
•  Current: 8.5% → Adjust metformin, consider GLP-1 agonist
•  Goal: HbA1c 7.0% by week 4
•  Anemia workup: Iron studies, B12, folate
•  If iron deficiency: IV iron supplementation
•  Target Hgb >12 (current 10.2)
WEEK 3-4: Intensification
•  Prehabilitation: Physical therapy, breathing exercises
•  Target: METs >6, walk 2 blocks without dyspnea
•  Smoking confirmation: Cotinine test (former smoker, verify)
•  Medication reconciliation: Hold anticoagulants per protocol
WEEK 5-6: Verification
•  Repeat labs: Hgb, HbA1c, creatinine, albumin
•  Cardiac clearance: Stress test result, optimization complete
•  Final anesthesia evaluation: Airway, OSA screening (STOP-BANG)
•  Readiness confirmation: All targets met → proceed
DAY OF SURGERY:
•  Glycemic control: Target 80-180 mg/dL
•  DVT prophylaxis: Heparin + SCDs
•  Antibiotics: Cefazolin within 60 min of incision
•  Temperature management: Forced air warming
SHARED DECISION-MAKING:
•  Risk communication: "Out of 100 people like you having this surgery,
about 12 have a serious complication, and 2 do not survive. With optimization,
we can reduce this risk by about 30%."
•  Alternatives discussed: Open colectomy (higher risk), non-operative management
(not curative for cancer), neoadjuvant chemotherapy first (delay surgery)
•  Patient preference: Proceed with optimization protocol, goal: surgery in 6 weeks
FORMAT:
•  Risk calculator integration
•  Modifiable risk factor identification
•  Optimization timeline with milestones
•  Multidisciplinary coordination checklist
•  Readiness assessment rubric
•  Shared decision-making documentation

## Architecture

P62 sits on the boundary between decision support and operative safety: its outputs gate whether surgery proceeds, so gating logic is deterministic and model inference is confined to synthesis, documentation, and communication.

**Deterministic-first safety pathways.** Risk figures come from validated calculators (ACS NSQIP, RCRI, Gupta; E-PASS in -AM) executed as deterministic code over structured inputs — the model never estimates a risk percentage. Optimization targets (hemoglobin, HbA1c, albumin, functional capacity) are tracked against fixed thresholds with deterministic readiness rules; the -G variant's WHO Surgical Safety Checklist is encoded as a mandatory state machine (sign-in / time-out / sign-out) that cannot report completion with unchecked items. Red-flag conditions (uncontrolled airway risk, critical anemia, active infection at surgical site) route through non-bypassable deterministic escalation to the responsible surgeon and anesthetist.

**FHIR R4 mapping.** Risk scores and assessment findings map to Observation; the optimization plan maps to CarePlan with activity targets and milestone dates; consultations map to ServiceRequest; labs map to DiagnosticReport; medication changes to MedicationRequest; the surgical case itself to Procedure (pre-op state) with Encounter linkage; the digitized WHO checklist maps to Questionnaire/QuestionnaireResponse with Task-driven sign-in/time-out/sign-out states; shared decision-making and consent discussions map to Consent and Communication. All resources carry signed Provenance.

**Interposition contract.** P62 executes behind the CLAI-OS interposition layer: no readiness statement, checklist state transition, or anesthesia protocol card reaches the operative record without Safety Kernel validation against deterministic rules (checklist completeness, contraindication screening, weight-based field bounds). Every risk figure and protocol step is emitted in a Clinical Assertion Wrapper with per-claim epistemic labels distinguishing calculator-derived values, clinician-entered findings, and model-drafted narrative.

**Audit and provenance stack.** Checklist state transitions, readiness determinations, overrides, and protocol deviations are written to an immutable Merkle-anchored audit trail suitable for surgical morbidity-and-mortality review; recursive self-audit monitors calculator input distributions and drift; prompt mortality governs version expiry of protocol logic.

**C0 classification.** This artifact is C0 informational: it confers no clinical, legal, financial, or safety authority. Operative decisions remain with credentialed surgical and anesthesia providers under local governance.

## Variations

### P62-G — Global Equity Variant

Author's variant abstract (*CLAI-OS Global Equity Extension*):

> We present P62-G, a surgical preparation system built around the WHO Surgical Safety Checklist as mandatory prompt logic, with audio guidance in local languages. The system includes cesarean section decision support—most common surgery globally—assessing fetal distress (Pinard stethoscope + partograph), obstructed labor (destruction pattern on partograph), and hemorrhage risk (previa history, prior cesareans). Anesthesia protocols default to ketamine (safe, no airway compromise, no equipment) and spinal anesthesia (no electricity), with ether/chloroform fallback where no alternatives exist. Trauma surgery modules include mass casualty triage (START protocol adapted), damage control surgery, and antibiotic prophylaxis with limited stock (cefazolin if available; metronidazole + gentamicin otherwise). Traditional surgery collaboration provides safe technique guidance for circumcision (tetanus prophylaxis, hemorrhage control) and distinguishes reducible fractures (acceptable for traditional bone setters) from open/compound fractures requiring orthopedic referral. SSI prevention functions without running water: alcohol-based hand rub (WHO formulation), chlorhexidine skin prep in single-use sachets, plastic sheet draping, and clipper-only hair removal.

Variant prompt compiled from the author's Global Equity Extension specification.

ROLE: You are a safe-surgery systems architect with experience in district hospitals and humanitarian surgical programs where there is no anesthesia machine, no blood bank, no ICU, and often no running water. You treat the WHO Surgical Safety Checklist as non-negotiable logic, and you design around the resources that actually exist: pulse oximetry, clinical exam, conjunctival pallor for anemia, same-day optimization, blankets for warming, and family-directed blood donation.

ACTION: Design a complete surgical preparation and safety workflow for the deployment context below. Deliver:
1. A digitized WHO Surgical Safety Checklist (sign-in, time-out, sign-out) adapted to the local cadre structure, with an audio guidance script outline in the deployment language(s) and a paper fallback
2. A cesarean section decision-support module: fetal distress assessment using Pinard stethoscope and partograph, obstructed labor recognition from partograph pattern, and hemorrhage risk stratification (previa history, prior cesareans), each with explicit escalation criteria
3. An anesthesia protocol selector defaulting to ketamine (no airway compromise, no equipment dependency) and spinal anesthesia (no electricity requirement), with weight-based dosing fields, contraindication checks, and ether/chloroform documented only as last-resort fallback where no alternatives exist
4. A trauma module: adapted START mass-casualty triage algorithm, damage control surgery sequencing, and antibiotic prophylaxis logic keyed to actual stock (cefazolin if available; metronidazole plus gentamicin otherwise)
5. A traditional surgery collaboration module: safe-technique guidance for circumcision (tetanus prophylaxis, hemorrhage control) and a fracture boundary classifier distinguishing reducible fractures acceptable for traditional bone setters from open/compound fractures requiring orthopedic referral
6. An SSI prevention protocol for no-running-water settings: alcohol-based hand rub (WHO formulation), chlorhexidine skin prep in single-use sachets, plastic sheet draping, and clipper-only hair removal (no shaving)
7. A same-day preoperative optimization checklist using pulse oximetry, clinical exam, and conjunctival pallor, with family-directed blood donation coordination steps

SCOPE:
• The WHO Surgical Safety Checklist is mandatory logic, not optional guidance; every pathway must pass through it
• All modules must function without electricity-dependent equipment, cross-matched blood banks, or ICU backup; state the contingency for each missing resource
• Traditional practitioner collaboration is structured as referral boundaries and shared safety technique, not displacement
• The system supports clinical decision-making and checklist enforcement; final operative decisions rest with the responsible surgical provider

CONTEXT:
[INSERT: facility type and staffing (surgeon, medical officer, nurse-anesthetist); available anesthesia agents and stock; blood sourcing arrangements; water and power reliability; common case mix (obstetric, trauma, elective); local language(s); traditional practitioner presence]

FORMAT:
• Checklist modules as timed sections (sign-in / time-out / sign-out) with per-item audio script lines
• Decision-support modules as tables: finding | assessment method | threshold | action | escalation
• Triage algorithm as ASCII flow or numbered decision steps
• Prophylaxis and anesthesia sections as protocol cards: indication | agent | weight-based field | contraindications | fallback
• "Resource Absence Map": table of assumed-missing resources (anesthesia machine, blood bank, ICU, running water) against the specified substitute
• "Do Not" list: prohibited practices (razor shaving, proceeding without checklist completion, open fracture management by traditional bone setters)

Deployment constraint (invariant for this variant): offline-first; open-weight models only (Llama 3 / Mistral / Phi-3 class); no closed-API processing of patient-identifiable data.

### P62-AM — Advanced Markets Variant

From the author's *CLAI-OS Advanced Markets Extension (P51-AM – P70-AM)*. No AM prompt body exists in the source; the variant is specified as deltas against the base prompt.

**What Changes**
| Dimension | US-Centric (P62) | Asia-Pacific (P62-AM) |
|-----------|------------------|----------------------|
| Risk Calculators | ACS NSQIP, RCRI | **Asia-specific**: Japan JCVB (Japanese Comprehensive Validation for Bleeding), E-PASS (Estimation of Physiologic Ability and Surgical Stress — Japan-validated), APACHE for ICU (universal but calibrated), tailored for Asian body habitus (lower BMI but higher visceral fat) |
| Optimization | 6-week prehab | **Asia-adapted**: Shorter prehab (2-3 weeks, high patient volume East Asia). Pre-op TCM/Kampo optimization (some patients request). HBV screening before immunosuppressive surgery. H. pylori eradication before gastric surgery. |
| Anesthesia | Propofol, sevoflurane | **Asia-standard**: Propofol/sevoflurane universal, but epidural anesthesia preferred for GI surgery (Japan enhanced recovery after surgery — ERAS). Acupuncture-assisted anesthesia (China TCM-integrated hospitals). |
| Equipment | Forced air warming | **Standard**: Forced air warming (Japan/Korea/Singapore). China/India = mixed (some top hospitals have, rural do not). Robotic surgery (Da Vinci high adoption Japan/Korea/China urban). |
| Blood | Cross-matched units | **Universal**: Cross-matched blood (Japan/Korea/Singapore/China urban). Pre-op autologous donation (Japan). Directed donation (family) in India/SE Asia where supply is intermittent. |

**Extended Actions**
```
P62-AM EXTENDED ACTIONS:
6. Implement Japan ERAS protocols: 
   Enhanced Recovery After Surgery is 
   standard in Japan. AI guides: no NPO 
   after midnight (carbohydrate loading 
   2h pre-op), early mobilization (day 0), 
   early enteral feeding (day 0-1), 
   opioid-sparing analgesia (epidural + 
   acetaminophen + NSAID), no routine 
   drains.

7. Build gastric cancer surgery decision 
   support: Most common cancer surgery in 
   East Asia. AI assesses: EGC vs AGC, 
   ESD vs gastrectomy (distal/total/proximal), 
   lymph node dissection extent (D1 vs D2 
   vs D2+), splenic preservation, omentectomy, 
   Bursectomy (Japan JCOG1001 controversy).

8. Support robotic surgery optimization: 
   High Da Vinci adoption in Japan/Korea/
   China for prostate, gastric, colorectal. 
   AI predicts operative time, blood loss, 
   conversion risk by surgeon volume 
   (learning curve analysis).

9. Add HBV reactivation prophylaxis: 
   Before major surgery with immunosuppression 
   (transplant, cardiac with bypass, major 
   oncology), HBsAg/anti-HBc screening. 
   If positive → entecavir/tenofovir 
   prophylaxis starting pre-op.

10. Design for same-day surgery (Japan/
    Singapore): High adoption for 
    cataract, hernia, orthopedic. AI 
    optimizes discharge criteria, home 
    support assessment, and post-op 
    remote monitoring via messaging apps.
```

---

Named jurisdiction examples (from the source): Japan (E-PASS, JCVB bleeding validation, ERAS with carbohydrate loading and day-0 mobilization, pre-op autologous donation, Da Vinci adoption, same-day surgery); Korea (robotic surgery volume, sevoflurane/propofol standard); Singapore (same-day surgery, forced-air warming standard); China (acupuncture-assisted anesthesia in TCM-integrated hospitals, urban robotic adoption); India (directed family donation where supply is intermittent).

### Regional Adapters

Regional adapters re-point the same optimization spine at local surgical reality. -AF (Africa): the -G variant is primary — WHO checklist with local-language audio, partograph-based cesarean decision support, ketamine/spinal anesthesia defaults, family-directed blood donation coordination, no-water SSI prevention. -AR (Arab region): -G module for conflict-affected and low-resource facilities; adapted START triage for mass-casualty events; humanitarian supply-chain constraints on prophylaxis agents. -US: the base specification as written — NSQIP/RCRI risk quantification, 2–8 week prehabilitation, anesthesia pre-op clinics, ERAS pathways. APAC: the -AM variant — E-PASS and Japan-validated bleeding scores, Japan ERAS (carbohydrate loading, day-0 mobilization, opioid-sparing analgesia), gastric cancer surgery decision support, robotic volume analysis, HBV reactivation prophylaxis before immunosuppressive surgery. Adapters are configuration packs (calculator set, checklist language pack, anesthesia formulary, escalation endpoints); none relaxes checklist completeness or deterministic gating.

## Jurisdiction Matrix

| Regime | Variant applicability | Consent & de-identification posture | Residency & transfer |
|---|---|---|---|
| HIPAA (US) | Base variant (primary) | Operative and anesthesia records are PHI; pre-op optimization notes shareable within treatment context; anesthesia agent records retained per facility policy | US-hosted systems; BAAs for service layers; audit exports de-identified for QI |
| GDPR (EU/EEA) | Base-EU; -AM partnerships | Art. 9 special-category health data; DPIA for digitized checklist and risk scoring; explicit consent or care condition | EU/EEA residency; SCCs for transfer; de-identified audit aggregates only |
| NDPR (Nigeria) | -G variant (primary) | Operative, obstetric (partograph), and anesthesia records are sensitive personal data; explicit consent; witnessed verbal consent where literacy limited | In-country hosting; only de-identified audit aggregates leave the facility |
| Kenya DPA 2019 | -G variant (Kenya) | Sensitive health data; controller registration; plain-language consent notice | Transfer with adequacy/safeguards; local copy retained |
| India DPDP Act | -G/-AM (India; directed family donation contexts) | Consent plus notice; donor personal data (relationship, serostatus) at patient-level sensitivity; facility records governance | Sectoral program agreements may impose residency; confirm per program |
| Brazil LGPD | -G variant (Latin America) | Sensitive health data; explicit consent or care condition; ANPD oversight | Transfer per ANPD mechanisms |
| Saudi PDPL | -G/-AM (Arab region) | Sensitive data; strict transfer controls | In-Kingdom hosting default |
| China PIPL | -AM variant (China; TCM-integrated hospitals) | Sensitive personal information; separate consent; PIPIA; robotic/anesthesia data flows localized | Localization for large handlers; CAC assessment for export |
| Japan APPI | -AM variant (Japan; ERAS, E-PASS, autologous donation) | Special-care-required personal information; opt-in consent; pre-op autologous donation records as medical data | Transfer with consent or APPI-equivalent protections |
| Tribal / community consent | -G variant (traditional practitioner collaboration) | Traditional birth attendant and bone setter referral logs implicate practitioners as data subjects; community engagement precedes documentation programs | Community-governed records; practitioner withdrawal rights honored |

## Methodology

Base: surgical risk quantification (ACS NSQIP, Revised Cardiac Risk Index, Gupta calculator); modifiable risk factor identification (anemia, malnutrition, glycemic control, smoking); time-boxed optimization protocol generation (2–8 week window); multidisciplinary coordination (anesthesia, surgery, medicine, nutrition); readiness milestone tracking; frailty and OSA screening for special populations; shared decision-making structure.

Global Equity (P62-G): WHO Surgical Safety Checklist digitization with local-language audio; partograph digitization for cesarean decision support; weight-based ketamine/spinal anesthesia protocol templates; adapted START mass-casualty triage; traditional surgery safety boundary classifier; SSI prevention protocol for no-water settings (WHO hand-rub formulation, single-use chlorhexidine, clipper-only hair removal).

Advanced Markets (P62-AM): Japan ERAS protocol logic (carbohydrate loading, early mobilization and enteral feeding, opioid-sparing analgesia, no routine drains); gastric cancer surgery decision support (ESD versus gastrectomy, D1/D2/D2+ dissection); robotic surgery operative prediction by surgeon volume; HBV reactivation screening and prophylaxis before immunosuppressive surgery; same-day surgery discharge optimization with messaging-app remote monitoring.

## Merits

• Quantifies operative risk with validated calculators and makes optimization progress auditable against explicit targets
• Enforces the WHO Surgical Safety Checklist as non-skippable logic in every variant — the intervention with the strongest evidence base in surgical safety
• Enables structured cesarean and anesthesia decision-making where no anesthesia machine, blood bank, or ICU exists (-G)
• Carries the same discipline into Asia-Pacific high-volume systems: ERAS, gastric cancer surgery, robotic optimization, HBV prophylaxis (-AM)
• Structures collaboration with traditional practitioners as safety boundaries rather than displacement (-G)

## Guidance for Use

**Base deployments.** Wire the calculator inputs to structured EHR fields; confirm calculator versions against current publications; the readiness decision remains with the surgeon and anesthetist — the system tracks, it does not clear.

**Global Equity deployments (-G).** Offline-first on facility-controlled hardware; open-weight models only (Llama 3, Mistral, Phi-3 class); no closed-API processing of patient-identifiable operative data. Audio scripts must be recorded and validated by local clinicians in the deployment language — machine translation of anesthesia and obstetric safety language is not acceptable. Anesthesia and prophylaxis sections are protocol scaffolds; the responsible clinician confirms agents, doses, and contraindications against current WHO guidance and national formularies.

**Advanced Markets deployments (-AM).** Localize risk calculators (E-PASS, JCVB-class bleeding scores); confirm ERAS pathway elements against national society guidance; HBV screening and prophylaxis protocols per national hepatology guidelines.

**Prerequisites (all variants).** Named surgical and anesthesia owners; functioning escalation path; validated calculator versions; audit storage; checklist language packs validated.

**Misuse.** Do not use to override clinical judgment on proceeding, to skip checklist items under time pressure, to extrapolate calculator outputs outside validated populations, or to present risk percentages as certainties. Fracture and traditional-practice boundary logic defaults to referral on uncertainty.

**Pairings.** P70/P70-G (quality and surgical safety surveillance) for outcome feedback; P55 for medication reconciliation detail; P58 for EHR/FHIR integration; P64 for equity audit of surgical access.

C0 informational classification; confers no clinical, legal, financial, or safety authority.
