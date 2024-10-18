# SDK Examples

## Rust SDK

Rust SDK is much more complex since the entire Rusty Kaspa project is written in Rust. As such, the entire framework can serve as a reference.

A few key points can be found here:

- [Connecting to wRPC](../rpc/connecting-wrpc.md) - examples and specificities about connecting via wRPC
- [wRPC client examples](https://github.com/kaspanet/rusty-kaspa/tree/master/rpc/wrpc/examples) - examples on connecting to a Kaspa node using wRPC and executing RPC methods as well as subscribing to and processing notifications.
- [PSKT multisig example](https://github.com/kaspanet/rusty-kaspa/tree/master/wallet/pskt/examples) - a multisig example that uses PSKT primitives.
- [Kaspa Cli](https://github.com/kaspanet/rusty-kaspa/tree/master/cli) - a project that uses the Wallet subsystem as well as the RPC subsystem.
- [Kaspa NG](https://github.com/aspectron/kaspa-ng) - Kaspa NG is built using Rusty Kaspa SDK and is a good example of a full-fledged Rust application built using Rusty Kaspa.
