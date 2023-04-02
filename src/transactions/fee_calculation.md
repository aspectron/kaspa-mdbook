# Fee Calculation

While the transaction fee is a single amount, it is comprised of two amounts:
- Minimum Transaction Fee (determined from the transaction size)
- Priority fee (determined by the user)

The priority fee is any amount above the minimum transaction fee.

## Using SDK

WASM SDK provides a convenience function for fee calculation: 
```
minimumTransactionFee(tx : Transaction)
```
Any extra fee amount in the transaction will be considered as a priority fee.

### Recomputing fees

The following is true for any UTXO network where transaction fees depend on the transaction byte size.

If you accumulate a number of UTXOs with the goal of reaching the amount `A`, the `A + fees` may become larger than the total of all UTXOs. As a result, you may need to consume another UTXO to satisfy fees (and consuming another UTXO will result in higher fees).

A typical approach is to reserve an amount for fees or or fallback if the selected UTXO amounts is unable to accomodate fees and re-select UTXOS for a higher amount.

## Calculating fees using mass

The formula for the fee calculation using mass is as follows:
```
total_mass == tx_size_in_bytes * mass_per_tx_byte + 
    (sum of outputs.map(output => 2+output.script_public_key.script().len()) * mass_per_script_pub_key_byte +
    (sum of inputs.map(input => input.sig_op_count) * mass_per_sig_op 
```
where the following values are based on the network configuration and for the Mainnet are as follows:
```
mass_per_tx_byte: 1,
mass_per_script_pub_key_byte: 10,
mass_per_sig_op: 1000,
```

Mass calculation code can be found here: [https://github.com/aspectron/rusty-kaspa/blob/wasm-bindings/consensus/core/src/mass/mod.rs#L59-L89](https://github.com/aspectron/rusty-kaspa/blob/wasm-bindings/consensus/core/src/mass/mod.rs#L59-L89)

TODO - change the URL after PR merge to this: https://github.com/kaspanet/rusty-kaspa/blob/master/consensus/core/src/mass/mod.rs