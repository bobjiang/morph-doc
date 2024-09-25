[**@morph-l2/sdk**](../globals.md)• **文档**

***

[@morph-l2/sdk](../globals.md)/ 获取OE合同

# Function: getOEContract()

> **获取OE合同**(`contractName`,`l2ChainId`,`opts`): `Contract`

返回给定名称的 ethers.Contract 对象，连接到相应的地址
给定的 L2 链 ID。用户还可以提供自定义地址来连接合约
反而。如果链 ID 未知，则用户必须提供自定义地址或此地址
函数会抛出错误。

## Parameters

• **contractName**: `"L1MessageQueueWithGasPriceOracle"`\|`"L1GatewayRouter"`\|`"L2GatewayRouter"`\|`"MorphStandardERC20"`\|`"L2WETH"`\|`"L1WETHGateway"`\|`"L2WETHGateway"`\|`"L2ToL1MessagePasser"`\|`"Sequencer"`\|`"Gov"`\|`"L2ETHGateway"`\|`"L2CrossDomainMessenger"`\|`"L2StandardERC20Gateway"`\|`"L2ERC721Gateway"`\|`"L2TxFeeVault"`\|`"L2ERC1155Gateway"`\|`"MorphStandardERC20Factory"`\|`"GasPriceOracle"`\|`"WrappedEther"`\|`"MorphToken"`\|`"L1CrossDomainMessenger"`\|`"Staking"`\|`"Rollup"`\|`"L1ETHGateway"`\|`"L1StandardERC20Gateway"`\|`"L1ERC721Gateway"`\|`"L1ERC1155Gateway"`\|`"EnforcedTxGateway"`\|`"WETH"`

要连接的合约名称。

• **l2ChainId**: `number`

L2 网络的链 ID。

• **选择**=`{}`

连接到合同的其他选项。

• **opts.address?**: [`AddressLike`](../type-aliases/AddressLike.md)

连接到合约的自定义地址。

• **opts.signerOrProvider?**: `Provider`\|`Signer`

连接到合同的签名者或提供者。

## Returns

`Contract`

连接到适当地址和接口的 ethers.Contract 对象。

## Source

src/utils/contracts.ts:42
