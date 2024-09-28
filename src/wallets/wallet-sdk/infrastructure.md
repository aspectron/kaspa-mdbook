# Infrastructure

The Wallet SDK components are based on an event-driven architecture. As such, your application should listen to events to update its state.

The best way to build the wallet infrastructure using the Wallet SDK is by creating your own primitives that represent wallet components. These primitives should encapsulate `UtxoProcessor` and `UtxoContext`, while updating them in response to events.

For example, you can create a `Wallet` class that encapsulates the `UtxoProcessor` and an `Account` class that encapsulates the `UtxoContext`. The `Wallet` class can listen to events from the `UtxoProcessor` and update the `Account` instances accordingly.