---
Version: 1.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-08-11
SHA-256: [PENDING-FIRST-RELEASE]
---

# CLAI-OS — Directory Tree

> Repository role: the clinical instantiation of SAVANT FRAMEWORK. FHIR R4 native
> (ADR-006), deterministic-first reasoning (ADR-001), offline CRDT sync guaranteeing 18
> hours at zero bandwidth (ADR-003 / PPA-004), NDPR/GDPR conformant, with jurisdiction
> compliance adapters P61–P70 across 24 jurisdictions (ADR-007).

## 1. Tree

```
clai-os/
│
├── README.md
├── LICENSE                            ← inherited dual license (AGPL-3.0 / Savant-Commercial-1.0)
│
├── fhir-r4/
│   ├── README.md
│   ├── profiles/
│   │   ├── README.md
│   │   └── .gitkeep
│   ├── terminology/
│   │   ├── README.md
│   │   └── .gitkeep
│   └── validators/
│       ├── README.md
│       └── .gitkeep
│
├── deterministic/
│   ├── README.md
│   ├── reasoning-kernels/
│   │   ├── README.md
│   │   └── .gitkeep
│   ├── safety-vetoes/
│   │   ├── README.md
│   │   └── .gitkeep
│   ├── golden-cases/
│   │   ├── README.md
│   │   └── .gitkeep
│   └── crdt-sync/
│       ├── README.md
│       └── .gitkeep
│
├── patents/
│   ├── README.md
│   ├── PPA-002/
│   │   ├── README.md
│   │   └── .gitkeep
│   ├── PPA-004/
│   │   ├── README.md
│   │   └── .gitkeep
│   └── PPA-006-planned-not-filed/
│       ├── README.md
│       └── .gitkeep
│
├── compliance/
│   ├── README.md
│   ├── ndpr-gdpr-bridge/
│   │   ├── README.md
│   │   └── .gitkeep
│   ├── P61/
│   │   ├── README.md
│   │   └── .gitkeep
│   ├── P62/
│   │   ├── README.md
│   │   └── .gitkeep
│   ├── P63/
│   │   ├── README.md
│   │   └── .gitkeep
│   ├── P64/
│   │   ├── README.md
│   │   └── .gitkeep
│   ├── P65/
│   │   ├── README.md
│   │   └── .gitkeep
│   ├── P66/
│   │   ├── README.md
│   │   └── .gitkeep
│   ├── P67/
│   │   ├── README.md
│   │   └── .gitkeep
│   ├── P68/
│   │   ├── README.md
│   │   └── .gitkeep
│   ├── P69/
│   │   ├── README.md
│   │   └── .gitkeep
│   └── P70/
│       ├── README.md
│       └── .gitkeep
│
└── demos/
    ├── README.md
    ├── offline-18h/
    │   ├── README.md
    │   └── .gitkeep
    └── fhir-interop/
        ├── README.md
        └── .gitkeep
```

Directory count: 29 directories (including repo root). Ten adapter directories P61–P70
collectively cover 24 jurisdictions (each adapter is parameterized per jurisdiction per
ADR-007; adapters are never forked).

## 2. Leaf READMEs

### `fhir-r4/README.md`
- **Constitutional purpose:** root of the FHIR R4 native data plane. CLAI-OS models
  clinical data natively in FHIR R4; there is no translation layer in which clinical
  meaning can be lost (ADR-006).
- **Maps to:** compliance requirement — interoperability obligations in clinical
  procurement; grant deliverables for health-sector targets (`nih-nci/`,
  `wellcome-trust/`).
- **Will live here:** the three subdirectories below only.
- **Governing agent/phase:** Agent 04 (Backend/Hub); continuous.

### `fhir-r4/profiles/README.md`
- **Constitutional purpose:** CLAI-OS FHIR R4 profiles and StructureDefinitions —
  the constrained shapes of every resource the system will store, emit, or accept.
- **Maps to:** compliance requirement — profile conformance is the acceptance test for
  FHIR R4 nativity (ADR-006); grant deliverable evidence for interop milestones.
- **Will live here:** profile definitions, versioning pins, differential tables.
- **Governing agent/phase:** Agent 04; profiles frozen at release gates.

### `fhir-r4/terminology/README.md`
- **Constitutional purpose:** code systems, value sets, and bindings used by the
  deterministic kernels; terminology drift is a safety event, so bindings are pinned.
- **Maps to:** patent claim PPA-002 (deterministic reasoning depends on pinned
  terminology); compliance requirement — clinical coding standards per jurisdiction
  adapter P61–P70.
- **Will live here:** value set pins, expansion snapshots, drift-detection reports.
- **Governing agent/phase:** Agent 04 with Agent 05 review; per-release pins.

### `fhir-r4/validators/README.md`
- **Constitutional purpose:** validation rules and expected-results corpora proving that
  non-conformant resources are rejected at the boundary, never repaired silently.
- **Maps to:** compliance requirement — boundary validation evidence for auditors;
  falsifiability support (rejection behavior is a testable claim).
- **Will live here:** validator specifications, conformance test matrices, reject logs
  schema.
- **Governing agent/phase:** Agent 04; run at every release gate.

### `deterministic/README.md`
- **Constitutional purpose:** root of the deterministic-first reasoning plane: in
  life-critical paths, a rule that can be proven executes before a model that can only be
  estimated (ADR-001).
- **Maps to:** patent claim PPA-002 (FILED); the repository's central falsifiability
  claim (deterministic veto precedes any probabilistic output).
- **Will live here:** the four subdirectories below only.
- **Governing agent/phase:** Agent 04; Agent 05 audits; every release gate.

### `deterministic/reasoning-kernels/README.md`
- **Constitutional purpose:** specifications of the deterministic reasoning kernels —
  total, terminating, side-effect-free decision procedures for clinical safety logic.
- **Maps to:** patent claim PPA-002; compliance requirement — deterministic behavior is
  the system's primary safety case to regulators.
- **Will live here:** kernel specifications, totality/termination arguments, decision
  tables.
- **Governing agent/phase:** Agent 04; kernels frozen at constitutional gates.

### `deterministic/safety-vetoes/README.md`
- **Constitutional purpose:** the veto layer: contraindication and safety rules whose
  output overrides any downstream probabilistic recommendation, by construction.
- **Maps to:** patent claim PPA-002; the CLAI-OS falsifiability claim (a single recorded
  instance of probabilistic output overriding a deterministic veto invalidates the
  deployment).
- **Will live here:** veto rule catalog, precedence proofs, veto-event audit schema.
- **Governing agent/phase:** Agent 04 implements; Agent 05 audits; continuous.

### `deterministic/golden-cases/README.md`
- **Constitutional purpose:** the golden-case corpus: synthetic FHIR R4 bundles (including
  contraindicated drug-drug pairs) with pre-registered expected outputs; any output drift
  is a defect in the kernel, not in the test.
- **Maps to:** patent claim PPA-002 evidence; grant deliverable — regression evidence for
  health-sector funders (`nih-nci/`, `wellcome-trust/`).
- **Will live here:** synthetic bundles, expected outputs, drift reports.
- **Governing agent/phase:** Agent 09 (Evaluation) curates; run at every gate.

### `deterministic/crdt-sync/README.md`
- **Constitutional purpose:** hub-side specification of offline CRDT synchronization:
  divergent clinical state merges without connectivity, making offline operation a
  first-class guarantee (ADR-003) — 18 hours at zero bandwidth with provable merge.
- **Maps to:** patent claim PPA-004 (FILED); compliance requirement — data residency
  support (sync without a foreign cloud); cross-repo twin of
  `aegis-ng/firmware/F-05-crdt-sync/`.
- **Will live here:** CRDT specifications, merge proofs, 18h soak-test protocols.
- **Governing agent/phase:** Agent 04 with Agent 02 (firmware twin); per-release proofs.

### `patents/README.md` (clai-os)
- **Constitutional purpose:** implementation-evidence plane for the patent claims this
  repository embodies. Authoritative claim charts live in `savant-core/patents/`; this
  directory holds the pointers and the local evidence those charts cite (Rule M-1).
- **Maps to:** patent claims PPA-002, PPA-004 (FILED); PPA-006 (planned, not filed).
- **Will live here:** the three subdirectories below only.
- **Governing agent/phase:** Agent 10 owns filings; Agent 04 supplies evidence.

### `patents/PPA-002/README.md`
- **Constitutional purpose:** local evidence bundle for the deterministic-first clinical
  reasoning kernel claim: kernel specs, veto precedence proofs, golden-case results.
- **Maps to:** patent claim PPA-002 (FILED); claim chart in `savant-core/patents/PPA-002/`.
- **Will live here:** evidence index, reproducibility notes, examiner-response exhibits.
- **Governing agent/phase:** Agent 04; refreshed at each office action.

### `patents/PPA-004/README.md`
- **Constitutional purpose:** local evidence bundle for offline CRDT synchronization
  (18h zero bandwidth): merge proofs, soak-test records, divergence/merge traces.
- **Maps to:** patent claim PPA-004 (FILED); claim chart in `savant-core/patents/PPA-004/`.
- **Will live here:** evidence index, soak-test logs schema, exhibit pointers.
- **Governing agent/phase:** Agent 04 with Agent 02; refreshed at each office action.

### `patents/PPA-006-planned-not-filed/README.md`
- **Constitutional purpose:** implementation workspace for the **Jurisdiction Compiler** —
  the mechanism that compiles adapter parameters (P61–P70) into enforced configuration so
  sovereignty is a configuration of law, not a fork of code (ADR-007). **Status: planned,
  NOT filed.** The directory name is the honesty mechanism and may be shortened only in
  the commit that adds the filing receipt.
- **Maps to:** patent claim PPA-006 (planned, not filed); all ten `compliance/P61–P70/`
  adapters.
- **Will live here:** compiler design notes, draft-claim-to-adapter traceability,
  prior-art log.
- **Governing agent/phase:** Agent 10; filing decision at the next S50 gate.

### `compliance/README.md` (clai-os)
- **Constitutional purpose:** root of jurisdiction compliance for the clinical system.
  Compliance is parameterized per jurisdiction (ADR-007); this directory is where law
  becomes configuration.
- **Maps to:** compliance requirements NDPR/GDPR plus 24-jurisdiction adapter coverage;
  patent claim PPA-006 (planned).
- **Will live here:** `ndpr-gdpr-bridge/` and adapters P61–P70 only.
- **Governing agent/phase:** Agent 05 (Security Auditor); reviewed at every phase gate.

### `compliance/ndpr-gdpr-bridge/README.md`
- **Constitutional purpose:** the bridge from the framework-level NDPR/GDPR mappings (in
  `savant-core/compliance/`) to clinical deployment: residency attestations, DPIA
  instances, and the evidence that offline-first operation (18h zero bandwidth) satisfies
  data-localization obligations.
- **Maps to:** compliance requirements NDPR and GDPR; cross-referenced by
  `demos/offline-18h/`.
- **Will live here:** bridge tables, attestation templates, residency evidence.
- **Governing agent/phase:** Agent 05; continuous.

### `compliance/P61/README.md` … `compliance/P70/README.md` (ten adapters)
Each adapter directory `P61/` through `P70/` carries an identical constitutional contract;
the per-adapter jurisdiction assignments are enumerated in the adapter index inside
`compliance/README.md` (24 jurisdictions across 10 adapters, per ADR-007).

- **Constitutional purpose:** one parameterized compliance adapter per identifier. The
  adapter encodes a jurisdiction family as configuration — consent rules, residency,
  retention, reporting — so that entering a jurisdiction never forks code.
- **Maps to:** compliance requirement for its assigned jurisdictions (Rule M-2); patent
  claim PPA-006 (Jurisdiction Compiler — planned, not filed) compiles these parameters.
- **Will live here:** adapter parameter tables, clause-to-control mappings, conformance
  evidence, effective-date log. Identifier is immutable; a new jurisdiction adds
  parameters or a new adapter, never edits history.
- **Governing agent/phase:** Agent 05 owns all ten; per-jurisdiction activation is an
  S50-gated act with Agent 10 signature.

### `demos/README.md` (clai-os)
- **Constitutional purpose:** root of clinical demonstrations; each demo is a public,
  repeatable execution of a falsifiability claim.
- **Maps to:** grant deliverables — demonstration milestones for health-sector targets.
- **Will live here:** the two subdirectories below only.
- **Governing agent/phase:** Agent 08 with Agent 09; per-phase refresh.

### `demos/offline-18h/README.md`
- **Constitutional purpose:** the offline endurance demonstration: CLAI-OS operates 18
  hours at zero bandwidth, then merges via CRDT with provable zero-loss conflict
  resolution — the demo form of ADR-003 and PPA-004.
- **Maps to:** patent claim PPA-004; compliance requirement — data-residency evidence
  cited by `compliance/ndpr-gdpr-bridge/`; grant deliverable for connectivity-poor
  deployment targets (`target-XX/`, `target-XX/`).
- **Will live here:** demo protocol, timer/witness procedure, expected merge evidence.
- **Governing agent/phase:** Agent 09 runs; Agent 06 witnesses in field conditions.

### `demos/fhir-interop/README.md`
- **Constitutional purpose:** the interoperability demonstration: foreign FHIR R4 servers
  exchange bundles with CLAI-OS against the pinned profiles, proving nativity rather than
  adaptation (ADR-006).
- **Maps to:** compliance requirement — interop attestations; grant deliverable for
  `horizon-europe/` and `nih-nci/`.
- **Will live here:** partner-server matrix, exchange scripts, conformance scorecards.
- **Governing agent/phase:** Agent 04; run at each release gate.

## Falsifiability Test

**Gate question for `clai-os`:** from directory names alone, can a systems engineer
separate the data plane (`fhir-r4/`), the safety plane (`deterministic/`), the monopoly
plane (`patents/`), the law plane (`compliance/P61–P70/`), and the proof plane (`demos/`)?
Can the engineer further name which patent (PPA-002, PPA-004, PPA-006-planned) owns each
plane, and state that adapters are parameterized, never forked?

Test procedure: a cold reviewer maps each of the 28 governed directories to exactly one of
the five planes and one Rule (M-1/M-2/M-3) using names only; the reviewer must also
correctly identify `PPA-006-planned-not-filed/` as unfiled. Any misclassification triggers
a rename before the next S50 gate. **Invalidation condition:** if any adapter directory
(P61–P70) is found to contain a jurisdiction fork rather than parameters, ADR-007 is
violated and this tree's release signature is void.
