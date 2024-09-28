# Transaction Timestamps

Kaspa transactions do not contain timestamps. Instead, transactions contain the DAA (Difficulty Adjustment Algorithm) score. The DAA score can be translated into an approximate timestamp by using the [`RpcClient.getDaaScoreTimestampEstimate`](https://kaspa.aspectron.org/docs/classes/RpcClient.html#getDaaScoreTimestampEstimate) RPC method.

This method accepts a list of DAA scores and returns a list of approximate timestamps corresponding to each DAA score.

## Processing Timestamps

Transaction-related events contain a [`TransactionRecord`](https://kaspa.aspectron.org/docs/interfaces/ITransactionRecord.html) interface that includes the `unixtimeMsec?` property.

This property is always `undefined` if the transaction occurs in real time. There is no need to convert the DAA score to a timestamp if you are processing live transactions; you can simply capture the current system time on the client side.

However, if the transaction is of the `discovery` type, the `unixtimeMsec` property will contain the approximate timestamp of the transaction. 

_This behavior is subject to change in the future, so it is recommended to always follow these steps:_

1. If the transaction is not of the `discovery` type, use the current system time.
2. If the transaction is of the `discovery` type and the `unixtimeMsec` property is `undefined`, use the [`RpcClient.getDaaScoreTimestampEstimate`](https://kaspa.aspectron.org/docs/classes/RpcClient.html#getDaaScoreTimestampEstimate) method to get the approximate timestamp for the transaction.