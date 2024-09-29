# Direct Node RPC

The Wallet SDK and Wallet API are built using the direct node RPC. You can use direct node RPC to interface directly with the Kaspa network, however doing so requires additional logic and processing which can become taxing for the developer.

There are two primary API methods that are used with interfacing with the node to obtain transaction information:

- [`getUtxosByAddresses()`](https://kaspa.aspectron.org/docs/classes/RpcClient.html#getUtxosByAddresses) method - provides a list of UTXOs for a specific list of addresses
- [`subscribeUtxosChanges()`](https://kaspa.aspectron.org/docs/classes/RpcClient.html#subscribeUtxosChanged) event subscription - given a set of Kaspa addresses, you will receive transaction notifications against UTXOs affecting these addresses.

NOTE: When using these two methods, you should subscribe for notifications first and then call `getUtxosByAddresses()` - this sequence ensures that you will not miss any notifications while processing an existing set of UTXOs.

When using [`RpcClient`](https://kaspa.aspectron.org/docs/classes/RpcClient.html) directly, in addition to subscribing to events, you must also install your own event listener callback using [`addEventListener`](https://kaspa.aspectron.org/docs/classes/RpcClient.html#addEventListener) method. This callback will be called for any new subscription.

## Subscribing for Event Notifications

### WASM SDK

For each instance of the `RpcClient`, you must register an event listener once, but you must subscribe for node notifications each time you connect to the node - on connection, you have to inform the node that you are interested in specific events so that the node can start posting these events to your `RpcClient` instance.

[`addEventListener`](https://kaspa.aspectron.org/docs/classes/RpcClient.html#addEventListener) can be used with a single callback to receive all notifications or with an event name to receive only specific notifications.

```typescript
// consume all events
rpc.addEventListener((event) => {
    console.log(event);
});

// consume only utxos-changes events
rpc.addEventListener("utxos-changes", (event) => {
    console.log(event);
});
```

### Rust SDK (wRPC only)

In the Rust SDK, event notifications are provided via [async channels](https://docs.rs/async-channel/latest/async_channel/), which transport the [Notification](https://docs.rs/kaspa-wrpc-client/latest/kaspa_wrpc_client/prelude/enum.Notification.html) enum. A clone of the notification channel can be obtained by calling [`KaspaRpcClient::notification_channel_receiver()`](https://docs.rs/kaspa-wrpc-client/latest/kaspa_wrpc_client/client/struct.KaspaRpcClient.html#method.notification_channel_receiver).

Event notification handling in the Rust SDK is somewhat more complex due to the multi-layered nature of the RPC stack. There are three layers involved in handling event notifications:

1. **Invoking a subscription request**: This triggers the node to start posting events.
2. **Activating an internal notification listener**: This is done via the `register_notification_listener` method, which is part of the core RPC notification subsystem.
3. **Consuming notifications**: This is done via the receiver channel obtained from the [`KaspaRpcClient::notification_channel_receiver()`](https://docs.rs/kaspa-wrpc-client/latest/kaspa_wrpc_client/client/struct.KaspaRpcClient.html#method.notification_channel_receiver) method.

This layering exists because the RPC notification subsystem is integral to the Kaspa Consensus processor (used internally by the Rusty Kaspa p2p node) and the same primitives are also utilized in the client-side instance.

### RPC Connection and Disconnection Events

Note that RPC connection and disconnection events are managed via side channels known as `RpcCtl` channels, which are separate from the notification subsystem. A clone of the `RpcCtl` channel can be obtained by calling the [`KaspaRpcClient::ctl_multiplexer()`](https://docs.rs/kaspa-wrpc-client/latest/kaspa_wrpc_client/client/struct.KaspaRpcClient.html#method.ctl_multiplexer) method and creating a new receiver channel from it. The [Multiplexer](https://docs.rs/workflow-core/latest/workflow_core/channel/struct.Multiplexer.html) is a broadcast channel (MPMC) designed to handle multiple consumers.

```rust
// Create a new receiver channel bound to the RpcCtl multiplexer
let ctl_channel = rpc.clt_multiplexer().channel();
```

For a detailed example of how notifications are handled in the Rust SDK, refer to the [Rust wRPC subscriber example](https://github.com/kaspanet/rusty-kaspa/blob/master/rpc/wrpc/examples/subscriber/src/main.rs).

