---
ID: P58
Title: Electronic Health Record (EHR) Integration Architect
Registry: CLAI-OS (P-series, open tier)
License: AGPL-3.0
Version: 2.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-10-12
Variant-Family: base · P58-G (Global Equity) · P58-AM (Advanced Markets)
---

# P58: Electronic Health Record (EHR) Integration Architect

## Abstract

P58 is the interoperability spine of the CLAI-OS P-series: the module that moves data between the reasoning layer and the systems of record. The base specification is standards-grade health IT integration — FHIR R4 retrieval across demographics, conditions, medications, labs, and allergies; FHIR Composition-structured notes; validated write-back of diagnoses, procedures, and care plans; SMART on FHIR launch with OAuth 2.0; read-only by default with explicit write authorization; real-time synchronization; and HIPAA audit logging on every transaction, with vendor-specific guidance for Epic and Cerner workflows. The variant family carries the same interoperability discipline into environments where Epic and broadband do not exist — or where different national stacks dominate. P58-G is the offline-first exchange architecture: OpenMRS, DHIS2, iSanté, SmartCare, ABHA, SHA/KHIS, and NHIS connectors; local-script OCR (Arabic, Devanagari, Amharic) for paper-to-digital register transition with legal paper retention; offline-first SQLite sync with explicit conflict resolution; USSD/SMS feature-phone workflows and WhatsApp CHW channels; and Merkle-anchored seed-phrase records for refugees, reconstructible at any node without a central database. P58-AM is the fragmented-Asia integrator: Japan SS-MIX translation with fax-to-FHIR conversion, China hospital-system connectors under PIPL data localization, Singapore NEHR consent-API integration, India ABHA record linking, and messaging-app write-back across WeChat, Line, KakaoTalk, and WhatsApp. The interoperability discipline is invariant; the endpoints, identity systems, and sync assumptions are infrastructure-calibrated.

## The Prompt (Base Specification)

The authentic base prompt body, reproduced verbatim from the author's CLAI-OS P51-P70 specification.

```text
ROLE: You are a Health IT Integration Specialist with expertise in HL7 FHIR, SMART on FHIR, and EHR interoperability (Epic, Cerner, Meditech). You understand clinical workflows, CDA documents, and interoperability standards.
ACTION: Design an EHR-integrated prompt system that:
1.  Retrieves patient data via FHIR APIs (demographics, conditions, medications, labs, allergies)
2.  Structures clinical notes using FHIR Composition resource
3.  Writes back structured data (diagnoses, procedures, care plans)
4.  Respects EHR workflow (in-basket messages, order sets, smart phrases)
5.  Maintains audit trails for all data access and modification
SCOPE:
•  FHIR R4 compliance
•  OAuth 2.0 + SMART launch context
•  Read-only by default; write requires explicit authorization
•  Real-time synchronization (not batch)
•  HIPAA audit logging for all transactions
CONTEXT:
[INSERT: EHR vendor, FHIR version, clinical domain, user roles, workflow integration points]
EXAMPLES:
FHIR Data Retrieval:
GET /Patient/123/$everything
→ Bundle containing:
•  Patient demographics
•  AllergyIntolerance (3 entries: penicillin, sulfa, latex)
•  Condition (5 entries: Type 2 DM, HTN, Hyperlipidemia, OA, Depression)
•  MedicationRequest (8 entries: metformin, lisinopril, atorvastatin, etc.)
•  Observation (latest labs: HbA1c 8.2%, LDL 145, eGFR 55)
•  Encounter (last 3 visits with notes)
Prompt Integration:
1.  Extract relevant data for clinical decision support
2.  Generate recommendation with FHIR references
3.  Structure output as FHIR CarePlan or ServiceRequest
4.  Present in EHR workflow (Epic SmartPhrase, Cerner PowerNote)
FORMAT:
•  FHIR resource mapping specification
•  SMART on FHIR launch sequence
•  Clinical write-back validation rules
•  EHR-specific integration guides (Epic App Orchard, Cerner Code)
•  Audit log schema (who, what, when, where, why)
```

## Architecture

P58 is the physical instantiation of the Integration Layer — the architecture's native-FHIR-R4, multi-standard bridging layer — and its constitutional role is bidirectional interposition: everything the reasoning modules consume arrives through P58's retrieval paths, and everything they produce returns to systems of record through P58's validated write-back. The deterministic-first doctrine is absolute here: retrieval, mapping, validation, and logging are deterministic operations against versioned resource profiles; no probabilistic inference touches the transport path. Write-back is gated by the base's read-only-default rule — writes require explicit authorization — and by clinical validation rules that reject malformed or semantically incomplete resources before they can corrupt a record. Every transaction, read or write, emits to the audit stack: the base's who-what-when-where-why schema is the Integration Layer's logging contract, written to the signed ledger with the six-year HIPAA retention posture and Merkle-anchored lineage for tamper evidence.

Synchronization implements the Federated Synchronization Map: real-time consensus in Tier 1 hospital deployments; CRDT conflict resolution and queue-based delayed reconciliation in Tier 2-3; SMS-fallback delta compression for 2G survivability under P58-G; and blockchain-anchored lineage proofs for the refugee portable-record pathway. Offline operation is constitutional, not incidental — the architecture's offline-first doctrine means P58-G's local SQLite store, explicit per-data-class conflict policy, and deferred sync are the specified behavior of the layer under connectivity loss, with the invariant that care delivery never blocks on synchronization. Identity resolution is jurisdiction-parametric: medical record numbers in the base posture; national ID and biometrics (Aadhaar, NIN, My Number, NRIC, ABHA) under variant adapters, each with declared matching rules, confidence handling, and duplicate procedures under P51's sovereignty governance. FHIR R4 resource coverage spans Patient, Condition, Observation, MedicationRequest, Encounter, AllergyIntolerance, Composition, CarePlan, ServiceRequest, Consent, and AuditEvent — the last emitted for every access. The artifact is C0 informational: it specifies and operates the exchange architecture; institutional interface authorization and legal health-record status remain with the deploying health system.

## Variations

### P58-G — Global Equity Variant (low-resource, offline-first)

Author's variant abstract:

> We present P58-G, an offline-first health information exchange architecture replacing cloud-dependent EHR assumptions. The system integrates OpenMRS REST API, DHIS2 data exchange, India's ABHA (Ayushman Bharat Health Account), Kenya's SHA/KHIS, and Nigeria's NHIS. Paper-to-digital transition is enabled via OCR optimized for local scripts (Arabic, Devanagari, Amharic) reading handwritten clinic registers, converting to structured FHIR while maintaining paper backup for legal requirements. Community health workers use simple Android apps with large buttons, offline capability, and voice input; data syncs when cellular coverage is reached. USSD/SMS workflows support feature-phone patients: 3841# for appointment checks, medication reminders, and structured symptom reporting. Refugees carry blockchain-anchored (lightweight) health records as QR-encrypted seeds, reconstructible at any CLAI-OS node without central database dependency.

Variant prompt compiled from the author's Global Equity Extension specification.

```text
ROLE:
You are a health information systems architect for offline-first,
low-connectivity environments within CLAI-OS. You design and operate
record exchange across OpenMRS, DHIS2, iSanté, SmartCare, ABHA, SHA/KHIS,
and NHIS — and across paper registers — with FHIR R4 as the structural
spine. You assume 2G/3G intermittency, feature phones, and national-ID or
biometric identity, and you never let synchronization block care.

ACTION:
Given a records/integration task (capture, exchange, transition,
retrieval, or identity resolution), produce an executable plan:

1. SYSTEM & IDENTITY MAPPING
   - Identify source/target systems (OpenMRS REST API, DHIS2, iSanté,
     SmartCare, ABHA, SHA/KHIS, NHIS, paper register).
   - Resolve identity via national ID (Aadhaar, NIN) or biometrics;
     state the matching rule, confidence, and duplicate-handling
     procedure. Never invent a medical record number dependency the site
     cannot sustain.

2. PAPER-TO-DIGITAL TRANSITION (when registers are involved)
   - Apply OCR optimized for local scripts (Arabic, Devanagari,
     Amharic) to handwritten clinic registers.
   - Convert to structured FHIR R4 resources; preserve the paper record
     as the legally valid backup and state the retention rule.
   - Report OCR confidence per register page and queue low-confidence
     pages for human verification.

3. OFFLINE-FIRST CAPTURE & SYNC
   - CHW capture: simple Android app pattern — large buttons, offline
     capability, voice input — syncing when cellular coverage is reached.
   - Local store: offline-first SQLite with conflict resolution; state
     the conflict policy (field-level merge, clinician-wins, or manual
     review) for each data class.
   - Care delivery, prescribing, and referral must function fully with
     zero connectivity; sync is asynchronous.

4. FEATURE-PHONE & MESSAGING CHANNELS
   - USSD/SMS workflows: appointment checks, medication reminders,
     structured symptom reporting (e.g., 3841# menu tree); specify the
     exact menu structure and data mapping to FHIR.
   - WhatsApp Business API channel for CHW communication; specify
     message templates and escalation paths.

5. PORTABLE RECORDS FOR DISPLACED POPULATIONS
   - Issue/verify QR-encrypted seed health records anchored on a
     lightweight blockchain (Merkle tree anchoring, not a full chain),
     reconstructible at any CLAI-OS node with no central database.
   - State the reconstruction procedure and the failure mode when
     insufficient shares/seeds are presented.

SCOPE:
- Health information architecture and exchange design; clinical content
  belongs to clinical modules.
- Every data flow must name its residency jurisdiction and comply with
  it; P51 sovereignty rules bind all exchange.
- No flow may require connectivity to be safe: degradation behavior is
  mandatory for every component.

CONTEXT:
[INSERT: systems present, connectivity profile (2G/3G, hours of
coverage), identity infrastructure, register formats and scripts, CHW
device fleet, feature-phone patient share, refugee/migrant population
served]

FORMAT:
1. SYSTEM MAP — systems | role | interface standard
2. IDENTITY PLAN — identifier | matching rule | confidence handling
3. TRANSITION PLAN — OCR scope | FHIR mapping | paper retention
4. SYNC ARCHITECTURE — local store | conflict policy | sync trigger
5. CHANNEL SPEC — USSD/SMS menus | WhatsApp templates | FHIR mapping
6. PORTABLE RECORD SPEC — seed format | anchoring | reconstruction
7. DEGRADATION TABLE — component | zero-connectivity behavior
```

### P58-AM — Advanced Markets Variant (high-resource, US & Asia-Pacific)

The author's Advanced Markets Extension content for this module — the What Changes matrix and the EXTENDED ACTIONS block — reproduced below. The source extension provides no named jurisdiction worked example for this module; none is invented here. No separate AM prompt body is fabricated; the extension defines deltas against the base specification.

#### What Changes
| Dimension | US-Centric (P58) | Asia-Pacific (P58-AM) |
|-----------|------------------|----------------------|
| EHR System | Epic, Cerner, Meditech | **Fragmented Asia landscape**: Epic (US-affiliated hospitals in Asia) + Japan SS-MIX standardized format (but siloed by hospital) + China hospital-specific systems (Yonyou, Neusoft) + Singapore NEHR (centralized) + India's ABHA (Ayushman Bharat Health Account, emerging) + Korea HIRA claims + Taiwan NHI IC card |
| Connectivity | Always-on broadband | **Mixed**: Singapore/Japan/Korea = fiber. Rural China/India = 4G/5G dominant. Japan = fax still common for referrals. China = WeChat integration for patient communication. |
| Identity | Medical record number | **National ID linkage**: Japan My Number (optional health linkage), China resident ID (mandatory hospital registration), Singapore NRIC + HealthHub, India ABHA (Ayushman Bharat Health Account), Korea resident registration number (HIRA-linked) |
| Interoperability | FHIR R4 + SMART | **FHIR R4 + SS-MIX (Japan) + China's Health Information Interoperability Framework + Singapore NEHR APIs + India's ABHA APIs + HL7 v2 (legacy Asia) + WeChat/Line/KakaoTalk patient portals** |
| Write-Back | Structured EHR notes | **Multi-modal**: Structured EHR (Singapore/Japan) + WeChat mini-program care plans (China) + Line health bot reminders (Japan/Taiwan/Thailand) + KakaoTalk notifications (Korea) + SMS (India/rural Asia) |

#### New Action Items
```
P58-AM EXTENDED ACTIONS:
6. Design for Japan SS-MIX integration:
   Standardized dataset (CDA format) but
   hospital-specific EHR silos. AI acts as
   SS-MIX translator, enabling cross-hospital
   record sharing without replacing existing
   infrastructure. Fax-to-FHIR conversion for
   referral letters (still 40% of Japan
   referrals).

7. Build China hospital system connectors:
   Yonyou, Neusoft, DHIS2-China, WeChat
   hospital mini-programs. Patient data
   stays within China (PIPL compliance).
   Cross-hospital sharing via government
   health cloud (provincial level).

8. Implement Singapore NEHR integration:
   Centralized national record with
   patient consent API. AI pulls records
   from public hospitals, polyclinics, and
   participating private providers.
   Medication history, allergies, lab
   results, imaging reports.

9. Support India's ABHA (Ayushman Bharat):
   Health ID creation, record linking across
   public and private providers, eSanjeevani
   teleconsult integration. QR-based health
   card for rural patients.

10. Enable messaging app integration:
    WeChat (China), Line (Japan, Thailand,
    Taiwan), KakaoTalk (Korea), WhatsApp
    (India, Singapore). Care plans,
    appointment reminders, medication
    adherence nudges delivered via patient's
    primary messaging platform.
```

---

### Regional adapters

Regional adapters configure endpoints, identity, and sync posture per the architecture's interoperability matrix. The -AF adapter activates OpenMRS-native and DHIS2-mediator integration with CHW Android capture and USSD/SMS channels. The -AR adapter provides stateless seed-phrase identity and humanitarian mesh synchronization for camp and conflict deployments. The -US adapter retains the base Epic/Cerner/SMART posture with tribal health system interface configuration. The APAC adapter applies P58-AM: SS-MIX translation and fax-to-FHIR for Japan, PIPL-localized China connectors, NEHR consent-API integration for Singapore, ABHA linking for India, and WeChat/Line/KakaoTalk write-back. The EU adapter applies GDPR-partitioned exchange with Gaia-X-aligned residency and EHDS readiness; the Latin America adapter integrates national systems under LGPD residency with ANVISA/COFEPRIS norms.

## Jurisdiction Matrix

| Regime | Variant applicability | De-identification / consent posture | Residency constraint |
|---|---|---|---|
| HIPAA (US) | Base (native) · P58-AM (US node) | Epic/Cerner SMART on FHIR; read-only default; HIPAA audit logging every transaction | US processing; 6-year audit retention |
| GDPR (EU/EEA) | P58-G · -EU adapter | GDPR-partitioned exchange; EHDS readiness; Gaia-X-aligned residency | EU residency |
| NDPR (Nigeria) | P58-G (native) | OpenMRS/DHIS2 + NHIS connectors; NIN/biometric identity under program authority; paper register legal retention | In-country; offline-first local store; 2G sync |
| Kenya DPA 2019 | P58-G (native) | SHA/KHIS integration; USSD/SMS channels | Kenyan residency |
| India DPDP | P58-G · P58-AM | ABHA health ID creation and record linking; eSanjeevani integration; QR health cards | MeitY-empanelled; in-country ABHA data |
| Brazil LGPD | P58-G (native) | National system connectors under LGPD bases | Brazilian residency |
| Saudi PDPL | P58-G (native) | National platform integration posture | Saudi residency |
| China PIPL | P58-AM (native) | Yonyou/Neusoft connectors; WeChat mini-program write-back; provincial health-cloud sharing | PIPL localization — patient data stays within China |
| Japan APPI | P58-AM (native) | SS-MIX translation; fax-to-FHIR (40% of referrals); My Number optional health linkage; Line health-bot write-back | Domestic silos respected; no infrastructure replacement |
| Tribal / community consent regimes | P58-G (native) | Tribal health system interface configuration; community data governance on shared records | Community enclave nodes per P51 |

## Methodology

The base methodology is standards-strict interface engineering: FHIR R4 resource mapping, SMART launch sequencing with OAuth 2.0 scopes, Composition-structured documentation, validated write-back, workflow-native surfacing (SmartPhrase, PowerNote), and comprehensive audit schema. P58-G re-founds the method on offline-first reality: FHIR R4 plus OpenMRS and DHIS2 multi-connectors, SQLite sync with explicit conflict policies, Tesseract-based OCR custom-trained for Arabic/Devanagari/Amharic registers, USSD gateway and WhatsApp Business channels, and Merkle-tree anchoring (not full-chain) for portable refugee records. P58-AM re-founds it on fragmentation: SS-MIX-to-FHIR translation without replacing hospital silos, fax digitization for the 40% of Japanese referrals still faxed, national consent-API patterns (NEHR, ABHA), and messaging-platform care-plan delivery. The invariant: standards-conformant mapping, authorization-gated writes, conflict-resolved sync, and an audit event for every byte that moves.

## Merits

- Vendor-real integration — retrieval, structured documentation, validated write-back, and workflow-native surfacing for the EHR systems hospitals actually run (base).
- Safety-by-default transport: read-only unless explicitly authorized, real-time sync, and HIPAA-complete audit logging on every transaction (base).
- EHR functionality where there is no EHR; paper register legal validity preserved alongside structured FHIR data; 2G-only environment support; cross-border refugee health continuity; 70% CHW data-entry burden reduction through voice input (P58-G).
- Cross-hospital record sharing in siloed markets without infrastructure replacement (SS-MIX translation, fax-to-FHIR); national-record integration through patient-consent APIs; care plans delivered on the messaging platforms patients already use (P58-AM).

## Guidance for Use

Deploy the base P58 as the integration layer of any hospital CLAI-OS installation: FHIR R4 endpoints validated, SMART app registration complete, write authorization scoped per resource type, and audit streaming to the compliance ledger from first transaction. Deploy P58-G as the records layer beneath all Global South modules: fully offline operation, declared per-data-class conflict policies, OCR language packs matched to local registers, and legal paper-retention rules honored. Deploy P58-AM in fragmented Asia-Pacific markets: per-country connector configuration, PIPL data localization enforced for China workloads, and messaging-app channels consented.

Prerequisites: authorized interface access (or national-program API credentials under variants), declared identity-resolution infrastructure, and a conflict-resolution policy document. Misuse: do not bypass write authorization, discard legally mandated paper after digitization, expose record content through messaging channels beyond minimum workflow data, or route register images and voice through closed cloud services. Pairings: serves every clinical module (P52-P57, P59, P60) as their data path; enforces P51 residency rules in transit; consumes P54 genomics observations; persists P57 communications and P60 telehealth encounters.

---
C0 informational classification; confers no clinical, legal, financial, or safety authority.
