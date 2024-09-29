# Applications

The Kaspa ecosystem contains a number of applications that are useful for testing during development.

Please note that applications using the [Wallet API](./wallets/wallet-api/index.md) can interoperate with each other (i.e., they can open the same wallet files). There are currently two wallets based on the [Wallet API](./wallets/wallet-api/index.md):

## Kaspa CLI

[Kaspa CLI](https://crates.io/crates/kaspa-cli) is a terminal interface that includes the Kaspa Wallet and can be used to execute various RPC commands against a node.

#### Installation
```bash
cargo install kaspa-cli
kaspa-cli
```
Once running, you can type `help` or `settings` commands. 

By default, `kaspa-cli` connects to the Public Node Network (PNN). You can use `server <wRPC-url>` to change the RPC endpoint and `network` to change the network type.

## Kaspa NG

[Kaspa NG](https://aspectron.org/en/projects/kaspa-ng.html) is an interactive, multi-platform application developed in Rust on top of the Rusty Kaspa framework. It can be run as a desktop wallet or a web wallet. Kaspa NG incorporates the Rusty Kaspa p2p node when running as a desktop application and can also connect to PNN.

When running a local Rusty Kaspa p2p node, other applications using wRPC can connect to it locally.

In addition to the wallet, Kaspa NG also includes node performance metrics tracking and a BlockDAG visualizer.

### Releases

- [Desktop binary releases on the Kaspa NG GitHub repository](https://github.com/aspectron/kaspa-ng/releases/)
- The web instance can be accessed at [https://kaspa-ng.org](https://kaspa-ng.org)

