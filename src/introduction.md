<img align="right" alt="Rust" height="40px" style="margin: 5px;" src="images/kaspa.svg" />

# Introduction


This documentation covers Kaspa WASM SDK - Rust infrastructure (Rusty Kaspa) WASM bindings that allow Rust code to be used from within JavaScript/TypeScript environments.

Please contribute! This `mdbook` is very easy to edit. If you would like to suggest any changes or add anything, please check the [Contributing](./contributing.md) page.


# Technologies 

<img align="left" alt="Rust" height="32px" style="margin: 5px;" src="images/ferris.svg" />
<img align="left" alt="WASM" height="32px" style="margin: 5px;" src="images/wasm.svg" />
<img align="left" alt="JavaScript" height="32px" style="margin: 5px;" src="images/javascript.svg" />
<img align="left" alt="TypeScript" height="32px" style="margin: 5px;" src="images/typescript.svg" />
<img align="left" alt="NodeJS" height="32px" style="margin: 5px;" src="images/nodejs.svg" />
<img align="left" alt="NWJS" height="32px" style="margin: 5px;" src="images/nwjs.svg" />

<br/>&nbsp;<br/>

This project is built using multi-platform Rust crates (libraries). The Rust framework is exposed to JavaScript via WASM, while the Rust framework itself can be built to run on any native platform (i.e. for Windows, Linux and MacOS).

WASM32 is compatible with all major browsers and Node.js as well as environments such as [NWJS](https://nwjs.io).


# WASM SDK

This WASM SDK is generated directly from the Rusty Kaspa codebase, where Rust functions are compiled
into WebAssembly and then are offered in the JavaScript environment as native JavaScript functions.

Since the WASM SDK has an integrated WebSocket support, it offers RPC connectivity
turning all RPC calls into async function calls in JavaScript (in Rust these functions are also async).

The WASM SDK offers bindings for Transaction generation, address management, transaction signing as 
well as various helper classes for UTXO management.

# Documentation

Please note that documentation is very much a work in progress.

JavaScript and Rust API documentation is available at the following URLs:

* [Rust documentation](https://docs.rs/kaspa-wasm/latest/kaspa_wasm/) (Rustdoc)
* [JavaScript documentation](https://aspectron.com/docs/kaspa-wasm/) (JSDoc)

Various examples can be found here:
- [Creating Transactions](https://github.com/aspectron/rusty-kaspa/tree/wasm-bindings/wasm/nodejs)
- [interacting with RPC](https://github.com/aspectron/rusty-kaspa/blob/wallet-scaffolding/rpc/wrpc/wasm/nodejs/index.js)

# Discord

You can find help on the [Kaspa Discord](https://discord.com/invite/kS3SK5F36R) server, in the `#development` channel.

# Redistributables

WASM redistributables are available prebuilt for web browsers and for nodejs. The entire framework can also be built from Rusty Kaspa sources (into WASM) or used within Rust directly for Rust-based application integration.

You can currently download the latest version of the WASM SDK and the gRPC proxy from:
[https://aspectron.com/en/projects/kaspa-wasm.html](https://aspectron.com/en/projects/kaspa-wasm.html)

# Git

This SDK is a part of a larger Rusty Kaspa framework available at [https://github.com/rusty-kaspa/rusty-kaspa](https://github.com/rusty-kaspa/rusty-kaspa)

The following crates implement key functionality exposed by this SDK:

* Kaspa Consensus Core: [https://github.com/kaspanet/rusty-kaspa/tree/master/consensus/core/src](https://github.com/kaspanet/rusty-kaspa/tree/master/consensus/core/src)
* WASM SDK: [https://github.com/kaspanet/rusty-kaspa/tree/master/wasm](https://github.com/kaspanet/rusty-kaspa/tree/master/wasm)
* Wallet Core: [https://github.com/kaspanet/rusty-kaspa/tree/master/wallet/core/src](https://github.com/kaspanet/rusty-kaspa/tree/master/wallet/core/src)
* RPC Client: [https://github.com/kaspanet/rusty-kaspa/tree/master/rpc/wrpc/client/src](https://github.com/kaspanet/rusty-kaspa/tree/master/rpc/wrpc/client/src)
