# Discovery Events

When registering a new address with `UtxoContext`, the `UtxoContext` performs a scan for any UTXOs that belong to this address. This process is known as _Transaction Discovery_.

UTXOs detected during _Transaction Discovery_ may represent UTXOs previously seen by the wallet or UTXOs that arrived during the wallet's downtime. When receiving the `discovery` event, the client should take the transaction ID and check the transaction history to see if a transaction with that ID exists. If it does, the wallet can disregard the transaction (this means the wallet has seen it before); if it doesn't, the wallet should treat this UTXO as new (store it in the database and inform the wallet/account user of a new transaction).

## Under the Hood

When receiving new addresses for monitoring, `UtxoContext` registers for transaction event notifications against these addresses using `subscribeUtxosChanged()`, and then performs `getUtxosByAddresses()` to enumerate the matching UTXOs. All UTXOs detected during this enumeration phase are posted as `discovery` events.

## External access

**IMPORTANT:** It is crucial to understand the implications of sharing private keys between multiple wallets. If two wallets share the same private key and one wallet consumes incoming UTXOs to create transactions, the wallet that was offline will not be able to see these transactions once it comes back online, as the UTXOs that came in will have already been consumed by the other wallet. The only way to track this type of history is via Explorer APIs or DAG block aggregation. Therefore, to maintain a consistent transaction history, you should avoid sharing private keys between wallets.