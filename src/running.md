# Running

There are currently two full-node implementations for Kaspa, the original, developed in Golang and a new one called 'Rusty Kaspa', developed in Rust.  The Rust implementation has higher performance and it is expected that the Golang implementation will be deprecated.

Rust WASM framework can connect to the Rusty Kaspa node directly or to the Golang node via a Proxy.

# Running an RPC proxy

RPC proxy is required for Golang node implementation only.

Download the latest binaries from the WASM release page at [https://aspectron.com/projects/kaspa-wasm.html](https://aspectron.com/projects/kaspa-wasm.html)

Simply run `kaspa-wrpc-proxy`. By default, it will attempt to connect to the kaspad node on the local network. 

# Building from source

Please follow up to date build instructions at [https://github.com/kaspanet/rusty-kaspa/blob/master/README.md](https://github.com/kaspanet/rusty-kaspa/blob/master/README.md)

If your envifonment is already setup, you can build the proxy as follows:
```bash
cd rpc/wrpc/proxy
cargo build --release
cargo run --release
```

The resulting binary will be located in the workspace `target/` directory.

# Docker

Rusty Kaspa images based on Alpine linux can be found here:
- Docker build scripts: https://github.com/supertypo/docker-rusty-kaspa
- Published images: https://hub.docker.com/r/supertypo/rusty-kaspad