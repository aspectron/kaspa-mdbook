# Event-based architecture

The wallet architecture for both the wallet implementation and the underlying UtxoProcessor is event-driven.  This means you are meant to affect the wallet subsystem by registering addresses for monitoring and submitting transactions and the wallet will post appropriate transaction-related notification events and balance updates.

## Wallet SDK Events

[`UtxoProcessor.addEventListener()`](https://kaspa.aspectron.org/docs/classes/UtxoProcessor.html#addEventListener) function provides a way to register event listeners that receive events posted by the wallet.  These include standard events such as RPC connection and disconnection events as well as transaction-related events.

The full list of events posted by UtxoProcessor can be found here: 
- WASM: [`UtxoProcessorEvent`](https://kaspa.aspectron.org/docs/types/UtxoProcessorEvent.html), [`UtxoProcessorEventMap`](https://kaspa.aspectron.org/docs/types/UtxoProcessorEventMap.html)
- Rust: [Wallet SDK `Events` enum](https://docs.rs/kaspa-wallet-core/latest/kaspa_wallet_core/events/enum.Events.html)

