# Miner Selection

When transactions are selected from the mempool for block inclusion, a noise function is applied to the selection process to introduce slight randomness. This is an integral part of the transaction selection process, as blocks produced by different miners can carry the same transactions. By randomizing the selection, there is a higher probability of different transactions being included in mined blocks.

The number of unique transactions included in concurrently mined blocks is known as "Effective TPS" (Effective Transactions Per Second).

