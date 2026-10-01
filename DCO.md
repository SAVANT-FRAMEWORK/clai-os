---
Version: 1.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-08-11
SHA-256: [PENDING-FIRST-RELEASE]
---

# SAVANT FRAMEWORK — DEVELOPER CERTIFICATE OF ORIGIN (DCO)

Governance header: This DCO operates alongside the SAVANT FRAMEWORK CLA
(CLA.md). The CLA governs licensing of contributions; this DCO governs the
provenance of every commit. Both are mandatory. CLA Assistant enforces the
CLA; the S50 governance engine's SHA-256 checkpoint pipeline rejects any
commit lacking a valid `Signed-off-by:` line before merge into any protected
branch of `savant-core`, `clai-os`, `aegis-ng`, `aegis-global`, or `grants`.

---

## 1. REQUIREMENT — EVERY COMMIT

Every commit to any SAVANT FRAMEWORK repository must include the following
line in its commit message trailer:

    Signed-off-by: Real Legal Name <verifiable.email@example.com>

The name must be the contributor's real legal name as registered in the
signed CLA. Pseudonymous sign-offs are invalid. Where commit GPG signing is
enforced, the signing key's fingerprint must match the fingerprint declared
in the contributor's CLA record.

By adding the `Signed-off-by:` line, the contributor certifies the Developer
Certificate of Origin, Version 1.1, reproduced in Section 2.

## 2. DEVELOPER CERTIFICATE OF ORIGIN — VERSION 1.1 (ADAPTED)

Developer Certificate of Origin
Version 1.1
(SAVANT FRAMEWORK governance adaptation; certification text unchanged in
substance from DCO 1.1, Copyright (C) 2004, 2006 The Linux Foundation and its
contributors.)

By making a contribution to this project, I certify that:

  (a) The contribution was created in whole or in part by me and I have the
      right to submit it under the license indicated in the file
      and declared in the repository LICENSE (AGPL-3.0 OR
      Savant-Commercial-1.0, per the SAVANT dual-license model, it being
      understood that the commercial path is proprietary); or

  (b) The contribution is based upon previous work that, to the best of my
      knowledge, is covered under an appropriate open source license and I
      have the right under that license to submit that work with
      modifications, whether created in whole or in part by me, under the same
      open source license (unless I am permitted to submit under a different
      license), as indicated in the file; or

  (c) The contribution was provided directly to me by some other person who
      certified (a), (b) or (c) and I have not modified it.

  (d) I understand and agree that this project and the contribution are
      public and that a record of the contribution (including all personal
      information I submit with it, including my sign-off) is maintained
      indefinitely and may be redistributed consistent with this project or
      the open source license(s) involved.

## 3. SAVANT-SPECIFIC EXTENSIONS TO DCO PRACTICE

  3.1 Prompt provenance. Commits modifying any load-bearing prompt (SPOS-P1
      through SPOS-P12) must carry, in addition to `Signed-off-by:`, a
      genealogy trailer of the form:

          Spos-Genealogy: SPOS-P<n>-v<major.minor>-parent:<sha256-of-parent>

      The genealogy chain is a governance record; falsifying a parent hash is
      treated as a certificate violation equivalent to a false sign-off.

  3.2 SIP artifact commits. Commits produced through a SIP v1.0 invocation
      (e.g., `ARCHITECT: [S53] Constitutional Repository Genesis`) must cite
      the invocation string in the commit body so the S50 engine can associate
      the commit with the go/no-go checkpoint under which it was authorized.

  3.3 Third-party material. Contributions containing third-party material must
      identify the upstream license in the commit body and confirm
      compatibility with AGPL-3.0 redistribution and Savant-Commercial-1.0
      dual-licensing. Material that cannot be dual-licensed is not
      commit-eligible, regardless of technical merit.

  3.4 Data-bearing fixtures. Commits introducing test fixtures containing or
      derived from personal data must name the applicable compliance adapter
      (P61–P70) and jurisdiction (e.g., NDPR/Nigeria, GDPR/EU) in the commit
      body, certifying the fixture is synthetic or lawfully de-identified.

## 4. FALSE CERTIFICATION

A false or fraudulent `Signed-off-by:` certification is grounds for: (a)
revert of the implicated commits; (b) revocation of the contributor's CLA
record; (c) notice to downstream distributors where the false certification
affects license integrity; and (d) referral to the contributor's employer or
contracting entity where applicable. The Steward maintains a revocation
ledger, anchored via Hyperledger audit anchoring, recording all DCO
revocations.

## 5. INTERACTION WITH THE CLA

The DCO certifies origin; it does not grant the dual-license rights required
by CLA.md Section 2.1. A commit with a valid DCO sign-off from a contributor
without a signed CLA remains blocked. Both gates must pass independently; one
does not cure the other.

## Falsifiability Test

Test: Inspect a random sample of 50 merged commits across the five
repositories and verify, for each: (i) a `Signed-off-by:` trailer with a real
name matching a CLA record; (ii) for any SPOS-P1–P12 modification, a valid
`Spos-Genealogy:` trailer whose parent hash resolves in the genealogy ledger;
and (iii) for SIP-originated commits, a cited invocation string.
Expected result: 50 of 50 commits pass all applicable checks. A single merged
commit failing (i) falsifies the enforcement claim of Section 1; a single
prompt commit failing (ii) falsifies the genealogy claim of Section 3.1.
