# Creation

### Get available UTXOs for a given set of addresses
```javascript
    let addresses = [
        new Address("kaspatest:qz7ulu4c25dh7fzec9zjyrmlhnkzrg4wmf89q7gzr3gfrsj3uz6xjceef60sd")
    ];
    let utxos_by_address = await rpc.getUtxosByAddresses({ addresses });
```

### Create a UTXO collection from the received UTXO set and select UTXOs needed for a transaction
```javascript
    let utxoSet = UtxoSet.from(utxos_by_address);
    let amount = 1000n;
    let utxo_selection = await utxoSet.select(amount, UtxoOrdering.AscendingAmount);
```
UtxoSet is a custom collection designed to efficiently handle sorted collections of UTXOs.

### Specify destination amounts and 
```javascript

    let change_address = new Address("kaspatest:qz7ulu4c25dh7fzec9zjyrmlhnkzrg4wmf89q7gzr3gfrsj3uz6xjceef60sd");
    let output = new Output(
        new Address("kaspatest:qz7ulu4c25dh7fzec9zjyrmlhnkzrg4wmf89q7gzr3gfrsj3uz6xjceef60sd"),
        amount
    );

    let outputs = new Outputs([output])
    let priorityFee = 1500;
    let tx = createTransaction(utxo_selection, outputs, change_address, priorityFee);
```