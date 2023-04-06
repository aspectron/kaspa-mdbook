# Integrating

## Loading into a Web App

Loading in a Web Browser requires an import of the JavaScript module and an async await for a bootstrap handler as follows:

```html
<html>
    <head>
        <script type="module">
            import * as kaspa_wasm from './kaspa/kaspa-wasm.js';
            (async () => {
                const kaspa = await kaspa_wasm.default('./kaspa/kaspa-wasm_bg.wasm');
            })();
        </script>
    </head>
    <body></body>
</html>
```

## Loading into a Node.js App

For Node.js, Kaspa WASM SDK is available as a regular Node.js module that can be loaded using require().

```javascript
// W3C WebSocket module shim
globalThis.WebSocket = require('websocket').w3cwebsocket;

let {RpcClient,Encoding,init_console_panic_hook,defer} = require('./kaspa-rpc');
// init_console_panic_hook();

let URL = "ws://127.0.0.1:17110";
let rpc = new RpcClient(Encoding.Borsh,URL);

(async () => {
    await rpc.connect();
    let info = await rpc.getInfo();
    console.log(info);

    await rpc.disconnect();
})();
```

### The Node.js WebSocket shim

To use WASM RPC client in the Node.js environment, you need to introduce a W3C WebSocket-compatible object
before loading the WASM32 library. You can use any Node.js module that exposes a W3C-compatible
WebSocket implementation. Two of such modules are [WebSocket](https://www.npmjs.com/package/websocket)
(provides a custom implementation) and [isomorphic-ws](https://www.npmjs.com/package/isomorphic-ws)
(built on top of the ws WebSocket module).

You can use the following shims:

```js
// WebSocket
globalThis.WebSocket = require('websocket').w3cwebsocket;
// isomorphic-ws
globalThis.WebSocket = require('isomorphic-ws');
```
