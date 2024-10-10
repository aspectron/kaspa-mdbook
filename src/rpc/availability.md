# Checking RPC availability

There are two simple ways to check if the RPC server is running and listening on a port: Rusty Kaspa CLI Wallet and Kaspa NG desktop version.

## Using Rusty Kaspa CLI Wallet

Rusty Kaspa CLI Wallet is available as a part of official [Rusty Kaspa releases](https://github.com/rusty-kaspa/rusty-kaspa/releases).
Simply download the latest release, extract the archive and run `kaspa-wallet` from the command line. 
Once started you can use following commands to check if the RPC server is running and listening on a port:

```
network mainnet
connect localhost
rpc get-info
```

If you are building from source, you can run `cargo run --release` from the `/cli` folder in the Rusty Kaspa repository.

## Using Kaspa NG

1. Go to the `Settings` panel.
2. Navigate to `Kaspa p2p Network & Node Connection`
3. Make sure the `Kaspa Network` is set to the same network running on your node.
4. Make sure `Kaspa Node` is set to `Remote`
5. Under `Remote p2p Node Configuration` select `Custom`
6. In `wRPC ConnectionSettings` select the protocol and the wRPC URL.
7. Hit `Apply`

If connecting to default ports, you can simply enter `localhost`.

#### IMPORTANT

You can not use Kaspa NG online version at https://kaspa-ng.org to connect to your local RPC server. Web browser security restrictions only allow the online Kaspa NG version to connect to Kaspa nodes running on SSL endpoints, while the local RPC server does not use SSL (please see how to configure a proxy server for SSL endpoints in the [proxies](./proxies.md) section).  The desktop version of Kaspa NG does not have this restriction.
