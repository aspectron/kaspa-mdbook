# Account IDs

As mentioned in the [UtxoContext overview](./index.md#utxocontext), when creating an instance of `UtxoContext`, you should assign it an `id`. This `id` is posted with each `UtxoContext`-related event, allowing you to distinguish different accounts in a multi-account wallet.

Account IDs must be represented by a hash (a 64-character hex string representing a 32-byte hash). The hash can be generated using the [`sha256FromText`](https://kaspa.aspectron.org/docs/functions/sha256FromText.html) or [`sha256FromBinary`](https://kaspa.aspectron.org/docs/functions/sha256FromBinary.html) functions (as well as their `sha256d` counterparts).

This requirement is imposed by internal Wallet SDK data types that use 32-byte hashes to track `UtxoContext` IDs.