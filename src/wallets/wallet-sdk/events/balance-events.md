# Balance Events

Each time a transaction-related event occurs, the wallet subsystem emits a `balance` event ([`IBalanceEvent`](https://kaspa.aspectron.org/docs/interfaces/IBalanceEvent.html)) that contains the current [`IBalance`](https://kaspa.aspectron.org/docs/interfaces/IBalance.html) of the `UtxoContext`.

The `UtxoContext` balance consists of the following values:

- `mature`: The amount of funds available for spending.
- `pending`: The amount of funds that are being received but not yet confirmed.
- `outgoing`: The amount of funds that are being sent but have not yet been accepted by the network.

For more details, refer to the [`IBalance`](https://kaspa.aspectron.org/docs/interfaces/IBalance.html) interface.

## Rust Documentation

- [`Events::Balance`](https://docs.rs/kaspa-wallet-core/latest/kaspa_wallet_core/events/enum.Events.html#variant.Balance)
- [`Balance`](https://docs.rs/kaspa-wallet-core/latest/kaspa_wallet_core/utxo/balance/struct.Balance.html)

