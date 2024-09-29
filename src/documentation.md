# Documentation

- [Rusty Kaspa README.md](https://github.com/kaspanet/rusty-kaspa/blob/master/README.md) contains build instructions for the Rusty Kaspa framework.
- [WASM SDK README](https://github.com/kaspanet/rusty-kaspa/blob/master/wasm/README.md) contains build instructions for the WASM SDK as well as instructions on running WASM SDK examples.


## WASM SDK

TypeScript and Rust API documentation is available at the following URLs:

- [WASM TypeScript documentation](https://kaspa.aspectron.org/docs/) (TypeDoc is built from development releases)

## Rust crates

Rust documentation is broken into multiple crates (modules) comprising the Rusty Kaspa framework. Each crate is documented separately and can be accessed using links below.

### Client-side framework

These crates are available to client-side applications.

#### General
- [kaspa-consensus-client](https://docs.rs/kaspa-consensus-client) - client-side transaction primitives
- [kaspa-consensus-core](https://docs.rs/kaspa-consensus-core) - consensus primitives
- [kaspa-consensus-wasm](https://docs.rs/kaspa-consensus-wasm) - consensus primitives for WASM
- [kaspa-hashes](https://docs.rs/kaspa-hashes) - hash functions
- [kaspa-math](https://docs.rs/kaspa-math) - math functions
- [kaspa-metrics-core](https://docs.rs/kaspa-metrics-core) - performance metrics data
- [kaspa-notify](https://docs.rs/kaspa-notify) - notification subsystem
- [kaspa-pow](https://docs.rs/kaspa-pow) - proof-of-work primitives
- [kaspa-txscript](https://docs.rs/kaspa-txscript) - transaction scripts
- [kaspa-txscript-errors](https://docs.rs/kaspa-txscript-errors) - transaction script errors
- [kaspa-utils](https://docs.rs/kaspa-utils) - general utilities and trait extensions

#### Wallet
- [kaspa-addresses](https://docs.rs/kaspa-addresses) - address management
- [kaspa-bip32](https://docs.rs/kaspa-bip32) - BIP32 & BIP39 implementation
- [kaspa-wallet-keys](https://docs.rs/kaspa-wallet-keys) - `secp256k1` key management
- [kaspa-wallet-pskt](https://docs.rs/kaspa-wallet-pskt) - PSKT (Partially Signed Kaspa Transactions)
- [kaspa-wallet-core](https://docs.rs/kaspa-wallet-core) - Wallet SDK & core wallet implementation
- [kaspa-wallet-macros](https://docs.rs/kaspa-wallet-macros) - Wallet macros

#### RPC
- [kaspa-grpc-client](https://docs.rs/kaspa-grpc-client) - gRPC client
- [kaspa-grpc-core](https://docs.rs/kaspa-grpc-core) - gRPC core (used by client and server)
- [kaspa-rpc-core](https://docs.rs/kaspa-rpc-core) - Kaspa Node RPC API
- [kaspa-rpc-macros](https://docs.rs/kaspa-rpc-macros) - RPC macros
- [kaspa-wrpc-client](https://docs.rs/kaspa-wrpc-client) - wRPC client
- [kaspa-wrpc-wasm](https://docs.rs/kaspa-wrpc-wasm) - wRPC WASM client

#### WASM
- [kaspa-wasm](https://docs.rs/kaspa-wasm) - WASM SDK
- [kaspa-wasm-core](https://docs.rs/kaspa-wasm-core) - Base WASM type declarations

#### Applications
- [kaspa-cli](https://docs.rs/kaspa-cli) - Kaspa command line RPC interface and wallet

### Rusty Kaspa Node framework

These crates comprize the Rusty Kaspa node framework. They can be used in Rust native applications only.

#### Consensus & p2p
- [kaspa-addressmanager](https://docs.rs/kaspa-addressmanager) - p2p address management
- [kaspa-alloc](https://docs.rs/kaspa-alloc) - memory allocator
- [kaspa-connectionmanager](https://docs.rs/kaspa-connectionmanager) - p2p connection management
- [kaspa-consensus-notify](https://docs.rs/kaspa-consensus-notify) - consensus notifications
- [kaspa-consensus](https://docs.rs/kaspa-consensus) - consensus
- [kaspa-consensusmanager](https://docs.rs/kaspa-consensusmanager) - consensus
- [kaspa-core](https://docs.rs/kaspa-core) - node runtime management
- [kaspa-database](https://docs.rs/kaspa-database) - database
- [kaspa-index-core](https://docs.rs/kaspa-index-core) - UTXO indexing
- [kaspa-index-processor](https://docs.rs/kaspa-index-processor) - UTXO indexing
- [kaspa-merkle](https://docs.rs/kaspa-merkle) - Merkle tree processing
- [kaspa-mining](https://docs.rs/kaspa-mining) - PoW algorithms
- [kaspa-mining-errors](https://docs.rs/kaspa-mining-errors) - PoW errors
- [kaspa-muhash](https://docs.rs/kaspa-muhash) - MuHash
- [kaspa-p2p-flows](https://docs.rs/kaspa-p2p-flows) - p2p message flows
- [kaspa-p2p-lib](https://docs.rs/kaspa-p2p-lib) - p2p library
- [kaspa-perf-monitor](https://docs.rs/kaspa-perf-monitor) - performance monitoring
- [kaspa-utils-tower](https://docs.rs/kaspa-utils-tower) - gRPC tower middleware
- [kaspa-utxoindex](https://docs.rs/kaspa-utxoindex) - UTXO indexing

#### RPC
- [kaspa-grpc-server](https://docs.rs/kaspa-grpc-server) - gRPC server
- [kaspa-rpc-service](https://docs.rs/kaspa-rpc-service) - Kaspa RPC service
- [kaspa-wrpc-server](https://docs.rs/kaspa-wrpc-server) - wRPC server

#### Applications
- [kaspad](https://docs.rs/kaspad) - Kaspa p2p node daemon

