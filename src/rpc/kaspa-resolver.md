# Kaspa Resolver

Kaspa Resolver is an ALB (application load balancer) that can connect to a set of Rusty Kaspa p2p nodes and and then be queried via a REST API endpoint for the node with least active client connections.

Kaspa Resolver is the backbone of the Public Node Network (PNN) and is used to balance the load between the public nodes. Kaspa Resolver can also be used to create private node clusters.

Kaspa Resolver API is integrated directly within Rust and WASM SDKs, specifically within the `RpcClient` class, where instead of passing the endpoint URL, you can pass the `Resolver` object that will be used to obtain the node endpoint each time the client connects. If the node becomes unavailable, the client will automatically switch to the next best available node.

GitHub repository: [https://github.com/aspectron/kaspa-resolver](https://github.com/aspectron/kaspa-resolver)

