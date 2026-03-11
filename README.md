## Convergence Suite (CS)

### Convergence Suite is the canonical convergence authority for Covenant Systems instruments.

It defines and distributes deterministic test vectors and verification rules that allow independent implementations of ecosystem laws to prove they produce identical results.

Convergence Suite ensures that different instruments implementing the same protocols remain deterministically compatible.

Purpose

In a distributed ecosystem of independent instruments, protocol drift is a serious risk.

Convergence Suite solves this by providing:

• canonical schemas
• canonical vector sets
• canonical PASS / FAIL expectations
• deterministic verification runners
• reproducible freeze manifests
• cryptographic verification receipts

An instrument does not claim compliance.

It proves convergence by passing the Convergence Suite vectors.

Laws Currently Covered
CanonJSON v1

Deterministic JSON canonicalization rules.

Guarantees:

• stable key ordering
• deterministic encoding
• identical byte representation across implementations

CanonJSON ensures that hashing operations performed across instruments produce identical results.

### Packet Constitution v1 

---

Directory packet structure used across Covenant Systems.

Canonical packet layout:

manifest.json
packet_id.txt
sha256sums.txt
payload/

Encoding rules:

UTF-8
no BOM
LF line endings

PacketId derivation:

PacketId = SHA256(canonical manifest bytes without packet_id field)

The Convergence Suite vectors prove that implementations of Packet Constitution produce identical validation results.

Repository Structure
docs/
freeze/
proofs/
reports/
scripts/
vectors/

Key components:

Scripts
scripts/cs_run_v1.ps1
scripts/selftest_cs_v1.ps1
scripts/_RUN_cs_full_green_v1.ps1
scripts/_RUN_cs_freeze_release_v1.ps1
Vectors
vectors/canonjson/v1
vectors/packet_constitution/v1_optionA
Deterministic Outputs
reports/cs_convergence_report.v1.json
proofs/receipts/cs.ndjson
proofs/receipts/cs.release.v1.ndjson
freeze/CS_FREEZE_MANIFEST.v1.txt
Deterministic Runner

The full verification pipeline is executed using:

scripts/_RUN_cs_full_green_v1.ps1

Pipeline:

parse-gate
selftests
vector verification
receipts
FULL_GREEN

Expected output:

FULL_GREEN_OK
Freeze Release Runner

To produce a deterministic release snapshot:

scripts/_RUN_cs_freeze_release_v1.ps1

This runner:

executes FULL_GREEN verification

hashes the frozen surface

produces a freeze manifest

emits deterministic receipts

Outputs:

freeze/CS_FREEZE_MANIFEST.v1.txt
proofs/receipts/cs.release.v1.ndjson

Expected output:

CS_FREEZE_OK
Adoption Rule

Any Covenant Systems instrument reaching Tier-0 must prove Convergence Suite compatibility.

Tier-0 definition:

instrument FULL_GREEN
+
CS_CONVERGENCE_PASS
=
Tier-0 instrument

If CS vectors fail:

instrument is non-convergent
Integration

Instruments adopt Convergence Suite by:

loading the canonical vector sets

running their own implementation

verifying results match CS expectations

producing a convergence report


---

Example report:

instrument_cs_convergence_report.v1.json

Example structure:

{
  "instrument": "hashcanon",
  "instrument_version": "v1",
  "convergence_suite_version": "v1",
  "cases_total": 10,
  "cases_pass": 10,
  "cases_fail": 0,
  "convergence": "PASS"
}

---

Role in Covenant Systems

Convergence Suite acts as the protocol convergence layer in the Covenant Systems architecture.

Constellation
   │
Covenant Systems
   │
Convergence Suite
   │
HashCanon
TRIAD
WatchTower
Covenant Gate
PacketPuncture

It ensures all instruments implementing ecosystem protocols remain deterministic and compatible.

---

Definition of Done (Current Release)

The current Convergence Suite release is considered sealed when:

FULL_GREEN_OK
CS_FREEZE_OK

are produced on a clean machine and rerunning the freeze process produces no repository drift.

---

## License

TBD

## Status

Convergence Suite v1

Integration ready for Covenant Systems instruments.
