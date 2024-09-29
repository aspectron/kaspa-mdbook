# Derivations

The Standard Address derivation path for Kaspa is `m/44'/111111'/0'` (with 12 or 24 word BIP-39 seed phrases).

**IMPORTANT:** Please note, legacy wallets such as `wallet.kaspanet.io` and `KDX` use a different derivation path and a non-standard address derivation scheme. These wallets are not BIP-32 compatible and are deprecated.  Rust and WASM SDKs do not support these wallets and integrators should not attempt to integrate with them.  These wallets are being phased out and only a few applications will support their wallet imports, while advising users to migrate to accounts based on the standard derivation path.

## Implementation

There are two methods for key derivation in Rusty Kaspa: 
- `PrivateKeyGenerator` and  `PublicKeyGenerator` helpers.
- `DerivationPath` that can be used to create custom derivation paths.

### WASM SDK

- [PrivateKeyGenerator](https://kaspa.aspectron.org/docs/classes/PrivateKeyGenerator.html) and [PublicKeyGenerator](https://kaspa.aspectron.org/docs/classes/PublicKeyGenerator.html) classes in the WASM SDK that provide key derivation functionality based on the Kaspa derivation path standard.
- [DerivationPath](https://kaspa.aspectron.org/docs/classes/DerivationPath.html) class in the WASM SDK that provides a way to create and manage derivation paths.

### Rust SDK

- The functionality for key derivation is provided in the [`kaspa-wallet-keys`](https://docs.rs/kaspa-wallet-keys/latest/kaspa_wallet_keys/) crate.

## Examples

- [WASM SDK Key Derivation Example](https://github.com/kaspanet/rusty-kaspa/blob/master/wasm/examples/nodejs/javascript/general/derivation.js)