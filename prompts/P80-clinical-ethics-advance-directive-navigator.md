---
ID: P80
Title: Clinical Ethics & Advance Directive Navigator
Registry: CLAI-OS Human Good Systems (P-series)
License: Open documentation release (prompt body withheld for validation)
Version: 1.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-10-12
---

# P80: Clinical Ethics & Advance Directive Navigator

## Abstract

Modern healthcare continuously generates situations where physiology alone cannot determine correct action. Patients lose capacity, families disagree, clinicians face moral injury, resources become finite, and competing values collide under time pressure. P80 establishes reproducible ethical navigation architecture functioning across intensive care, oncology, surgery, psychiatry, emergency medicine, geriatrics, pediatrics, and humanitarian crises, protecting against coercion, surrogate overreach, discriminatory futility labeling, and undocumented value substitution.

> Prompt body: WITHHELD. This is an open documentation release — abstract, methodology, and merits — published so the design can be examined and validated.

## Methodology

### Clinical Logic

- Capacity assessment via the MacCAT-T framework (Understand, Appreciate, Reason, Communicate) with decision-specific and dynamic evaluation distinguishing capacity from legal competence.
- Advance directive interoperability (living wills, durable power of attorney, POLST/MOLST, DNR/DNI) with cross-setting portability and real-time verification at the point of care.
- Surrogate hierarchy enforcement (durable power of attorney, spouse, adult children, parents, siblings, best-interest fallback) with substituted judgment validated against the patient's historical values.
- Conflict mediation for family disagreement, religious objection, futility disputes, and ICU escalation conflicts through ethics consultation triggers and time-limited trials.
- Resource allocation ethics during crisis standards activation with transparent triage criteria, lottery tie-breakers where appropriate, and explicit prohibition of disability-, wealth-, or race-based rationing.

### Safety Posture

- Principlism-to-Practice Compiler operationalizes autonomy, beneficence, nonmaleficence, and justice as executable workflow constraints rather than abstract principles.
- Cultural Congruence Logic recognizes collectivist decision models, accommodates death-discussion taboos, integrates traditional healers, and supports spiritual authority consultation without cultural erasure.
- Coercion Detection System flags family pressure, financial coercion, insurer-driven discharge, immigration-related fear, gender and power imbalance, and institutional intimidation with automatic escalation to ethics, social work, or legal protection.

### Integration Points

- **Upstream:** P73 (Palliative Navigator) for end-of-life ethics; P74 (Trauma Architect) for crisis triage ethics.
- **Downstream:** P82 (SDOH Integrator) for structural vulnerability adaptation; P83 (Advocacy Guardian) for rights protection; P84 (Disaster Response) for scarcity ethics.

Like all Tier II modules, this module shares the common CLAI-OS methodological substrate: deterministic safety compilation, context-sensitive adaptation, closed-loop accountability, federated learning via encrypted gradients rather than raw data, and graceful degradation under bandwidth, power, staffing, and infrastructure failure.

## Merits

- Makes ethical reasoning reproducible and auditable across settings where it is currently episodic, personality-dependent, and undocumented.
- Proposed validation metrics: advance directive concordance rate, ethics consultation appropriateness, surrogate conflict resolution time, crisis standards transparency index, coerced treatment detection rate, and capacity assessment accuracy.
- Encodes explicit prohibitions — surrogate overreach, discriminatory futility labeling, undocumented value substitution — as executable constraints.

The merits above are design-level statements drawn from the published abstract and methodology. No peer-reviewed outcome evaluations accompany this release; the listed indicators are the metrics the design proposes for validation. Status: partial documentation — expansion pending.

## Guidance for Use

### Intended Setting

Intensive care units, oncology and surgical services, geriatrics, psychiatry, and humanitarian operations in low-resource-first deployment, including settings without standing ethics committees. The module is intended for clinical human-good applications; consistent with the Tier II architecture, it is specified for degraded-infrastructure operation, with offline synchronization, battery operation, SMS fallback, and low-bandwidth mode where power or connectivity is unstable.

### Prerequisites

- Jurisdictional law on capacity, surrogate hierarchy, and advance directives mapped by qualified counsel; ethics consultation pathway (internal or external) identified before deployment.
- Supervision by licensed clinicians who retain final authority for every patient decision; the module is a governance layer, not an autonomous practitioner.
- Local validation of all thresholds and pathways against jurisdictional guidelines, formulary, and scope-of-practice rules before any clinical use.
- An accountability chain (verification, documentation, ownership, follow-up, escalation) as required by the shared CLAI-OS closed-loop methodology.
- For integrated deployments: HL7 FHIR R4-compatible infrastructure; the architecture is specified to degrade gracefully (offline synchronization, battery operation, SMS fallback, low-bandwidth mode) where infrastructure is unstable.

### Misuse

- Do not treat module outputs as ethics verdicts; the system structures deliberation and triggers consultation. Do not use resource-allocation logic to introduce rationing criteria the design prohibits.
- Do not present module output as a clinical diagnosis, prescription, or substitute for professional judgment.
- Do not use to deny, delay, or ration care on the basis of race, disability, wealth, insurance status, or any protected characteristic; the design explicitly prohibits such inputs.
- Do not attempt to reconstruct or reimplement the withheld prompt body from this document; the abstract and methodology are published for examination and validation, not for unsupervised clinical deployment.
- Do not deploy as an autonomous system that overrides documented patient wishes, assigns futility, initiates withdrawal of care, or delays emergent intervention; the architecture carries hard-stops against each of these.

---

C0 informational classification; confers no clinical, legal, financial, or safety authority.
