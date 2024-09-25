[**@morph-l2/sdk**](../globals.md)• **文档**

***

[@morph-l2/sdk](../globals.md)/ asL2Provider

# Function: asL2Provider()

> **asL2Provider**\<`TProvider`\>(`provider`): [`L2Provider`](../type-aliases/L2Provider.md)\<`TProvider`\>

返回包装为 Morph L2 提供程序的提供程序。添加一些额外的辅助函数
简化 Morph 上交易的 Gas 使用量估算过程。返回副本
原始提供商的。

## Type parameters

• **TProvider** *扩展*`Provider`\<`TProvider`\>

## Parameters

• **provider**: `TProvider`

包装到 L2 提供程序中的提供程序。

## Returns

[`L2Provider`](../type-aliases/L2Provider.md)\<`TProvider`\>

提供者包装为 L2 提供者。

## Source

src/l2-provider.ts:171
