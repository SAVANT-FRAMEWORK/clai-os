---
ID: P99
Title: Geriatric Oncology & Frailty Integrator
Registry: CLAI-OS Precision Engine (P-series)
License: Open documentation release (prompt body withheld for validation)
Version: 1.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-10-12
---

# P99: Geriatric Oncology & Frailty Integrator

## Abstract

Older adults represent the fastest-growing oncology population, yet traditional oncology systems remain calibrated around younger physiologies. P99 replaces chronological age as the dominant treatment determinant with multidimensional reserve analysis, frailty quantification, organ resilience modeling, neurocognitive assessment, and survivability-adjusted therapeutic calibration. The architecture is designed to prevent catastrophic overtreatment while protecting older adults from discriminatory undertreatment that denies potentially curative therapy solely because of chronology.

> Prompt body: WITHHELD. This is an open documentation release — abstract, methodology, and merits — published so the design can be examined and validated.

## Methodology

**Design objectives**

- Comprehensive geriatric assessment core (ADL, IADL, mobility, cognition via Mini-Cog/MoCA, mood via GDS-5, nutrition via MNA-SF, falls risk, social support, polypharmacy) with frailty phenotype classification (robust, pre-frail, frail, severely frail).
- Physiologic reserve modeling across cardiopulmonary function, renal clearance, hepatic metabolism, bone marrow reserve, sarcopenia (CT psoas area, muscle attenuation, grip strength, gait velocity), and inflammatory aging markers.
- Chemotherapy toxicity prediction via CARG toxicity score, CRASH score, and Hurria model integration, predicting grade 3-5 hematologic toxicity, neurotoxicity, delirium, functional collapse, falls, hospitalization, and treatment discontinuation.
- Treatment intensity arbitration (curative versus palliative intent, combination versus single-agent, dose attenuation, radiation modification, surgical eligibility, immunotherapy appropriateness) with dynamic recalibration: toxicity-triggered de-escalation, recovery-guided escalation, and adaptive supportive care expansion.
- Sickle-cell disease geriatric considerations (chronic cardiopulmonary disease, iron overload, pulmonary hypertension, renal dysfunction, cognitive decline, frailty acceleration) with exchange transfusion support for any cytotoxic therapy and quality-over-quantity prioritization.

**Methodological innovation**

- Physiological-age compiler: direct measurement of reserve, resilience, cognition, and functional survivability replaces calendar-age assumptions.
- Neurocognitive protection: mandatory baseline cognitive screening, delirium vulnerability modeling, medication neurotoxicity surveillance, sleep-wake stabilization, benzodiazepine minimization, and anticholinergic burden detection.
- Polypharmacy governance: drug interaction surveillance (QT prolongation, sedative stacking, CYP interactions, renal accumulation, fall amplification) with deprescribing architecture based on Beers Criteria and STOPP/START.

**Key performance indicators**

- Comprehensive geriatric assessment completion rate
- Treatment intensity appropriateness
- Grade 3-5 toxicity rate in frail patients
- Functional independence preservation
- Cognitive decline prevention
- Hospitalization reduction
- Sickle-cell-specific geriatric complication rate

**Integration**

- Upstream: P73 (Palliative Navigator) for goals-of-care integration; P80 (Ethics Navigator) for capacity and autonomy frameworks.
- Downstream: P108 (Rehabilitation & Survivorship Architect) for geriatric survivorship and rehabilitation; P109 (Health Economics & Value-Based Care Optimizer) for value-based care optimization.

## Merits

- Replaces age-based treatment assumptions with physiologic vulnerability modeling.
- Integrates cognitive status, frailty scoring, nutritional decline, toxicity forecasting, and quality-of-life optimization into one calibration layer.
- Guards simultaneously against overtreatment of the frail and undertreatment of the fit older adult.
- Provides toxicity-reduction infrastructure calibrated to validated geriatric assessment instruments.
- Supports healthcare optimization for aging populations, the fastest-growing oncology demographic.

## Guidance for Use

This document records the design intent and scientific rationale of P99 (Geriatric Oncology & Frailty Integrator) as published in the CLAI-OS Tier III (Savant Precision Engine, P91–P110) compendium. The executable prompt body is withheld; nothing in this file is sufficient to operate the module. The material is released openly so that the design can be examined, critiqued, and independently validated.

Appropriate use:

- Scientific review, replication design, and methodological critique by researchers and validation groups.
- Reference for integration planning across the P-series registry.
- Citation in scholarly or institutional work describing the CLAI-OS Precision Engine.

Limitations:

- This is not a medical device, a clinical decision-support product, or a standard of care. Nothing in this document may be used to direct diagnosis, treatment, dosing, or triage for any patient.
- Genomic and oncology statements reflect only the claims made in the source compendium; publication of this documentation does not constitute independent clinical validation.
- Assessment instruments and scores are named as design inputs; clinical interpretation belongs to geriatric oncology specialists using current SIOG/ASCO guidance.

---

C0 informational classification; confers no clinical, legal, financial, or safety authority.
