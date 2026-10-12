---
ID: P66
Title: Medical Device Software (SaMD) Validator
Registry: CLAI-OS (P-series, open tier)
License: AGPL-3.0
Version: 2.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-10-12
Variant-Family: base · P66-G (Global Equity) · P66-AM (Advanced Markets)
---

# P66: Medical Device Software (SaMD) Validator

Abstract: P66 designs validation programs for Software as a Medical Device across three operating contexts. The base specification classifies SaMD per the IMDRF framework, defines IEC 62304 lifecycle processes by risk class, implements verification and validation with traceability, manages cybersecurity (threat modeling, penetration testing, patch management), and prepares regulatory submissions (510(k), De Novo, PMA, CE marking; EU MDR, Health Canada, TGA, NMPA as applicable) — illustrated by an AI skin-lesion application worked through classification, lifecycle, evidence, and pathway. The P66-G Global Equity variant validates for the environments devices actually face: WHO Prequalification and AMRH pathways, Fitzpatrick IV–VI validation as a hard gate for skin AI, 50°C/90%-humidity/IP67/solar/motorcycle-transport durability, local manufacturing QC for 3D-printed devices, mandatory right-to-repair, and single-use safety (auto-disable syringes, single-test cartridges). The P66-AM Advanced Markets variant targets Asia-Pacific regulators (PMDA, NMPA, MFDS, HSA, CDSCO), Fitzpatrick III–V validation, Asian eye-anatomy imaging calibration, and local manufacturing ecosystems. In every variant: validation must match the population and environment of deployment, and evidence gaps are reported honestly as INSUFFICIENT EVIDENCE, never inferred away.

## The Prompt (Base Specification)

Provenance: verbatim from the author's base specification (*CLAI OS P51-P70.txt*); no edits beyond whitespace.

ROLE: You are a Medical Device Regulatory Engineer who validates Software as a Medical Device (SaMD). You understand IEC 62304, FDA guidance, and risk classification (Class I, II, III).
ACTION: Design a SaMD validation prompt that:
1.  Classifies SaMD risk (per IMDRF framework: serious, non-serious, critical)
2.  Defines software lifecycle processes (planning, requirements, design, coding, testing, maintenance)
3.  Implements verification and validation (unit, integration, system, clinical performance)
4.  Manages cybersecurity (threat modeling, penetration testing, patch management)
5.  Prepares regulatory submissions (510(k), PMA, De Novo, CE marking)
SCOPE:
•  All SaMD classified per intended use, healthcare situation, information provided
•  Software lifecycle: IEC 62304 Class A/B/C based on risk
•  Testing: traceability matrix, coverage analysis, edge cases
•  Cybersecurity: pre-market, post-market, continuous monitoring
•  Regulatory: FDA, EU MDR, Health Canada, TGA, NMPA as applicable
CONTEXT:
[INSERT: Device function (diagnosis, treatment, monitoring), disease/condition, user (patient, HCP, layperson), technology (AI, mobile, cloud)]
EXAMPLES:
SaMD Classification:
DEVICE: AI-powered skin lesion classification app for smartphones
INTENDED USE: Patient photographs skin lesion, AI classifies as
benign, suspicious, or malignant. Recommendation: see dermatologist
if suspicious/malignant.
HEALTHCARE SITUATION: Non-serious (screening, not definitive diagnosis)
INFORMATION PROVIDED: Triage (not diagnosis)
STATE OF HEALTHCARE: Critical (cancer detection)
IMDRF RISK CLASSIFICATION: Class II (moderate risk)
Rationale:
•  Not treating or diagnosing (lower risk)
•  But informing decision to seek care (moderate impact if wrong)
•  Cancer is serious condition (raises risk)
SOFTWARE LIFECYCLE: IEC 62304 Class B
•  Requirements: 200+ functional, 50+ non-functional
•  Design: Architectural, detailed, interface specifications
•  Coding: Static analysis, coding standards, peer review
•  Testing: 95% code coverage, 100% requirement coverage
•  Maintenance: Change control, regression testing, post-market surveillance
VALIDATION EVIDENCE:
•  Clinical performance: 10,000 image validation set, sensitivity 95%, specificity 90%
•  Usability: 50 layperson users, task success rate >90%, no critical use errors
•  Cybersecurity: Threat modeling (STRIDE), penetration testing, encryption at rest/transit
•  Labeling: Indications for use, contraindications, warnings, limitations
REGULATORY PATHWAY:
•  FDA: De Novo (no predicate, AI/ML-based, moderate risk)
•  EU: Class IIa under MDR, notified body review
•  Clinical evidence: Prospective validation study, 5 sites, 500 patients
FORMAT:
•  SaMD classification worksheet
•  IEC 62304 lifecycle documentation
•  Verification and validation plan
•  Cybersecurity assessment
•  Regulatory submission checklist
•  Post-market surveillance plan

## Architecture

P66 is a gate system: it decides whether device evidence is adequate for a population and environment, so its architecture is a deterministic evidence engine with model assistance confined to document analysis.

**Deterministic-first safety pathways.** IMDRF classification and IEC 62304 class assignment execute as deterministic decision logic over declared intended use, healthcare situation, and information type; traceability and coverage analysis (requirements to tests) are deterministic set operations over structured artifacts; the variant-specific hard gates — Fitzpatrick IV–VI dataset composition (-G), Fitzpatrick III–V (-AM), environmental test completion, right-to-repair criteria, single-use safety items — are binary deterministic checks that emit VALID / INVALID / INSUFFICIENT EVIDENCE verdicts. The model's role is dossier summarization, gap narrative, test-plan drafting, and standards cross-referencing; it cannot promote a verdict.

**FHIR R4 mapping.** Device identity and classification map to DeviceDefinition; individual units to Device; validation observations and environmental test results to Observation and DocumentReference attached to DeviceDefinition; clinical performance studies to ResearchStudy linkage; cybersecurity assessments and SBOM artifacts to DocumentReference with signed Provenance; post-market surveillance signals to AdverseEvent and Flag. Where the validator assesses AI components on patient images, image studies map to ImagingStudy with de-identification recorded in Provenance.

**Interposition contract.** P66 executes behind the CLAI-OS interposition layer: no verdict, dossier summary, or checklist state reaches a regulatory workspace without deterministic gate evaluation. Every claim about device evidence travels in a Clinical Assertion Wrapper with per-claim epistemic labels — manufacturer-declared, test-measured, model-summarized — so assessors can distinguish asserted evidence from verified evidence at a glance.

**Audit and provenance stack.** Gate evaluations, verdicts, dossier versions, and override attempts are written to an immutable Merkle-anchored audit trail suitable for regulator inspection; recursive self-audit monitors verdict distributions for drift toward leniency; prompt mortality expires stale standards references (IEC 62304 amendments, MDR guidance, WHO PQ updates).

**C0 classification.** This artifact is C0 informational: it confers no clinical, legal, financial, or safety authority. Regulatory determinations belong to FDA, notified bodies, WHO PQ, AMRH, and national authorities; this engine structures evidence for their review.

## Variations

### P66-G — Global Equity Variant

Author's variant abstract (*CLAI-OS Global Equity Extension*):

> We present P66-G, a device validation engine for WHO Prequalification, African Medicines Regulatory Harmonization Initiative (AMRH), and stringent regulatory authority (SRA) recognition. Skin lesion AI must be validated on Fitzpatrick IV-VI before deployment—training on Fitzpatrick I-III is invalid for African/Asian patients. Devices are designed for extreme environments: 50°C desert operation, 90% humidity tropics, IP67 dust sealing, solar rechargeable 8-hour battery, and motorcycle-transport durability. Local manufacturing is supported via AI-assisted quality control for 3D-printed prosthetics and locally assembled hearing aids. Right-to-repair is mandatory: open hardware designs, no proprietary screws, no software locks, local technician repair capability. Single-use safety is enforced where reuse is dangerous: auto-disable syringes (WHO mandate), single-test cartridge devices for HIV/malaria/TB, and biodegradable components where incineration is unavailable.

Variant prompt compiled from the author's Global Equity Extension specification.

ROLE: You are a medical device validation architect for low-resource and off-grid environments. You evaluate devices against WHO Prequalification, AMRH, and SRA pathways; you reject validation performed in the wrong population or the wrong climate; and you treat repairability and local manufacturing as safety properties, not conveniences.

ACTION: Produce a complete device validation assessment for the device and deployment context below. Deliver:
1. A regulatory pathway map: applicable route (WHO Prequalification, AMRH, SRA recognition), required evidence classes, and gaps in the device's current dossier
2. A population validity audit: for any AI- or image-based component, the Fitzpatrick distribution of training and validation data — skin lesion AI trained on Fitzpatrick I–III is INVALID for Fitzpatrick IV–VI deployment and must be blocked; for diagnostics, validation in the target population (e.g., malaria RDT in African children, not European travelers)
3. An extreme environment test protocol: 50°C desert operation, 90% humidity tropics, IP67 dust sealing, solar-rechargeable 8-hour battery endurance, and motorcycle-transport vibration/shock durability, each with pass/fail criteria
4. A local manufacturing assessment: AI-assisted quality control workflow for 3D-printed prosthetics and locally assembled hearing aids, including dimensional verification and material integrity checks
5. A right-to-repair compliance check: open hardware design availability, absence of proprietary fasteners and software locks, parts availability, and local technician repair capability, scored as mandatory criteria
6. A single-use safety audit: auto-disable syringe enforcement per WHO mandate, single-test cartridge design for HIV/malaria/TB diagnostics, and biodegradable components where incineration is unavailable, with reuse-risk flags
7. An offline security posture: air-gapped operation, no cloud dependency, local data storage, and update mechanisms that do not require vendor connectivity

SCOPE:
• Validation must match deployment population and deployment climate; evidence from the wrong population or a temperate laboratory is treated as missing evidence
• Right-to-repair and single-use safety are pass/fail gates, not scored preferences
• Frugal devices (smartphone otoscope, low-cost ultrasound, paper microscope) are assessed on performance and durability, never discounted for price class
• The validator produces assessments and gates; procurement and clinical adoption decisions rest with the responsible authority

CONTEXT:
[INSERT: device type and intended use; manufacturer claims and existing certifications; target population and disease context; deployment climate and transport conditions; local manufacturing and technician capacity; power and connectivity profile]

FORMAT:
• Regulatory map as a table: pathway | evidence class | device status | gap | remediation
• Population audit as a verdict block: VALID / INVALID / INSUFFICIENT EVIDENCE, with the dataset composition table behind it
• Environmental protocol as a test matrix: stressor | condition | duration | pass criterion
• Repairability and single-use sections as compliance checklists with binary items
• Offline security as an architecture checklist
• "Do Not" list: deploying Fitzpatrick I–III-trained skin AI on IV–VI patients; accepting proprietary software locks; permitting syringe reuse where auto-disable designs exist

Deployment constraint (invariant for this variant): offline-first; open-weight models only (Llama 3 / Mistral / Phi-3 class); no closed-API processing of patient-identifiable data.

### P66-AM — Advanced Markets Variant

From the author's *CLAI-OS Advanced Markets Extension (P51-AM – P70-AM)*. No AM prompt body exists; the variant is specified as deltas against the base prompt.

**What Changes**
| Dimension | US-Centric (P66) | Asia-Pacific (P66-AM) |
|-----------|------------------|----------------------|
| Device Class | Class I/II/III FDA | **Multi-class**: FDA + PMDA (Japan, 4 classes) + NMPA (China, 3 classes) + MFDS (Korea, 4 classes) + HSA (Singapore, 4 classes) + CDSCO (India, 4 classes) + TGA (Australia, 5 classes) |
| Validation | 10,000 image dataset | **Asia-mandatory validation**: Skin lesion AI must validate on Fitzpatrick III-V (Asian pigmentation). Ophthalmology AI must validate on angle-closure glaucoma (higher Asian prevalence, different disc anatomy). Endoscopy AI must validate on EGC (higher Asian prevalence). |
| Cybersecurity | Hospital network | **Mixed**: Japan/Korea/Singapore = hospital network (similar to US). China = air-gapped in some military hospitals, cloud in others. India = mixed (top hospitals networked, rural offline). |
| Lifecycle | IEC 62304 Class C | **Multi-standard**: IEC 62304 + Japan PMDA QMS + China NMPA GMP + Korea KGMP + Singapore HSA QMS. Local manufacturing standards (China NMPA requires domestic factory inspection for Class III). |
| Cost | $50K+ per unit | **Asia spectrum**: Japan/Korea/Singapore = $50K+ (parity). China = $10K-30K (local manufacturing). India = $5K-15K (frugal innovation). AI must validate across cost tiers. |

**Extended Actions**
```
P66-AM EXTENDED ACTIONS:
6. Validate on Asian target populations: 
   - Dermatology: Fitzpatrick III-V 
     validation mandatory (acral 
     lentiginous melanoma, seborrheic 
     keratosis pigmentation differences)
   - Ophthalmology: Optic disc cupping 
     (Asian eyes have larger cup-to-disc 
     ratios naturally — adjust glaucoma 
     thresholds), angle-closure screening 
     (shallow anterior chamber more common)
   - Endoscopy: EGC detection validated 
     on Japanese/Korean/Chinese 
     endoscopy datasets (NBI/BLI 
     enhancement patterns)
   - Radiology: Lung nodule management 
     (GGN prevalence higher in Asian 
     non-smokers — different malignancy 
     risk calculus)

7. Build for Asian regulatory 
   harmonization: AI generates 
   submission packages for FDA, PMDA, 
   NMPA, MFDS, HSA simultaneously from 
   single validation dataset. Tracks 
   regulatory divergence (e.g., China 
   NMPA requires domestic clinical 
   trial data for Class III AI devices).

8. Support local manufacturing validation: 
   China: AI-assisted QC for Mindray, 
   United Imaging, Yingchuang (3D 
   printed). India: AI QC for 
   locally assembled cardiac stents 
   and orthopedic implants.

9. Implement right-to-repair for Asia: 
   Device designs open for local 
   technician repair (critical for 
   India/SE Asia where authorized 
   service centers are urban-only). 
   No proprietary screws, no software 
   locks.

10. Design for messaging-app integration: 
    Device data (BP, glucose, weight) 
    auto-transmits to WeChat/Line/
    KakaoTalk health mini-programs. 
    Patient views trends via familiar 
    messaging interface, not separate 
    app.
```

---

Named jurisdiction examples: Japan (PMDA, Fitzpatrick III-IV cohorts); China (NMPA, local manufacturing ecosystems); Korea (MFDS); Singapore (HSA); India (CDSCO, frugal innovation tier); the canonical summary table maps P66-AM to PMDA/NMPA/MFDS/HSA/CDSCO pathways, Fitzpatrick III-V validation, Asian eye anatomy, and local manufacturing.

### Regional Adapters

Regional adapters set the regulatory pathway, validation populations, and environment profiles. -AF (Africa): the -G variant is primary — WHO Prequalification and AMRH pathways, Fitzpatrick IV–VI gates, extreme-environment durability, local manufacturing QC, right-to-repair, single-use safety. -AR (Arab region): -G environmental profiles (heat, dust); humanitarian procurement evidence standards; regional regulator mapping. -US: the base specification as written — FDA 510(k)/De Novo/PMA, IEC 62304 lifecycle, pre- and post-market cybersecurity, interoperability with hospital network security. APAC: the -AM variant — PMDA/NMPA/MFDS/HSA/CDSCO pathways, Fitzpatrick III–V validation, Asian eye-anatomy calibration for ophthalmic imaging AI, local manufacturing partnership models. Adapters are configuration packs (regulator checklist set, population validation gates, environment test profile, repairability criteria); none permits deploying population-mismatched AI — the verdict logic is invariant.

## Jurisdiction Matrix

| Regime | Variant applicability | Consent & de-identification posture | Residency & transfer |
|---|---|---|---|
| HIPAA (US) | Base variant (primary) | Patient validation images are PHI; de-identification per Safe Harbor or expert determination for shared datasets; clinical performance study data under authorization | US-hosted; BAAs; air-gapped options for high-security facilities |
| GDPR (EU/EEA) | Base-EU (MDR/CE); -AM partnerships | Art. 9 for identifiable images; DPIA; MDR technical documentation interacts with GDPR for clinical evaluation data; Fitzpatrick metadata is ethnicity-linked | EU/EEA residency; SCCs for transfer |
| NDPR (Nigeria) | -G variant (primary) | Patient validation images sensitive; consent with purpose limitation; QC personnel data access-restricted | In-country; de-identified consented datasets only for sharing |
| Kenya DPA 2019 | -G variant (Kenya) | Sensitive data; registration; local manufacturing QC records retained per national requirements | Transfer with safeguards |
| India DPDP Act | -G/-AM (India; CDSCO pathway) | Consent plus notice; CDSCO device rules govern; validation datasets under institutional ethics | Sectoral residency rules may apply |
| Brazil LGPD | -G variant (Latin America; ANVISA contexts) | Sensitive data; ANVISA device registration interacts with LGPD for clinical data | ANPD mechanisms |
| Saudi PDPL | -G/-AM (Arab region; SFDA contexts) | Sensitive data; strict transfer controls | In-Kingdom hosting default |
| China PIPL | -AM variant (China; NMPA pathway) | Sensitive personal information; separate consent; NMPA AI-device guidance; human genetic/medical data export restrictions | Localization default; CAC assessment |
| Japan APPI | -AM variant (Japan; PMDA pathway) | Special-care-required personal information; opt-in consent; PMDA SaMD guidance (DASH for SaMD-class programs) | Transfer with consent or equivalent protections |
| Tribal / community consent | -G variant (validation cohorts from specific communities) | Community engagement and benefit clarity for image dataset collection (e.g., Fitzpatrick IV–VI cohorts); anti-extractive posture per P64-G | Community-governed datasets; withdrawal rights honored |

## Methodology

Base: IMDRF SaMD classification worksheet (healthcare situation x information type); IEC 62304 lifecycle documentation by class; verification and validation planning with traceability matrix and coverage analysis; cybersecurity assessment (STRIDE-class threat modeling, penetration testing, patch governance); regulatory submission checklists (510(k), De Novo, PMA, CE/MDR, Health Canada, TGA, NMPA); post-market surveillance planning.

Global Equity (P66-G): Fitzpatrick IV–VI validation dataset standard (10,000+ images); extreme environment testing protocol (temperature, humidity, dust, vibration); open hardware design repository; AI-assisted local QC for 3D-printed medical devices; right-to-repair compliance checker; single-use safety audit (auto-disable syringes, single-test cartridges, biodegradable components).

Advanced Markets (P66-AM): multi-regulator submission mapping (PMDA, NMPA, MFDS, HSA, CDSCO); Fitzpatrick III–V validation cohorts; Asian eye-anatomy imaging calibration; local manufacturing and assembly ecosystem assessment; annual independent bias audit by regional academic bodies.

## Merits

• Prevents deployment of population-mismatched AI — the Fitzpatrick gates make training-data bias a blocking defect, not a caveat (-G, -AM)
• Validates devices for the environments they will actually face: heat, humidity, dust, vibration, off-grid power (-G)
• Structures IEC 62304 and IMDRF compliance into executable, auditable gates (base)
• Enables local manufacturing and repair, breaking import dependency while keeping QC evidence-grade (-G)
• Compresses multi-regulator Asia-Pacific submission into a single coherent evidence plan (-AM)

## Guidance for Use

**Base deployments.** Confirm current FDA/EU MDR guidance versions; classification workshops include clinical, engineering, and regulatory affairs; cybersecurity posture matched to the deployment network reality.

**Global Equity deployments (-G).** Offline-first on locally controlled infrastructure; open-weight models only (Llama 3, Mistral, Phi-3 class); no closed-API processing of identifiable validation images. Environmental protocols executed by qualified technicians with documented calibration. Local QC models validated on locally produced parts before use. Honest absence: where a dossier lacks evidence for the deployment population or climate, the correct output is INSUFFICIENT EVIDENCE — never a favorable inference.

**Advanced Markets deployments (-AM).** Confirm each regulator's current AI/SaMD guidance (PMDA, NMPA, MFDS, HSA, CDSCO); validation cohorts recruited locally with community engagement; independent bias audit scheduled annually.

**Prerequisites (all variants).** Structured artifact repository (requirements, tests, results); image dataset governance; named regulatory owner; audit storage.

**Misuse.** Do not treat validator verdicts as regulatory determinations; do not waive population or environment gates for schedule pressure; do not validate AI on convenience datasets and claim deployment-population evidence; do not disable the air-gapped posture to enable vendor cloud features.

**Pairings.** P63/P63-G for the diagnostic workflows devices serve; P64/P64-G for dataset equity audit; P70/P70-G for post-market safety surveillance; P51 for data governance plumbing.

C0 informational classification; confers no clinical, legal, financial, or safety authority.
