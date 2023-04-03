# UTXO Index

*UTXO Index* is an auxiliary database that enables the Kaspa node to perform additional tracking of transaction addresses. This allows you to setup notifications for when a new transaction matching your addresses has been detected.

If *UTXO Index* is not enabled, RPC calls requesting *UTXO By Addresses* information will result in an error.

To enable *UTXO Index* run the node with the `--utxoindex` command-line argument.

