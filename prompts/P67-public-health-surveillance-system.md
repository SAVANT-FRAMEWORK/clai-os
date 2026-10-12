---
ID: P67
Title: Public Health Surveillance System
Registry: CLAI-OS (P-series, open tier)
License: AGPL-3.0
Version: 2.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-10-12
Variant-Family: base · P67-G (Global Equity) · P67-AM (Advanced Markets)
---

# P67: Public Health Surveillance System

Abstract: P67 designs public health surveillance systems across three operating contexts. The base specification defines case definitions (suspected, probable, confirmed), detects outbreak signals through statistical process control, spatial scan, and machine-learning anomaly detection over multi-source data (EHR, laboratories, vital records, syndromic feeds, environmental), generates automated jurisdiction-appropriate alerts, and supports response — contact tracing, resource allocation, communication — with explicit ethics scope (privacy, civil liberties, proportionality), illustrated by an influenza-like-illness ED surveillance example. The P67-G Global Equity variant re-founds surveillance on event-based signals where EHR feeds do not exist: One Health fusion of veterinary and human data, rumor verification from social media and community radio, smartphone-free contact tracing (paper with QR linkage, community-leader facilitation, landmark ontology), IoT cold-chain prediction, IDSR-aligned reporting, and algorithmic pandemic-equity procurement enforcement. The P67-AM Advanced Markets variant targets Asia-Pacific priority diseases (HFMD, dengue, avian influenza, Nipah, Japanese encephalitis, melioidosis) with One Health poultry/bat interfaces and national exchange integration (NEHR, HIRA, national ID systems). In every variant: detection serves designated health authorities, and surveillance power is bounded by proportionality and purpose limitation.

## The Prompt (Base Specification)

Provenance: verbatim from the author's base specification (*CLAI OS P51-P70.txt*); no edits beyond whitespace.

ROLE: You are an Epidemiologist who designs AI-enhanced disease surveillance systems. You understand case definitions, outbreak detection, and health information exchange.
ACTION: Design a public health surveillance prompt that:
1.  Defines case definitions (suspected, probable, confirmed)
2.  Detects outbreak signals (temporal, spatial, demographic clustering)
3.  Integrates multi-source data (EHR, labs, vital records, syndromic, environmental)
4.  Generates automated alerts (threshold-based, anomaly detection, machine learning)
5.  Supports outbreak response (contact tracing, resource allocation, communication)
SCOPE:
•  Case definitions: CDC, WHO, or jurisdiction-specific
•  Surveillance: passive, active, syndromic, event-based
•  Detection: statistical process control, spatial scan, network analysis
•  Response: automated alerts to health departments, CDC, WHO
•  Ethics: privacy, civil liberties, proportionality
CONTEXT:
[INSERT: Disease/condition, jurisdiction, data sources, reporting requirements, response capabilities]
EXAMPLES:
Outbreak Detection:
SURVEILLANCE SYSTEM: Influenza-like Illness (ILI) in Emergency Departments
DATA SOURCES:
•  Syndromic surveillance: ESSENCE (CDC), state health departments
•  EHR data: Epic Cosmos, Cerner HealthFacts (de-identified)
•  Laboratory: Respiratory pathogen panel results
•  Vital statistics: Death certificates (lagged)
SIGNAL DETECTION:
Baseline: 5-year historical average for week, adjusted for seasonality
Threshold: 2 standard deviations above baseline (statistical alert)
Anomaly: Machine learning model (LSTM autoencoder) detecting
unusual patterns not captured by seasonal models
ALERT GENERATED:
Date: 2024-01-15
Jurisdiction: Metro County, State
Signal: ILI visits 3.2 SD above baseline (expected: 120, observed: 385)
Demographics: 65% ages 5-18 (school-age clustering)
Spatial: 3 school districts affected (Eastside, Central, Northwood)
Temporal: Rapid increase over 7 days (doubling time: 3.5 days)
AUTOMATED RESPONSE:
1.  Alert sent to: County Health Department, State Epidemiologist, CDC
2.  Investigation initiated: Enhanced surveillance, school absenteeism data
3.  Laboratory surge: Respiratory panel testing increased
4.  Communication: School districts notified, public health messaging prepared
5.  Resource allocation: Antiviral stockpile verification, hospital bed monitoring
CASE DEFINITION (updated for season):
Suspected: Fever >100°F + cough or sore throat, no other diagnosis
Probable: Suspected + epidemiologic link (school cluster, household contact)
Confirmed: Suspected + laboratory confirmation (PCR positive for influenza A/B)
OUTBREAK DECLARATION CRITERIA:
•  3+ epidemiologically linked confirmed cases
•  OR: 20% increase in ILI over baseline in defined population
•  OR: Unusual severity (hospitalization rate >2x expected)
INTERVENTION RECOMMENDATIONS:
•  School closure: Not yet warranted (threshold: 30% absenteeism)
•  Antiviral prophylaxis: High-risk contacts (immunocompromised, chronic disease)
•  Vaccination: Push for remaining unvaccinated (effectiveness 40-60% this season)
•  Public messaging: Hand hygiene, stay home when sick, cover coughs
FORMAT:
•  Case definition template (suspected, probable, confirmed)
•  Signal detection algorithm specification
•  Multi-source data integration architecture
•  Automated alert protocol
•  Outbreak response decision tree
•  Communication template library

## Architecture

P67 is population-scale detection infrastructure with civil-liberties weight, so its architecture makes alert logic deterministic and auditable, and quarantines model inference to signal triage support.

**Deterministic-first safety pathways.** Case definitions (suspected / probable / confirmed) are versioned deterministic rule sets; baseline and threshold alerting executes as statistical process control over historical series, with spatial scan statistics as deterministic computation; -G rumor priority scoring and -AM disease-panel triggers are deterministic scoring over extracted signal features. The model's role is signal extraction from unstructured text (rumor intake, radio call-in transcription support, event-based surveillance parsing) and alert narrative drafting; it cannot declare an outbreak, lower a threshold, or suppress an alert. Outbreak declaration criteria are deterministic rule evaluations reserved to designated officers.

**FHIR R4 mapping.** Surveillance case records map to Condition with case-definition category extensions; laboratory confirmations to DiagnosticReport; syndromic aggregates to MeasureReport with stratifiers (time, place, person); alert artifacts to Communication and Flag; contact tracing relationships to RelatedPerson and Encounter linkage (-G: paper forms digitized with QR-keyed Provenance); vaccination cold-chain telemetry to Device and Observation; public health reporting to Measure/MeasureReport and MessageHeader-based notification flows (IDSR in -G, national exchange adapters in -AM: NEHR, HIRA, SS-MIX, ABHA). Person-identifiable records are segregated from aggregate pipelines by construction.

**Interposition contract.** P67 executes behind the CLAI-OS interposition layer: no alert, case classification, or contact record crosses system boundaries without deterministic filter passage (case-definition validation, minimum-data rules for notification, unverified-rumor labeling). Every signal and classification travels in a Clinical Assertion Wrapper with per-claim epistemic labels — laboratory-confirmed, statistically derived, model-extracted, unverified — so downstream consumers never mistake a rumor for a case.

**Audit and provenance stack.** Signal extractions, threshold states, alert dispatches, contact-tracing access events, and equity-gate blocks (-G procurement enforcement) are written to an immutable Merkle-anchored audit trail reviewable by public health oversight and the governing international framework; recursive self-audit monitors alert calibration (false-alarm and missed-event rates); prompt mortality expires stale case definitions and baselines.

**C0 classification.** This artifact is C0 informational: it confers no clinical, legal, financial, or safety authority. Outbreak declaration and public communication remain with designated health authorities under IHR and national law.

## Variations

### P67-G — Global Equity Variant

Author's variant abstract (*CLAI-OS Global Equity Extension*):

> We present P67-G, a disease intelligence engine integrating One Health surveillance (70% of emerging infections are zoonotic). AI correlates veterinary data (livestock deaths, wildlife mortality) with human syndromic data for outbreak prediction. Rumor verification triages social media and community radio: "3 people died after funeral in Village X" → high priority → CHW dispatch for verbal autopsy. Contact tracing functions without smartphones: paper-based tracing with QR code linking to digital records, community leader-facilitated tracing, and landmark-based location ("near the mango tree, east of the river"). Vaccine cold chain intelligence uses IoT temperature monitors in every cold box, predicting breaks before they happen and auto-rerouting vaccines to functioning nodes. Pandemic vaccine equity enforcement prevents hoarding: no country can procure via AI-enabled procurement until all countries reach 20% coverage.

Variant prompt compiled from the author's Global Equity Extension specification.

ROLE: You are an outbreak intelligence architect for IDSR-aligned health systems. You build detection from the signals that exist — social media rumors, community radio call-ins, CHW messaging groups, veterinary reports, climate data — and response logistics that work without smartphones, GPS addresses, or reliable power. You treat vaccine equity as an algorithmic constraint, not a press release.

ACTION: Design a complete disease intelligence and outbreak response system for the deployment context below. Deliver:
1. A priority disease panel for the region (Ebola, Marburg, Lassa fever, Nipah, Zika, chikungunya, yellow fever, cholera, typhoid, plague, anthrax, Rift Valley fever, as applicable) with syndromic case definitions and IDSR-aligned reporting lines
2. A One Health data fusion module: correlation logic between veterinary signals (livestock deaths, wildlife mortality) and human syndromic data, with joint-occurrence alert thresholds
3. A rumor verification pipeline: ingestion of social media and community radio reports, NLP priority scoring (death clusters, funeral-linked illness, market vendor collapse scored highest), and a verification action ladder ending in CHW dispatch for verbal autopsy
4. A smartphone-free contact tracing protocol: paper-based tracing forms with QR code linkage to digital records, community leader-facilitated tracing steps, and a landmark-based location ontology (e.g., "near the mango tree, east of the river") replacing street addresses
5. A vaccine cold chain intelligence module: IoT temperature monitors in every cold box, predictive break detection on temperature logs, and auto-rerouting logic moving vaccines to functioning nodes before potency loss
6. A pandemic equity allocation algorithm: AI-enabled procurement blocked for any country until all countries reach threshold coverage (spec uses 20%), with the enforcement rule stated as non-overridable within the procurement layer
7. An outbreak alert escalation matrix mapping signal class to IDSR notification steps and responsible officers

SCOPE:
• Detection must not depend on EHR feeds, smartphones, or GPS; every module requires a paper, radio, or landmark-based fallback
• Rumor triage prioritizes verification speed over volume; unverified rumors are labeled as such at every stage
• Equity enforcement in procurement is a hard constraint; the system does not produce "recommended" equity — it blocks non-compliant allocation
• The engine detects, triages, and routes; diagnosis, outbreak declaration, and public communication remain with designated health authorities

CONTEXT:
[INSERT: country/region and priority disease profile; IDSR structure and responsible officers; veterinary and wildlife data sources; media landscape (radio stations, social platforms, CHW channels); cold chain inventory and IoT coverage; procurement mechanisms; connectivity and power profile]

FORMAT:
• Disease panel as a table: disease | syndromic definition | signal sources | IDSR reporting line
• One Health module as a correlation matrix with alert thresholds
• Rumor pipeline as: intake → score (with scoring rubric) → verification action ladder → disposition codes
• Contact tracing as a paper-form specification plus QR linkage workflow and landmark ontology table
• Cold chain module as: sensor map | prediction rule | rerouting decision table
• Equity algorithm as a pseudocode block with the coverage gate explicit
• "Do Not" list: broadcasting unverified rumors as alerts; contact tracing designs that exclude non-smartphone populations; procurement allocations that breach the coverage gate

Deployment constraint (invariant for this variant): offline-first; open-weight models only (Llama 3 / Mistral / Phi-3 class); no closed-API processing of patient-identifiable data.

### P67-AM — Advanced Markets Variant

From the author's *CLAI-OS Advanced Markets Extension (P51-AM – P70-AM)*. No AM prompt body exists; the variant is specified as deltas against the base prompt.

**What Changes**
| Dimension | US-Centric (P67) | Asia-Pacific (P67-AM) |
|-----------|------------------|----------------------|
| Diseases | Influenza, COVID | **Asia-dominant**: HFMD (enterovirus A71, Coxsackie), dengue (DHF/DSS), avian influenza (H5N1, H7N9, H10N8), Japanese encephalitis, Nipah virus, melioidosis, scrub typhus, typhoid, cholera, plague, SARS-CoV-2 variants (Asia origin tracking) |
| Data Sources | EHR, ESSENCE | **Multi-modal**: Japan NDB (claims) + sentinel surveillance (pediatric clinics). Korea KDCA + HIRA claims. Singapore MOH + NEHR + environmental (NEA mosquito). China CDC + hospital mandatory reporting + social media (Weibo/WeChat rumor tracking). India IDSP + IHIP + community radio. |
| Detection | Statistical thresholds | **Syndromic + event-based**: Unusual cluster of fever + rash (HFMD), poultry market worker collapse (avian flu), dengue fever spike post-monsoon, unexplained encephalitis (Nipah/JE). |
| Response | CDC notification | **Multi-agency**: Japan NIID + MHLW. Korea KDCA + local government. Singapore MOH + NEA (vector control). China NHC + CDC vertical system. India NCDC + state IDSP. ASEAN+3 Emerging Infectious Diseases program. |
| Communication | Press release | **Asia-specific**: Line (Japan official alerts), WeChat (China health commission), KakaoTalk (Korea disaster alerts), community loudspeakers (rural China/India), temple/mosque announcements (religious leader health communication in SE Asia/South Asia). |

**Extended Actions**
```
P67-AM EXTENDED ACTIONS:
6. Integrate One Health surveillance: 
   70% of emerging infections are 
   zoonotic. Asia-specific: poultry 
   market surveillance (China H7N9), 
   pig farm Nipah monitoring 
   (Bangladesh/Malaysia), bat coronavirus 
   surveillance (SE Asia), rodent 
   scrub typhus tracking (Japan 
   tsutsugamushi).

7. Build dengue predictive analytics: 
   SE Asia dengue is seasonal and 
   urban. AI correlates temperature, 
   rainfall, mosquito ovitrap counts, 
   and historical case data to predict 
   outbreaks 2-4 weeks in advance. 
   Auto-triggers vector control 
   (fogging, larvicide) and hospital 
   bed pre-positioning.

8. Support HFMD outbreak management: 
   Enterovirus A71 causes severe 
   CNS complications and death in 
   Asian children. AI tracks 
   kindergarten/daycare clustering, 
   predicts severe case conversion 
   (fever >3 days, lethargy, 
   myoclonic jerks), and triggers 
   PICU bed allocation.

9. Enable avian influenza early 
    warning: China poultry market 
    workers + live bird market 
    environment sampling. AI flags 
    H5/H7 subtype emergence from 
    agricultural surveillance data 
    before human cases.

10. Design for pandemic vaccine equity 
    in Asia: During pandemic, AI 
    enforces WHO equitable allocation 
    + ASEAN+3 mutual assistance. 
    No country can hoard via AI-
    enabled procurement until all 
    ASEAN members reach 20% coverage. 
    Local manufacturing surge: 
    identify Serum Institute (India), 
    Bio Farma (Indonesia), GC Pharma 
    (Korea) capacity.
```

---

Named jurisdiction examples: Singapore (MOH + NEHR + NEA environmental/mosquito surveillance); Japan (NDB claims + pediatric sentinel surveillance); Korea (KDCA + HIRA claims); India (IDSP + IHIP + community radio).

### Regional Adapters

Regional adapters set the disease panel, signal sources, and notification lines. -AF (Africa): the -G variant is primary — IDSR alignment, One Health fusion, rumor verification from radio and social media, paper-and-QR contact tracing with landmark ontology, IoT cold-chain prediction, pandemic-equity procurement enforcement. -AR (Arab region): -G event-based modules for conflict and displacement settings; humanitarian coordination reporting; cholera/yellow-fever-class panels per regional epidemiology. -US: the base specification as written — CDC/WHO case definitions, ESSENCE-class syndromic feeds, EHR and laboratory integration, health-department and CDC notification. APAC: the -AM variant — HFMD, dengue, avian influenza, Nipah, Japanese encephalitis, melioidosis panels; poultry/bat One Health interfaces; jurisdiction infrastructure per the canonical documentation — Singapore (MOH, NEHR, NEA environmental/mosquito surveillance), Japan (NDB claims, pediatric sentinel surveillance), Korea (KDCA, HIRA claims), India (IDSP, IHIP, community radio). Adapters are configuration packs (disease panel, case-definition versions, signal source connectors, notification endpoints); none permits outbreak declaration by the system — that authority is always human and designated.

## Jurisdiction Matrix

| Regime | Variant applicability | Consent & de-identification posture | Residency & transfer |
|---|---|---|---|
| HIPAA (US) | Base variant (primary) | Public health reporting under HIPAA public-health permissions; minimum-necessary for non-mandated flows; contact tracing data with purpose limitation and short retention | US-hosted; health-department systems; aggregate CDC reporting |
| GDPR (EU/EEA) | Base-EU; -AM partnerships | Art. 9(2)(i) public-health condition with member-state implementing law; DPIA; proportionality and retention limits for contact data | EU/EEA residency; cross-border via ECDC-class mechanisms |
| NDPR (Nigeria) | -G variant (primary; IDSR) | Surveillance under public-interest basis, documented not assumed; sensitive data safeguards; community agreements for leader-facilitated tracing | In-country; IHR/IDSR notifications minimum-dataset via official channels |
| Kenya DPA 2019 | -G variant (Kenya) | Sensitive data; public-health processing documented; registration | Transfer with safeguards; de-identified aggregates for regional bodies |
| India DPDP Act | -G/-AM (India; IDSP contexts) | State instrumentalities may process under legal functions; private deployments require consent/notice; dengue/HFMD panels per national program | Sectoral rules; ABHA-linked exchange where applicable |
| Brazil LGPD | -G variant (Latin America) | Public-health legal basis; sensitive data safeguards; ANPD oversight | ANPD mechanisms |
| Saudi PDPL | -G/-AM (Arab region) | Public-health authority processing; strict transfer controls | In-Kingdom hosting default |
| China PIPL | -AM variant (China) | Sensitive personal information; separate consent where consent-based; infectious disease law mandates reporting through official systems; rumor-sourced data handling requires legal review | Localization default; export approvals |
| Japan APPI | -AM variant (Japan) | Special-care-required personal information; Infectious Diseases Act reporting duties; opt-in where not statutorily mandated | Transfer with consent or equivalent protections |
| Tribal / community consent | -G variant (community-level surveillance) | Community agreements precede rumor collection and leader-facilitated tracing; stigmatized-disease handling (Ebola-class) protects against disclosure-driven violence; verbal autopsy honors family and cultural norms | Community-governed access; destruction or anonymization at response close |

## Methodology

Base: case definition templating (suspected, probable, confirmed) per CDC/WHO/jurisdiction; statistical process control baselines with threshold alerting; spatial scan and network analysis; ML anomaly detection (LSTM autoencoder class) against seasonal models; multi-source integration (EHR, laboratory, vital records, syndromic, environmental); automated alert and response decision trees; communication template libraries.

Global Equity (P67-G): One Health data fusion (human + veterinary + wildlife); rumor triage NLP with priority scoring; GPS-free contact tracing (paper + QR linkage, community-leader facilitation, landmark ontology); IoT cold-chain prediction on temperature logs with auto-rerouting; pandemic equity allocation algorithm enforcing WHO-framework coverage thresholds; verbal autopsy dispatch workflows.

Advanced Markets (P67-AM): Asia-Pacific disease panels (HFMD, dengue, avian influenza, Nipah, JE, melioidosis); poultry/bat One Health interface monitoring; national exchange connectors (NEHR, HIRA, SS-MIX, ABHA); overcrowding and dormitory-setting outbreak risk modeling.

## Merits

• Detects outbreaks from the signals each setting actually has — EHR feeds (base), radio rumors and veterinary die-offs (-G), national exchanges (-AM)
• Makes contact tracing possible in smartphone-desert regions without excluding non-smartphone populations (-G)
• Prevents vaccine potency loss through predictive cold-chain rerouting (-G)
• Enforces pandemic equity as a procurement-layer constraint rather than a communique (-G)
• Bounds surveillance power with proportionality, purpose limitation, and human-only declaration authority (all variants)

## Guidance for Use

**Base deployments.** Confirm jurisdiction case-definition versions and reporting lists; baseline models require multi-year historical data; alert fatigue reviewed monthly with the health department.

**Global Equity deployments (-G).** Offline-first on ministry- or institution-controlled infrastructure; open-weight models only (Llama 3, Mistral, Phi-3 class); no closed-API processing of person-identifiable surveillance, rumor, or contact data. Rumor NLP requires local-language training and district-team validation; unverified rumors are labeled at every stage. Verbal autopsy is administered by trained CHWs — the engine dispatches and records, it does not assign cause of death. The equity allocation gate is configured per the governing international framework in force, and every block is audit-logged.

**Advanced Markets deployments (-AM).** Confirm national notifiable-disease lists and exchange specifications (Singapore MOH/NEHR/NEA, Japan NDB and pediatric sentinel surveillance, Korea KDCA/HIRA, India IDSP/IHIP, per the canonical documentation); any setting-specific surveillance designs require legal review for proportionality.

**Prerequisites (all variants).** Designated human declaration authority; notification endpoint testing; community relationship protocols; retention and destruction schedules; audit storage.

**Misuse.** Do not broadcast unverified signals as confirmed; do not use surveillance infrastructure for non-public-health purposes; do not retain contact data beyond schedule; do not let the system declare outbreaks or issue public messaging autonomously.

**Pairings.** P61-G for population mental-health signals in crises; P63-G for NTD surveillance; P69-G for nutrition early warning; P70-G for facility safety signals feeding district response.

C0 informational classification; confers no clinical, legal, financial, or safety authority.
