<img align="right" alt="Rust" height="40px" style="margin: 5px;" src="images/kaspa.svg" />

# Introduction


This documentation covers Kaspa Rust and WASM SDKs - Rust infrastructure (Rusty Kaspa) and WASM bindings that allow Rust code to be used from within JavaScript and TypeScript environments.

_Please contribute! This `mdbook` is very easy to edit. If you would like to suggest any changes or add anything, please check the [Contributing](./contributing.md) page._

# Technologies 

<img align="left" alt="Rust" height="32px" style="margin: 5px;" src="images/ferris.svg" />
<img align="left" alt="WASM" height="32px" style="margin: 5px;" src="images/wasm.svg" />
<img align="left" alt="JavaScript" height="32px" style="margin: 5px;" src="images/javascript.svg" />
<img align="left" alt="TypeScript" height="32px" style="margin: 5px;" src="images/typescript.svg" />
<img align="left" alt="NodeJS" height="32px" style="margin: 5px;" src="images/nodejs.svg" />
<img align="left" alt="Bun" height="32px" style="margin: 5px;" src="images/bun.svg" />
<img align="left" alt="Electron" height="32px" style="margin: 5px;" src="images/electron.svg" />
<img align="left" alt="NWJS" height="32px" style="margin: 5px;" src="images/nwjs.svg" />

<br/>&nbsp;<br/>

This project is built using multi-platform Rust crates (libraries). The Rust framework is exposed to JavaScript via WASM, while the Rust framework itself can be built to run on any native platform (i.e. for Windows, Linux and MacOS).

WASM SDK is compatible with all major browsers, [Node.js](https://nodejs.org), [Bun](https://bun.sh) as well as environments such as [NWJS](https://nwjs.io) and [Electron](https://www.electronjs.org/). It is also compatible with [Chrome Extension manifest version 3](https://developer.chrome.com/docs/extensions/develop/migrate/what-is-mv3), which allows it to be used in Chrome browser extensions.

# WASM SDK

This WASM SDK is generated directly from the Rusty Kaspa codebase, where Rust functions are compiled
into WebAssembly and then are offered in the JavaScript or TypeScript environments as native JavaScript functions.

Since the WASM SDK has an integrated WebSocket support, it offers RPC connectivity
turning all RPC calls into async function calls in JavaScript (in Rust these functions are also async).

The WASM SDK offers bindings for Transaction generation, address management, transaction signing as 
well as various helper classes for UTXO management.

# Documentation

TypeScript and Rust API documentation is available at the following URLs:

* [Rust documentation](https://docs.rs/kaspa-wasm/latest/kaspa_wasm/) (Rustdoc)
* [TypeScript documentation](https://kaspa.aspectron.org/docs/) (TypeDoc is built for development releases)

# Discord

You can find help on the [Kaspa Discord](https://discord.com/invite/kS3SK5F36R) server, in the `#development` channel.

# Git

WASM SDK is a part of a larger Rusty Kaspa framework available at [https://github.com/kaspanet/rusty-kaspa](https://github.com/kaspanet/rusty-kaspa)

