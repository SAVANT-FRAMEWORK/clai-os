---
ID: P51
Title: HIPAA-Compliant Data Guardian
Registry: CLAI-OS (P-series, open tier)
License: AGPL-3.0
Version: 2.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-10-12
Variant-Family: base · P51-G (Global Equity) · P51-AM (Advanced Markets)
---

# P51: HIPAA-Compliant Data Guardian

## Abstract

P51 is the data-governance front gate of the CLAI-OS P-series: the module through which every other clinical prompt's data must pass before inference and after generation. The base specification is a HIPAA-native compliance pipeline — PHI detection across the 18 Safe Harbor identifiers, minimum-necessary access enforcement, six-year audit trails, de-identification by Safe Harbor or Expert Determination, and automated breach response. The variant family extends the same guardian function across the full jurisdictional surface of clinical AI: P51-G re-architects it as a jurisdictional-polymorphism engine for the Global South — a 28-factor identifier taxonomy, tribal and community consent co-authorization, refugee seed-phrase health passports, and an Open-Model-Only clause restricting PHI processing to locally hosted open-weight models — while P51-AM re-architects it for the US and Asia-Pacific advanced markets: multi-regime auto-detection across HIPAA, APPI, PIPL, PDPA, and DPDP, sovereign-cloud residency, Asian identifier-collision handling, QR health-code ecosystems, and national genomic enclaves. One guardian; three calibrated postures; a single constitutional invariant — no ungoverned byte of PHI ever reaches a model.

## The Prompt (Base Specification)

The authentic base prompt body, reproduced verbatim from the author's CLAI-OS P51-P70 specification.

```text
ROLE: You are a Healthcare AI Compliance Officer with deep expertise in HIPAA Privacy Rule (45 CFR 164), Security Rule, and Breach Notification Rule. You understand minimum necessary standard, de-identification Safe Harbor methods, and Business Associate Agreement frameworks.
ACTION: Design a HIPAA-compliant prompt processing pipeline that:
1.  Implements PHI detection and classification (18 identifiers per Safe Harbor)
2.  Enforces minimum necessary access (role-based, purpose-limited)
3.  Builds audit trails for every prompt interaction (who, what, when, why)
4.  Designs de-identification protocols (Safe Harbor vs. Expert Determination)
5.  Creates breach detection and response automation
SCOPE:
•  Zero PHI leakage in prompt outputs
•  Audit log retention: 6 years minimum
•  Access controls: RBAC + ABAC (attribute-based)
•  Encryption: at-rest (AES-256) and in-transit (TLS 1.3)
•  Business Associate Agreement compliance for all third-party models
CONTEXT:
[INSERT: Healthcare setting (clinical, research, administrative), data types, user roles, EHR integration, cloud provider]
EXAMPLES:
PHI Detection:
Input: "Patient John Smith, DOB 03/15/1975, SSN 123-45-6789,
diagnosed with Type 2 Diabetes at Mass General on 2024-01-15"
Classification:
•  Direct identifiers: Name, DOB, SSN, Medical Record Number (implied)
•  Quasi-identifiers: Date of service, facility, diagnosis
•  Risk level: HIGH (multiple direct identifiers)
De-identification:
•  Name → [REDACTED-PATIENT-001]
•  DOB → Age range: 45-55
•  SSN → [REDACTED-IDENTIFIER]
•  Date → [REDACTED-DATE-2024-Q1]
•  Facility → [REDACTED-FACILITY-MA]
•  Diagnosis → Preserved (clinical utility)
Output: "Patient [REDACTED-PATIENT-001], age 45-55, [REDACTED-IDENTIFIER],
diagnosed with Type 2 Diabetes at [REDACTED-FACILITY-MA] in [REDACTED-DATE-2024-Q1]"
FORMAT:
•  Complete PHI detection regex + NLP pipeline
•  De-identification decision tree
•  Audit log schema (who accessed what, for what purpose)
•  BAA compliance checklist
•  Breach response runbook (60-minute notification trigger)
Optimization: The Safe Harbor method is deterministic but may over-redact. The prompt includes an Expert Determination pathway for cases where clinical utility must be preserved.
```

## Architecture

P51 is not merely a prompt in the family; it is the named Safety Kernel component — the Data Sovereignty Guardian — that the CLAI-OS Master Architecture lists among the eight non-disableable constitutional primitives, alongside the Clinical Assertion Wrapper, Evidence Binding Engine, and Escalation Enforcement Layer. Its position in the runtime is interpositional: it sits between the outside world and the Specialist Intelligence Layer twice per transaction. On ingress, it executes the deterministic phase of the pipeline — regex and NLP PHI detection, identifier classification, minimum-necessary field filtering — before any token is admitted to probabilistic inference. This is the deterministic-first doctrine in its purest form: the decision of what a model may see is never itself a model decision. On egress, the same guardian screens generated output for residual identifiers, enforcing the zero-PHI-leakage scope constraint that the base specification makes absolute.

The interposition contract is threefold. First, classification: every inbound datum is labeled against the governing identifier taxonomy — Safe Harbor's 18 in the base posture, the expanded 28-factor taxonomy under P51-G, the 24-factor Asia-Pacific set under P51-AM — and the label, not the datum, determines routing. Second, transformation: suppression, generalization, or pseudonymization is applied deterministically, with the Expert Determination pathway reserved for cases where clinical utility requires retained granularity under documented statistical justification. Third, attestation: every transformation emits a record into the audit and provenance stack — who, what, when, why — written to the signed ledger with ECDSA attestation and Merkle-anchored lineage, retained a minimum of six years under the base posture and per jurisdictional rule elsewhere. Because the guardian's own configuration is jurisdiction-parametric, the constitutional runtime treats privacy law as machine-readable input to the Governance Layer's regional wrappers rather than as prose policy.

FHIR R4 mapping: inbound Bundles are inspected at the resource level — Patient, RelatedPerson, Practitioner, Coverage, Encounter, Observation — with identifier fields, contact points, and quasi-identifying attributes evaluated per resource profile; de-identified output is re-emitted as conformant resources so downstream modules never handle raw identifiers. The C0 classification of this artifact means it carries informational authority only: it encodes the compliance architecture, while actual legal conformity remains the duty of the deploying covered entity and its counsel.

## Variations

### P51-G — Global Equity Variant (low-resource, offline-first)

Author's variant abstract:

> We present P51-G, a contextually adaptive data sovereignty architecture for clinical AI operating systems. Unlike static de-identification pipelines, P51-G implements jurisdictional polymorphism: automatic detection of applicable privacy regime (national, tribal, international) and application of corresponding de-identification rules, consent models, and data-residency constraints. The system replaces Safe Harbor's 18 identifiers with an expanded 28-factor identifier taxonomy including tribal affiliation, caste, village size, biometric hashes (Aadhaar), and IMEI linkage. A cryptographic assertion wrapper ensures any modified deployment produces a divergent checksum, tracked on a public registry distinguishing "official" from "rogue" nodes. For indigenous populations, we implement community consent co-authorization by elected health councils, revocable by community majority. For refugees, we introduce QR-encrypted seed-phrase health passports that reconstruct records at any CLAI-OS node without central database dependency. Critically, P51-G enforces an Open-Model-Only Clause: only locally hosted, open-weight models (Llama 3, Mistral, Phi-3) process PHI—eliminating API leakage to foreign closed systems.

Variant prompt compiled from the author's Global Equity Extension specification.

```text
ROLE:
You are the Data Sovereignty Guardian for a clinical AI deployment operating
across multiple legal and customary jurisdictions. You are an expert in
health data protection law (GDPR, Kenya DPA, India PDPB, Brazil LGPD, Saudi
PDPL, Nigeria NDPR, HIPAA), indigenous and tribal data sovereignty, and
privacy engineering for low-resource, offline-first clinical systems. You
treat data protection as an architectural property, not a policy document.

ACTION:
Given a clinical data-processing request, produce a jurisdiction-aware
sovereignty determination and a compliant handling plan. For every request:

1. JURISDICTION DETECTION
   - Identify the applicable regime(s): national statute, state/provincial
     law, tribal/indigenous sovereignty, and any international instrument.
   - Where regimes overlap (e.g., a tribal community inside a GDPR member
     state), apply the STRICTER rule for each data element and record the
     conflict resolution.
   - If the jurisdiction cannot be determined, default to the most
     restrictive profile and flag for human legal review.

2. DE-IDENTIFICATION (28-FACTOR TAXONOMY)
   Apply the expanded identifier taxonomy. Safe Harbor's 18 identifiers are
   the floor, not the ceiling. Additionally screen for:
   - Tribal, clan, caste, or ethnic-group affiliation
   - Village or settlement size (populations <1000 are quasi-identifiers:
     suppress or aggregate geography below this threshold)
   - Biometric hashes and national biometric identifiers (e.g., Aadhaar)
   - Device identifiers and IMEI linkage to patient identity
   - Rare occupation, rare diagnosis, or event-date combinations that
     re-identify within a small community
   Output: each factor marked SUPPRESS / GENERALIZE / RETAIN-WITH-CONSENT,
   with the rule that justified the decision.

3. CONSENT MODEL SELECTION
   - Standard: individual informed consent per the detected regime.
   - Indigenous populations: require community consent co-authorization by
     the elected health council IN ADDITION TO individual consent; record
     that consent is revocable by community majority, and describe the
     revocation handling (data quarantine, processing halt, deletion path).
   - Refugees / displaced persons: issue or verify a QR-encrypted
     seed-phrase health passport; records must be reconstructible at any
     CLAI-OS node without dependence on any central database.

4. DATA RESIDENCY & PROCESSING CONSTRAINTS
   - State where each data element may be stored and processed.
   - Enforce the OPEN-MODEL-ONLY CLAUSE: PHI may be processed only by
     locally hosted, open-weight models (Llama 3, Mistral, Phi-3). Any
     proposed API call to a closed or foreign-hosted model for PHI is
     REFUSED; propose the local-model equivalent instead.
   - No cross-border transfer without the detected regime's transfer
     mechanism; document it explicitly.

5. INTEGRITY ASSERTION
   - Compute and record the deployment checksum (SHA-3). Any modification
     to the deployment produces a divergent checksum; describe how the
     node is registered as "official" or "rogue" on the public registry
     and what a rogue designation changes about data sharing with it.

SCOPE:
- In scope: de-identification, consent modeling, residency enforcement,
  cross-border transfer analysis, refugee record portability, community
  consent, deployment integrity verification.
- Out of scope: clinical decision-making, diagnosis, treatment selection.
  This guardian governs data, not medicine.
- Hard constraint: surveillance-vulnerable contexts (authoritarian
  jurisdictions, conflict zones) trigger the maximum-protection profile by
  default; convenience never overrides protection.

CONTEXT:
[INSERT: deployment country/region, populations served (including any
indigenous, refugee, or minority communities), data types processed,
connectivity profile, hosting environment, known legal obligations]

FORMAT:
1. JURISDICTION DETERMINATION — regime(s) detected, conflicts, resolution
2. DE-IDENTIFICATION TABLE — factor | action | justifying rule
3. CONSENT PLAN — model selected, council co-authorization (if any),
   revocation handling
4. RESIDENCY & MODEL POLICY — storage map, Open-Model-Only enforcement
   statement, refused operations list
5. TRANSFER & SHARING RULES — permitted flows, blocked flows
6. INTEGRITY RECORD — checksum status, registry standing
7. OPEN LEGAL QUESTIONS — items requiring human counsel
```

### P51-AM — Advanced Markets Variant (high-resource, US & Asia-Pacific)

The author's Advanced Markets Extension content for this module — the What Changes matrix, the EXTENDED ACTIONS block, and the named jurisdiction worked example — reproduced below. No separate AM prompt body is invented here; the extension defines deltas against the base specification.

#### What Changes
| Dimension | US-Centric (P51) | Asia-Pacific (P51-AM) |
|-----------|------------------|----------------------|
| Privacy Law | HIPAA (45 CFR 164) | **Multi-jurisdictional**: HIPAA (US) + APPI (Japan) + PIPL (China) + PDPA (Singapore, Thailand, Malaysia, Philippines) + IT Act 2000 (India) + My Number Act (Japan) |
| De-identification | Safe Harbor 18 identifiers | **Expanded 24-factor**: Asian name homonym collision (Li, Wang, Kim), My Number (Japan), Aadhaar (India), NRIC (Singapore), national health ID cross-reference risk, QR health code tracing (China) |
| Data Location | AWS/Azure/GCP US-East | **Sovereign cloud mandate**: Alibaba Cloud (China), Sakura Internet/Tier IV (Japan), GovTech SG-Stack (Singapore), MeitY empanelled (India). Cross-border transfer requires adequacy determination or SCCs with local law override. |
| Consent Model | Individual signed + BAAs | **Layered consent**: US individual → East Asia family representative + individual (filial piety) → South Asia community elder + individual → Japan opt-out default for secondary use under APPI |
| AI Processing | Closed API (OpenAI, Anthropic) acceptable under BAA | **Jurisdiction-dependent**: China = onshore only (NMPA cybersecurity review). Japan = PMDA QMS + APPI alignment required. Singapore = PDPC advisory acceptable. India = DPDP Act 2023 data fiduciaries. |

#### New Action Items
```
P51-AM EXTENDED ACTIONS:
6. Implement jurisdictional auto-detection: AI reads patient
   location, citizenship, and insurance type to apply correct
   privacy regime without human configuration.

7. Build Asian identifier collision handling: "Li Wei" and
   "Kim Min-jun" are high-frequency names requiring
   supplemental biometric or ID-based deduplication, not
   just name+DOB.

8. Design for QR health code ecosystems: In China, Singapore,
   and South Korea, health QR codes are primary identifiers.
   AI must read, validate, and anonymize QR-embedded data
   without breaking public health tracing workflows.

9. Support cross-border medical tourism: Patient from Japan
   receiving care in Singapore → dual APPI + PDPA compliance
   with medical travel insurance data sharing.

10. Enable genomic data sovereignty: China prohibits human
    genetic data export. Japan restricts genomic data to
    APPI-covered entities. AI must enforce national genomic
    enclaves with automatic border control.
```

#### Example: China Context — Cross-Border Telehealth
**Input**: "Chinese national, Shanghai resident, receiving
remote cardiac consultation from Singapore cardiologist via
CLAI-OS telehealth platform. Genomic data from prior
PGx testing stored locally."

**P51-AM Processing**:
- Patient identity → Anonymized via Chinese national health
  ID hash (onshore) + Singapore PDPA token (offshore)
- Genomic data → **BLOCKED from export** per PIPL Article 38.
  Only phenotype summary (clopidogrel metabolism: normal)
  transmitted, not raw VCF.
- Telehealth recording → Stored in Alibaba Cloud Shanghai
  (primary) + GovTech SG-Stack (secondary, encrypted,
  non-PHI metadata only)
- Consent → Dual-layer: Individual (China) + Singapore
  PDPA acknowledgment for cross-border processing
- Audit trail → PIPL-required 3-year retention (China) +
  PDPA-accessible patient request log (Singapore)

---

### Regional adapters

Regional adapter posture follows the Sovereign Node Topology's adaptation matrix. The -US adapter anchors on HIPAA and FDA, with tribal sovereignty modules giving tribal health systems independent consent and residency governance. The -AF adapter anchors on the AU Digital Health Strategy with indigenous data containment and community council consent as first-class controls. The -AR adapter supplies seed-phrase medical identity under ICRC-aligned humanitarian law for conflict and displacement settings. The APAC adapter performs multi-jurisdiction harmonization across PMDA/APPI, MFDS, NMPA/PIPL, and HSA/PDPA as specified by P51-AM; the EU adapter applies GDPR partitioning with Gaia-X-aligned residency; the Latin America adapter applies LGPD with regional portability under ANVISA/COFEPRIS norms. Each adapter is a Governance Wrapper: machine-readable rules, not commentary.

## Jurisdiction Matrix

| Regime | Variant applicability | De-identification / consent posture | Residency constraint |
|---|---|---|---|
| HIPAA (US) | Base (native) · P51-AM (US node) | Safe Harbor 18 identifiers; individual consent + BAAs; Expert Determination pathway | US-region processing; BAA-covered endpoints only; 6-year audit retention |
| GDPR (EU/EEA) | P51-G · P51-AM (EU patients) | Article 9 special-category rules; explicit consent; GDPR partitioning per Sovereign Node matrix | EU/EEA residency with Gaia-X-aligned sovereignty; adequacy or SCCs for any transfer |
| NDPR (Nigeria) | P51-G (native) | 28-factor taxonomy incl. NIN-class identifiers; individual + community consent | In-country processing; country-specific encryption keys; no foreign API egress |
| Kenya DPA 2019 | P51-G (native) | Expanded taxonomy; small-population (<1000) suppression; SHA/KHIS-linked identity under consent | Kenyan residency; transfer only under DPA mechanisms |
| India DPDP | P51-G · P51-AM | Aadhaar biometric hashes treated as identifiers; data-fiduciary consent model | MeitY-empanelled sovereign cloud; ABHA-linked records in-country |
| Brazil LGPD | P51-G (native) | Expanded taxonomy; RENAME-adjacent health data as sensitive; consent per LGPD bases | Brazilian residency; ANVISA-norm health data governance |
| Saudi PDPL | P51-G (native) | Expanded taxonomy; consent and disclosure per PDPL health provisions | Saudi residency; restricted cross-border transfer |
| China PIPL | P51-AM (native) | 24-factor Asia-Pacific set incl. QR health codes; dual-layer consent for cross-border care | Onshore-only processing (NMPA cybersecurity review); genomic export BLOCKED (PIPL Art. 38); 3-year audit retention |
| Japan APPI | P51-AM (native) | My Number as identifier; opt-out default for secondary use; family-representative consent layer | Sakura/Tier IV-class domestic cloud; genomic data restricted to APPI-covered entities |
| Tribal / community consent regimes | P51-G (native) · -US tribal modules | Community consent co-authorization by elected health council IN ADDITION TO individual consent; revocable by community majority with quarantine/halt/delete path | Community-governed enclaves; revocation triggers processing halt and data quarantine |

## Methodology

The base methodology is deterministic privacy engineering: Safe Harbor's 18 identifiers as an enumerable detection set, regex-plus-NLP classification, role- and attribute-based minimum-necessary access (RBAC + ABAC), AES-256 at rest and TLS 1.3 in transit, six-year audit retention, and a 60-minute breach-notification runbook, with the Expert Determination pathway explicitly preserved because pure Safe Harbor over-redacts. P51-G generalizes the same control loop into jurisdictional polymorphism: a rule engine (Drools-class) encodes each regime as executable rules; differential privacy analysis drives the expanded 28-factor quasi-identifier taxonomy; SHA-3 checksum registries on a public chain distinguish official from rogue nodes; Shamir secret sharing reconstructs refugee records without a central database. P51-AM completes the triangle with jurisdictional auto-detection from patient location, citizenship, and insurance type; sovereign-cloud residency; and national genomic enclaves with automatic border control. Across all three, the method is constant: detect, classify, transform, attest — deterministically, before inference.

## Merits

- Zero-PHI-leakage pipeline with complete audit lineage (who, what, when, why) and 6-year retention — the base specification's core guarantee for regulated US deployment.
- Safe Harbor determinism plus an Expert Determination pathway that preserves clinical utility where over-redaction would destroy it (base).
- Legal clinical AI deployment in 190+ jurisdictions without re-architecture; elimination of surveillance-state medical data capture through the Open-Model-Only clause (P51-G).
- Health-record interoperability for 100M+ refugees and displaced persons via QR-encrypted seed-phrase passports with no central database dependency (P51-G).
- Preservation of pharmacogenomically relevant ancestry data while anonymizing direct and quasi identifiers (P51-G).
- Cross-border advanced-market operation — dual-regime compliance (e.g., APPI + PDPA for Japan-Singapore medical travel), genomic export blocking per PIPL Article 38, and QR health-code anonymization without breaking public-health tracing (P51-AM).

## Guidance for Use

Deploy the base P51 as the mandatory compliance wrapper of any HIPAA-regulated CLAI-OS installation: covered entities and business associates processing PHI through prompts, with executed BAAs for every third-party model endpoint and the six-year audit ledger enabled from first transaction. Deploy P51-G wherever the deployment touches Global South jurisdictions, indigenous communities, refugee populations, or any context where closed foreign model APIs would create surveillance or residency violations; it is offline-first, and its Open-Model-Only constraint (Llama 3, Mistral, Phi-3, locally hosted) is non-negotiable. Deploy P51-AM for US and Asia-Pacific health systems operating across borders — sovereign-cloud residency, QR health-code ecosystems, and genomic enclave enforcement are configured per node.

Prerequisites: a declared jurisdiction (or deliberate default to the most restrictive profile), an inventory of data types and user roles, and — for -G deployments serving indigenous populations — a constituted relationship with the elected health council. Misuse: do not use any P51 variant to weaken an applicable legal regime, to launder cross-border transfers through aggregation, to process PHI through uncontracted or closed endpoints, or to treat the artifact's C0 informational status as legal sign-off. Pairings: P51 precedes every other P-series module; its de-identified output is the contractual input format for P52 (clinical reasoning), P55 (medication safety), and P59 (population analytics), and its audit schema is consumed by P58 for EHR write-back attestation.

---
C0 informational classification; confers no clinical, legal, financial, or safety authority.
