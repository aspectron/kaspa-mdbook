# Addresses

## Address Format

A kaspa address contains 3 components:
- Network Type
- Public Key Version (type)
- Public Key

The string representation of a kaspa address contains the network type and a `bech32` encoded public key suffixed with a checksum.

#### Example of a network address:

#### Mainnet
```
kaspa:qpauqsvk7yf9unexwmxsnmg547mhyga37csh0kj53q6xxgl24ydxjsgzthw5j
```

#### Testnet
```
kaspatest:qqnapngv3zxp305qf06w6hpzmyxtx2r99jjhs04lu980xdyd2ulwwmx9evrfz
```

### References
- [`Address` class in WASM SDK](https://kaspa.aspectron.org/docs/classes/Address.html)
- [WASM SDK JavaScript example](https://github.com/kaspanet/rusty-kaspa/blob/master/wasm/examples/nodejs/javascript/general/addresses.js)
- [WASM SDK TypeScript example](https://github.com/kaspanet/rusty-kaspa/blob/master/wasm/examples/nodejs/typescript/src/address.ts)
- [Rust source code (implementation)](https://github.com/kaspanet/rusty-kaspa/blob/master/crypto/addresses/src/lib.rs)
- [Rust SDK `kaspa-addresses` crate](https://docs.rs/kaspa-addresses/) 
