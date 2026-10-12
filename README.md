# CLAI-OS

**The clinical cognition engine of the SAVANT FRAMEWORK** — deterministic-first,
FHIR R4 native, offline-capable clinical decision infrastructure designed for the
jurisdictions and connectivity conditions that conventional health-IT ignores.

Author and sole IP holder: **Dr. Christabel Odeta** — Nigerian systems architect,
systems engineer, LLM engineer, prompt engineer.

---

## What CLAI-OS Is

CLAI-OS is a clinical cognition engine built on one constitutional rule: in
life-critical decision paths, **a rule that can be proven executes before a model
that can only be estimated**. Probabilistic model output — including large-language
-model inference — is structurally inadmissible to any decision path until it has
passed a deterministic rule engine encoding clinical constraints, contraindications,
and jurisdictional practice rules. The deterministic layer holds veto authority;
models propose, rules dispose.

Canonical facts:

- **Deterministic-first safety** — deterministic admission gate between any model
  output and any actuation, display, or record-write (PPA-002, filed).
- **FHIR R4 native** — clinical data is modeled natively in FHIR R4; there is no
  translation layer in which clinical meaning can be lost.
- **18-hour offline guarantee** — CRDT synchronization defined natively over FHIR R4
  resources guarantees 18 hours of operation at zero bandwidth with provable,
  zero-loss merge on reconnection.
- **24 jurisdictions, 10 adapters** — compliance adapters **P61–P70** cover 24
  jurisdictions as parameterized configuration; adapters are never forked. NDPR
  (Nigeria) and GDPR (EU) are first-class conformance targets.
- **5 Nigerian languages** — Hausa, Fulfulde, Igbo, Yoruba, and Efik are supported
  across the clinical interface layer.
- **Patent posture** — 5 provisional patent applications filed (PPA-001 … PPA-005);
  PPA-006 (Jurisdiction Compiler) is **planned, not filed**. See
  [PATENTS.md](PATENTS.md) for the enabling-level public abstracts and the
  defensive-publication strategy.

## Status — Read This First

This repository is an **engineering artifact in progressive public release**. The
governance instruments, licensing, patent abstracts, and architecture published here
are complete and canonical. The subsystem implementations themselves are released
progressively under governance gates; [STATUS.md](STATUS.md) is the honest-absence
roadmap: every planned subsystem is listed by name and marked
`PENDING — progressive public release` until its artifacts land. Nothing here
pretends to be what it is not.

## The CLAI Prompt Corpus (P51–P110)

**CLAI prompts exist only in the P51–P110 range** (author ruling 2026-10-12).
The SAVANT FRAMEWORK operations registry (P01–P50) lives in
[`savant-prompts`](https://github.com/SAVANT-FRAMEWORK/savant-prompts) — the
two registries are distinct and must not be conflated.

- **P51–P70 — AGPL-3.0, open** ([`prompts/`](prompts/)): the complete open
  tier. Each artifact carries the authentic base prompt (verbatim), the
  Global Equity variant (low-resource, offline-first), the Advanced Markets
  variant (US & Asia-Pacific), a ten-regime jurisdiction matrix, architecture,
  methodology, merits, and guidance for use.
- **P61–P70 jurisdiction compliance notes** ([`compliance/`](compliance/)):
  per-prompt regime maps — HIPAA, GDPR, NDPR, Kenya DPA, India DPDP, LGPD,
  PDPL, PIPL, APPI, tribal/community consent.
- **P71–P110 — open documentation release** ([`prompts/`](prompts/)):
  de-commercialized per author ruling 2026-10-12; prompt bodies withheld,
  names, methodologies, and merits published so the designs can be examined
  and validated.

## Repository Contents

| Path | Contents |
|------|----------|
| [prompts/](prompts/) | The CLAI prompt corpus P51–P110 (see above) |
| [compliance/](compliance/) | Jurisdiction compliance notes P61–P70 |
| [LICENSE](LICENSE) | Dual license: AGPL-3.0 OR Savant-Commercial-1.0 |
| [GOVERNANCE.md](GOVERNANCE.md) | Constitutional governance (SPOS / SIP / S50 gates) |
| [TRADEMARK.md](TRADEMARK.md) | Trademark policy |
| [DCO.md](DCO.md) | Developer Certificate of Origin |
| [PATENTS.md](PATENTS.md) | Defensive-publication strategy + PPA-001…005 public abstracts; PPA-006 gap disclosure |
| [STATUS.md](STATUS.md) | Honest-absence subsystem roadmap |
| [docs/architecture/00-master-tree.md](docs/architecture/00-master-tree.md) | Five-repository sovereign-deployment master tree |
| [docs/architecture/clai-os-tree.md](docs/architecture/clai-os-tree.md) | CLAI-OS directory architecture and subsystem contracts |

## Planned Subsystem Planes (see STATUS.md)

- `fhir-r4/` — profiles, terminology, validators (the data plane)
- `deterministic/` — reasoning-kernels, safety-vetoes, golden-cases, crdt-sync (the safety plane)
- `compliance/` — P61–P70 jurisdiction adapters, ndpr-gdpr-bridge (the law plane)
- `demos/` — fhir-interop, offline-18h (the proof plane)

## Ecosystem

| Resource | Link |
|----------|------|
| Organization | https://github.com/SAVANT-FRAMEWORK |
| Documentation | https://savant-framework.github.io/savant-docs/ |
| Live demo | https://savant-framework.github.io/savant-demo/ |
| Prompt library | https://github.com/SAVANT-FRAMEWORK/savant-prompts |
| Companion hardware mesh | AEGIS-NG (sovereign node infrastructure) |

## Contributing

Contributions are accepted under [DCO.md](DCO.md) sign-off and the governance
process in [GOVERNANCE.md](GOVERNANCE.md). All clinical-safety-affecting changes
pass through the deterministic-first falsifiability gates described in the
architecture documents.

## Licensing

CLAI-OS is dual-licensed: **AGPL-3.0** for the open layer, or
**Savant-Commercial-1.0** for commercial deployments. Patent rights in PPA-001
through PPA-005 flow to AGPL-3.0 users per AGPL-3.0 Section 11 and are extinguished
for any party instituting patent litigation against the project. See
[LICENSE](LICENSE) and [PATENTS.md](PATENTS.md).

---

*CLAI-OS is a constitutional instantiation of the SAVANT FRAMEWORK; this is the
canonical public repository.*
