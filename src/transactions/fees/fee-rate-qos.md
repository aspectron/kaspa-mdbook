# Fee Rate & QoS

## Fee Rate

The transaction mass determines the mandatory network fees, which are translated into KAS using the "Fee Rate" multiplier. A `1:1` translation (i.e., a `fee rate` of `1.0`) represents the minimum mandatory fees required by the network to process a transaction. Thus, the network's minimum accepted fee rate is `1.0`. A fee rate higher than `1.0` gives the transaction priority over others.

For example, a transaction with a mass of `2,000 grams` requires a minimum fee of `2,000 SOMPI` (with a `fee rate` of `1.0`). If the fee rate is increased to `2.0`, the fee becomes `4,000 SOMPI`, where `2,000 SOMPI` are the mandatory fees, and the additional `2,000 SOMPI` represent the priority (QoS) fee.

When selecting transactions from the mempool for mining, they are ordered by fee rate, with higher fee rate transactions being prioritized. (For more information, see [Miner Selection](../miner-selection.md)).

## Estimating Fee Rate

Rusty Kaspa node provides a [`getFeeEstimate()`](https://kaspa.aspectron.org/docs/classes/RpcClient.html#getFeeEstimate) RPC method. This method performs real-time analysis of the mempool and suggests fee rate values based on the current load.

The returned estimates are grouped into three sections—low, normal, and priority—and provide a fee rate along with a time estimate for transaction confirmation. By using one of these values, or interpolating between them, you can significantly increase the chances of your transaction being confirmed within the desired time frame.

**NOTE:** Fee rate estimates are best-effort analytical guesses. Sudden spikes in transaction volume are unpredictable, so there is always a chance that your transaction might take longer to be confirmed. However, this is a rare occurrence, and it is more likely that transaction pressure will decrease, allowing your transaction to be confirmed sooner than expected.

## Estimating with Transaction Generator

When creating transactions using the [Transaction Generator](../../wallets/wallet-sdk/#transaction-generator), you can specify the `feeRate` (or `fee_rate` in Rust) setting to apply the desired fee rate to the transactions. If no fee rate is specified, the default value of `1.0` is used.

If you want to allocate a specific fixed amount of KAS for priority fees, follow these steps:

1. Run the transaction generator with a fee rate set to `1.0`. The generator will produce a `GeneratorSettings` object containing the total mass used by the generated transactions.
2. Divide the priority fee amount by the total mass to calculate the fee rate multiplier for the priority.
3. Add `1.0` to this multiplier to get the final fee rate.

### Example

If you want to allocate 5 KAS for priority fees, and the total mass for your transaction is `2,043 grams`, the mandatory fee would be `2,043 SOMPI`. To allocate 5 KAS for priority, divide `5 KAS` by `2,043 SOMPI`, resulting in `0.002448`. Adding `1.0` gives a fee rate of `1.002448`.

When you pass this fee rate (`1.002448`) to the Transaction Generator, it will create transactions with the intended priority fee, increasing the total transaction fee by approximately `5 KAS`.

### Fee Estimate Data

The fee estimator is an integrated component in the Rusty Kaspa p2p node that performs real-time analysis of the mempool and suggests fee rate values based on the current load. The fee estimator returns a `RpcFeeEstimate` object, which contains a set of [`RpcFeerateBucket`](https://docs.rs/kaspa-rpc-core/latest/kaspa_rpc_core/model/feerate_estimate/struct.RpcFeerateBucket.html) objects. Each [`RpcFeerateBucket`](https://docs.rs/kaspa-rpc-core/latest/kaspa_rpc_core/model/feerate_estimate/struct.RpcFeerateBucket.html) contains `fee_rate` and `estimated_seconds` fields.

The buckets are divided into three categories:

- **Priority Bucket:** The top-priority feerate bucket provides an estimate of the fee rate required for sub-second DAG inclusion. For all buckets, feerate values are expressed in `sompi/gram` units. The required fee can be calculated by multiplying the transaction mass by the feerate: `fee = feerate * mass(tx)`.

- **Normal Buckets (`Vec<RpcFeerateBucket>`):** A vector of *normal* priority feerate values. The first value guarantees an estimate for sub-minute DAG inclusion. Other values in the vector have shorter estimation times compared to `low_bucket` values. You can interpolate between the priority, normal, and low buckets to compose a complete feerate function on the client side. The API makes an effort to sample enough key points on the feerate-to-time curve for meaningful interpolation.

- **Low Buckets (`Vec<RpcFeerateBucket>`):** A vector of *low* priority feerate values. The first value guarantees an estimate for sub-hour DAG inclusion.

Most wallets will use the `priority_bucket` and the first values of `normal_buckets` and `low_buckets` to offer users three choices: `priority`, `normal`, and `low` fee rates.

## Documentation

- [Rust SDK `get_fee_estimate_call` RPC method](https://docs.rs/kaspa-wrpc-client/latest/kaspa_wrpc_client/prelude/api/rpc/trait.RpcApi.html#tymethod.get_fee_estimate_call)
- [Rust SDK `RpcFeeEstimate` struct](https://docs.rs/kaspa-wrpc-client/latest/kaspa_wrpc_client/prelude/struct.RpcFeeEstimate.html) returned inside the [`GetFeeEstimateResponse`](https://docs.rs/kaspa-wrpc-client/latest/kaspa_wrpc_client/prelude/struct.GetFeeEstimateResponse.html)
- [WASM SDK `RpcClient.getFeeEstimate()` method](https://kaspa.aspectron.org/docs/classes/RpcClient.html#getFeeEstimate)
- [WASM SDK `IFeeEstimate` interface](https://kaspa.aspectron.org/docs/interfaces/IFeeEstimate.html)

