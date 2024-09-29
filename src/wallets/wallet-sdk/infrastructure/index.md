# Infrastructure

## Overview

The Wallet SDK components are based on an event-driven architecture, meaning your application should listen to events to update its state.

The recommended approach for building wallet infrastructure with the Wallet SDK is to create your own primitives that represent wallet components. These primitives should encapsulate the `UtxoProcessor` and `UtxoContext` and be updated in response to events.

For example:
- You can create a `Wallet` class that encapsulates the `UtxoProcessor`.
- You can create an `Account` class that encapsulates the `UtxoContext`.

The `Wallet` class can listen to events from the `UtxoProcessor` and update the corresponding `Account` instances accordingly.

## Data Storage

When using the Wallet SDK, you need to provide your own storage backend to manage and track wallet data, including:

- Wallet Keys
- Wallet Derivation Data (BIP44 account index assignments)
- Transaction History

Additionally, you must implement logic to capture transaction timestamps and perform additional transaction processing on startup, as outlined in the [Discovery Events](./discovery-events.md) section.
