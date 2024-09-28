# Direct Node RPC

The Wallet SDK and Wallet API are built using the direct node RPC. You can use direct node RPC to interface directly with the Kaspa network, however doing so requires additional logic and processing which can become taxing for the developer.

There are two primary API methods that are used with interfacing with the node to obtain transaction information:

- [`getUtxosByAddresses()`](https://kaspa.aspectron.org/docs/classes/RpcClient.html#getUtxosByAddresses) method - provides a list of UTXOs for a specific list of addresses
- [`subscribeUtxosChanges()`](https://kaspa.aspectron.org/docs/classes/RpcClient.html#subscribeUtxosChanged) event subscription - given a set of Kaspa addresses, you will receive transaction notifications against UTXOs affecting these addresses.

NOTE: When using these two methods, you should subscribe for notifications first and then call `getUtxosByAddresses()` - this sequence ensures that you will not miss any notifications while processing an existing set of UTXOs.

When using [`RpcClient`](https://kaspa.aspectron.org/docs/classes/RpcClient.html) directly, in addition to subscribing to events, you must also install your own event listener callback using [`addEventListener`](https://kaspa.aspectron.org/docs/classes/RpcClient.html#addEventListener) method. This callback will be called for any new subscription.

## Registering for Event Notifications

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

