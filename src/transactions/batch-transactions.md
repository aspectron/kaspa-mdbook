# Batch Transactions

Transaction mass limits can result in the following problem:

A standard transfer transaction can typically carry `83` inputs and `2` outputs. If you have `1_000` UTXOs with a value of `1 KAS` each and want to transfer `99 KAS` (with `1 KAS` reserved for fees), you will not be able to create such a transaction due to the mass limit.

There are two ways to handle this problem:

1. Create a set of compound transactions where all KAS is transferred to the user's address (thus "compounding" them) and then use the newly created UTXOs to transfer out.
2. Create a set of "chained" (a.k.a. "batch") transactions where you have "in-flight" compounding by submitting transactions that reference each other sequentially to the node.

# Chaining Transactions

The Kaspa p2p node will accept transactions that contain inputs from the UTXO index or inputs of transactions currently present in the mempool. As such, you can create transactions that reference each other within your application and then submit them sequentially (or in the reference order).

When referencing a previously created transaction that has not yet been submitted, you need to create a "virtual UTXO" that uses the previous transaction as a previous transaction outpoint (txid + outpoint index) and specifies the DAA score of the UTXO to be [`u64::MAX`](https://doc.rust-lang.org/std/u64/constant.MAX.html).

The above example can be handled in the following manner:

1. Create the 1st transaction containing `83` inputs and `1` output (typically to a wallet's change address).
2. Create the 2nd transaction, consuming the output of the first transaction (`~83 KAS`), and then add the remaining `17` inputs. The 2nd transaction can now have `2` outputs (the outbound transfer and, if needed, a change output).

# Transaction Parallelism

Transactions that reference each other cannot be included in the same mined block. As such, the above example will be mined across two distinct DAA scores, taking at least 1 DAA score per transaction.

However, if you need to compound UTXOs requiring more than two transactions, you can compound them by creating and submitting `2` transactions in parallel and then submitting a final transaction that unifies them.

Example:
```
80 -> A
80 -> B
A + B -> C
```

In this example, `A` and `B` will be processed in parallel, and `C` will join them at the final stage, resulting in a processing duration of `2 DAA` scores.

