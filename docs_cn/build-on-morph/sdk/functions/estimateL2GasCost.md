[**@morph-l2/sdk**](../globals.md)• **文档**

***

[@morph-l2/sdk](../globals.md)/ 估计L2Gas成本

# Function: estimateL2GasCost()

> **估计L2GasCost**(`l2Provider`,`tx`): `Promise`\<`BigNumber`\>

估计给定 L2 交易的 L2 Gas 成本（以 wei 为单位）。

## Parameters

• **l2Provider**: [`ProviderLike`](../type-aliases/ProviderLike.md)

用于查询 Gas 使用情况的 L2 提供商。

• **tx**: `TransactionRequest`

用于估算 L2 Gas 成本的交易。

## Returns

`Promise`\<`BigNumber`\>

估计的 L2 Gas 成本。

## Source

src/l2-provider.ts:119
