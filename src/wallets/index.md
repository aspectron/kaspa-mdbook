# Wallets

## Overview

Kaspa p2p node is a high-performance data processing system.  Due to the sheer amount of data the network is designed to process, the Kaspa p2p node employs a process known as "pruning".  The node retains all network data for 3 days and discards it afterward.  The only data permanently retained is DAG related data needed for cryptographic proof of network continuity and an optional UTXO index database that contains the current state of all network UTXOs.


Given these considerations, there are the following ways to create wallet systems that operate against the Kaspa network:

- [Direct Node RPC](./direct-node-rpc.md)
- [Wallet SDK](./wallet-sdk.md)
- [Wallet API](./wallet-api.md)

There exist 3rd party solutions that can be used to interface with the Kaspa network such as 

- [Explorer API](../explorers.md)
- [REST API server Docker Image](https://docker.kaspa.org/)

## UTXO Processing

One of the distinctive elements in Kaspa from other cryptocurrency networks is that it operates directly on UTXOs and as such, all wallet-related functionality communicates with UTXO updates.  If a single transaction is sent to your wallet with 2 outputs, you will receive 2 separate UTXO notifications. Wallet SDK solves this by performing additional client-side processing for incoming UTXO notifications grouping them into transaction-like objects.

#### IMPORTANT

When working with UTXOs, to ensure optimal performance, it is desirable to reduce UTXOs by compounding them. This can be done by creating [Batch Transactions](../transactions/batch-transactions.md) to the corresponding account change address. Each UTXO loaded by the wallet occupies memory. JavaScript runtime environments, such as web browsers and NodeJS, typically have a memory limitation of 2 GB. Native applications utilizing Rust do not have this limitation; however, a very high number of UTXOs can impact RPC and wallet processing performance, resulting in slower processing times. It is highly recommended that if a single address (or a single account) contains more than 1 million UTXOs, they should be compounded via batch transactions.

## 3rd party APIs

While 3rd-party APIs are developed by community contributors working closely with Kaspa core developers, they are not an integral part of the Kaspa network and as such can undergo their own breaking changes as well as experience downtime not related to the Kaspa p2p network operation. As such, they pose additional downtime and stability risks to your infrastructure. 

However, if that is not a concern, these solutions might be the easiest to use, especially if your development environment can not easily utilize available Node RPC endpoints. If you need to build a resilient infrastructure that provides you with a high level of uptime guarantees, you should use Rust SDK or WASM SDK directly as they are built directly from the Rusty Kaspa framework codebase.
