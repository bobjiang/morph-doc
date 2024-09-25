[**@morph-l2/sdk**](../globals.md)• **文档**

***

[@morph-l2/sdk](../globals.md)/ 估计总 Gas 成本

# Function: estimateTotalGasCost()

> **估计总燃气成本**(`l2Provider`,`tx`): `Promise`\<`BigNumber`\>

估计给定 L2 交易的总 Gas 成本（以 wei 为单位）。

## Parameters

• **l2Provider**: [`ProviderLike`](../type-aliases/ProviderLike.md)

用于查询 Gas 使用情况的 L2 提供商。

• **tx**: `TransactionRequest`

用于估算总 Gas 成本的交易。

## Returns

`Promise`\<`BigNumber`\>

估计的总天然气成本。

## Source

src/l2-provider.ts:136
