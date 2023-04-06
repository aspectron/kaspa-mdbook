# Integration Overview

This section provides a basic overview of Kaspa from the standpoint of integration.

## Wallet Address Derivation

Address [HD Derivation Paths](https://learnmeabitcoin.com/technical/derivation-paths) used by Kaspa wallets are [BIP-0032](https://en.bitcoin.it/wiki/BIP_0032) compatible, using the following derivation path: 

```
m / purpose' / coin_type' / account' / change / address_index
```

- Single signers use purpose value `44'`
- Multi-signers use purpose value `45'`  
- The coin type value is `111111'`
- KDX and kaspanet.io wallets used a different derivation path of `972'`, which is now deprecated.

## Transactions

Transaction constraints are measured using a custom `mass` units as well as serialized byte sizes. For detailed overview please see the [Transactions](./transactions.md) section.

## RPC and UTXO aggregation

To get access to UTXOs, you need to use `getUtxosByAddress()` API call and register for `UtxosChangedNotification` updates.  To enable this functionality, the `kaspad` node needs to be started with [UTXO index](./utxo_index.md) enabled.

## DAA Score

DAA (Difficulty Adjustment Algorithm) score is used as time measurement units in Kaspa (similar to "block height" in Bitcoin). 

## WIF

Kaspa does not support [WIF (Wallet Import Format)](https://en.bitcoin.it/wiki/Wallet_import_format) as Kaspa wallets use XPrv or a seed/mnemonic for wallet import and export.

## Other Common Parameters

Below, you will find some parameters that are commonly used in multi-coin wallets:

```
name = Kaspa
unit = KAS

// Derivation parameters
SingleSignerPurpose = 44
MultiSigPurpose = 45
CoinType = 111111

// KaspaMainnetPrivate is the version that is used for
// kaspa mainnet bip32 private extended keys.
// Ecnodes to xprv in base58.
const KaspaMainnetPrivate = [4] byte {
    0x03,
    0x8f,
    0x2e,
    0xf4,
}

// KaspaMainnetPublic is the version that is used for
// kaspa mainnet bip32 public extended keys.
// Encodes to kpub in base58.
const KaspaMainnetPublic = [4] byte {
    0x03,
    0x8f,
    0x33,
    0x2e,
}

const (
    // PubKey addresses always have the version byte set to 0.
    pubKeyAddrID = 0x00

    // PubKey addresses always have the version byte set to 1.
    pubKeyECDSAAddrID = 0x01

    // ScriptHash addresses always have the version byte set to 8.
    scriptHashAddrID = 0x08
)

// Map from strings to Bech32 address prefix constants for parsing purposes.
const stringsToBech32Prefixes = map[string] Bech32Prefix {
    "kaspa":     Bech32PrefixKaspa,
    "kaspadev":  Bech32PrefixKaspaDev,
    "kaspatest": Bech32PrefixKaspaTest,
    "kaspasim":  Bech32PrefixKaspaSim,
}