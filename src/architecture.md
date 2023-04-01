# Architecture

WASM SDK is built by exposing Rust functionality to JS using [`wasm_bindgen`](https://rustwasm.github.io/wasm-bindgen/) 

RPC calls produce pure JavaScript objects.  These objects can then be use to create local instances of classes backed by Rust API functionality.


