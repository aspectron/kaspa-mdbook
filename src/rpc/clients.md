# Clients

## WASM SDK - wRPC

- [RpcClient class](https://aspectron.com/docs/kaspa-wasm/RpcClient.html) - main RPC class for interacting with the node
- [Resolver class](https://kaspa.aspectron.org/docs/classes/Resolver.html) - class for resolving public nodes against PNN

### Examples

- [RpcClient methods](https://github.com/kaspanet/rusty-kaspa/blob/master/wasm/examples/nodejs/javascript/general/rpc.js)
- [RpcClient subscriptions](https://github.com/kaspanet/rusty-kaspa/blob/master/wasm/examples/nodejs/javascript/general/subscribe-daa-score.js)


## Rust SDK - wRPC

- [KaspaRpcClient struct](https://docs.rs/kaspa-wrpc-client/latest/kaspa_wrpc_client/client/struct.KaspaRpcClient.html) - main wRPC struct for interfacing with the node
- [RpcApi trait](https://docs.rs/kaspa-wrpc-client/latest/kaspa_wrpc_client/prelude/api/rpc/trait.RpcApi.html) - trait that defines RPC methods
- [Resolver struct](https://docs.rs/kaspa-wrpc-client/latest/kaspa_wrpc_client/resolver/struct.Resolver.html) - struct for resolving public nodes against PNN

### Examples

- [wRPC client methods](https://github.com/kaspanet/rusty-kaspa/blob/master/rpc/wrpc/examples/simple_client/src/main.rs)
- [wRPC client subscriptions](https://github.com/kaspanet/rusty-kaspa/blob/master/rpc/wrpc/examples/subscriber/src/main.rs)

## Rust SDK - gRPC

- [GrpcClient struct](https://github.com/kaspanet/rusty-kaspa/blob/master/rpc/grpc/client/src/lib.rs) implementation.

## gRPC `.proto` definitions

gRPC integration provides `.proto` files that can be used to generate client code in multiple languages. gRPC `.proto` files `messages.proto` and `rpc.proto` can be found in the Rusty Kaspa repository at [https://github.com/kaspanet/rusty-kaspa/tree/master/rpc/grpc/core/proto](https://github.com/kaspanet/rusty-kaspa/tree/master/rpc/grpc/core/proto).

