[**@morph-l2/sdk**](../globals.md)• **文档**

***

[@morph-l2/sdk](../globals.md)/ L1 提供商

# Type alias: L1Provider\<TProvider\>

> **L1 提供商**\<`TProvider`\>: `TProvider`&`object`

代表普通以太坊提供者的扩展版本，返回额外的 L1 信息和
具有针对 L1 特定交互的特殊功能。

## Type declaration

### \_isL1Provider

> **\_isL1Provider**: `true`

用于确定提供程序是否为 L1Provider 的内部属性
您可能正在寻找 isL2Provider 函数

### estimateCrossDomainMessageFee()

获取当前 L1（数据）汽油价格。

#### Parameters

• **l1Provider**: [`ProviderLike`](ProviderLike.md)

• **sender**: `string`

• **gasLimit**: `number`\|`bigint`\|`BigNumber`

#### Returns

`Promise`\<`BigNumber`\>

当前 L1 数据 Gas 价格（以 wei 为单位）。

## Type parameters

• **TProvider** *扩展*`Provider`

## Source

src/interfaces/l1-provider.ts:11
