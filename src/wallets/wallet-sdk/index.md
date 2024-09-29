# Wallet SDK

Wallet SDK provides a set of primitives built in Rust that help the client to process wallet-related events.  Wallet SDK serves as a foundation for the Wallet API (integrated wallet) and provides all the necessary tools to develop a custom Kaspa wallet solution.

There are three key components in the Wallet SDK that operate in tandem to provide functionality to monitor specific addresses on the network for transactions against them, create transactions and submit them to the network.

Note that the Wallet SDK infrastructure [employs an event-based architecture](./events/index.md).

## UtxoProcessor

[`UtxoProcessor`](./infrastructure/utxo-processor.md) is a singleton representing the wallet interface. This can be viewed as a wallet - it connects to the node and ensures that all internal processing is handled correctly.  UtxoProcessor also provides an event processing interface where you can register for wallet-related event notifications.

## UtxoContext

[`UtxoContext`](./infrastructure/utxo-context.md) interface represents a wallet account. It monitors any given subset of addresses and emits wallet-related events via the associated UtxoProcessor.  On creation, UtxoContext can be provided with an `id` (a.k.a. Account id). This `id` is posted with each UtxoContext-related event allowing you to distinguish different accounts in a multi-account subsystem.

## Transaction Generator

The Transaction [`Generator`](./infrastructure/generator.md) interface is designed to create transactions using either a `UtxoContext` or a manually supplied set of UTXOs. The `Transaction Generator` is a helper class that simplifies the transaction creation process and handles various edge cases that can arise during transaction generation.

The Transaction Generator functions as an iterator, producing [`PendingTransaction`](./infrastructure/pending-transaction.md) objects. These transactions can either be aggregated or submitted to the network. Additionally, the generator produces [`GeneratorSummary`](./infrastructure/generator-summary.md) objects, which provide an overview of the entire transaction creation process.
