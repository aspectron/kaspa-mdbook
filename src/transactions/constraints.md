# Constraints

Kaspa transactions have the following constraints:

# Transaction size limits

one input mass = ((36 + 8 + 66 + 8) * 1) + (1 * 1000) = 1118

```

const HASH_SIZE:usize = 32;

fn transaction_input_estimated_serialized_size(input: &TransactionInput) -> u64 {
    let mut size = 0;
    size += outpoint_estimated_serialized_size();

    size += 8; // length of signature script (u64)
    size += input.signature_script.len() as u64;

    size += 8; // sequence (uint64)
    size
}

const fn outpoint_estimated_serialized_size() -> u64 {
    let mut size: u64 = 0;
    size += HASH_SIZE as u64; // Previous tx ID
    size += 4; // Index (u32)
    size
}
```

```
output_size * mass_per_tx_byte (which is 1)
(1 * 1000) == (sig_op_count * mass_per_sig_op)

```


There is a maximum numner of inputs and outputs that is allowed for each transaction.

# TODO ^^^

# Dust

A transaction output is considered dust, if its 
```
(transaction_output.value as u128 * 1000 / (3 * total_serialized_size as u128))
    < self.config.minimum_relay_transaction_fee as u128
```

### TODO - ADD HELPER API

# Fees

Fees are discussed in the next [Fee Calculation](./fee_calculation.md) section.