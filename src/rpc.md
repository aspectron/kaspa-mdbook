# RPC

Rusty Kaspa integrates support for the following RPC protocols:
- gRPC (native to Kaspa)
- WebSocket-framed wRPC/JSON-RPC protocol
- WebSocket-framed wRPC/Borsh protocol

When using Borsh, server and client should be built from the same source.

## gRPC

gRPC connection can be established by any gRPC-capable client and follow for Kaspa gRPC protocol specifications.

## wRPC

Protocol encoding for wRPC is configurable within the initialization API or as command line switches in applications such as `kaspa-wrpc-proxy` or Rusty Kaspa full-node daemon.

Rusty Kaspa framework includes RPC client and server offering creation of wRPC endpoints easily from within Rust as well as from within JavaScript using WASM SDK.

### WASM RpcClient

#### RpcClient Documentation

- JSDoc - [https://aspectron.com/docs/kaspa-wasm/RpcClient.html](https://aspectron.com/docs/kaspa-wasm/RpcClient.html)
- Rustdoc - [https://docs.rs/kaspa_wasm/latest/kaspa_wasm/rpc/trait.RpcApi.html](https://docs.rs/kaspa_wasm/latest/kaspa_wasm/rpc/trait.RpcApi.html)

#### Example

The following example runs under NodeJS and registers to receive a certain number of notifications, after which it cleanly shuts-down and exits.

---
We start by declaring a websocket shim needed for the RPC connection in NodeJS, then we load required imports and initialize the RPC client.
```javascript
// W3C WebSocket module shim
globalThis.WebSocket = require('websocket').w3cwebsocket;

let {RpcClient,Encoding,defer} = require('./kaspa-rpc');

const MAX_NOTIFICATIONS = 10;
let URL = "ws://127.0.0.1:17110";
let rpc = new RpcClient(Encoding.Borsh, URL);
```

Once we have the `RPC` client, we call an async connect() function that bloks the async execution until the connection is resolved.

```javascript
(async () => {
    // ...
    await rpc.connect();
    // ...
```

Once connected, you can make RPC requests to the Kaspa daemon. RPC functions are always `async` and currently return pure JavaScript objects.
For example `getInfo()` will return an object as follows:
```javascript
    let info = await rpc.getInfo();
    console.log(info);
    // {
    //   serverVersion : "0.12.8",
    //   isSynced : false,
    //   ...
    // }
```

You can also subscribe for event notifications using `rpc.notify()` function to register a notification handler callback.
In this example `defer()` returns a "deferred promise" that can be resolved manually at a later time.

```javascript    
    let finish = defer();
    let seq = 0;
    // register notification handler
    await rpc.notify(async (op, payload) => {
        console.log(`#${seq} - `,"op:",op,"payload:",payload);
        seq++;
        if (seq == MAX_NOTIFICATIONS) {
            // await rpc.disconnect();
            console.log(`exiting after ${seq} notifications`);
            finish.resolve();
        }
    });

    // test subscription
    console.log("subscribing...");
    await rpc.subscribeDaaScore();
```

At this point we block on the `finish` promise, and wait for `MAX_NOTIFICATIONS` to occur. 
The notification handler will execute `finish.resolve()` after `MAX_NOTIFICATIONS`, allowing the 
`await finish;` to resolve and the execution on the primary async pathway to continue.

We then unregister the notification handler to cleanup by calling `rpc.notify(null);` and 
`rpc.disconnect()` to disconnect from the RPC endpoint.
```javascript
    // wait until notifier signals completion
    await finish;
    // clear notification handler
    await rpc.notify(null);
    // disconnect RPC interface
    await rpc.disconnect();

})();

```

