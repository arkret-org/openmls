# Arkret RustCrypto maintenance

Branch `arkret/rustcrypto-constant-time` continues `arkret/hpke-0.8-audit`
from commit c8baa074b65053fd21fc2711ab15870a1d092b94 in this OpenMLS fork.
The original source remains https://github.com/openmls/openmls and retains its MIT license.

RUSTSEC-2026-0387 (https://rustsec.org/advisories/RUSTSEC-2026-0387.html)
requires crypto-bigint >=0.7.6. The p256/p384 0.13 signature dependencies
retained crypto-bigint 0.5, so both credential generation and the RustCrypto
provider now use p256/p384 0.14. SEC1 public-key and DER signature wire
formats remain unchanged. The provider adapts its existing cryptographic RNG
to rand_core 0.10; credential generation propagates operating-system RNG errors.

Validation: the two owning crates run their library tests, including P-256,
P-384 and Ed25519 signature generation, verification and tampering rejection.
Consumers must pin this fork to the reviewed full commit SHA and refresh locks.
