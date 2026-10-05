# corpus-mitre-attck

Per-technique (ID-level) text mirror of the MITRE ATT&CK knowledge base, one
plain-text file per technique and sub-technique (`techniques/<ID>.txt`). Built
so that retrieval over ATT&CK content hits the technique document itself
instead of a giant STIX bundle.

## Source

- Upstream: https://github.com/mitre-attack/attack-stix-data
- Pinned commit: `6cda5ad8462c79e14fbb872f4e09059b18e0cfc4` ("feat: add ATT&CK v19.2", 2026-08-05)
- Extraction date: 2026-10-05
- Licence: MITRE Free License (permissive use with attribution) — see [LICENSE](LICENSE)

## Bundles used

| Bundle file | ATT&CK version | SHA-256 |
|---|---|---|
| enterprise-attack/enterprise-attack.json | 19.2 | dc1639caa5501d720e280cf1cbd8fbe009884a0c9b3e6e9ed9d0c25166c3d8f4 |
| mobile-attack/mobile-attack.json | 19.2 | acfa5ca2d93484476f79bf38590e2b55bb675fc0ce85e76bffa0af2c82dada64 |
| ics-attack/ics-attack.json | 19.2 | 08b83d2cea6b6d6752468ef0e62e2ab2a53c9443ef72c439ecccb07ab9e89da9 |

## Contents

- `techniques/<ID>.txt` — 1166 files, 1806997 bytes total
- `MANIFEST.tsv` — path, technique ID, name for every file
- `LICENSE` — MITRE Free License with provenance note

Counts by domain: enterprise-attack 858, mobile-attack 190, ics-attack 118
(total 1166). Of these, 558 are sub-techniques, 211 are revoked and
37 are deprecated; revoked/deprecated objects are included and marked in the
file header, because they remain the authoritative answer for their ID.

## File format

Each file is plain text: a header line (ID, name, domain, matrix), then
DESCRIPTION (full STIX description), KILL CHAIN PHASES, PLATFORMS,
PERMISSIONS REQUIRED / EFFECTIVE PERMISSIONS / DATA SOURCES (only when present
on the object), MITIGATIONS (resolved from `mitigates` relationships to
course-of-action objects in the same bundle), and DETECTION STRATEGIES
(resolved from `detects` relationships to x-mitre-detection-strategy objects).
No JSON syntax appears in the files.

Notes on the v19.2 STIX model: the classic `x_mitre_detection`,
`x_mitre_data_sources`, and permissions fields no longer exist on
attack-pattern objects in this release, so those sections are absent;
detection guidance is carried by x-mitre-detection-strategy objects and is
surfaced above. Procedure examples (`uses` relationships from groups/software)
are intentionally omitted. 14 revoked mobile techniques have no description
text upstream; their files carry the header and status only.

Regenerate with `xerj`'s reference-coding corpus tooling or any STIX parser;
the three bundles above are the only inputs.
