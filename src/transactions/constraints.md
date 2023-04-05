# Constraints

Kaspa transactions have the following constraints:
- [Transaction mass](./constraints/size.md)
- [Dust outputs](./constraints/dust.md)
- [Fees](./constraints/fees.md)

*Transaction size* metrics are used to calculate *transaction mass* and to check against *dust limits*.

## Note on serialization

Kaspa is *serialization-agnostic* - the software infrastructure provides compatibility layers such as gRPC (which uses `protobuf` under the hood) and WebSockets with JSON or Borsh (binary) serialization.

However, when considering transaction metrics, sizes of different elements must follow some deterministic serialization rules. To address this, Kaspa builds estimates based on it's own internal serialization.  The following [Transaction Size](./constrants/size.md) section describes how transactions are serialized in order to obtain their metrics.