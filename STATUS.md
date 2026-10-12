# STATUS.md — CLAI-OS Honest-Absence Roadmap

**What this file is:** the public record of what does *not yet* exist in this
repository. CLAI-OS is released progressively under governance gates; rather than
staging empty directories or placeholder files, every planned subsystem is listed
here by name, with a one-line description of what it will contain. Each entry is
marked `PENDING — progressive public release` until its artifacts land, at which
point the entry is removed and the directory appears in the tree.

**Rule:** an absence listed here is a commitment, not a gap. An absence *not*
listed here does not exist anywhere in the program.

Last updated: initial public mirror release.

---

## Compliance Plane (`compliance/`)

| Subsystem | Status | Will contain |
|-----------|--------|--------------|
| `P61` | PENDING — progressive public release | Parameterized jurisdiction-compliance adapter: consent, residency, retention, and reporting rules as configuration (adapter family 1 of 10; 24 jurisdictions across P61–P70, never forked). |
| `P62` | PENDING — progressive public release | Parameterized jurisdiction-compliance adapter (family 2 of 10): clause-to-control mappings and conformance evidence for its assigned jurisdictions. |
| `P63` | PENDING — progressive public release | Parameterized jurisdiction-compliance adapter (family 3 of 10): adapter parameter tables and effective-date log. |
| `P64` | PENDING — progressive public release | Parameterized jurisdiction-compliance adapter (family 4 of 10): residency and retention configuration with conformance evidence. |
| `P65` | PENDING — progressive public release | Parameterized jurisdiction-compliance adapter (family 5 of 10): consent-rule configuration and reporting obligations. |
| `P66` | PENDING — progressive public release | Parameterized jurisdiction-compliance adapter (family 6 of 10): clause-to-control mappings and activation records. |
| `P67` | PENDING — progressive public release | Parameterized jurisdiction-compliance adapter (family 7 of 10): jurisdiction parameter tables with S50-gated activation. |
| `P68` | PENDING — progressive public release | Parameterized jurisdiction-compliance adapter (family 8 of 10): residency, retention, and reporting configuration. |
| `P69` | PENDING — progressive public release | Parameterized jurisdiction-compliance adapter (family 9 of 10): conformance evidence and effective-date log. |
| `P70` | PENDING — progressive public release | Parameterized jurisdiction-compliance adapter (family 10 of 10): completes 24-jurisdiction coverage across the P61–P70 family. |
| `ndpr-gdpr-bridge` | PENDING — progressive public release | Bridge from framework-level NDPR/GDPR mappings to clinical deployment: residency attestations, DPIA instances, and evidence that 18h offline-first operation satisfies data-localization obligations. |

## Deterministic Plane (`deterministic/`)

| Subsystem | Status | Will contain |
|-----------|--------|--------------|
| `reasoning-kernels` | PENDING — progressive public release | Specifications of the deterministic reasoning kernels — total, terminating, side-effect-free decision procedures for clinical safety logic (PPA-001). |
| `safety-vetoes` | PENDING — progressive public release | The veto layer: contraindication and safety rules whose output overrides any downstream probabilistic recommendation by construction, with precedence proofs and veto-event audit schema. |
| `golden-cases` | PENDING — progressive public release | Synthetic FHIR R4 bundles (including contraindicated drug–drug pairs) with pre-registered expected outputs; any output drift is a defect in the kernel, not the test. |
| `crdt-sync` | PENDING — progressive public release | Hub-side offline CRDT synchronization over FHIR R4 resources: merge proofs and 18-hour zero-bandwidth soak-test protocols (PPA-002; twin of `aegis-ng` F-05). |

## FHIR R4 Data Plane (`fhir-r4/`)

| Subsystem | Status | Will contain |
|-----------|--------|--------------|
| `profiles` | PENDING — progressive public release | FHIR R4 profiles and StructureDefinitions — the constrained shapes of every resource CLAI-OS stores, emits, or accepts, with versioning pins and differential tables. |
| `terminology` | PENDING — progressive public release | Code systems, value sets, and pinned bindings used by the deterministic kernels; terminology drift is treated as a safety event. |
| `validators` | PENDING — progressive public release | Validation rules and expected-results corpora proving non-conformant resources are rejected at the boundary, never silently repaired. |

## Proof Plane (`demos/`)

| Subsystem | Status | Will contain |
|-----------|--------|--------------|
| `fhir-interop` | PENDING — progressive public release | Interoperability demonstration: foreign FHIR R4 servers exchange bundles with CLAI-OS against the pinned profiles, proving nativity rather than adaptation. |
| `offline-18h` | PENDING — progressive public release | The offline endurance demonstration: 18 hours at zero bandwidth, then CRDT merge with provable zero-loss conflict resolution (the demo form of PPA-002). |

## Patents Plane (`patents/`)

| Subsystem | Status | Will contain |
|-----------|--------|--------------|
| `PPA-001` | PENDING — progressive public release | Local implementation-evidence bundle for the deterministic-first clinical reasoning claim (filed): kernel specs, veto precedence proofs, golden-case results. |
| `PPA-002` | PENDING — progressive public release | Local implementation-evidence bundle for offline CRDT synchronization (filed): merge proofs, soak-test records, divergence/merge traces. |
| `PPA-006-planned-not-filed` | PENDING — progressive public release | Jurisdiction Compiler workspace (planned, **not filed**): compiler design notes, draft-claim-to-adapter traceability, prior-art log. See [PATENTS.md](PATENTS.md) Section 3. |


## Deployment Agent Corpus — CLAI-OS Track (2026-10-06)

The CLAI-OS deployment agent corpus (v2.0) is canonical: ten specialist agents
(CLAI-DEPLOY-01..10) spanning publication, regulation, funding, partnership,
validation, FHIR integration, community, co-authorship, precision medicine, and
master orchestration. Agents are licensed Savant-Commercial-1.0 — public
catalog, SIP trigger matrix, and SHA-256 existence-commitments live in
[savant-prompts](https://github.com/SAVANT-FRAMEWORK/savant-prompts) and the
[agent stack documentation](https://savant-framework.github.io/savant-docs/agents/).
Full RASCEF bodies remain commercial.

Governance: PRIME → S1 → S50 → S52. Clinical invariant: no autonomous clinical
diagnosis without human-in-the-loop at T2 minimum.

Corpus-map note (2026-10-12): the canonical range is now P-051–P-110 —
P-051–P-070 sovereign infrastructure (AGPL-3.0, this repository),
P-071–P-090 Clinical Human Good and P-091–P-110 Precision Oncology & Global
Health (open documentation release — de-commercialized 2026-10-12; prompt
bodies withheld for validation; ledger rows in savant-prompts).

---

*Entries are removed from this file only in the commit that lands the subsystem's
artifacts. This file is the honesty mechanism of the progressive public release.*
