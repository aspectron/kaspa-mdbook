# Transaction Fees

Kaspa transaction fees are determined by the cumulative difference between output amounts and input amounts, i.e., `fees = sum(inputs) - sum(outputs)`.

Kaspa transaction fees are based on transaction mass, which is measured in grams.

Each transaction has a mass limit of `100,000 grams` (imposed by the mempool standard), and each block has a mass limit of `500,000 grams` (imposed by consensus rules).


# Mass Components

The following elements need to be taken into account during transaction fee calculations:
- [Compute Mass](./compute-mass.md)
- [Storage Mass](./storage-mass.md)
- [Change Outputs](./change-outputs.md)
- [Fee Rate & Priority (QoS)](./fee-rate-qos.md)

# Network Fees

Network mass are comprised of [compute mass](./fees/compute-mass.md) and [storage mass](./fees/storage-mass.md) where

`network_mass = max(compute_mass, storage_mass)`

Network mass are governed by the [KIP-0009 standard](https://github.com/kaspanet/kips/blob/master/kip-0009.md), the basic principles of which are described in the [Storage Mass](./fees/storage-mass.md) section below.

The implementation of network fee calculation can be found in the [`kaspa_consensus_core::mass` module](https://github.com/kaspanet/rusty-kaspa/blob/master/consensus/core/src/mass/mod.rs).

# Signed vs Unsigned Transactions

When calculating transaction fees, it is important to distinguish between signed and unsigned transactions. The node expects all mass calculations to be performed on signed transactions, as the signature is part of the transaction data and is thus a part of the compute mass.

Given that both ECDSA and Schnorr signatures are 64 bytes in size, functions calculating mass for unsigned transactions pad the calculated mass with the signature size (64 bytes) to account for the signature that will be added when the transaction is signed.

WASM SDK helper functions such as [`calculateTransactionMass()`](https://kaspa.aspectron.org/docs/functions/calculateTransactionMass.html) are explicitly expecting unsigned transactions.

