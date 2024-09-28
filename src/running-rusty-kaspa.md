# Building from source

Please follow up to date build instructions in the Rusty Kaspa [README](https://github.com/kaspanet/rusty-kaspa/blob/master/README.md)

# Docker

Rusty Kaspa images based on Alpine linux can be found here:
- Docker build scripts: [https://github.com/supertypo/docker-rusty-kaspa](https://github.com/supertypo/docker-rusty-kaspa)
- Published images: [https://hub.docker.com/r/supertypo/rusty-kaspad](https://hub.docker.com/r/supertypo/rusty-kaspad)

# Running Rusty Kaspa p2p Node

A typical execution arguments for a `mainnet` Rusty Kaspa p2p node are as follows:

```
cargo run --release -- --utxoindex --disable-upnp --maxinpeers=64 --perf-metrics --outpeers=32 --yes --perf-metrics-interval-sec=1 --rpclisten=127.0.0.1:16110 --rpclisten-borsh=127.0.0.1:17110 --rpclisten-json=127.0.0.1:18110
```

To configure the node for `testnet`, simply add the `--testnet` flag. 

This will power up the node connecting it to the currently default `testnet-10` network.  

To connect to an alternate testnet network, use the `--testnet` flag followed by `--netsuffix=<id>` where the `<id>` is the testnet id. For example, to connect to `testnet-11`, use `--testnet --netsuffix=11`.

Please see the [RPC ports](./rpc/ports.md) documentation for more information on RPC port selection.

# UTXO Index

*UTXO Index* is an auxiliary database that enables the Kaspa node to perform additional tracking of transaction addresses. This allows you to setup notifications for when a new transaction matching your addresses has been detected.

If *UTXO Index* is not enabled, RPC calls requesting *UTXO By Addresses* information will result in an error.

To enable *UTXO Index* run the node with the `--utxoindex` command-line argument.


# Systemd Service

```toml
[Unit]
Description=Kaspad p2p Node (mainnet)
 
[Service]
User=aspect
ExecStart=/home/user/rusty-kaspa/target/release/kaspad --utxoindex --disable-upnp --maxinpeers=64 --perf-metrics --outpeers=32 --yes --perf-metrics-interval-sec=1 --rpclisten=127.0.0.1:16110 --rpclisten-borsh=127.0.0.1:17110 --rpclisten-json=127.0.0.1:18110
RestartSec=5
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

