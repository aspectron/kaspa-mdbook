
# Dust Outputs

A transaction output is considered dust, if: 
```rust
(transaction_output.value * 1000 / (3 * transaction_output_serialized_size))
    < self.config.minimum_relay_transaction_fee
```

`config.minimum_relay_transaction_fee` specifies the minimum transaction fee for a transaction to be accepted to
the mempool and relayed. It is specified in sompi per 1kg (or 1000 grams) of transaction mass.
```rust
pub(crate) const DEFAULT_MINIMUM_RELAY_TRANSACTION_FEE: u64 = 1000;
```

The following functions can be used to check if `TransactionOutput` is dust.
- `TransactionOutput.isDust()`
- `isTransactionOutputDust(transaction_output: TransactionOutput)`
