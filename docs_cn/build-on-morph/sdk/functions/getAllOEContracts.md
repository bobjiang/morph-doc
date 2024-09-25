[**@morph-l2/sdk**](../globals.md)• **文档**

***

[@morph-l2/sdk](../globals.md)/ 获取所有OE合同

# Function: getAllOEContracts()

> **获取所有OE合同**(`l2ChainId`,`opts`): [`OEContracts`](../interfaces/OEContracts.md)

对于给定的 L2 链 ID，自动连接到所有合约地址（L1 和 L2）。这
用户可以为 L1 或 L2 合约提供自定义合约地址覆盖。如果给定的链 ID
未知，则用户必须为所有 L1 合约提供自定义合约地址，或者此
函数会抛出错误。

## Parameters

• **l2ChainId**: `number`

L2 网络的链 ID。

• **选择**=`{}`

连接到合约的其他选项。

• **opts.l1SignerOrProvider?**: `Provider`\|`Signer`

• **opts.l2SignerOrProvider?**: `Provider`\|`Signer`

• **opts.overrides?**: [`DeepPartial`](../type-aliases/DeepPartial.md)\<[`OEContractsLike`](../interfaces/OEContractsLike.md)\>

自定义合约地址覆盖 L1 或 L2 合约。

## Returns

[`OEContracts`](../interfaces/OEContracts.md)

包含 ethers.Contract 对象的对象连接到相应的地址
L1 和 L2。

## Source

src/utils/contracts.ts:88
