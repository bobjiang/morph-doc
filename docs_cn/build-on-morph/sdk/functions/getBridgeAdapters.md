[**@morph-l2/sdk**](../globals.md)• **文档**

***

[@morph-l2/sdk](../globals.md)/ 获取BridgeAdapters

# Function: getBridgeAdapters()

> **获取BridgeAdapters**(`l2ChainId`,`messenger`,`opts`?): [`BridgeAdapters`](../interfaces/BridgeAdapters.md)

获取给定 L2 链 ID 的一系列桥接适配器。

## Parameters

• **l2ChainId**: `number`

L2 网络的链 ID。

• **messenger**: [`CrossChainMessenger`](../classes/CrossChainMessenger.md)

连接到桥适配器的跨链信使

• **选择？**

用于连接到自定义桥的附加选项。

• **opts.contracts?**: [`DeepPartial`](../type-aliases/DeepPartial.md)\<[`OEContractsLike`](../interfaces/OEContractsLike.md)\>

• **opts.overrides?**: [`BridgeAdapterData`](../interfaces/BridgeAdapterData.md)

定制桥接适配器。

## Returns

[`BridgeAdapters`](../interfaces/BridgeAdapters.md)

包含所有桥接适配器的对象

## Source

src/utils/contracts.ts:142
