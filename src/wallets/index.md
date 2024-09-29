# Wallets

## Overview

The Kaspa p2p node is a high-performance data processing system. Due to the significant volume of data processed by the network, the Kaspa p2p node uses a process called "pruning." The node retains all network data for 3 days and discards it afterward. The only data permanently retained is the DAG-related data required for cryptographic proof of network continuity, along with an optional UTXO index database that stores the current state of all network UTXOs.

Given these constraints, there are several ways to create wallet systems that operate with the Kaspa network:

- [Direct Node RPC](./direct-node-rpc.md)
- [Wallet SDK](./wallet-sdk.md)
- [Wallet API](./wallet-api.md)

Additionally, there are third-party solutions for interfacing with the Kaspa network, such as:

- [Explorer API](../explorers.md)
- [REST API server Docker Image](https://docker.kaspa.org/)
- [REST API integration guide](https://kaspa.org/wp-content/uploads/2023/03/Integration_Guide_for_Kaspa_BlockDAG.pdf)

## 3rd Party APIs

While third-party APIs are developed by community contributors in close collaboration with Kaspa core developers, they are not an integral part of the Kaspa network. This means they may experience breaking changes or downtime independent of the Kaspa p2p network. As such, relying on third-party APIs poses additional risks to your infrastructure in terms of downtime and stability.

If these concerns are not critical to your project, third-party APIs can be an easier option, especially if your development environment cannot easily interact with Node RPC endpoints. However, for a more resilient infrastructure with high uptime guarantees, it is recommended to use the Rust SDK or WASM SDK, as they are built directly from the Rusty Kaspa framework.

## UTXO Processing

One of the key differences between Kaspa and other cryptocurrency networks is that Kaspa operates directly on UTXOs. As a result, all wallet-related functionality interacts with UTXO updates, not transactions. For example, if a single transaction sends two outputs to your wallet, you will receive two separate UTXO notifications. In general, the usage pattern is that you send transactions but your receive UTXOs. The client-side Wallet SDK simplifies this by performing additional client-side processing, grouping incoming UTXO notifications into transaction-like objects.

#### IMPORTANT

To ensure optimal performance when working with UTXOs, it is advisable to reduce the number of UTXOs by compounding them. This can be achieved by creating [Batch Transactions](../transactions/batch-transactions.md) to the corresponding account's change address. Each UTXO loaded by the wallet consumes memory. In JavaScript runtime environments, such as web browsers and Node.js, there is typically a memory limitation of 2 GB. While native applications utilizing Rust do not face this limitation, a very high number of UTXOs can still affect RPC and wallet processing performance, leading to slower processing times.

It is highly recommended that if a single address (or account) contains more than 1 million UTXOs, they should be compounded via batch transactions to optimize performance.