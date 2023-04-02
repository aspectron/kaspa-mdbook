# Constraints

Kaspa transactions have the following constraints:
- Transaction size
- Dust outputs
- Fees


# Transaction size limits



---
one input mass = (input-size * mass_per_tx_byte) + (input-sig-op-count * mass_per_sig_op) 

input-size = outpoint-size + u64 (storage for length of signature script) + signature script length + u64 (sequence)

so one input mass = ((36 + 8 + 66<sup>*</sup> + 8) * 1) + (1 * 1000) = 1118

*here value "66" is not fixed but depends on signature script length; see `size += input.signature_script.len() as u64;`
line in the `transaction_input_estimated_serialized_size()` function below.

---

### Mass parameters
```rust
pub const MAINNET_PARAMS: Params = Params {
    mass_per_tx_byte: 1,
    mass_per_script_pub_key_byte: 10,
    mass_per_sig_op: 1000,
    ...
}
```
### How input estimated serialized size is calculated

```rust

pub fn transaction_estimated_serialized_size(tx: &Transaction) -> u64 {
    let mut size: u64 = 0;
    size += 2; // Tx version (u16)
    size += 8; // Number of inputs (u64)
    let inputs_size: u64 = tx.inputs.iter().map(transaction_input_estimated_serialized_size).sum();
    size += inputs_size;

    size += 8; // number of outputs (u64)
    let outputs_size: u64 = tx.outputs.iter().map(transaction_output_estimated_serialized_size).sum();
    size += outputs_size;

    size += 8; // lock time (u64)
    size += SUBNETWORK_ID_SIZE as u64;
    size += 8; // gas (u64)
    size += HASH_SIZE as u64; // payload hash

    size += 8; // length of the payload (u64)
    size += tx.payload.len() as u64;
    size
}

const HASH_SIZE:usize = 32;

// 36 + 8 + <signature script length> + 8
fn transaction_input_estimated_serialized_size(input: &TransactionInput) -> u64 {
    let mut size = 0;
    size += outpoint_estimated_serialized_size();

    size += 8; // length of signature script (u64)
    size += input.signature_script.len() as u64;

    size += 8; // sequence (u64)
    size
}

// 32 + 4 = 36
const fn outpoint_estimated_serialized_size() -> u64 {
    let mut size: u64 = 0;
    size += HASH_SIZE as u64; // Previous tx ID
    size += 4; // Index (u32)
    size
}

// 8 + 2 + 8 + <script_public_key length>
pub fn transaction_output_estimated_serialized_size(output: &TransactionOutput) -> u64 {
    let mut size: u64 = 0;
    size += 8; // value (u64)
    size += 2; // output.ScriptPublicKey.Version (u16)
    size += 8; // length of script public key (u64)
    size += output.script_public_key.script().len() as u64;
    size
}

```

```rust
let total_sigops: u64 = tx.inputs.iter().map(|input| input.sig_op_count as u64).sum();
let total_sigops_mass = total_sigops * self.mass_per_sig_op;

```


# Dust

A transaction output is considered dust, if: 
```rust
(transaction_output.value * 1000 / (3 * transaction_output_serialized_size))
    < self.config.minimum_relay_transaction_fee
```

The following functions can be used to check if `TransactionOutput` is dust.
- `TransactionOutput.isDust()`
- `isTransactionOutputDust(transaction_output: TransactionOutput)`

# Fees

Fees are discussed in the next [Fee Calculation](./fee_calculation.md) section.