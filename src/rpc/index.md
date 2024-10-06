# RPC

Rusty Kaspa integrates support for the following RPC protocols:
- gRPC (streaming gRPC, protobuf encoding)
- wRPC (WebSocket-framed, JSON-RPC-like encoding)
- wRPC (WebSocket-framed, high-performance Borsh encoding)

For comparison of these protocols and client documentation, please see the [Protocols](./protocols.md) and [Clients](./clients.md) sections.

#### IMPORTANT

_When subscribing to event notifications against the Kaspa node, the subscription lifetime is tied to the RPC client connection. If the connection is lost and reconnected, the subscription will be lost. You will have to resubscribe for notifications against the node._

_The best way to handle this is to listen to RPC events such as `connect` and subscribe to node notifications from within this handler._
