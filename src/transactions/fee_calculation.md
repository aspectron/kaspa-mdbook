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
### Calculate transaction mass
transaction mass = ( tx-size * mass_per_tx_byte ) + ( total-ouput-script-size * mass_per_script_pub_key_byte ) + ( total-input-sigops * mass_per_sig_op )

```rust
let size = transaction_estimated_serialized_size(tx);
let mass_for_size = size * self.mass_per_tx_byte;
let total_script_public_key_size: u64 = tx
    .outputs
    .iter()
    .map(|output| 2 /* script public key version (u16) */ + output.script_public_key.script().len() as u64)
    .sum();
let total_script_public_key_mass = total_script_public_key_size * self.mass_per_script_pub_key_byte;

let total_sigops: u64 = tx.inputs.iter().map(|input| input.sig_op_count as u64).sum();
let total_sigops_mass = total_sigops * self.mass_per_sig_op;

let transaction_mass = mass_for_size + total_script_public_key_mass + total_sigops_mass
```
where the following values are based on the network configuration and for the Mainnet are as follows:

```rust
mass_per_tx_byte: 1,
mass_per_script_pub_key_byte: 10,
mass_per_sig_op: 1000,
```

Mass calculation code can be found here: [https://github.com/aspectron/rusty-kaspa/blob/wasm-bindings/consensus/core/src/mass/mod.rs#L59-L89](https://github.com/aspectron/rusty-kaspa/blob/wasm-bindings/consensus/core/src/mass/mod.rs#L59-L89)

TODO - change the URL after PR merge to this: https://github.com/kaspanet/rusty-kaspa/blob/master/consensus/core/src/mass/mod.rs

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