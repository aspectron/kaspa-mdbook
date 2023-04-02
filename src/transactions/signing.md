# Signing


## Internal signing

To sign a transaction using the WASM SDK, you can call `sign()` method with an array of `Signer`-compatible class instances or a set of private keys.

```javascript
    let xkey = new XPrivateKey(
        "kprv5y2qurMHCsXYrNfU3GCihuwG3vMqFji7PZXajMEqyBkNh9UZUJgoHYBLTKu1eM4MvUtomcXPQ3Sw9HZ5ebbM4byoUciHo1zrPJBQfqpLorQ",
        false,
        0n
    );

    let private_key = xkey.receiveKey(0);
    let transaction = signTransaction(tx, [private_key], true);
    transaction = transaction.toRpcTransaction();
    let result = await rpc.submitTransaction({transaction, allowOrphan:false});
```


## External signing

In cases where inputs need to be signed externally, you can create a transaction, obtain it's input sighashes, sign these sighashes externally and then apply the signatures back to the transaction.

```javascript
    let scriptHashes = tx.getScriptHashes();
    let signatures = scriptHashes.map(hash=>signScriptHash(hash, private_key));
    console.log("signatures", signatures)
    let transaction = tx.setSignatures(signatures);
    let result = await rpc.submitTransaction({transaction, allowOrphan:false});

```

