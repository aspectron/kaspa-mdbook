# Addresses


## Address derivations

KDX/Kaspanet Web Wallet uses `m/44'/972/0'` derivation path (with 12 word seed phrases)

The Core Golang cli wallet and Kaspium uses `m/44'/111111'/0'` (with 24 word seed phrases)

`972` and `111111` are coin types (they are different for historical reasons)

**IMPORTANT:** KDX wallets are not BIP-32 compatible, so KDX derivation path is supported but is considered deprecated.
