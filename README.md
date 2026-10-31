# slh-dsa-cryptol

A formally checked Cryptol specification of SLH-DSA, the stateless hash based signature scheme in FIPS 205, written for the NSA Foundation framework.

SLH-DSA is one of the post quantum signature standards NIST published in FIPS 205, and the Foundation repository of formal cryptographic specifications does not yet cover any post quantum scheme. This fills that gap. SLH-DSA is built entirely on the hash functions Foundation already specifies, so the specification reuses Foundation's own SHAKE and Keccak modules and is laid out to drop into its algorithms directory as algorithms/SLH_DSA.

## What is here

Seven modules that follow FIPS 205 section by section.

- HashesShake, the tweakable hash and pseudorandom functions for the SHAKE parameter sets, section 11.2.
- Address, the ADRS structure and its member functions, sections 4.2 and 4.3.
- WOTS, the one time signature, section 5.
- FORS, the few time signature, section 8.
- XMSS, the Merkle tree over WOTS public keys, section 6.
- HyperTree, the composition of XMSS across layers, section 7.
- SLH_DSA, key generation, signing and verification, sections 9 and 10.

## Assurance

- Every file loads under the Foundation load all check.
- The six SHAKE hash functions are proven byte equal to a direct SHAKE256 computation.
- The one time, few time, Merkle and whole scheme signatures each carry a proof that a signature recovers the signer's public key, so verification accepts a genuine signature.
- The tree and signing routines were ported function by function from an implementation validated against the NIST ACVP vectors, so the address indexing and the digest split match the standard exactly.

The test properties are in algorithms/SLH_DSA/tests.

## License

Apache 2.0. See LICENSE.
