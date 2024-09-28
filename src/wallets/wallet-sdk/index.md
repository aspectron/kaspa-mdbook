# Wallet SDK

Wallet SDK provides a set of primitives built in Rust that help the client to process wallet-related events.  Wallet SDK serves as a foundation for the Wallet API (integrated wallet) and provides all the necessary tools to develop a custom Kaspa wallet solution.

There are three key components in the Wallet SDK that operate in tandem to provide functionality to monitor specific addresses on the network for transactions against them, create transactions and submit them to the network.

Note that the Wallet SDK infrastructure [employs an event-based architecture](./events/index.md).

## UtxoProcessor

[`UtxoProcessor`](https://kaspa.aspectron.org/docs/classes/UtxoProcessor.html) is a singleton representing the wallet interface. This can be viewed as a wallet - it connects to the node and ensures that all internal processing is handled correctly.  UtxoProcessor also provides an event processing interface where you can register for wallet-related event notifications.

## UtxoContext

[`UtxoContext`](https://kaspa.aspectron.org/docs/classes/UtxoContext.html) interface represents a wallet account. It monitors any given subset of addresses and emits wallet-related events via the associated UtxoProcessor.  On creation, UtxoContext can be provided with an `id` (a.k.a. Account id). This `id` is posted with each UtxoContext-related event allowing you to distinguish different accounts in a multi-account subsystem.

## Transaction Generator

Transaction [`Generator`](https://kaspa.aspectron.org/docs/classes/Generator.html) interface is designed to create transactions via UtxoContext or a manually supplied set of UTXOs.  Transaction generator simplifies transaction processing by dynamically calculating transaction mass, accounting for a custom transaction Fee Rate, creating daisy-chained (a.k.a. batch/sweep) transactions if your UTXO set exceeds the maximum mass allowed in a single transaction, and calculating the correct transaction change output.

