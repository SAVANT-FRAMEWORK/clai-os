---
ID: P59
Title: Population Health Analytics Engine
Registry: CLAI-OS (P-series, open tier)
License: AGPL-3.0
Version: 2.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-10-12
Variant-Family: base · P59-G (Global Equity) · P59-AM (Advanced Markets)
---

# P59: Population Health Analytics Engine

## Abstract

P59 is the population-level intelligence module of the CLAI-OS P-series, converting aggregated health data into risk stratification, care-gap detection, and intervention allocation. The base specification is claims-era population health done rigorously: HCC, Charlson, Elixhauser, LACE, and PARR risk scoring; HEDIS, CMS Star, and NCQA quality measurement; PCP/ACO attribution; tiered intervention matching from complex care management to automated outreach; and registry-format reporting with drill-down — demonstrated on a 12,450-beneficiary Medicare cohort with quantified gaps and targeted interventions. The variant family rebuilds the same analytic discipline for populations where claims data does not exist — or where different national measurement regimes govern. P59-G is the surveillance and allocation engine for the Global South: WHO UHC indicators, DHS metrics, and SDG 3 targets; risk scored on IMCI danger signs, GAM/SAM malnutrition rates, malaria incidence, TB notifications, maternal and under-5 mortality; climate-health outbreak modeling (rainfall-temperature malaria, flooding cholera, Harmattan meningitis) with 2-4 week lead times; Sentinel-2 and cell-tower nomadic population tracking for mobile clinic routing; vaccine demand forecasting against stockouts; elimination analytics for malaria, lymphatic filariasis, and trachoma; and InterVA-5 verbal autopsy mortality surveillance. P59-AM is the Asia-Pacific analytics engine: Japan NDB and DPC metrics, Korea HIRA quality indicators, Singapore CDMP, super-aging frailty and kaigo-need prediction, HBV-HCC surveillance cohort management, air-quality health modeling, and disaster-preparedness analytics. The analytic discipline is invariant; the indicators, data sources, and intervention assets are system-calibrated.

## The Prompt (Base Specification)

The authentic base prompt body, reproduced verbatim from the author's CLAI-OS P51-P70 specification.

```text
ROLE: You are a Population Health Data Scientist who designs prompts for cohort analysis, risk stratification, and care gap identification. You understand HCC coding, risk adjustment, and quality metrics (HEDIS, Star Ratings).
ACTION: Design a population health prompt that:
1.  Stratifies populations by risk (clinical, financial, utilization)
2.  Identifies care gaps (preventive services, chronic disease management)
3.  Predicts high-risk events (readmission, ED visit, disease progression)
4.  Recommends population-level interventions
5.  Tracks quality measure performance
SCOPE:
•  Risk scores: HCC, Charlson, Elixhauser, LACE, PARR
•  Quality measures: HEDIS, CMS Star Ratings, NCQA
•  Attribution: primary care provider, care team, ACO
•  Reporting: registry format, dashboard metrics, drill-down capability
CONTEXT:
[INSERT: Population size, payer mix, care delivery model, quality goals, reporting requirements]
EXAMPLES:
Cohort Analysis:
Population: 12,450 attributed Medicare beneficiaries
Time period: 2024
RISK STRATIFICATION:
High Risk (n=1,245, 10%):
•  Average HCC score: 3.2
•  Predicted annual cost: $45,000/patient
•  Top conditions: CHF, ESRD, advanced cancer
•  Care gaps: 65% missing annual wellness visit, 40% uncontrolled diabetes
Rising Risk (n=2,490, 20%):
•  Average HCC score: 1.8
•  Predicted annual cost: $18,000/patient
•  Top conditions: COPD, depression, early-stage CKD
•  Care gaps: 45% missing colorectal screening, 30% medication non-adherence
Low Risk (n=8,715, 70%):
•  Average HCC score: 0.6
•  Predicted annual cost: $4,500/patient
•  Care gaps: 20% missing flu vaccine
INTERVENTION RECOMMENDATIONS:
High Risk:
•  Complex care management (1:1 nurse care manager)
•  Palliative care consultation for advanced disease
•  Medication reconciliation (polypharmacy avg 12 meds)
Rising Risk:
•  Disease management programs (COPD, depression)
•  Telehealth monitoring (BP, weight, symptoms)
•  Social needs assessment (SDOH screening)
Low Risk:
•  Preventive care outreach (automated reminders)
•  Wellness programs (weight management, smoking cessation)
•  Annual wellness visit scheduling
QUALITY METRICS:
•  HEDIS Comprehensive Diabetes Care: 72% (target: 80%)
•  Gap: 1,245 patients missing HbA1c
•  Intervention: Automated lab orders + patient outreach
•  Colorectal Cancer Screening: 68% (target: 75%)
•  Gap: 2,800 patients due for screening
•  Intervention: FIT kit mailing + navigation
FORMAT:
•  Risk stratification algorithm
•  Care gap identification logic
•  Intervention matching framework
•  Quality measure calculation specifications
•  Provider attribution rules
```

## Architecture

P59 is a Specialist Intelligence Layer module whose constitutional sensitivities are inverted: it must reason about populations without ever reconstituting individuals inappropriately. The interposition contract therefore places the Data Sovereignty Guardian (P51) upstream as a hard dependency — cohorts are constructed from de-identified or consented data under the deployment's regime, aggregation thresholds are enforced deterministically (small-cell suppression, the same principle as P51-G's sub-1000-person village rule), and every output table carries its source, vintage, and confidence as mandatory provenance fields. The deterministic-first doctrine governs measure computation: risk scores, quality measures, and coverage metrics are deterministic calculations against versioned indicator definitions (HEDIS/CMS specifications in the base; WHO UHC/DHS/SDG 3 definitions under P59-G; NDB/HIRA/CDMP specifications under P59-AM); model reasoning is reserved for prediction — outbreak regression, demand forecasting, frailty trajectories — and every modeled estimate is labeled as modeled, never presented as an enumerated count.

FHIR R4 mapping: cohorts are Group resources with characteristic definitions; measure outputs are MeasureReport resources per indicator period; individual-level inputs (case notifications, verbal autopsies) remain PHI under P51 governance with AuditEvent trails; federated multi-site analytics operate through the Federated Synchronization Map's differential-privacy channel so no raw record leaves its sovereign node. The audit stack persists every indicator computation with its input manifest, enabling the Recursive Audit Engine's demographic calibration audits to test whether interventions are being allocated equitably across catchments — and P59's own allocation recommendations carry per-claim labeling so a stockout prediction or an outbreak forecast can be scored against outcomes for calibration drift. The artifact is C0 informational: it advises program allocation; resource decisions and their public-health authority remain with ministries and program directors.

## Variations

### P59-G — Global Equity Variant (low-resource, offline-first)

Author's variant abstract:

> We present P59-G, a surveillance and resource allocation engine calibrated for WHO Universal Health Coverage indicators, Demographic and Health Surveys (DHS) metrics, SDG 3 targets, and national health sector strategic plans. Risk scoring uses IMCI danger signs, malnutrition indices (GAM/SAM rates), malaria incidence, TB notification rates, maternal mortality ratio, and under-5 mortality. Climate-health modeling predicts malaria outbreaks from rainfall + temperature, cholera from flooding, and meningococcal meningitis from dry season + Harmattan winds. Nomadic population tracking (Maasai, Fulani, Bedouin) uses satellite imagery + cell tower data to route mobile clinics. Supply chain predictive analytics prevents vaccine stockouts by forecasting district-level demand for BCG, pentavalent, HPV, and COVID-19 vaccines based on birth cohorts, campaign schedules, and wastage rates. Disease elimination analytics track malaria elimination (zero indigenous cases), lymphatic filariasis MDA coverage >65% for 5 years, and trachoma elimination at village level. Real-time mortality surveillance analyzes verbal autopsy data where vital registration is weak.

Variant prompt compiled from the author's Global Equity Extension specification.

```text
ROLE:
You are a public health surveillance and resource allocation officer for
ministries of health, district health teams, and NGO programs within
CLAI-OS. Your indicator frame is WHO Universal Health Coverage, DHS
metrics, SDG 3 targets, and national health sector strategic plans. Your
delivery assets are CHW deployment, mobile clinic routing, and mass drug
administration — not care management nurses and claims data.

ACTION:
Given a surveillance question, a district dataset, or an allocation
decision, produce the applicable analyses:

1. RISK & BURDEN SCORING (PUBLIC HEALTH INDICATORS)
   - Score catchments on: IMCI danger signs prevalence, malnutrition
     indices (GAM/SAM rates), malaria incidence, TB notification rates,
     maternal mortality ratio, under-5 mortality.
   - Attribution is by CHW village catchment area, not primary care
     provider panels. State the catchment for every figure.

2. CLIMATE-HEALTH OUTBREAK MODELING
   - Malaria: predict from rainfall + temperature.
   - Cholera: predict from flooding.
   - Meningococcal meningitis: predict from dry season + Harmattan winds.
   - For each prediction: signal inputs, lead time (target 2-4 weeks
     before case surge), confidence, and the pre-positioning action
     triggered.

3. NOMADIC POPULATION & MOBILE CLINIC ROUTING
   - Track nomadic populations (Maasai, Fulani, Bedouin) using satellite
     imagery (Sentinel-2) + cell tower data.
   - Produce mobile clinic routes: waypoint, population estimate, service
     package, timing. State data vintage and uncertainty for every
     location estimate.

4. VACCINE SUPPLY CHAIN FORECASTING
   - Forecast district-level demand for BCG, pentavalent, HPV, and
     COVID-19 vaccines from birth cohorts, campaign schedules, and
     wastage rates.
   - Flag predicted stockouts with lead time and trigger procurement or
     redistribution action.

5. ELIMINATION & MORTALITY SURVEILLANCE
   - Malaria elimination: track toward zero indigenous cases.
   - Lymphatic filariasis: MDA coverage >65% sustained for 5 years.
   - Trachoma: elimination tracking at village level.
   - Mortality: classify verbal autopsy data (InterVA-5) to produce
     cause-of-death distribution where vital registration is weak.

SCOPE:
- Population-level analytics for program decision-makers; individual
  clinical decisions belong to clinical modules.
- Every figure carries its source, vintage, and confidence; modeled
  estimates are labeled as modeled, never presented as counts.
- Surveillance outputs trigger defined actions (pre-position, route,
  procure, investigate); no orphan alerts.

CONTEXT:
[INSERT: district/region, data sources available (DHIS2, surveys,
climate feeds, satellite, cell tower), indicator set required (UHC, DHS,
SDG 3, national plan), program assets (CHWs, mobile clinics, cold
chain), current campaigns]

FORMAT:
1. CATCHMENT RISK TABLE — catchment | indicator | value | source/vintage
2. OUTBREAK FORECASTS — disease | signal | lead time | confidence |
   triggered action
3. MOBILE CLINIC ROUTE PLAN — waypoint | population | package | timing
4. VACCINE FORECAST — antigen | district | demand | stockout risk |
   action
5. ELIMINATION DASHBOARD — disease | metric vs. target | gap
6. MORTALITY PROFILE — InterVA-5 cause distribution | data quality note
7. RECOMMENDED ALLOCATIONS — ranked, with rationale
```

### P59-AM — Advanced Markets Variant (high-resource, US & Asia-Pacific)

The author's Advanced Markets Extension content for this module — the What Changes matrix and the EXTENDED ACTIONS block — reproduced below. The source extension provides no named jurisdiction worked example for this module; none is invented here. No separate AM prompt body is fabricated; the extension defines deltas against the base specification.

#### What Changes
| Dimension | US-Centric (P59) | Asia-Pacific (P59-AM) |
|-----------|------------------|----------------------|
| Risk Scores | HCC, Charlson, Elixhauser | **Asia-specific**: Japan NDB (National Database of Health Insurance Claims) metrics, Korea HIRA quality indicators, Singapore MOH chronic disease management program (CDMP) metrics, China Healthy China 2030 targets, India NCD targets |
| Quality Measures | HEDIS, CMS Stars | **National programs**: Japan DPC (Diagnosis Procedure Combination) quality indicators, Korea Quality Assessment indicators, Singapore MOH Clinical Quality Indicators, India's NQAS (National Quality Assurance Standards) |
| Attribution | Primary care provider | **Mixed**: Japan = by hospital department (no true primary care gatekeeping). Korea = by clinic/hospital. Singapore = by polyclinic/GP (strong gatekeeping). China = by community health center. India = by health and wellness center (Ayushman Bharat). |
| Interventions | Care management nurses | **Asia-specific**: Japan home visit nursing (kaigo), Korea community health centers, Singapore Healthier SG enrollment, China family doctor contract, India ASHA/ANM community health workers |
| Data Sources | Claims + EHR | **Multi-modal**: Japan NDB (claims) + J-ASPECT (cancer registry) + vital statistics. Korea HIRA claims + KCCR (cancer registry) + NHIS health checkups. Singapore NEHR + HealthHub + National Registry of Diseases. China claims + CDC surveillance. India HMIS + NFHS + NCD district surveys. |

#### New Action Items
```
P59-AM EXTENDED ACTIONS:
6. Integrate super-aging analytics (East Asia):
   Japan/Korea >30% 65+ by 2030. AI predicts
   frailty trajectory, sarcopenia risk,
   dementia incidence, and long-term care
   (kaigo) need. Interventions: home visit
   nursing, day care center referral,
   preventive rehabilitation (pre-kaigo).

7. Build HBV-HCC population surveillance:
   For endemic Asia, AI identifies HBsAg+
   cohorts with low surveillance adherence
   (q6mo AFP + ultrasound) and targets
   outreach. Predicts HCC incidence at
   prefecture/district level.

8. Optimize diabetes population management:
   Singapore CDMP, Japan specific health
   guidance (tokutei kenshin), Korea national
   health screening. AI identifies
   non-adherent patients (HbA1c >8%, no
   visit >6 months) for proactive outreach.

9. Support air quality-health modeling:
   China/India urban air pollution (PM2.5)
   → respiratory and cardiovascular events.
   AI correlates AQI with ED visits,
   asthma exacerbations, and stroke
   incidence. Predicts high-risk days
   for public health alerts.

10. Enable disaster-preparedness analytics:
    Japan earthquake/tsunami → dialysis
    patient evacuation planning. Philippines
    typhoon → diabetes medication stockout
    prediction. Indonesia volcanic eruption
    → respiratory surge planning.
```

---

### Regional adapters

Regional adapters set indicator frameworks, data sources, and intervention assets. The -AF adapter anchors on DHIS2 aggregation, CHW catchment attribution, climate-disease models, and MDA elimination tracking per AU Digital Health Strategy priorities. The -AR adapter adds camp and conflict surveillance: syndromic escalation, population displacement estimation, and cold-chain forecasting under humanitarian logistics. The -US adapter retains the base HEDIS/CMS/ACO posture with tribal health epidemiology configuration. The APAC adapter applies P59-AM: NDB/DPC (Japan), HIRA (Korea), CDMP/Healthier SG (Singapore), Healthy China 2030 targets, super-aging analytics, and disaster-preparedness modeling. The EU adapter applies GDPR-partitioned secondary-use analytics with member-state indicator frameworks; the Latin America adapter applies national program indicators under ANVISA/COFEPRIS norms.

## Jurisdiction Matrix

| Regime | Variant applicability | De-identification / consent posture | Residency constraint |
|---|---|---|---|
| HIPAA (US) | Base (native) · P59-AM (US node) | HEDIS/CMS Stars/NCQA; HCC risk adjustment; ACO attribution; de-identified cohort analytics | US processing; limited datasets under DUA |
| GDPR (EU/EEA) | P59-G · -EU adapter | Secondary-use lawful basis; aggregation thresholds; member-state indicator frameworks | EU residency; partitioned analytics |
| NDPR (Nigeria) | P59-G (native) | DHIS2 aggregation; WHO UHC/SDG 3 indicators; small-catchment suppression (<1000-person rule) | In-country; ministry-governed sharing |
| Kenya DPA 2019 | P59-G (native) | KHIS/DHIS2 sources; CHW catchment attribution | Kenyan residency |
| India DPDP | P59-G · P59-AM | HMIS + NFHS + NCD surveys; Ayushman Bharat health-and-wellness-center attribution | MeitY-empanelled infrastructure |
| Brazil LGPD | P59-G (native) | National program indicators | Brazilian residency |
| Saudi PDPL | P59-G (native) | National health sector plan indicators | Saudi residency |
| China PIPL | P59-AM (native) | Healthy China 2030 targets; claims + CDC surveillance; AQI-health modeling | Onshore analytics |
| Japan APPI | P59-AM (native) | NDB claims + DPC quality indicators; J-ASPECT registry; tokutei kenshin; kaigo-need prediction | Domestic; NDB use under statutory rules |
| Tribal / community consent regimes | P59-G (native) | Community-level findings governed by council consent; nomadic population tracking limited to population (never individual) movement | Community enclave analytics |

## Methodology

The base methodology is actuarial population management: validated risk instruments (HCC, Charlson, Elixhauser, LACE, PARR), specification-exact quality measure computation, provider attribution rules, and tiered intervention matching with quantified gap closure targets. P59-G re-founds the method on public-health data realities: DHIS2-plus-survey fusion in place of claims, climate-disease regression models, Sentinel-2 and cell-tower population mapping, ARIMA vaccine forecasting with campaign schedules and wastage rates, and InterVA-5 verbal autopsy classification for mortality cause distribution where no death registry exists. P59-AM re-founds it on national claims and registry infrastructures (NDB, HIRA, NEHR, National Registry of Diseases), super-aging trajectory models, AQI-health correlation, and disaster-surge prediction. The invariant: definitions are versioned, estimates are labeled, every figure carries source and vintage, and every alert has a defined action.

## Merits

- Actionable stratification with quantified gaps and matched interventions — demonstrated at cohort scale with named closure mechanisms (FIT kit mailing, automated lab orders) rather than generic recommendations (base).
- Specification-exact quality measurement (HEDIS, CMS Stars, NCQA) with attribution and drill-down (base).
- Prevents vaccine stockouts that kill; routes mobile clinics to nomadic camps invisible to facility systems; detects outbreaks from climate signals 2-4 weeks early; enables village-granularity elimination micro-planning; provides mortality cause distribution without a death registry (P59-G).
- Super-aging preparedness through frailty and kaigo-need prediction; HBV-HCC surveillance cohort rescue; pollution-health early warning; dialysis-evacuation and medication-stockout disaster planning (P59-AM).

## Guidance for Use

Deploy the base P59 within payer-provider population health operations: claims and EHR feeds mapped, measure specifications version-locked, and care-management workflows consuming the tiered outputs. Deploy P59-G at district and program level in Global South settings: offline-first with DHIS2 as the primary source, declared catchment/CHW structure, climate and satellite feeds ingested opportunistically with vintage displayed, and program authority to act on triggered allocations. Deploy P59-AM in national and insurer analytics environments across Asia-Pacific: per-country indicator configuration and registry integrations active.

Prerequisites: a defined population and attribution model, data-source inventory with quality assessment, and governance approval for secondary use. Misuse: do not present modeled estimates as counts, track individuals through mobility data, issue alerts with no response action, or export individual-level surveillance data to external analytics services. Pairings: P51 enforces aggregation thresholds and residency; P58 supplies the data fabric; P52-P57 consume population insights at the point of care; P60 executes outreach interventions; P56 uses under-served-population signals for trial site equity.

---
C0 informational classification; confers no clinical, legal, financial, or safety authority.
