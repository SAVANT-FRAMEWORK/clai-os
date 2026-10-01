---
Version: 1.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-08-11
SHA-256: [PENDING-FIRST-RELEASE]
---

# SAVANT FRAMEWORK — GOVERNANCE.md

## SPOS v1.0 · SIP v1.0 · S50 Absolute Governance Engine

This document is the operational constitution of the SAVANT FRAMEWORK. It is
written so that a grant officer, patent examiner, or sovereign partner can
understand exactly how the architecture governs itself — who may act, at which
layer, under which authorization, with which evidence trail — WITHOUT READING
A SINGLE LINE OF CODE. If any mechanism described here cannot be understood
from this text alone, that mechanism is not governed, and the defect is in
this document.

Three instruments do the governing:

  1. SPOS v1.0 — the Savant Prompt Operating System: a six-layer fractal
     prompt architecture that decides WHAT kind of work may happen and WHO
     (human or agent) may do it.
  2. SIP v1.0 — the Savant Invocation Protocol: a strict grammar of trigger
     prefixes that decides HOW work is requested and WHERE it is routed.
  3. S50 — the Absolute Governance Engine: a checkpoint, regression, and
     genealogy system that decides WHETHER the results of work may enter the
     canonical tree, and keeps the cryptographic evidence of every decision.

Nothing merges, releases, or ships except through these three instruments.

---

## 1. SPOS v1.0 — THE SIX-LAYER FRACTAL

SPOS is a fractal: the same six-layer pattern recurs at repository scale, at
module scale, and inside individual prompt chains. Authority flows downward;
evidence flows upward. No layer may perform the function of a layer above it.

| Layer | Name      | Function                                            | Acts on                        |
|-------|-----------|-----------------------------------------------------|--------------------------------|
| L0    | Kernel    | Constitutional authority; issues binding rules      | The other five layers          |
| L1    | Audit     | Independent verification; cannot be overruled below | All outputs of L2–L5           |
| L2    | Strategic | Multi-cycle planning; scope and sequencing          | Programs, releases, repos      |
| L3    | Tactical  | Single-cycle decomposition; task graphs             | Features, files, prompts       |
| L4    | Agentic   | Autonomous execution agents under constraint        | Code, tests, docs, artifacts   |
| L5    | Execution | Deterministic, mechanical operations                | Builds, merges, hashes, deploys|

  1.1 L0 — Kernel. The Kernel holds constitutional documents (LICENSE, CLA.md,
      CAA.md, DCO.md, this file, TRADEMARK.md, PATENTS.md), the twelve
      load-bearing prompts SPOS-P1 through SPOS-P12, and the root keys that
      sign S50 checkpoints. Only the Steward (Dr. Christabel Odeta) or a
      successor designated by a notarized succession instrument holds L0
      authority. L0 changes require a signed ARCHITECT invocation and an L1
      audit countersignature. There is no self-amendment shortcut.

  1.2 L1 — Audit. The Audit layer verifies, at every checkpoint, that work
      product matches the authorization that produced it: the SIP invocation,
      the assigned layer, the genealogy of any prompt touched, and the
      SHA-256 checkpoint record. L1 findings are binding. No layer — including
      L0 — may suppress an L1 finding; L0 may only appeal it to a second,
      independent L1 review with a different reviewer.

  1.3 L2 — Strategic. The Strategic layer owns roadmaps, release scopes,
      grant milestone definitions (including the metric gates of the `grants`
      repository's tranching engine), and the decision of whether a work item
      should exist at all. L2 output is a signed strategy brief; nothing below
      L2 may create scope that lacks one.

  1.4 L3 — Tactical. The Tactical layer decomposes a strategy brief into a
      task graph: files to touch, prompts to modify, tests to satisfy, and
      the regression suite each task must pass. L3 assigns tasks to L4 agents
      with explicit constraint envelopes (time, files, forbidden operations).

  1.5 L4 — Agentic. The Agentic layer is where autonomous and semi-autonomous
      agents (LLM-driven or human) execute assigned tasks. L4 agents have no
      scope authority: they may not create work outside their L3 envelope, may
      not modify L0 constitutional documents, and may not alter SIP routing
      tables or S50 checkpoint rules. Deterministic-first safety paths apply:
      in clinical and safety domains, an L4 agent's probabilistic output is
      inadmissible until a deterministic rule check passes it.

  1.6 L5 — Execution. The Execution layer performs mechanical, deterministic
      operations: builds, test runs, hash computations, merges, releases,
      Hyperledger audit anchoring writes. L5 has no discretion whatsoever. If
      an L5 operation's inputs do not satisfy the checkpoint predicate, the
      operation does not run. There is no manual override path in L5; an
      override is, by definition, an L0 constitutional act.

  1.7 Fractal recurrence. Within a single module, the same six roles recur:
      the module's constitution (its spec), its audit harness (its regression
      suite), its strategy (its design brief), its tactics (its task list),
      its agents (its functions), its execution (its runtime). A module
      missing any role is architecturally incomplete and fails L1 audit.

## 2. THE TWELVE LOAD-BEARING PROMPTS — SPOS-P1 THROUGH SPOS-P12

  2.1 Twelve prompts are declared load-bearing: SPOS-P1 through SPOS-P12.
      They encode the constitutional behaviors of each layer (two per layer).
      Everything else in the prompt corpus is replaceable; these twelve are
      not, except through L0 amendment with L1 countersignature.

  2.2 Each load-bearing prompt carries: a unique ID (SPOS-P<n>), a semantic
      version, a SHA-256 content hash, a parent hash (genealogy, Section 4.3),
      the layer it binds, and the SIP triggers authorized to invoke it.

  2.3 Removal or silent modification of any SPOS-P<n> without an L0 amendment
      record is a constitutional breach. L5 refuses to build a tree whose
      load-bearing prompt hashes do not match the signed manifest.

## 3. SIP v1.0 — THE INVOCATION PROTOCOL

SIP is the only lawful way to request work inside the architecture. An
invocation is a string of the form:

    <TRIGGER>: [<SESSION-ID>] <TITLE>

Example: `ARCHITECT: [S53] Constitutional Repository Genesis`.

The trigger determines the SPOS layer that owns the work, the prompts that
may be used, the checkpoint class that must be passed, and the evidence that
must be left behind. Free-form requests have no routing target and therefore
no authority; they are treated as discussion, not work.

### 3.1 The Fifteen Trigger Prefixes and Their Routing

| Trigger      | Routes to | Function                                                    | Checkpoint class |
|--------------|-----------|-------------------------------------------------------------|------------------|
| ARCHITECT    | L0        | Constitutional design; creates/amends governed structure    | C0 (L0 + L1 dual sign) |
| AUDIT        | L1        | Independent verification of any artifact or decision        | C1 (L1 signed finding) |
| STRATEGIZE   | L2        | Produce or revise strategy briefs and release scopes        | C2 |
| DECOMPOSE    | L3        | Break a strategy brief into a constrained task graph        | C2 |
| HARDEN       | L3        | Security/robustness analysis of existing artifacts          | C2 + regression |
| REDTEAM      | L1        | Adversarial challenge of assumptions, prompts, or claims    | C1 |
| FORESIGHT    | L2        | Scenario analysis feeding future strategy                   | C2 (advisory) |
| EXECUTE      | L5        | Run a fully-specified mechanical operation                  | C3 (predicate-only) |
| SYNTHESIZE   | L4        | Merge evidence from multiple layers into a single artifact  | C3 |
| OPTIMIZE     | L4        | Improve performance/cost within an L3 envelope              | C3 + regression |
| COMPLETE     | L4        | Finish a partially done task to its acceptance criteria     | C3 + regression |
| BUILD        | L5        | Construct artifacts under a signed build manifest           | C3 (predicate-only) |
| ORCHESTRATE  | L3        | Coordinate multi-agent work under one L3 task graph         | C2 |
| SAFETY       | L1        | Deterministic-first safety verification (clinical/mesh)     | C1 (blocking) |
| RAG          | L4        | Retrieval-augmented evidence gathering for other layers     | C3 (evidence-logged) |

### 3.2 The Ten One-Letter Shortcuts

For high-frequency operations, SIP defines ten single-letter shortcuts. Each
shortcut is an exact alias of one full trigger and inherits its routing,
constraints, and checkpoint class. Shortcuts exist for ergonomics only; they
create no additional authority.

| Shortcut | Alias of    | Routes to | Typical use                                   |
|----------|-------------|-----------|-----------------------------------------------|
| A        | ARCHITECT   | L0        | Constitutional acts                           |
| R        | REDTEAM     | L1        | Adversarial review                            |
| S        | STRATEGIZE  | L2        | Planning cycles                               |
| H        | HARDEN      | L3        | Security passes                               |
| E        | EXECUTE     | L5        | Mechanical runs                               |
| O        | ORCHESTRATE | L3        | Multi-agent coordination                      |
| C        | COMPLETE    | L4        | Task completion                               |
| T        | AUDIT       | L1        | ("Testify") audit findings                    |
| D        | DECOMPOSE   | L3        | Task graph generation                         |
| B        | BUILD       | L5        | Manifest builds                               |

  3.2.1 No shortcut aliases to SAFETY, RAG, SYNTHESIZE, OPTIMIZE, or
        FORESIGHT. SAFETY has no shortcut by deliberate policy: safety
        verification must never be invoked casually or ambiguously.

### 3.3 Routing Logic

When an invocation is received:

  (1) PARSE the trigger (full word or shortcut; shortcuts expand first).
  (2) ROUTE to the owning SPOS layer per Sections 3.1/3.2.
  (3) CHECK AUTHORITY: does the invoking party (human or agent) hold
      credentials for that layer? L0 invocations require the Steward's key;
      L1 invocations require an auditor credential independent of the party
      whose work is audited.
  (4) BIND the permitted prompt set (from the SPOS-P1–P12 manifest) and the
      constraint envelope (scope, files, time).
  (5) EXECUTE under the layer's rules (Section 1).
  (6) GATE the result through the trigger's checkpoint class (Section 4).
  (7) RECORD the invocation string, the checkpoint hash, and the genealogy
      of every prompt touched, anchored via Hyperledger audit anchoring.

An invocation failing any step produces a signed REJECTION record, not silent
failure. Rejections are auditable evidence, not errors to be hidden.

## 4. S50 — THE ABSOLUTE GOVERNANCE ENGINE

S50 is the mechanism that makes the above binding rather than aspirational.

### 4.1 SHA-256 Signed Go/No-Go Checkpoints

  4.1.1 Every transition of work between layers, and every merge into a
        protected branch, passes a numbered S50 checkpoint. A checkpoint
        computes a SHA-256 digest over: the invocation string, the input
        artifact set, the output artifact set, the prompt manifest version,
        and the regression suite result.

  4.1.2 The digest is signed by the key of the layer authorizing the
        transition. Checkpoint class C0 additionally requires the L1 auditor's
        countersignature. The signed digest is written to the checkpoint
        ledger and anchored on Hyperledger, so checkpoint history is
        tamper-evident outside the repository itself.

  4.1.3 Go/No-Go semantics are binary and predicate-only at L5: either the
        predicate holds (digest verified, signatures valid, regression suite
        green) and the transition proceeds, or it does not and the transition
        is rejected with a signed reason. There is no "proceed with warning"
        state.

  4.1.4 A release tag is valid only if the full checkpoint chain from L2
        strategy brief to L5 build verifies end-to-end. A grant officer can
        recompute any checkpoint digest from the published artifacts and
        compare it to the anchored record — governance verification without
        reading code.

### 4.2 Regression Detection

  4.2.1 Every repository maintains a named regression suite per module. Any
        invocation of class C2 or C3 that modifies artifacts must run the
        suites of every module it touches plus the constitutional suite
        (prompt-manifest integrity, checkpoint-ledger continuity, license
        header presence).

  4.2.2 A regression is defined as: any previously-passing check now failing,
        any load-bearing prompt hash diverging from the signed manifest, any
        checkpoint ledger gap, or any drop below a declared metric floor
        (e.g., deterministic-first clinical rule coverage, FHIR R4
        conformance vectors, LoRa mesh delivery-rate floors for AEGIS-NG).

  4.2.3 Detected regressions block the checkpoint and emit a signed REGRESSION
        record naming the failing check, the introducing commit, and the
        responsible invocation. Remediation must itself arrive via SIP
        (typically COMPLETE or HARDEN); manual tree surgery outside SIP is a
        constitutional breach.

### 4.3 Prompt Genealogy Rules

  4.3.1 Every prompt in the corpus has a genealogy record: ID, semantic
        version, SHA-256 content hash, parent hash, author (CLA-registered
        real name), originating SIP invocation, and checkpoint that admitted
        it. Genealogy records form a hash chain; the head of each chain for
        SPOS-P1 through SPOS-P12 is pinned in the signed manifest.

  4.3.2 A prompt modification is admissible only if its declared parent hash
        equals the current chain head, its author holds layer authority for
        the layer the prompt binds, and the admitting checkpoint is signed.
        Orphaned (parent-less) or forked-without-authority prompts are
        rejected at checkpoint time.

  4.3.3 Genealogy is public within the repository. Any auditor can answer,
        for any prompt: who changed it, under which invocation, with which
        parent's consent, at which checkpoint — again, without reading code.

## 5. ROLES, SUCCESSION, AND CONFLICT

  5.1 The Steward (Dr. Christabel Odeta) holds L0 authority and is sole
      author of record of all associated IP. L1 auditors are appointed by the
      Steward and must be independent of the work they audit in any given
      cycle. L2–L4 roles may be delegated by signed delegation instruments
      recorded in the checkpoint ledger.

  5.2 Conflict of authority resolves upward: a dispute between L3 and L4 is
      decided at L2; between layers generally, at the lowest layer superior
      to both disputants; any dispute touching constitutional documents is
      L0-only, subject to L1 audit of the decision process itself.

  5.3 Succession: L0 authority transfers only by the Steward's signed
      succession instrument, which takes effect upon anchoring to Hyperledger
      and publication in this repository. Absent a valid instrument, no
      person holds L0 authority, and the repositories enter audit-preservation
      mode: L1 continues, L2–L5 freeze.

## 6. WHAT A GRANT OFFICER CAN VERIFY FROM THIS DOCUMENT ALONE

  (a) WHO authorized any change: the SIP invocation string recorded at its
      checkpoint names the trigger, layer, and session.
  (b) WHETHER the change was permitted: the routing tables in Section 3 map
      trigger to layer; the authority rules in Section 1 map layer to actor.
  (c) WHETHER the change was verified: the S50 checkpoint ledger carries a
      SHA-256 digest and signatures, recomputable from published artifacts and
      anchored on Hyperledger.
  (d) WHETHER quality moved backward: regression records (Section 4.2) are
      signed, named, and blocking.
  (e) WHETHER the intellectual lineage is intact: the prompt genealogy chain
      (Section 4.3) is hash-linked and pinned to a signed manifest.

If any of (a)–(e) cannot be answered from repository evidence for a given
change, that change is, by definition, ungoverned and must be reverted.

## Falsifiability Test

Test: Hand this document, the checkpoint ledger, and the prompt genealogy
ledger to an evaluator with no access to source code. Select any merged
change at random. Ask the evaluator to answer all five questions of
Section 6: who authorized it, whether it was permitted, whether it was
verified, whether quality regressed, and whether lineage is intact.
Expected result: the evaluator answers all five questions from ledger
evidence alone, and recomputes the change's checkpoint SHA-256 to a value
matching the Hyperledger-anchored record. If any question is unanswerable, or
the recomputed digest diverges, the claim that the architecture governs
itself — the central claim of this document — is falsified.
