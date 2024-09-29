# Wallet API

Wallet API is a Rust implementation of the core wallet functionality built on top of the Wallet SDK.

Core wallet implementation include the following features:

- Support for opening multiple wallet files
- BIP39 mnemonic phrase support (with optional passphrase)
- Support for multiple private keys
- Concurrent support for BIP42 multi-account operations and monitoring
- Real-time transaction notifications
- Transfers between accounts
- Wallet file encryption
- Memory erasure of sensitive data
- Transaction history with transaction notes

Supported target platforms:

- Native (Linux, MacOS, Windows)
- NodeJS (via WASM build target)
- Browsers (via WASM build target)
- Browser Extensions (via WASM build target)

Storage backends:

- Native - Filesystem (rust `std::fs`)
- NodeJS - Filesystem (using `fs` module)
- Browsers - `localStorage` + `IndexDB`
- Browser Extensions - `chrome.storage.local`

Wallets using the Wallet API (such as Kaspa CLI wallet and Kaspa NG) can interoperate and open each-other's wallet files.

The Wallet implementation provides a procedural interface to the wallet creation and management. You can create a wallet file, create any number of accounts in this wallet file, create, import or export private keys, estimate and submit transactions.

Wallet API is used by [Kaspa CLI Wallet](../../applications.md#kaspa-cli) and [Kaspa NG](../../applications.md#kaspa-ng) applications.

## References

### WASM SDK

- [Wallet usage example](https://github.com/kaspanet/rusty-kaspa/blob/master/wasm/examples/nodejs/javascript/wallet/wallet.js)
- [Wallet class (API)](https://kaspa.aspectron.org/docs/classes/Wallet.html)

### Rust

- [WalletApi trait](https://docs.rs/kaspa-wallet-core/latest/kaspa_wallet_core/api/traits/trait.WalletApi.html) - Rust trait declaring Wallet API methods.
- [WalletAPI method arguments](https://docs.rs/kaspa-wallet-core/latest/kaspa_wallet_core/api/message/index.html) - structs used as arguments and return types for Wallet API methods.
- [WalletAPI transports](https://docs.rs/kaspa-wallet-core/latest/kaspa_wallet_core/api/transport/index.html) - transport implementation for Wallet API methods. NOTE transport client & server implementations represent data serialization only, not the actual transport protocol.
