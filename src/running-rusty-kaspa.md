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

Please see the [RPC ports](./rpc/ports.md) section for more information on RPC port selection.

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

# Command line arguments

```
Kaspa full node daemon (rusty-kaspa) v0.15.2

Usage: kaspad [OPTIONS]

Options:
  -C, --configfile <CONFIG_FILE>
          Path of config file.
  -b, --appdir <DATA_DIR>
          Directory to store data.
      --logdir <LOG_DIR>
          Directory to log output.
      --nologfiles
          Disable logging to files.
  -t, --async-threads=<async_threads>
          Specify number of async threads (default: 10).
  -d, --loglevel=<LEVEL>
          Logging level for all subsystems {off, error, warn, info, debug, trace}
          -- You may also specify <subsystem>=<level>,<subsystem2>=<level>,... to set the log level for individual subsystems. [default: info]
      --rpclisten[=<IP[:PORT]>]
          Interface:port to listen for gRPC connections (default port: 16110, testnet: 16210).
      --rpclisten-borsh[=<IP[:PORT]>]
          Interface:port to listen for wRPC Borsh connections (default port: 17110, testnet: 17210).
      --rpclisten-json[=<IP[:PORT]>]
          Interface:port to listen for wRPC JSON connections (default port: 18110, testnet: 18210).
      --unsaferpc
          Enable RPC commands which affect the state of the node
      --connect=<IP[:PORT]>
          Connect only to the specified peers at startup.
      --addpeer=<IP[:PORT]>
          Add peers to connect with at startup.
      --listen=<IP[:PORT]>
          Add an interface:port to listen for connections (default all interfaces port: 16111, testnet: 16211).
      --outpeers=<outpeers>
          Target number of outbound peers (default: 8).
      --maxinpeers=<maxinpeers>
          Max number of inbound peers (default: 128).
      --rpcmaxclients=<rpcmaxclients>
          Max number of RPC clients for standard connections (default: 128).
      --reset-db
          Reset database before starting node. It's needed when switching between subnetworks.
      --enable-unsynced-mining
          Allow the node to accept blocks from RPC while not synced (this flag is mainly used for testing)
      --utxoindex
          Enable the UTXO index
      --max-tracked-addresses=<max-tracked-addresses>
          Max (preallocated) number of addresses being tracked for UTXO changed events (default: 0, maximum: 14680063). 
          Setting to 0 prevents the preallocation and sets the maximum to 1835007, leading to 0 memory footprint as long as unused but to sub-optimal footprint if used.
      --testnet
          Use the test network
      --netsuffix=<netsuffix>
          Testnet network suffix number
      --devnet
          Use the development test network
      --simnet
          Use the simulation test network
      --archival
          Run as an archival node: avoids deleting old block data when moving the pruning point (Warning: heavy disk usage)
      --sanity
          Enable various sanity checks which might be compute-intensive (mostly performed during pruning)
      --yes
          Answer yes to all interactive console questions
      --uacomment=<user_agent_comments>
          Comment to add to the user agent -- See BIP 14 for more information.
      --externalip=<externalip>
          Add a socket address(ip:port) to the list of local addresses we claim to listen on to peers
      --perf-metrics
          Enable performance metrics: cpu, memory, disk io usage
      --perf-metrics-interval-sec=<perf-metrics-interval-sec>
          Interval in seconds for performance metrics collection.
      --disable-upnp
          Disable upnp
      --nodnsseed
          Disable DNS seeding for peers
      --nogrpc
          Disable gRPC server
      --ram-scale=<ram-scale>
          Apply a scale factor to memory allocation bounds. Nodes with limited RAM (~4-8GB) should set this to ~0.3-0.5 respectively. Nodes with
          a large RAM (~64GB) can set this value to ~3.0-4.0 and gain superior performance especially for syncing peers faster
  -h, --help
          Print help
  -V, --version
          Print version
```