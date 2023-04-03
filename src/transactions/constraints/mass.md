# Transaction Mass


## Transaction mass limits

Transaction mass is a value calculated from the transaction by applying different weights to transaction metrics. These metrics include the *mass per transaction byte*, *mass per script public key byte*, and *mass per signing operation*. Theese costs are network-specific and for the Mainnet have the following parameters:

```rust
pub const MAINNET_PARAMS: Params = Params {
    mass_per_tx_byte: 1,
    mass_per_script_pub_key_byte: 10,
    mass_per_sig_op: 1000,
    ...
}
```

The maximum allowed transaction mass is `100_000` mass.


```rust
const MAXIMUM_STANDARD_TRANSACTION_MASS: u64 = 100_000;
```

## Calculating transaction mass

### SigOps mass

```rust
let total_sigops: u64 = tx.inputs.iter().map(|input| input.sig_op_count as u64).sum();
let total_sigops_mass = total_sigops * self.mass_per_sig_op;

```

### Input mass

one input mass = (input-size * mass_per_tx_byte) + (input-sig-op-count * mass_per_sig_op) 

input-size = outpoint-size + u64 (storage for length of signature script) + signature script length + u64 (sequence)

so one input mass = ((36 + 8 + 66<sup>*</sup> + 8) * 1) + (1 * 1000) = 1118

*here value "66" is not fixed but depends on signature script length; see `size += input.signature_script.len() as u64;`
line in the `transaction_input_estimated_serialized_size()` function below.


## Transaction mass

```
transaction mass = 
    ( tx-size * mass_per_tx_byte ) + 
    ( total-ouput-script-size * mass_per_script_pub_key_byte ) + 
    ( total-input-sigops * mass_per_sig_op )
```

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


## Other resources

Mass calculation code can be found here: [https://github.com/aspectron/rusty-kaspa/blob/wasm-bindings/consensus/core/src/mass/mod.rs#L59-L89](https://github.com/aspectron/rusty-kaspa/blob/wasm-bindings/consensus/core/src/mass/mod.rs#L59-L89)

TODO - change the URL after PR merge to this: https://github.com/kaspanet/rusty-kaspa/blob/master/consensus/core/src/mass/mod.rs
