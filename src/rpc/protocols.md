# Protocols

The Rusty Kaspa p2p node supports two protocols, described below:

## gRPC

gRPC is an open-source universal RPC framework. It is designed to be efficient and scalable, with support for multiple programming languages.

Foro the list of gRPC clients please take a look at [https://github.com/grpc-ecosystem/awesome-grpc](https://github.com/grpc-ecosystem/awesome-grpc)

### Benefits

- Wide support across multiple languages and development environments.
- Efficient due to protobuf serialization, which gRPC relies on.

### Drawbacks

- Lack of well-established support for protocol routing infrastructure.
- Rusty Kaspa uses a streaming version of gRPC, which is incompatible with some existing gRPC routing infrastructures.
- While gRPC is intended to be high-performance due to protobuf serialization, much of the data in Rusty Kaspa is passed as hex or string-serialized data, which reduces efficiency. However, this can make integration easier with client-side infrastructure.
- No support in the Rusty Kaspa WASM SDK.

## wRPC

wRPC is a proprietary RPC layer developed in Rust by the members of the Rusty Kaspa development team. It is designed for high efficiency, multi-platform compatibility and uses standard WebSockets for transport.

### Benefits

- Full integration with Rust and WASM SDKs, including support for application load-balancing.
- Easy to use.
- High performance.
- Supports protocol routing infrastructure (it uses standard WebSockets).
- Supports both binary and JSON serialization.
- The JSON encoding follows a WebSocket-framed JSON-RPC-like protocol, making it usable in third-party applications.

### Drawbacks

- Limited support in other languages (currently only supported in Rust and WASM SDKs).

