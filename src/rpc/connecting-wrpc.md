# Connecting to RPC

## Rust KaspaRpcClient (wRPC)

There are 3 ways to define a target node when initiating a connection.

Ordered by priority (the first override the last):

1. define url when programatically call `connect` on the previously defined `KaspaRpcClient`
2. define url when creating a new `KaspaRpcClient` instance
3. automatically delegating url retreieval and re-connection(s) to [Kaspa Public Nodes (Resolvers)](./kaspa-resolver.md)

### Examples

1. ```rs
    let wrpc_client = KaspaRpcClient::new(
        WrpcEncoding::Borsh,
        None,
        None,
        Some(NetworkId::new(NetworkType::Mainnet)),
        None,
    )?;

    wrpc_client
        .connect(Some(ConnectOptions {
            url: Some("ws://ip:port")
            ..Default::default()
        }))
        .await?;
   ```

2. ```rs
    let wrpc_client = KaspaRpcClient::new(
        WrpcEncoding::Borsh,
        Some("ws://ip:port"),
        None,
        Some(NetworkId::new(NetworkType::Mainnet)),
        None,
    )?;

    wrpc_client.connect(None).await?;
   ```

3. ```rs
   let resolver = Resolver::default();

   let wrpc_client = KaspaRpcClient::new(
       WrpcEncoding::Borsh,
       Some(resolver),
       None,
       Some(NetworkId::new(NetworkType::Mainnet)),
       None,
   )?;

   wrpc_client.connect(None).await?;
   ```


