[**@morph-l2/sdk**](../globals.md)• **文档**

***

[@morph-l2/sdk](../globals.md)/估计L1Gas

# Function: estimateL1Gas()

> **估计L1Gas**(`l2Provider`,`tx`): `Promise`\<`BigNumber`\>

估计给定 L2 交易所需的 L1 Gas 量。

## Parameters

• **l2Provider**: [`ProviderLike`](../type-aliases/ProviderLike.md)

用于查询 Gas 使用情况的 L2 提供商。

• **tx**: `TransactionRequest`

用于估算 L1 气体的交易。

## Returns

`Promise`\<`BigNumber`\>

估计 L1 气体。

## Source

src/l2-provider.ts:71
