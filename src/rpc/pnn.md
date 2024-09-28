# Public Node Network

Kaspa Public Node Network is a contributor-driven initiative to provide a public nodes that are available for use by the community. The network is managed by the [Kaspa Resolver](./kaspa-resolver.md) load-balancer that monitors public nodes and can be queried for a node that has least number of active client connections.

This infrastructure is primarily used for development and testing purposes. It is not recommended to use the public node network for large-scale production applications or exchanges, albeit many web wallets do as web wallets are not capable of running their own nodes.

PNN is fully decentralized - nodes are operated by independent PNN contributors. A Telegram channel and Discord are used to coordinate updates and maintenance activities among the contributors.

If you are interested in contributing to the PNN, please reach out developers on the Discord #development channel.  Running a node within PNN requires a stable internet connection and a dedicated VPS server. All node deployments are standardized to run on Debian-compatible Linux distribution (Debian / Ubuntu) and deployed using [kHOST](./khost.md) deployment automation tool.

The status of PNN nodes can be viewed at the [PNN Status Page](https://pnn.kaspa.stream).
