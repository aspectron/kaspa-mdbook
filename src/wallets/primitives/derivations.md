# Derivations

The Standard Address derivation path for Kaspa is `m/44'/111111'/0'` (with 12 or 24 word BIP-39 seed phrases).

**IMPORTANT:** Please note, legacy wallets such as `wallet.kaspanet.io` and `KDX` use a different derivation path and a non-standard address derivation scheme. These wallets are not BIP-32 compatible and are deprecated.  Rust and WASM SDKs do not support these wallets and integrators should not attempt to integrate with them.  These wallets are being phased out and only a few applications will support their wallet imports, while advising users to migrate to accounts based on the standard derivation path.

## Implementation

Derivations 