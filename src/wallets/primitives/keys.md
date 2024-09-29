# Key Management

Rusty Kaspa uses [secp256k1](https://crates.io/crates/secp256k1) elliptic curve cryptography library in conjunction with a customized [kaspa-bip32](https://crates.io/crates/kaspa-bip32) crate that was forked from [bip32](https://crates.io/crates/bip32) crate in order to extend it's serialization and WASM capabilities.

## Examples

WASM SDK examples of use can be found within other examples in the SDK repository:

- [WASM SDK Key Derivation Example](https://github.com/kaspanet/rusty-kaspa/blob/master/wasm/examples/nodejs/javascript/general/derivation.js)
- [WASM SDK Address Creation Example](https://github.com/kaspanet/rusty-kaspa/blob/master/wasm/examples/nodejs/javascript/general/addresses.js)
