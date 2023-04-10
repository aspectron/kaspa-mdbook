# Tracking Transactions

When interacting with Kaspa nodes for the wallet purposes, you are meant to interface using UTXOs.  UTXOs allow you to track per-address balances and create outgoing transactions.

Kaspa nodes currently do not provide an RPC call to lookup transactions by their id.

As such, you do have txid reference in each UTXO, but you do not have a way to get any additional transaction information via a direct RPC lookup.


The kaspanet.io web wallet, for the purposes of record-keeping, creates transaction records containing txids aggregated from UTXOs.  


Transaction records can also be looked up externally using the Kaspa block explorer: [https://explorer.kaspa.org/txs](https://explorer.kaspa.org/txs)

## Side Effects

Due to the lack of `getTransactionById()` RPC call, you can not tell exactly when a transaction has occurred. UTXOs do not contain any timestamp data, as such, you can only estimate the transaction timestamp based on the time the wallet has observed the transaction.



