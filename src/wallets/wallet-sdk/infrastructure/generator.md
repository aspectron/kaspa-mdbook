# Generator

The Transaction [`Generator`](https://kaspa.aspectron.org/docs/classes/Generator.html) simplifies the transaction creation process by:

- Dynamically calculating transaction mass.
- Accounting for custom transaction Fee Rates.
- Automatically creating daisy-chained (batch/sweep) transactions if your UTXO set exceeds the maximum mass allowed in a single transaction.
- Calculating the correct transaction change output.

The Transaction Generator functions as an iterator, producing a [`PendingTransaction`](./infrastructure/pending-transaction.md) object that can be submitted to the Kaspa network. A `PendingTransaction` wraps a regular [`Transaction`](https://kaspa.aspectron.org/docs/classes/Transaction.html) and provides additional metadata, such as:

- A list of UTXO entries (required for transaction signing).
- A reference to the originating `UtxoContext` (useful for distinguishing regular outbound transactions from inter-account transfers).

Upon completion, the [`Generator::summary()`](https://kaspa.aspectron.org/docs/classes/Generator.html#summary) function can be used to generate a [`GeneratorSummary`](./infrastructure/generator-summary.md) object. This summary provides cumulative information about the transaction generation process, including the total transaction mass, which can be useful for calculating transaction fees.

## References

### WASM SDK

- [Generator](https://kaspa.aspectron.org/docs/classes/Generator.html) class.
- [Example of use](https://github.com/kaspanet/rusty-kaspa/blob/master/wasm/examples/nodejs/javascript/transactions/utxo-context-generator.js).

### Rust SDK

- [Generator](https://docs.rs/kaspa-wallet-core/latest/kaspa_wallet_core/tx/generator/generator/index.html) struct.
- [Example of use in the Wallet API](https://github.com/kaspanet/rusty-kaspa/blob/master/wallet/core/src/account/mod.rs#L334).

