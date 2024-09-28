# Fee Calculation

While the transaction fee is a single amount, it is comprised of two amounts:
- Minimum Transaction Fee (determined from the transaction size)
- Priority fee (determined by the user)

The priority fee is any amount above the minimum transaction fee.

## Using SDK

WASM SDK provides a convenience function for fee calculation: 
```typescript
minimumTransactionFee(tx : Transaction, network: NetworkType)
```
Any extra fee amount in the transaction will be considered as a priority fee.

### Recomputing fees

The following is true for any UTXO network where transaction fees depend on the transaction byte size.

If you accumulate a number of UTXOs with the goal of reaching the amount `A`, the `A + fees` may become larger than the total of all UTXOs. As a result, you may need to consume another UTXO to satisfy fees (and consuming another UTXO will result in higher fees).

A typical approach is to reserve an amount for fees or fallback if the selected UTXO amounts is unable to accomodate fees and re-select UTXOS for a higher amount.

## Calculating fees using mass

The formula for the fee calculation using mass is as follows:

### Calculate minimum fee based on transaction mass

MINIMUM_RELAY_TRANSACTION_FEE is in
sompi/kg so multiply by mass (which is in grams) and divide by 1000 to get
minimum sompis.

```rust
let mut minimum_fee = (transaction_mass * MINIMUM_RELAY_TRANSACTION_FEE) / 1000;

if minimum_fee == 0 {
    minimum_fee = MINIMUM_RELAY_TRANSACTION_FEE;
}

// Set the minimum fee to the maximum possible value if the calculated
// fee is not in the valid range for monetary amounts.
minimum_fee = minimum_fee.min(MAX_SOMPI);
```

```rust
/// DEFAULT_MINIMUM_RELAY_TRANSACTION_FEE specifies the minimum transaction fee for a transaction to be accepted to
/// the mempool and relayed. It is specified in sompi per 1kg (or 1000 grams) of transaction mass.
pub(crate) const DEFAULT_MINIMUM_RELAY_TRANSACTION_FEE: u64 = 1000;
```