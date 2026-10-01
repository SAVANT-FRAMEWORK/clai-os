---
Version: 1.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-08-11
SHA-256: [PENDING-FIRST-RELEASE]
---

# 00 — MASTER TREE: Five-Repository Sovereign Deployment

> SIP Invocation: `ARCHITECT: [S55] Six-Layer Directory Tree`
> Scope: directory-level architecture only. No code. Every directory is a governance claim.

## 1. The Five Repositories

The sovereign technology stack is partitioned into five repositories. The partition is not
organizational convenience; it is the constitutional separation of powers made physical.
Each repository has exactly one constitutional role, and no artifact may live in two
repositories at once.

```
sovereign-deployment/
│
├── savant-core/          ← Constitutional core: SPOS layers, SIP grammar, S50 gates,
│                            falsifiability harnesses, patent claim charts, global
│                            compliance frameworks (NDPR/GDPR), doctrine, media, demos.
│
├── clai-os/              ← Clinical intelligence instantiation: FHIR R4 native,
│                            deterministic-first reasoning, offline CRDT sync (18h at
│                            zero bandwidth), jurisdiction adapters P61–P70 (24
│                            jurisdictions), NDPR/GDPR conformance evidence.
│
├── aegis-ng/             ← Sovereign safety mesh instantiation: 14 hardware node types
│                            (N-A01…N-D02), 12 firmware subsystems (F-01…F-12) on
│                            STM32L072 / ESP32-S3 / ESP32-C3, 6 TFLite Micro edge models
│                            (M-01…M-06), 433 MHz LoRa mesh, CRDT sync, solar-only power,
│                            anti-tamper, field operations across 12 Nigerian LGAs at
│                            $46.30/node BOM.
│
├── aegis-global/         ← Sovereign technology transfer instantiation: LCSC/JLCPCB
│                            manufacturing pipeline ($46.30/unit, DAP Lagos), engineer
│                            certification curriculum, bandwidth-zero
│                            evaluation (10 metrics, Bayesian), grant packaging.
│
└── grants/               ← Funding operations: one directory per grant target in the
                             24-target grant portfolio; metric-gated tranche evidence;
                             Hyperledger-anchored milestones.
```

## 2. How the Tree Encodes Governance

A directory tree in this program is a **governance instrument**. Three mapping rules bind
every directory to an external obligation. A directory that cannot state its mapping under
at least one rule does not exist.

### Rule M-1 — Patent Claim Mapping

Every filed or planned patent claim has exactly one owning directory, and the directory
name carries the patent identifier verbatim.

- `PPA-001` … `PPA-005` — **filed**. Directories are named with the bare identifier
  (e.g., `patents/PPA-001/`). Filing receipts, claim charts, and examiner correspondence
  live inside.
- `PPA-006` — *Jurisdiction Compiler* — **planned, NOT filed**. Its directory is named
  `PPA-006-planned-not-filed/` so that no engineer, auditor, or examiner can mistake a
  plan for a filing. Renaming it to the bare identifier is itself a governed act,
  permitted only after the filing receipt is committed.

Canonical patent-to-repository assignment (used consistently across all six tree files):

| Patent | Title (working) | Owning repository | Status |
|--------|-----------------|-------------------|--------|
| PPA-001 | Anti-tamper solar-only mesh node architecture | `aegis-ng` | FILED |
| PPA-002 | Deterministic-first clinical reasoning kernel | `clai-os` | FILED |
| PPA-003 | Federated edge learning with differential privacy at zero bandwidth | `aegis-ng` + `clai-os` (joint; claim chart in `savant-core`) | FILED |
| PPA-004 | Offline CRDT synchronization for intermittently connected sovereign meshes (18h zero bandwidth) | `clai-os` + `aegis-ng` (joint; claim chart in `savant-core`) | FILED |
| PPA-005 | Bandwidth-zero evaluation methodology (10-metric Bayesian protocol) | `aegis-global` | FILED |
| PPA-006 | Jurisdiction Compiler (compliance-as-configuration across P61–P70) | `clai-os` | **PLANNED — NOT FILED** |

### Rule M-2 — Compliance Requirement Mapping

Every regulatory obligation has a directory named by its clause or adapter identifier, and
conformance evidence lives inside it — never in prose documents elsewhere.

- Global frameworks: `compliance/ndpr/`, `compliance/gdpr/` (in `savant-core`).
- Jurisdiction adapters: `compliance/P61/` … `compliance/P70/` (in `clai-os`), covering
  24 jurisdictions. Adapter identifiers are immutable; a new jurisdiction adds an adapter,
  it never forks one (ADR-007).
- Offline-operation guarantees (18h zero-bandwidth CRDT sync) are compliance-relevant
  evidence and are cross-referenced from both `clai-os/demos/offline-18h/` and the
  relevant adapter directories.

### Rule M-3 — Grant Deliverable Mapping

Every grant deliverable maps 1:1 to a directory inside the target's directory in `grants/`,
and the directory name is the funder's canonical slug (e.g., `doj-ojjdp/`). Tranche
evidence is metric-gated and Hyperledger-anchored; a deliverable without a directory is an
unfunded promise, and a directory without a deliverable mapping is deleted at the next S50
gate review. Targets 11–24 of the portfolio exist as honestly-reserved placeholders
(`target-11/` … `target-24/`) pending the Chunk 8 grant registry; reserved directories are
labeled as such and contain no invented content.

## 3. The `.gitkeep` + `README.md` Convention

Two files make empty directories legible to both Git and humans:

1. **`README.md` — required in every directory, empty or not.** It states, in fixed order:
   (a) constitutional purpose, (b) the patent claim / compliance requirement / grant
   deliverable the directory maps to, (c) what will live here, (d) governing agent and
   phase. A directory without a `README.md` fails the falsifiability gate automatically.
2. **`.gitkeep` — required in every directory that is currently empty.** Git does not
   track empty directories; `.gitkeep` pins the directory into version control so the
   governance structure is clone-complete on day one. When real content arrives, the
   `.gitkeep` is removed in the same commit. A directory containing neither content nor
   `.gitkeep` is a structural defect.

Convention test: after `git clone`, `find . -type d -empty | grep -v .git` must return no
directory lacking a `.gitkeep`, and every directory must contain a `README.md`.

## 4. Naming Law

- **kebab-case** for all prose-named directories (`edge-ai/`, `field-ops/`).
- **Identifiers are preserved verbatim** and never translated into prose: `F-04-edge-ai/`
  keeps the subsystem ID `F-04`; `PPA-006-planned-not-filed/` keeps the patent ID;
  `P61/`–`P70/` keep the adapter IDs; `M-01`…`M-06`, `N-A01`…`N-D02` keep model and node
  IDs. The ID is the audit key; the prose suffix is the human key; both are mandatory.
- **No ambiguous names.** If a systems engineer cannot predict a directory's contents from
  its name, the name is renamed before merge (see Falsifiability Test).
- **No overlapping scope.** Two directories that would hold the same artifact are merged;
  one artifact, one home.

F-, N-, M-, P-, and PPA-series identifiers are assigned by this architecture and carry no external-registry meaning.

## 5. Governing Agents and Phases (INFINITE Agent Roster)

| Agent | Role | Primary repository scope |
|-------|------|--------------------------|
| Agent 01 | Hardware Engineer | `aegis-ng/hardware/` |
| Agent 02 | Firmware Engineer | `aegis-ng/firmware/` |
| Agent 03 | ML / Edge AI Engineer | `aegis-ng/firmware/F-04-edge-ai/`, models M-01…M-06 |
| Agent 04 | Backend / Hub Engineer | `clai-os/`, hub-side sync |
| Agent 05 | Security Auditor | anti-tamper, threat models, all repos |
| Agent 06 | Field Deployment Lead | `aegis-ng/field-ops/`, 12 LGAs |
| Agent 07 | Grant Strategist | `grants/`, `aegis-global/grants/` |
| Agent 08 | Documentation Lead | `docs/`, `media/`, README law enforcement |
| Agent 09 | Evaluation Scientist | `aegis-global/evaluation/` |
| Agent 10 | Master Orchestrator | cross-repo S50 gates, this tree |

## Falsifiability Test

**Gate question:** can a systems engineer clone any of the five repositories and
understand the entire sovereign technology stack from directory names alone?

Test procedure:
1. Clone all five repositories fresh.
2. For every directory, attempt to predict its contents from its name and its `README.md`
   first line *before* opening any other file.
3. Any directory whose contents surprise the engineer is renamed, and the rename is
   recorded as an ADR.
4. Any directory failing Rule M-1/M-2/M-3 mapping, or lacking `README.md`/`.gitkeep` per
   §3, blocks the S50 go/no-go gate until cured.

**Invalidation condition:** if an independent gate reviewer finds a single directory that
is simultaneously (a) ambiguously named, (b) unmapped to any patent claim, compliance
requirement, or grant deliverable, and (c) undocumented, then this master tree is invalid
and must be re-issued under a new version. The commitment is not that the tree is perfect;
the commitment is that its defects are legible, located, and blocking.
