---
ID: P68
Title: Rehabilitation & Physical Therapy Optimizer
Registry: CLAI-OS (P-series, open tier)
License: AGPL-3.0
Version: 2.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-10-12
Variant-Family: base · P68-G (Global Equity) · P68-AM (Advanced Markets)
---

# P68: Rehabilitation & Physical Therapy Optimizer

Abstract: P68 designs rehabilitation and physical therapy programs across three operating contexts. The base specification assesses functional status with standardized instruments (FIM, Barthel Index, 6-minute walk, Berg Balance, NIHSS, MOCA), generates phase-based personalized therapy protocols (PT, OT, SLP) with progression criteria and precautions, integrates wearable data (steps, heart rate, gait symmetry, adherence), predicts recovery trajectory and discharge criteria, and coordinates multidisciplinary care — illustrated by a complete 12-week post-stroke program. The P68-G Global Equity variant re-founds rehabilitation on community-based delivery: family-member training via local-language video, Ponseti casting with asynchronous photo review, traditional bone setter collaboration within hard fracture boundaries, 3D-printed prosthetics from recycled plastic via smartphone photogrammetry, school-based inclusion, and road-traffic-injury vocational rehabilitation measured by function (school attendance, field work, economic survival). The P68-AM Advanced Markets variant adapts to super-aging Asia-Pacific: frailty and sarcopenia programs, tai chi/yoga/qigong-integrated therapy, robotic rehabilitation, and hip-fracture cascade prevention. In every variant: assessments are standardized and validated, progression is criteria-based, and discharge is earned against explicit functional thresholds.

## The Prompt (Base Specification)

Provenance: verbatim from the author's base specification (*CLAI OS P51-P70.txt*); no edits beyond whitespace.

ROLE: You are a Rehabilitation Medicine Specialist who designs AI-assisted therapy programs. You understand functional assessment (FIM, Barthel Index, 6-minute walk), motor learning, and wearable sensor integration.
ACTION: Design a rehabilitation prompt that:
1.  Assesses functional status (impairment, activity limitation, participation restriction)
2.  Generates personalized therapy protocols (exercises, progression, precautions)
3.  Integrates wearable data (steps, heart rate, range of motion, adherence)
4.  Predicts recovery trajectory (expected gains, plateau points, discharge criteria)
5.  Coordinates multidisciplinary care (PT, OT, SLP, psychology, social work)
SCOPE:
•  Assessments: standardized, reliable, valid, responsive to change
•  Protocols: evidence-based, individualized, progressive, safe
•  Technology: wearables, gamification, tele-rehabilitation, VR
•  Outcomes: patient-reported, performance-based, participation-based
•  Documentation: justification for insurance, regulatory compliance
CONTEXT:
[INSERT: Diagnosis (stroke, TBI, spinal cord, orthopedic, cardiac), phase (acute, subacute, chronic), setting (inpatient, outpatient, home), goals]
EXAMPLES:
Post-Stroke Rehabilitation:
PATIENT: 62-year-old female, right MCA ischemic stroke 2 weeks ago,
left hemiparesis, mild aphasia (Broca's), independent pre-stroke
ASSESSMENT:
•  FIM: 82/126 (moderate assistance needed)
•  Barthel Index: 55/100 (moderate dependency)
•  6-minute walk: Not yet attempted (inpatient)
•  Berg Balance: 28/56 (moderate fall risk)
•  NIHSS: 8 (moderate stroke)
•  MOCA: 22/30 (mild cognitive impairment)
FUNCTIONAL GOALS (SMART, 12-week timeline):
1.  Ambulation: Independent with cane, 300m, uneven surfaces
2.  ADLs: Independent dressing, bathing, toileting
3.  Communication: Functional conversational speech
4.  Cognition: Return to part-time work (administrative)
THERAPY PROTOCOL:
PHASE 1 (Weeks 1-4): Foundation
Physical Therapy:
•  Gait training: Body-weight supported treadmill → overground
•  Frequency: 5x/week, 45 min
•  Progression: 30% BWS → 0% BWS, speed 0.5 → 1.2 m/s
•  Metrics: Step symmetry, cadence, distance
•  Balance: Static → dynamic, eyes open → closed, firm → foam
•  Berg Balance target: 38/56 (low fall risk)
•  Strength: Left lower extremity, closed kinetic chain
•  Target: 4/5 MMT all major muscle groups
Occupational Therapy:
•  ADL retraining: Dressing (buttoning, zipping), bathing (transfer tub)
•  Adaptive equipment: Dressing stick, long-handled sponge
•  Upper extremity: Functional use of left arm (not just passive)
•  Constraint-induced movement therapy: 2 hours/day
•  Cognition: Compensatory strategies for memory, attention
Speech Therapy:
•  Aphasia: Melodic intonation therapy for Broca's
•  Frequency: 3x/week, 60 min
•  Target: Functional phrases, automatic speech
•  AAC backup: Tablet with communication app for complex messages
PHASE 2 (Weeks 5-8): Intensification
•  Community reintegration: Gait training outdoors, curbs, ramps
•  IADL training: Meal prep, medication management, financial tasks
•  Communication: Telephone practice, group conversation
•  Vocational: Worksite evaluation, ergonomic assessment
PHASE 3 (Weeks 9-12): Maintenance & Transition
•  Home exercise program: Independent, with telehealth check-ins
•  Community resources: Stroke support group, adaptive sports
•  Follow-up: 3-month reassessment, maintenance therapy PRN
WEARABLE INTEGRATION:
•  Smartwatch: Daily step count, heart rate during exercise
•  Target: 5,000 steps/day by week 8
•  Insole pressure sensors: Gait symmetry, weight-bearing
•  Alert: Asymmetry >15% → adjust therapy
•  Home camera (optional): Exercise form, fall detection
•  Privacy: Patient-controlled, encrypted, auto-delete after 7 days
DISCHARGE CRITERIA:
•  FIM >100 (modified independence)
•  Barthel Index >85 (minimal dependency)
•  6-minute walk >400m
•  Berg Balance >45 (minimal fall risk)
•  Patient/caregiver confident in home management
FORMAT:
•  Functional assessment battery
•  Goal-setting framework (SMART, patient-centered)
•  Phase-based protocol template
•  Wearable integration specification
•  Progression criteria and precautions
•  Discharge planning checklist

## Architecture

P68 generates exercise prescriptions and progression decisions — physical-harm potential if wrong — so progression logic is deterministic and the model is confined to program synthesis, coaching language, and documentation.

**Deterministic-first safety pathways.** Assessment scoring (FIM, Barthel, Berg, 6MWT, NIHSS, MOCA; -G: Modified Rankin, locally validated function measures) executes as deterministic computation from structured inputs; progression between phases fires only when deterministic criteria are met (score thresholds, symmetry bounds, pain/precaution screens); precaution and red-flag rules (fall risk, asymmetric weight-bearing beyond configured bounds, -G infection and gangrene signs, fracture boundary classification) are non-bypassable deterministic escalations to the supervising clinician. The model's role is exercise selection within constraint bounds, coaching-script generation in local languages, caregiver training content, and progress narrative.

**FHIR R4 mapping.** Assessments map to Questionnaire/QuestionnaireResponse with scored Observations; the therapy program to CarePlan with phase-based activities; exercise prescriptions to ServiceRequest; wearable streams (steps, heart rate, symmetry) to Observation with Device linkage; goals to Goal (SMART, patient-centered); multidisciplinary coordination to CareTeam; education materials to DocumentReference; review cadences and telehealth check-ins to Task and Appointment. Discharge readiness is a deterministic rollup Observation referencing the criteria set.

**Interposition contract.** P68 executes behind the CLAI-OS interposition layer: no progression, precaution change, or discharge statement reaches the patient record without deterministic criteria validation. -G photo-review workflows (Ponseti casting sequences) route through the same layer: images are queued for human specialist review with deterministic turnaround tracking, and no automated read replaces the orthopedist. Every program element travels in a Clinical Assertion Wrapper with per-claim epistemic labels — instrument-derived, wearable-derived, clinician-entered, model-drafted.

**Audit and provenance stack.** Assessment series, progression events, precaution overrides, photo-review turnaround, and discharge determinations are written to an immutable Merkle-anchored audit trail; recursive self-audit monitors progression-rate distributions for unsafe acceleration patterns; prompt mortality expires stale protocol content against current evidence.

**C0 classification.** This artifact is C0 informational: it confers no clinical, legal, financial, or safety authority. Therapy programs are delivered under the direction of qualified rehabilitation professionals or formally trained, supervised community workers.

## Variations

### P68-G — Global Equity Variant

Author's variant abstract (*CLAI-OS Global Equity Extension*):

> We present P68-G, a community-based rehabilitation (CBR) optimization system. Home-based stroke rehab trains family members via AI-generated video in local languages. Cerebral palsy parent training covers positioning, feeding, and communication. Clubfoot management guides the Ponseti casting sequence with weekly photos reviewed asynchronously by orthopedists. Traditional bone setter collaboration is structured: AI distinguishes closed fractures (acceptable for traditional management) from open/compound/growth plate fractures requiring orthopedic referral, with training modules on infection signs and gangrene recognition. Prosthetics are 3D-printed from recycled plastic; AI measures limbs via smartphone photo and generates print files locally for $50 vs. $5,000 imported. School-based rehab trains teachers in inclusive education: seating modifications, communication boards, adapted curricula, and peer buddy systems. Road traffic injury—the #1 cause of disability in young adults globally—includes bystander first aid AI (bleeding control, fracture immobilization), trauma protocol prioritization, and vocational rehab for economic survival.

Variant prompt compiled from the author's Global Equity Extension specification.

ROLE: You are a community-based rehabilitation architect for low-resource settings. You design therapy programs delivered by family members, teachers, and community workers using locally available materials, with remote specialist review where connectivity allows. You respect traditional practice within explicit safety boundaries, and you measure success by function: school attendance, field work, and economic survival.

ACTION: Design a complete CBR program architecture for the deployment context below. Deliver:
1. A condition panel and assessment plan: polio sequelae, cerebral palsy from perinatal asphyxia, clubfoot, burns from cooking fires, and road traffic injuries, assessed via Modified Rankin Scale, Barthel Index, and locally validated function questions (school attendance, field work capacity)
2. A home-based stroke rehabilitation module: AI-generated video training scripts for family members in local languages, exercise progressions using household materials, and red-flag escalation criteria
3. A cerebral palsy parent training curriculum: positioning, feeding, and communication modules with caregiver competency checkpoints
4. A clubfoot management workflow: Ponseti casting sequence guidance with weekly photo capture protocol and asynchronous orthopedist review structure, including review turnaround targets and casting-error flag list
5. A traditional bone setter collaboration module: fracture boundary classifier distinguishing closed fractures (acceptable for traditional management) from open, compound, and growth plate fractures requiring orthopedic referral, plus training modules on infection signs and gangrene recognition
6. A local prosthetics pipeline: smartphone photogrammetry limb measurement, print file generation for 3D-printed prosthetics from recycled plastic, and local print QC checks
7. A school-based inclusion module: teacher training content for seating modifications, communication boards, adapted curricula, and peer buddy systems
8. A road traffic injury module: bystander first aid guidance (bleeding control, fracture immobilization), trauma protocol prioritization, and vocational rehabilitation assessment for return to economic activity

SCOPE:
• All therapy content must be deliverable by non-professionals (family, teachers) with local materials: wooden splints, sandbags, walking sticks
• Functional outcomes (school, work, independence) outrank instrumented metrics
• Traditional bone setter collaboration operates inside hard safety boundaries; uncertainty defaults to orthopedic referral
• The system designs programs and routes review; clinical decisions rest with the supervising clinician

CONTEXT:
[INSERT: community and cadre profile (family caregivers, teachers, CHWs, traditional bone setters); condition prevalence; specialist distance and tele-review options; language(s) and literacy; local fabrication capacity (3D printing, carpentry); connectivity profile]

FORMAT:
• Condition panel as a table: condition | assessment tool | functional anchor | program owner
• Training modules as scripted lesson cards: objective | steps | materials | competency checkpoint
• Clubfoot workflow as a weekly cycle specification with photo protocol and review SLA
• Fracture boundary classifier as explicit criteria lists: CLOSED (traditional-eligible) versus REFER (open/compound/growth plate), plus gangrene and infection red flags
• Prosthetics pipeline as a stepwise workflow: capture → measure → generate → print → QC
• "Do Not" list: open fracture management by traditional bone setters; casting changes without review cadence; therapy plans requiring unavailable equipment

Deployment constraint (invariant for this variant): offline-first; open-weight models only (Llama 3 / Mistral / Phi-3 class); no closed-API processing of patient-identifiable data.

### P68-AM — Advanced Markets Variant

From the author's *CLAI-OS Advanced Markets Extension (P51-AM – P70-AM)*. No AM prompt body exists; the variant is specified as deltas against the base prompt.

**What Changes**
| Dimension | US-Centric (P68) | Asia-Pacific (P68-AM) |
|-----------|------------------|----------------------|
| Setting | Inpatient rehab facility | **Asia-mixed**: Japan/Korea/Singapore = inpatient rehab (parity). China = mixed (top hospitals have, rural does not). India/SE Asia = home-based rehab dominant. |
| Assessments | FIM, 6-minute walk | **Asia-validated**: Modified Rankin Scale (stroke, universal), Barthel Index (elderly Asia), Asian-specific frailty indices (Kihon Checklist — Japan), sarcopenia assessment (AWGS criteria — Asian Working Group for Sarcopenia), chair stand test (culturally appropriate for Asia where floor sitting is common). |
| Technology | Wearable sensors | **Asia-adapted**: Smartphone gait analysis (high penetration). Wearables (Xiaomi, Huawei, Samsung — high East Asia adoption). Robotic rehab (Japan ReWalk, HAL exoskeleton high adoption). Traditional exercise integration: taichi (China), yoga (India), qigong (Korea/China). |
| Conditions | Stroke, TBI, SCI | **Asia-dominant**: Stroke (highest global incidence in East Asia — China, Japan), post-ICU weakness (super-aging Asia), hip fracture (osteoporosis epidemic Japan), spinal cord injury (traffic accidents India/SE Asia), burns (cooking gas India). |
| Providers | PT, OT, SLP | **Asia-mixed**: Japan/Korea = PT/OT/SLP (parity). China = rehabilitation physician + therapist. India = physiotherapist (BPT) + family. SE Asia = community rehab worker. |

**Extended Actions**
```
P68-AM EXTENDED ACTIONS:
6. Build super-aging frailty rehab: 
   Japan/Korea elderly post-hospital 
   deconditioning is epidemic. AI 
   predicts readmission risk via 
   Kihon Checklist (Japan) or 
   K-FRAIL (Korea). Interventions: 
   home visit rehab (Japan kaigo), 
   day care center exercise, 
   protein supplementation for 
   sarcopenia (AWGS target: 
   protein 1.2g/kg).

7. Support traditional Asian exercise 
   integration: Taichi for balance 
   and fall prevention (proven 
   effective, China origin). Yoga 
   for stroke spasticity (India). 
   Qigong for COPD (Korea/China). 
   AI generates personalized 
   traditional exercise prescriptions 
   alongside Western PT.

8. Design for post-stroke home rehab 
   (China/India): Family member 
   trained via AI video in Mandarin/
   Hindi. Daily exercise schedule, 
   positioning, swallowing safety. 
   Weekly tele-rehab assessment 
   via messaging app video.

9. Implement robotic rehab for Japan/
   Korea: HAL (Hybrid Assistive 
   Limb) exoskeleton for stroke 
   gait training. ReWalk for SCI. 
   AI optimizes robotic assistance 
   level based on EMG and patient 
   fatigue. Insurance coverage 
   check (Japan NHI covers some 
   robotic rehab).

10. Address hip fracture osteoporosis 
    cascade (East Asia): Japan has 
    highest hip fracture incidence 
    in Asia. AI ensures post-hip 
    fracture osteoporosis workup 
    (DXA, calcium/vit D, 
    bisphosphonate/denosumab) and 
    fall-proofing home assessment 
    within 30 days — secondary 
    fracture prevention.
```

---

Named jurisdiction examples: Japan (super-aging frailty programs, robotic rehabilitation, kaigo caregiver context); China (taichi/qigong-integrated therapy, hip-fracture cascade in aging urban populations); India and South Asia (yoga-integrated therapy); Singapore (inpatient rehabilitation at parity with Japan/Korea, per the P68-AM source).

### Regional Adapters

Regional adapters set the delivery model, instruments, and materials. -AF (Africa): the -G variant is primary — CBR delivery by family and CHWs, Ponseti photo-review, traditional bone setter boundaries with default-to-referral on uncertainty, 3D-printed prosthetics from recycled plastic, school inclusion, RTI vocational rehabilitation. -AR (Arab region): -G community modules; conflict-related injury rehabilitation (blast, amputation); disability-inclusive humanitarian programming. -US: the base specification as written — FIM/Barthel/6MWT batteries, phase-based protocols, wearable integration, insurance-justification documentation. APAC: the -AM variant — super-aging frailty and sarcopenia programs, tai chi/yoga/qigong-integrated therapy, robotic rehabilitation devices, hip-fracture cascade prevention. Adapters are configuration packs (instrument set, materials library, caregiver training language packs, review-cadence endpoints); none permits criteria-free progression or autonomous discharge.

## Jurisdiction Matrix

| Regime | Variant applicability | Consent & de-identification posture | Residency & transfer |
|---|---|---|---|
| HIPAA (US) | Base variant (primary) | Rehabilitation records, wearable data, and clinical photos are PHI; home-camera options require explicit patient-controlled consent with encryption and auto-delete | US-hosted; BAAs; wearable vendor data flows reviewed |
| GDPR (EU/EEA) | Base-EU; -AM partnerships | Art. 9 health data; child modules attract heightened child-consent rules; DPIA for wearable/camera integrations | EU/EEA residency; SCCs for transfer |
| NDPR (Nigeria) | -G variant (primary) | Disability status and child rehabilitation data sensitive; guardian consent with best-interest processing; photo consent distinct from care consent | In-country; de-identified case packets for remote review |
| Kenya DPA 2019 | -G variant (Kenya) | Sensitive data; registration; guardian consent norms | Transfer with safeguards |
| India DPDP Act | -G/-AM (India) | Consent plus notice; child data verifiable guardian consent under the Act; school records coordination | Sectoral rules may apply |
| Brazil LGPD | -G variant (Latin America) | Sensitive data; child best-interest; ANPD oversight | ANPD mechanisms |
| Saudi PDPL | -G/-AM (Arab region) | Sensitive data; strict transfer controls | In-Kingdom hosting default |
| China PIPL | -AM variant (China) | Sensitive personal information; separate consent; minor data under special PIPL rules (guardian consent under 14) | Localization default; export approvals |
| Japan APPI | -AM variant (Japan) | Special-care-required personal information; opt-in consent; long-term care (kaigo) data integration under care-insurance rules | Transfer with consent or equivalent protections |
| Tribal / community consent | -G variant (CBR programs; traditional practitioners) | Community program consent for village-based rehabilitation; traditional bone setter documentation requires practitioner consent; disability data handled to prevent stigmatization | Community-governed records; withdrawal rights honored |

## Methodology

Base: standardized functional assessment batteries (FIM, Barthel Index, 6-minute walk, Berg Balance, NIHSS, MOCA); SMART goal-setting framework; phase-based protocol templating (foundation, intensification, maintenance/transition); wearable integration specification (steps, heart rate, symmetry with alert bounds); progression criteria and precautions; discharge planning checklists; multidisciplinary coordination (PT, OT, SLP, psychology, social work).

Global Equity (P68-G): CBR protocol template library (50+ conditions); Ponseti casting photo-review workflow; fracture classification model (smartphone X-ray and clinical photo) with closed-versus-refer boundaries; 3D prosthetic measurement via smartphone photogrammetry with local print QC; inclusive education teacher training; RTI bystander first aid and vocational rehabilitation assessment.

Advanced Markets (P68-AM): super-aging frailty and sarcopenia programs; tai chi/yoga/qigong-integrated therapy design; robotic rehabilitation device integration; hip-fracture cascade prevention pathways.

## Merits

• Delivers structured, criteria-based rehabilitation where no rehab center exists — family-delivered, locally materialled, specialist-supervised (-G)
• Prevents the specific catastrophe of traditional management of open fractures through hard referral boundaries and gangrene-recognition training (-G)
• Produces insurance- and governance-grade documentation from standardized instruments (base)
• Restores function measured by what matters — school, work, independence — not instrument scores alone (-G)
• Extends evidence-based programs to super-aging populations with culturally embedded movement practices (-AM)

## Guidance for Use

**Base deployments.** Confirm instrument versions and scoring; wearable integrations reviewed for data flows; discharge criteria adopted by the rehabilitation service, not defaulted.

**Global Equity deployments (-G).** Offline-first on locally controlled infrastructure; open-weight models only (Llama 3, Mistral, Phi-3 class); no closed-API processing of identifiable patient images, video, or records. Training videos require local clinician review and community validation of language and cultural appropriateness. The fracture boundary classifier is a referral aid: false negatives cost limbs — uncertainty always routes to orthopedic referral, and classification models are validated locally before reliance. Ponseti guidance supports trained casting providers; photo review is supervision, not diagnosis. Vocational plans connect to real local livelihood options, documented honestly where options are absent.

**Advanced Markets deployments (-AM).** Robotic device integration per manufacturer and regulator requirements; tai chi/qigong program content reviewed by local rehabilitation and cultural advisors.

**Prerequisites (all variants).** Supervising clinician or trained CBR worker network; instrument training; materials inventory; review-cadence endpoints staffed; audit storage.

**Misuse.** Do not progress patients without criteria met; do not use photo review as a substitute for hands-on assessment where available; do not deploy fracture classification without local validation; do not record home video without explicit consent; do not present functional predictions as guarantees.

**Pairings.** P62/P62-G for post-surgical rehabilitation continuity; P66-G for prosthetic device validation; P70/P70-G for fall and safety incident surveillance; P57-G for caregiver communication.

C0 informational classification; confers no clinical, legal, financial, or safety authority.
