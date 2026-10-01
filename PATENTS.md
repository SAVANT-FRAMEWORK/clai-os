---
Version: 1.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-08-11
SHA-256: [PENDING-FIRST-RELEASE]
---

# SAVANT FRAMEWORK — PATENTS.md

## Defensive Publication Strategy and Public Abstracts (PPA-001 — PPA-005)

Inventor and sole IP author: Dr. Christabel Odeta — Nigerian systems
architect, system engineer, LLM engineer, prompt engineer.

This document (a) publishes enabling-level public abstracts of the five
provisional patent applications PPA-001 through PPA-005 as a defensive
publication establishing prior art as of this document's dated, hash-anchored
release, and (b) discloses the patent-licensing position of the SAVANT
FRAMEWORK. Full claims have been filed with the respective patent offices;
nothing in these abstracts limits the scope of the filed claims, and the
abstracts are not claim charts. This document is anchored via Hyperledger
audit anchoring at release, fixing its date and content for prior-art
purposes (defensive publication v3.1 reconciliation series).

---

## 1. STRATEGY — WHY DEFENSIVE PUBLICATION

  1.1 The SAVANT FRAMEWORK is dual-licensed (AGPL-3.0 OR
      Savant-Commercial-1.0). Patents on the commercial layer must not become
      instruments for third parties to close the open layer or to attack
      sovereign humanitarian deployments.

  1.2 Publishing enabling abstracts here: (a) creates dated prior art
      defeating later third-party patents on the same subject matter; (b)
      signals to grant officers and patent examiners that the IP position is
      deliberate and mapped, not improvised; and (c) preserves the
      Inventor's own filings, which precede or accompany this publication.

  1.3 Licensing position (restated from LICENSE and CAA.md): patent rights in
      PPA-001 through PPA-005, as embodied in the software, flow to
      AGPL-3.0 users per AGPL-3.0 Section 11, to commercial licensees per
      CAA.md Section 4, and are extinguished for any party instituting patent
      litigation against the project per the patent retaliation clause
      (LICENSE Section 4). Sovereign humanitarian deployers under the
      technology-transfer carve-out receive a no-fee covenant not to sue for
      in-territory non-commercial manufacture and use.

## 2. PUBLIC ABSTRACTS

### PPA-001 — Deterministic-First Clinical Reasoning

A clinical decision-support architecture in which all probabilistic model
output (including large-language-model inference) is structurally
inadmissible to a decision path until it has passed a deterministic rule
engine encoding clinical constraints, contraindications, and jurisdictional
practice rules. The deterministic layer — not the model — holds veto
authority: model proposals are treated as candidate inputs to rule-bounded
admission, never as decisions. The architecture includes: a rule-compilation
pipeline from clinical protocol documents; a deterministic admission gate
placed between model output and any actuation, display, or record-write; and
an audit record binding each admitted decision to the rule version and model
version that produced it. Implemented in CLAI-OS; governed as the
deterministic engine layer per CAA.md Section 2.1. Full claims filed with
the respective patent office.

### PPA-002 — FHIR R4 Native Offline CRDT Synchronization

A method and system for synchronizing clinical records across intermittently
connected facilities using conflict-free replicated data types (CRDTs)
defined natively over FHIR R4 resources — not over generic JSON documents.
Resource-specific merge semantics (e.g., Observation, MedicationRequest,
Encounter) are defined per FHIR R4 resource type so that concurrent offline
edits merge deterministically without a central coordinator and without
violating FHIR R4 conformance. Includes: per-resource-type CRDT schemas;
vector-clock-free convergence using resource identity and clinical
event-time; and a conformance test vector suite proving merged states remain
valid FHIR R4. The FHIR R4 resource layer itself remains open (CAA.md
Section 3); the claimed subject matter is the production synchronization
engine. Full claims filed with the respective patent office.

### PPA-003 — LoRa Mesh Safety Infrastructure (AEGIS-NG / AEGIS-GLOBAL)

A safety-alerting infrastructure built on a 433MHz LoRa mesh of
ultra-low-cost units (reference per-unit cost USD 46.30) providing
store-and-forward safety messaging with no dependence on cellular or
internet infrastructure. Claimed subject matter includes: the mesh routing
protocol optimized for alert delivery-rate floors under node churn; the
power and duty-cycle management enabling extended field operation; and the
cost-reduction architecture achieving the USD 46.30 unit cost while
preserving alert integrity, including deterministic-first alert admission
(analogous to PPA-001) so that automated alert content is rule-gated before
broadcast. Deployed as AEGIS-NG (national) and AEGIS-GLOBAL (international).
Full claims filed with the respective patent office.

### PPA-004 — Federated Edge Learning with Differential Privacy

A federated learning system for edge-deployed clinical and safety devices in
which model improvement occurs without centralizing personal data. Claimed
subject matter includes: edge-node gradient computation with per-node
differential-privacy noise calibration; a privacy-budget accounting ledger
tracking cumulative epsilon expenditure per node and per cohort, with
budget exhaustion halting participation; and aggregation logic robust to
intermittent connectivity consistent with the PPA-002 offline operating
model. Data-protection posture aligns with NDPR (Nigeria) and GDPR (EU) as
routed by compliance adapters P61–P70; the privacy-budget ledger is anchored
via Hyperledger audit anchoring for regulator-verifiable compliance
evidence. Full claims filed with the respective patent office.

### PPA-005 — Metric-Gated Blockchain Grant Tranching

A grant-administration system in which disbursement of grant capital occurs
in tranches released only upon cryptographic attestation that predefined
measurable metrics have been met. Claimed subject matter includes: the
metric-gate specification language binding each tranche to verifiable,
machine-checkable metrics; the attestation pipeline in which S50-class
SHA-256 signed checkpoints (see GOVERNANCE.md) constitute the release
predicate; and the Hyperledger-anchored tranche ledger giving grantors and
auditors a tamper-evident disbursement history. Implemented in the `grants`
repository; designed so that a grant officer can verify tranche legitimacy
from ledger evidence without reading source code. Full claims filed with
the respective patent office.

## 3. THE JURISDICTION COMPILER GAP — PPA-006 (PLANNED)

  3.1 Per the defensive publication v3.1 reconciliation, the Jurisdiction
      Compiler — the system that compiles jurisdiction-specific regulatory
      rule sets (24 jurisdictions across compliance adapters P61–P70,
      including NDPR and GDPR) into deterministic rule packs consumed by the
      PPA-001 admission gate — is disclosed here as an identified gap:
      PPA-006 is PLANNED BUT NOT YET FILED at the date of this document.

  3.2 This section constitutes the defensive publication of the Jurisdiction
      Compiler concept at enabling level: a compilation pipeline from
      machine-readable regulatory sources, through a jurisdiction-normalized
      intermediate representation, to deterministic rule packs whose versions
      are pinned in the signed prompt/rule manifest and checkpointed under
      S50, such that clinical and safety decisions are always traceable to a
      specific compiled rule-pack version for a specific jurisdiction.

  3.3 Until PPA-006 is filed: (a) no patent license, covenant, or expectation
      regarding the Jurisdiction Compiler is granted under LICENSE, CLA.md,
      or CAA.md (CAA.md Section 4.3 states this explicitly); (b) this
      publication stands as dated prior art against third-party filings on
      the same subject matter; and (c) the filing of PPA-006 will be recorded
      by amendment to this document with a new SHA-256 and Hyperledger anchor.

## 4. EXAMINER AND PARTNER NOTES

  4.1 The five abstracts above are deliberately written at enabling level:
      a person skilled in the relevant art, with the repository and these
      abstracts, could reduce each invention to practice. This is intentional;
      a non-enabling "abstract" would fail as defensive prior art.

  4.2 Nothing in this document dedicates the claimed subject matter to the
      public. Defensive publication establishes prior art as of the
      publication date; it does not waive the Inventor's filed rights.

  4.3 Versioning: this document is part of the defensive publication v3.1
      reconciliation series. Amendments follow the prompt genealogy rules of
      GOVERNANCE.md Section 4.3 (hash-chained, checkpointed, anchored).

## Falsifiability Test

Test: For each of PPA-001 through PPA-005, ask a person skilled in the art
whether the abstract in Section 2 is (a) enabling enough to serve as
defensive prior art and (b) consistent with the repository component it
claims. Then check the ledger for a dated Hyperledger anchor of this
document, and check CAA.md Section 4.3 for the PPA-006 exclusion.
Expected result: all five abstracts pass (a) and (b); the anchored hash of
this document matches its published SHA-256 field upon first release; and no
agreement in the repository purports to license PPA-006 before its filing.
If any abstract is non-enabling, inconsistent with the shipped component, or
the document's anchor is absent, the defensive-publication claim fails for
that item.
