# Transaction Fees

Kaspa transaction fees are determined by the cumulative difference between the input and output amounts, i.e., `fees = sum(inputs) - sum(outputs)`.

Kaspa transaction fees are based on transaction mass, which is measured in grams.

- Each transaction has a mass limit of `100,000 grams` (imposed by the mempool standard).
- Each block has a mass limit of `500,000 grams` (imposed by consensus rules).

# Mass Components

The following elements must be considered during transaction fee calculations:

- [Compute Mass](./compute-mass.md)
- [Storage Mass](./storage-mass.md)
- [Change Outputs](./change-outputs.md)
- [Fee Rate & Priority (QoS)](./fee-rate-qos.md)

# Network Mass

Network mass is the larger value between [compute mass](./fees/compute-mass.md) and [storage mass](./fees/storage-mass.md), calculated as:

`network_mass = max(compute_mass, storage_mass)`

Network mass is governed by the [KIP-0009 standard](https://github.com/kaspanet/kips/blob/master/kip-0009.md), with the basic principles explained in the [Storage Mass](./fees/storage-mass.md) section.

The implementation of network mass calculations can be found in the [`kaspa_consensus_core::mass` module](https://github.com/kaspanet/rusty-kaspa/blob/master/consensus/core/src/mass/mod.rs).

# Signed vs Unsigned Transactions

When calculating transaction fees, it is important to distinguish between signed and unsigned transactions. The node expects all mass calculations to be performed on signed transactions because the signature is part of the transaction data, contributing to the compute mass.

Both ECDSA and Schnorr signatures are 64 bytes in size. Therefore, when calculating mass for unsigned transactions, functions pad the calculated mass by 64 bytes to account for the signature that will be added upon signing.

WASM SDK helper functions, such as [`calculateTransactionMass()`](https://kaspa.aspectron.org/docs/functions/calculateTransactionMass.html), explicitly expect unsigned transactions.