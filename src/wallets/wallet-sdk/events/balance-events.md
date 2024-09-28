# Balance Events

Each time a transaction-related event occurs, the wallet subsystem emits the `balance` event ([`IBalanceEvent`](https://kaspa.aspectron.org/docs/interfaces/IBalanceEvent.html)) containing the current [`IBalance`](https://kaspa.aspectron.org/docs/interfaces/IBalance.html) of the UtxoContext that includes `mature` and `pending` balances.

## Rust Documentation

- [`Events::Balance`](https://docs.rs/kaspa-wallet-core/latest/kaspa_wallet_core/events/enum.Events.html#variant.Balance)
- [`Balance`](https://docs.rs/kaspa-wallet-core/latest/kaspa_wallet_core/utxo/balance/struct.Balance.html)