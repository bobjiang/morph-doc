[**@morph-l2/sdk**](../globals.md)• **文档**

***

[@morph-l2/sdk](../globals.md)/ L2提供商

# Type alias: L2Provider\<TProvider\>

> **L2Provider**\<`TProvider`\>: `TProvider`&`object`

代表普通以太坊提供者的扩展版本，返回额外的 L2 信息和
具有针对 L2 特定交互的特殊功能。

## Type declaration

### \_isL2Provider

> **\_isL2Provider**: `true`

用于确定提供程序是否为 L2Provider 的内部属性
您可能正在寻找 isL2Provider 函数

### estimateL1Gas()

估计交易所需的 L1（数据）gas。

#### Parameters

• **tx**: `TransactionRequest`

用于估算 L1 气体的交易。

#### Returns

`Promise`\<`BigNumber`\>

估计 L1 气体。

### estimateL1GasCost()

通过乘以估计的 L1 Gas 来估计交易的 L1（数据）Gas 成本（以 wei 为单位）
成本按当前 L1 Gas 价格计算。

#### Parameters

• **tx**: `TransactionRequest`

用于估算 L1 Gas 成本的交易。

#### Returns

`Promise`\<`BigNumber`\>

估计的 L1 Gas 成本。

### estimateL2GasCost()

通过乘以估计的 L1 来估计交易的 L2（执行）gas 成本（以 wei 为单位）
Gas 成本按当前 L2 Gas 价格计算。这是结果的简单乘法
给定交易请求的 getGasPrice 和estimateGas。

#### Parameters

• **tx**: `TransactionRequest`

用于估算 L2 Gas 成本的交易。

#### Returns

`Promise`\<`BigNumber`\>

估计的 L2 Gas 成本。

### estimateTotalGasCost()

通过添加估计的 L1 Gas 成本来估计交易的总 Gas 成本（以 wei 为单位）
以及估计的 L2 Gas 成本。

#### Parameters

• **tx**: `TransactionRequest`

用于估算总 Gas 成本的交易。

#### Returns

`Promise`\<`BigNumber`\>

估计的总天然气成本。

### getL1GasPrice()

获取当前 L1（数据）汽油价格。

#### Returns

`Promise`\<`BigNumber`\>

当前 L1 数据 Gas 价格（以 wei 为单位）。

## Type parameters

• **TProvider** *扩展*`Provider`

## Source

src/interfaces/l2-provider.ts:43
