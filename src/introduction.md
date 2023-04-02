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

# WASM SDK

This WASM SDK is generated directly from the Rusty Kaspa codebase, where Rust functions are compiled
into WebAssembly and then are offered in the JavaScript environment as native JavaScript functions.

Since the WASM SDK has an integrated WebSocket support, it offers RPC connectivity
turning all RPC calls into async function calls in JavaScript (in Rust these functions are also async).

The WASM SDK offers bindings for Transaction generation, address management, transaction signing as 
well as various helper classes for UTXO management.


# Documentation

* [Rust documentation](https://docs.rs/kaspa-wasm/latest/kaspa_wasm/) (Rustdoc)
* [JavaScript documentation](https://aspectron.com/docs/kaspa-wasm/) (JSDoc)

# Redistributables

WASM redistributables are available for web browsers and for nodejs. The entire framework can also be built from Rusty Kaspa sources (into WASM) or used within Rust directly for Rust-based application integration.

You can currently download the latest version of the WASM SDK and to gRPC proxy from:
[https://aspectron.com/en/projects/kaspa-wasm.html](https://aspectron.com/en/projects/kaspa-wasm.html)