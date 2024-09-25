[**@morph-l2/sdk**](../globals.md)• **文档**

***

[@morph-l2/sdk](../globals.md)/ isL2Provider

# Function: isL2Provider()

> **isL2Provider**\<`TProvider`\>(`provider`): `provider is L2Provider<TProvider>`

确定给定的 Provider 是否为 L2Provider。  会强制类型
如果是真的

## Type parameters

• **TProvider** *扩展*`Provider`\<`TProvider`\>

## Parameters

• **provider**: `TProvider`

要检查的提供商

## Returns

`provider is L2Provider<TProvider>`

布尔值

## Example

```ts
if (isL2Provider(provider)) {
  // typescript now knows it is of type L2Provider
  const gasPrice = await provider.estimateL2GasPrice(tx)
}
```

## Source

src/l2-provider.ts:157
