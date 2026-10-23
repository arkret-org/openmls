# Arkret maintenance branch

Base: upstream OpenMLS 0.9.1 commit `1762090a4523cdd241f454b4058e91b64bbdc6de`. Its RustCrypto 0.6.0 backend and shared traits have the same source as the published backend at `3a3e35de3feeca8f6605143c464d5452ae584d43`.

This branch backports the HPKE 0.8 dependency updates for both RustCrypto and the optional libcrux provider, plus the upstream HMAC output-buffer API adaptation, from upstream commit `e0b21a70a55a9014b8de2772b36bf3d638adad51` (OpenMLS PR #2261). It preserves OpenMLS package versions, protocol code, serialization, traits, licenses and the existing RustCrypto provider. No algorithm, protocol, signature transcript or wire encoding is modified; the HMAC call adaptation is taken directly from upstream.

HPKE 0.7 pinned its optional libcrux backend to libcrux-kem 0.0.9. HPKE 0.8 replaces that dependency path, allowing the complete consumer lockfile to pass RUSTSEC-2026-0330 and RUSTSEC-2026-0331 without advisory ignores or manually deleting optional packages.

Consumers pin all used OpenMLS packages to the same complete Git revision so internal path dependencies share one trait identity. No third-party source is vendored into Arkret repositories. The maintenance branch is `arkret/hpke-0.8-audit`; the fork default branch is left unchanged. Remove this fork dependency once a compatible official release includes the update, after running the consumer MLS and conformance suites.
