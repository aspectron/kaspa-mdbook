# Monitoring UTXOs

UTXOs can be obtained via the `getUtxosByAddresses` method or by registering and listening for UTXO updates via notifications.

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
