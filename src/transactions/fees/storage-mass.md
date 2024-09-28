# Storage Mass

Storage mass is calculated using the [KIP-0009 algorithm](https://github.com/kaspanet/kips/blob/master/kip-0009.md), which takes into account the number of inputs, outputs, and their values to ensure that transactions fall within certain constraints. If a transaction exceeds these constraints, the mass will rapidly increase, resulting in the transaction being rejected by the network.

The constraints imposed by KIP-0009 can be simplified as follows:

- You cannot create transactions that significantly "fan out" small amounts of KAS into many outputs. For example, if you have one input and try to create many small outputs, the transaction mass will increase quickly, eventually reaching a limit that will cause the transaction to be rejected by the network. The general rule is that the number of outputs should not exceed 10 times the number of inputs. For instance, a transaction with 1 input and 10 outputs (1->10) will be rejected, while a transaction with 5 inputs and 10 outputs (5->10) will be accepted. The following logic also applies:
    - If all outputs are greater than `100 KAS`, there is effectively no limit on the number of outputs you can have.
    - If all outputs are greater than `10 KAS`, you can have up to approximately `100` outputs before the transaction mass reaches `100k grams`.
    - If all outputs are greater than `1 KAS`, you are limited to `10` outputs.
    
- You are allowed to combine or transfer inputs without increasing the transaction mass, as long as the number of outputs is equal to or fewer than the number of inputs (e.g., 10->10 or 10->1 transactions are allowed).

- The value of each output must not deviate too much from the input amounts, as explained in the **Output Deviation** section.

## Output Deviation

Output deviation refers to an output value that is significantly smaller than the input.

This constraint can be simplified as follows:

- The KAS amount of any output must not be less than 0.019 KAS (0.02 KAS can be used as a safe cut-off point). Having any output below this amount will result in rejection.

However, while this constraint can be used as a simple general rule for transaction creation, the actual relationship between input and output values allows for some flexibility. For example, you can create two outputs of `0.001` and `0.003` if your input is `0.003`. Additionally, an output of `0.003` can be created if you have an input of `0.007` (you can break down `0.007` into `0.004 + 0.003`), etc.

Please see the [Change Outputs](./change-outputs.md) section for more information on handling change outputs.