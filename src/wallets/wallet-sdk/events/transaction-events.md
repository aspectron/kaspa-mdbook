# Transaction Events

Transaction events are posted when a transaction-related activity occurs on the network and is related to your monitored address set or when transactions are submitted via the Wallet SDK.

All transaction-related event data contains an instance of the [`TransactionRecord`](https://kaspa.aspectron.org/docs/classes/TransactionRecord.html). The `data` field in the transaction record has the type [`ITransactionData`](https://kaspa.aspectron.org/docs/interfaces/ITransactionData.html), which changes depending on the type of the transaction event.

Transaction events exist in the following variants:

- `maturity` - The transaction has reached its maturity (the minimum required number of confirmations) and can be considered valid for use.
- `pending` - The transaction has been detected on the network and mined into a block but is not yet considered valid for use.
- `stasis` - This event is emitted only if a coinbase transaction is detected. Transactions identified in `stasis` mode should not be accounted for or communicated to the end user. Stasis transactions may undergo multiple reorg changes; as such, the information in the `stasis` event can be used to track mined transactions and UTXOs, but the wallet balance should not be updated. Eventually, the transaction migrates from the `stasis` to the `pending` state, at which point it should be processed by the wallet. (You can think of `stasis` as debug information for miners.)
- `reorg` - This event indicates that a UTXO has been invalidated due to a network reorg event. This event can generally be ignored, as the wallet will appropriately update its UTXO set in reaction to such an event.
- `discovery` - A discovery event is posted when the wallet starts up and enumerates existing UTXOs that belong to the addresses registered by the client. Please see the [Discovery Events](./discovery-events.md) section for more information on handling transaction discovery.

**NOTE:** Durations used to measure transaction maturity can be configured using the [`UtxoProcessor::setCoinbaseTransactionMaturityDAA()`](https://kaspa.aspectron.org/docs/classes/UtxoProcessor.html#setCoinbaseTransactionMaturityDAA) and [`UtxoProcessor::setUserTransactionMaturityDAA()`](https://kaspa.aspectron.org/docs/classes/UtxoProcessor.html#setUserTransactionMaturityDAA) functions. However, while user transaction maturity is configurable and can be considered valid if mined into a block, coinbase transaction maturity must meet the minimum DAA score of the network coinbase maturity (which is 100 DAA at 1 BPS and 1,000 DAA at 10 BPS).

# Transaction Data Variants

While the name of the event denotes the state of the transaction, the `TransactionRecord.data` field denotes the type of the transaction and the data it contains. In the WASM SDK, the `data` field will contain two subfields: `type`, which will contain the kebab-case name of the data type, and `data`, which will contain the associated transaction data variant as follows:

- [`ITransactionDataReorg`](https://kaspa.aspectron.org/docs/interfaces/ITransactionDataReorg.html) - Reorg data containing UTXOs that were removed.
- [`ITransactionDataIncoming`](https://kaspa.aspectron.org/docs/interfaces/ITransactionDataIncoming.html) - Incoming transaction data.
- [`ITransactionDataStasis`](https://kaspa.aspectron.org/docs/interfaces/ITransactionDataStasis.html) - Coinbase transaction data.
- [`ITransactionDataExternal`](https://kaspa.aspectron.org/docs/interfaces/ITransactionDataExternal.html) - Unknown outgoing transaction* (see below).
- [`ITransactionDataOutgoing`](https://kaspa.aspectron.org/docs/interfaces/ITransactionDataOutgoing.html) - Standard outgoing transaction.
- [`ITransactionDataBatch`](https://kaspa.aspectron.org/docs/interfaces/ITransactionDataBatch.html) - Batch transaction data*.
- [`ITransactionDataTransferIncoming`](https://kaspa.aspectron.org/docs/interfaces/ITransactionDataTransferIncoming.html) - Incoming transfer* (from another UtxoContext).
- [`ITransactionDataTransferOutgoing`](https://kaspa.aspectron.org/docs/interfaces/ITransactionDataTransferOutgoing.html) - Outgoing transfer* (to another UtxoContext).
- [`ITransactionDataChange`](https://kaspa.aspectron.org/docs/interfaces/ITransactionDataChange.html) - Change input from the outgoing transaction*.

While most of these variants are self-explanatory, the following variants need additional explanation:

- [`ITransactionDataExternal`](https://kaspa.aspectron.org/docs/interfaces/ITransactionDataExternal.html) - Indicates that a UTXO has been removed from the monitored set. This can occur only when a transaction is issued from another wallet based on the same private key set. For example, if you import the wallet mnemonic/private key into "Wallet B" and issue a transaction from it (not initiated from "Wallet A"), "Wallet A" will receive such an event.
- [`ITransactionDataBatch`](https://kaspa.aspectron.org/docs/interfaces/ITransactionDataBatch.html) - Indicates that the transaction being processed is a batch transaction. Batch transactions compound UTXOs into a single change output that is then used as a source for the final transaction to the destination.
- [`ITransactionDataTransferIncoming`](https://kaspa.aspectron.org/docs/interfaces/ITransactionDataTransferIncoming.html) - Posted when `UtxoContext` detects a transfer from another `UtxoContext` attached to the same `UtxoProcessor`.
- [`ITransactionDataTransferOutgoing`](https://kaspa.aspectron.org/docs/interfaces/ITransactionDataTransferOutgoing.html) - Posted when `UtxoContext` makes a transfer to another `UtxoContext` attached to the same `UtxoProcessor`.
- [`ITransactionDataChange`](https://kaspa.aspectron.org/docs/interfaces/ITransactionDataChange.html) - Posted when an outgoing transaction is created that contains change. Generally, change transactions do not need to be recorded in the wallet history, as they are the same as the outgoing transaction.

## Rust Documentation

- [`TransactionRecord`](https://docs.rs/kaspa-wallet-core/latest/kaspa_wallet_core/storage/transaction/record/struct.TransactionRecord.html)
- [`TransactionData`](https://docs.rs/kaspa-wallet-core/latest/kaspa_wallet_core/storage/transaction/data/enum.TransactionData.html)

