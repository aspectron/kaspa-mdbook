# Pending Transaction

`PendingTransaction` is a wrapper around a regular [`Transaction`](https://kaspa.aspectron.org/docs/classes/Transaction.html) that provides additional metadata, such as:

- The list of UTXO entries (required for transaction signing).
- A reference to the originating `UtxoContext` (used for distinguishing regular outbound transactions from inter-account transfers).

## References

### WASM SDK

- [PendingTransaction](https://kaspa.aspectron.org/docs/classes/PendingTransaction.html) class

### Rust SDK

- [PendingTransaction](https://docs.rs/kaspa-wallet-core/latest/kaspa_wallet_core/tx/generator/pending/struct.PendingTransaction.html) struct
