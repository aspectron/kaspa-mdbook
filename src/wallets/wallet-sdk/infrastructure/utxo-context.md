# UtxoContext

[`UtxoContext`](https://kaspa.aspectron.org/docs/classes/UtxoContext.html) allows you to track address activity on the Kaspa network. When an address is registered with `UtxoContext`, it aggregates all UTXO entries for that address and emits events whenever any activity occurs on these addresses.

The `UtxoContext` constructor accepts the [`IUtxoContextArgs`](https://kaspa.aspectron.org/docs/interfaces/IUtxoContextArgs.html) interface, which can optionally include an `id` parameter. If supplied, this `id` will be included in all notifications emitted by the `UtxoContext` and in the [`ITransactionRecord`](https://kaspa.aspectron.org/docs/interfaces/ITransactionRecord.html) object when transactions occur. _If not provided, a random id will be generated._ This `id` typically [represents an account `id`](../account-ids.md) in the context of a wallet application.

`UtxoContext` maintains a real-time cumulative balance for all addresses registered with it and [`emits balance update notification events`](../events/balance-events.md) when the balance changes.

`UtxoContext` can also be supplied as a UTXO source for the transaction [`Generator`](./generator.md), allowing the `Generator` to create transactions using the UTXO entries it manages.

### IMPORTANT

`UtxoContext` is intended to represent a single account. It is not designed to serve as a global UTXO manager for all addresses in a large wallet (such as an exchange wallet). For such use cases, it is recommended to perform manual UTXO management, as described in the [Direct Node RPC](../../direct-node-rpc.md) section.

### NOTE TO EXCHANGES

If you are building an exchange wallet, it is recommended to use `UtxoContext` for each user account. This allows you to track and isolate each user's activity (address set, balances, transaction records).

## References

### WASM SDK

- [UtxoContext listener example](https://github.com/kaspanet/rusty-kaspa/blob/master/wasm/examples/nodejs/javascript/transactions/utxo-context-listener.js)
- [UtxoContext + Generator example](https://github.com/kaspanet/rusty-kaspa/blob/master/wasm/examples/nodejs/javascript/transactions/utxo-context-generator.js)

### Rust SDK

- [UtxoContext struct](https://docs.rs/kaspa-wallet-core/latest/kaspa_wallet_core/utxo/context/struct.UtxoContext.html)