# Integrating

## Loading into a Web App

Loading in a Web Browser requires an import of the JavaScript module and an async await for a bootstrap handler as follows.

### Example

```html
<html>
    <head>
        <script type="module">
            import * as kaspa_wasm from './kaspa/kaspa-wasm.js';
            (async () => {
                const kaspa = await kaspa_wasm.default('./kaspa/kaspa-wasm_bg.wasm');
                // you are now ready to use the kaspa object
                // print the version of WASM SDK into the browser console
                console.log(kaspa.version());
            })();
        </script>
    </head>
    <body></body>
</html>
```

## Loading into a Node.js App

For Node.js, Kaspa WASM SDK is available as a regular common-js module that can be loaded using the `require()` function.

### Example

```javascript
// W3C WebSocket module shim
// (not needed in a browser or Bun)
// @ts-ignore
globalThis.WebSocket = require('websocket').w3cwebsocket;

let kaspa = require('./kaspa');
let { RpcClient, Resolver } = kaspa;

kaspa.initConsolePanicHook();

const rpc = new RpcClient({
    // url : "127.0.0.1",
    resolver: new Resolver(),
    networkId : "mainnet",
});

(async () => {
    await rpc.connect();

    console.log(`Connected to ${rpc.url}`)
    const info = await rpc.getBlockDagInfo();
    console.log("GetBlockDagInfo response:", info);

    await rpc.disconnect();
})();
```

### The Node.js WebSocket shim

To use WASM RPC client in the Node.js environment, you need to introduce a W3C WebSocket-compatible object
before using the `RpcClient` class. You can use any Node.js module that exposes a W3C-compatible
WebSocket implementation. The recommended package that implements this functionality is 
[WebSocket](https://www.npmjs.com/package/websocket).

Add the following to your `package.json`: 

```json
"dependencies": {
    "websocket": "1.0.34",
}
```

Following that, you can use the following shim:

```js
// WebSocket
globalThis.WebSocket = require('websocket').w3cwebsocket;
```
