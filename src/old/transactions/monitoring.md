# Monitoring UTXOs

UTXOs can be obtained via the `getUtxosByAddresses` method or by registering and listening for UTXO updates via notifications.

### Getting UTXOs by Address

```javascript
let addresses = [
    new Address("kaspatest:qz7ulu4c25dh7fzec9zjyrmlhnkzrg4wmf89q7gzr3gfrsj3uz6xjceef60sd"),
    new Address("kaspatest:qzn3qjzf2nzyd3zj303nk4sgv0aae42v3ufutk5xsxckfels57dxjnltw0jwz",),
];

let utxos = await rpc.getUtxosByAddresses({ addresses });
utxos.forEach((utxo) => {
    console.log(utx.address);
    console.log(utx.outpoint);
    console.log(utx.utxoEntry);
})
```

### Registering for UTXO notifications - TODO

```javascript    
    let addresses = [
        new Address("kaspatest:qz7ulu4c25dh7fzec9zjyrmlhnkzrg4wmf89q7gzr3gfrsj3uz6xjceef60sd"),
        new Address("kaspatest:qzn3qjzf2nzyd3zj303nk4sgv0aae42v3ufutk5xsxckfels57dxjnltw0jwz",),
    ];

    // register notification handler
    await rpc.notify(async (op, payload) => {
        // TODO test
        if op == "NotifyUtxosChanged" {
            // TODO - new UTXO entry ...
        }
    });
    // subscribe addresses for notifications
    await rpc.subscribeUtxosChanged(addresses);
    // ...
    // unsubscribe addresses
    await rpc.unsubscribeUtxosChanged(addresses);
    // reset notification handler
    await rpc.notify(null);
```
