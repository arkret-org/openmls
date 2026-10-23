# Arkret maintenance branch

Base: upstream OpenMLS commit `3a3e35de3feeca8f6605143c464d5452ae584d43`, the source of the published OpenMLS RustCrypto 0.6.0 package.

This branch backports the three HPKE 0.8 dependency updates from upstream commit `e0b21a70a55a9014b8de2772b36bf3d638adad51` (OpenMLS PR #2261). It preserves OpenMLS package versions, protocol code, serialization, traits, licenses and the existing RustCrypto provider. No cryptographic implementation is modified.

HPKE 0.7 pinned its optional libcrux backend to libcrux-kem 0.0.9. HPKE 0.8 replaces that dependency path, allowing the complete consumer lockfile to pass RUSTSEC-2026-0330 and RUSTSEC-2026-0331 without advisory ignores or manually deleting optional packages.

Consumers pin all used OpenMLS packages to the same complete Git revision so internal path dependencies share one trait identity. No third-party source is vendored into Arkret repositories. The maintenance branch is `arkret/hpke-0.8-audit`; the fork default branch is left unchanged. Remove this fork dependency once a compatible official release includes the update, after running the consumer MLS and conformance suites.
