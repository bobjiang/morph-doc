[**@morph-l2/sdk**](../globals.md)• **文档**

***

[@morph-l2/sdk](../globals.md)/ 跨链信使

# Class: CrossChainMessenger

## Constructors

### new CrossChainMessenger()

> **新的跨链信使**(`opts`): [`CrossChainMessenger`](CrossChainMessenger.md)

创建一个新的 CrossChainProvider 实例。

#### Parameters

• **选择**

提供者的选项。

• **opts.backendURL?**: `string`

提款证明生成的后端。

• **opts.bridges?**: [`BridgeAdapterData`](../interfaces/BridgeAdapterData.md)

可选的网桥地址列表。

• **opts.contracts?**: [`DeepPartial`](../type-aliases/DeepPartial.md)\<[`OEContractsLike`](../interfaces/OEContractsLike.md)\>

可选的合约地址覆盖。

• **opts.l1ChainId**: [`NumberLike`](../type-aliases/NumberLike.md)

L1 链的链 ID。

• **opts.l1SignerOrProvider**: [`SignerOrProviderLike`](../type-aliases/SignerOrProviderLike.md)

L1 链的签名者或提供者，或 JSON-RPC url。

• **opts.l2ChainId**: [`NumberLike`](../type-aliases/NumberLike.md)

L2 链的链 ID。

• **opts.l2SignerOrProvider**: [`SignerOrProviderLike`](../type-aliases/SignerOrProviderLike.md)

L2 链的签名者或提供者，或 JSON-RPC url。

#### Returns

[`CrossChainMessenger`](CrossChainMessenger.md)

#### Source

src/cross-chain-messenger.ts:130

## Properties

### backendURL

> **backendURL**: `string`

提现证明服务器后端url

#### Source

src/cross-chain-messenger.ts:76

***

### bridges

> **bridges**: [`BridgeAdapters`](../interfaces/BridgeAdapters.md)

给定网络的自定义网桥列表。

#### Source

src/cross-chain-messenger.ts:116

***

### contracts

> **contracts**: [`OEContracts`](../interfaces/OEContracts.md)

合约对象附加到其各自的提供者和地址。

#### Source

src/cross-chain-messenger.ts:111

***

### estimateGas

> **estimateGas**: `object`

包含估计给定交易所需气体的函数的对象。
遵循 ethers.js 使用的模式。

#### approveERC20()

> **approveERC20**: (`l1Token`,`l2Token`,`amount`,`opts`?) =>`Promise`\<`BigNumber`\>

估计批准一些代币存入 L2 链所需的天然气。

##### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 代币地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 代币地址。

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

要批准的代币数量。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

##### Returns

`Promise`\<`BigNumber`\>

#### depositERC20()

> **depositERC20**: (`l1Token`,`l2Token`,`amount`,`opts`?) =>`Promise`\<`BigNumber`\>

估计将一些 ERC20 代币存入 L2 链所需的天然气。

##### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 令牌的地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 令牌的地址。

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

存入金额。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

##### Returns

`Promise`\<`BigNumber`\>

#### depositETH()

> **depositETH**: (`amount`,`opts`?) =>`Promise`\<`BigNumber`\>

估计将一些 ETH 存入 L2 链所需的天然气。

##### Parameters

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

存入的 ETH 金额。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

##### Returns

`Promise`\<`BigNumber`\>

#### proveAndRelayMessage()

> **proveAndRelayMessage**: (`message`,`opts`?) =>`Promise`\<`BigNumber`\>

估计证明并中继跨链消息所需的气体。仅适用于 L2 到 L1 消息。

##### Parameters

• **message**: [`MessageLike`](../type-aliases/MessageLike.md)

用于生成证明交易的消息。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

##### Returns

`Promise`\<`BigNumber`\>

#### sendMessage()

> **sendMessage**: (`message`,`opts`?) =>`Promise`\<`BigNumber`\>

估计发送跨链消息所需的天然气。

##### Parameters

• **message**: [`CrossChainMessageRequest`](../interfaces/CrossChainMessageRequest.md)

跨链消息发送。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

##### Returns

`Promise`\<`BigNumber`\>

#### withdrawERC20()

> **withdrawERC20**: (`l1Token`,`l2Token`,`amount`,`opts`?) =>`Promise`\<`BigNumber`\>

估计将一些 ERC20 代币提取回 L1 链所需的 Gas 量。

##### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 令牌的地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 令牌的地址。

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

提取金额。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

##### Returns

`Promise`\<`BigNumber`\>

#### withdrawETH()

> **withdrawETH**: (`amount`,`opts`?) =>`Promise`\<`BigNumber`\>

估算将一些 ETH 提取回 L1 链所需的 Gas 费用。

##### Parameters

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

要提取的 ETH 数量。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

##### Returns

`Promise`\<`BigNumber`\>

#### Source

src/cross-chain-messenger.ts:1600

***

### l1ChainId

> **l1ChainId**: `number`

L1 网络的链 ID。

#### Source

src/cross-chain-messenger.ts:101

***

### l1CrossDomainMessenger

> **l1CrossDomainMessenger**: `Contract`

连接到 L1 链的跨域信使。

#### Source

src/cross-chain-messenger.ts:91

***

### l1SignerOrProvider

> **l1SignerOrProvider**: `Provider`\|`Signer`

连接到 L1 链的提供商。

#### Source

src/cross-chain-messenger.ts:81

***

### l2ChainId

> **l2ChainId**: `number`

L2 网络的链 ID。

#### Source

src/cross-chain-messenger.ts:106

***

### l2CrossDomainMessenger

> **l2CrossDomainMessenger**: `Contract`

CrossDomainMessenger 连接到 L2 链。

#### Source

src/cross-chain-messenger.ts:96

***

### l2SignerOrProvider

> **l2SignerOrProvider**: `Provider`\|`Signer`

连接到 L2 链的提供商。

#### Source

src/cross-chain-messenger.ts:86

***

### populateTransaction

> **populateTransaction**: `object`

包含生成由用户签名的交易的函数的对象。
遵循 ethers.js 使用的模式。

#### approveERC20()

> **approveERC20**: (`l1Token`,`l2Token`,`amount`,`opts`?) =>`Promise`\<`TransactionRequest`\>

生成一个交易，用于批准一些代币存入 L2 链。

##### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 代币地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 代币地址。

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

要批准的代币数量。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

##### Returns

`Promise`\<`TransactionRequest`\>

#### depositERC20()

> **depositERC20**: (`l1Token`,`l2Token`,`amount`,`opts`?,`isEstimatingGas`) =>`Promise`\<`TransactionRequest`\>

生成一笔交易，将一些 ERC20 代币存入 L2 链。

##### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 令牌的地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 令牌的地址。

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

存入金额。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

• **isEstimatingGas?**: `boolean`=`false`

##### Returns

`Promise`\<`TransactionRequest`\>

#### depositETH()

> **depositETH**: (`amount`,`opts`?,`isEstimatingGas`) =>`Promise`\<`TransactionRequest`\>

生成一笔交易，将一些 ETH 存入 L2 链。

##### Parameters

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

存入的 ETH 金额。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

• **isEstimatingGas?**: `boolean`=`false`

##### Returns

`Promise`\<`TransactionRequest`\>

#### proveAndRelayMessage()

> **proveAndRelayMessage**: (`message`,`opts`?) =>`Promise`\<`TransactionRequest`\>

生成一条消息，证明并中继可以签名和执行的交易。仅有的
适用于 L2 到 L1 消息。

##### Parameters

• **message**: [`MessageLike`](../type-aliases/MessageLike.md)

用于生成证明交易的消息。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

##### Returns

`Promise`\<`TransactionRequest`\>

#### sendMessage()

> **sendMessage**: (`message`,`opts`?) =>`Promise`\<`TransactionRequest`\>

生成发送给定跨链消息的交易。这笔交易可以签署
并由签名者执行。

##### Parameters

• **message**: [`CrossChainMessageRequest`](../interfaces/CrossChainMessageRequest.md)

跨链消息发送。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

##### Returns

`Promise`\<`TransactionRequest`\>

#### withdrawERC20()

> **withdrawERC20**: (`l1Token`,`l2Token`,`amount`,`opts`?,`isEstimatingGas`?) =>`Promise`\<`TransactionRequest`\>

生成一笔交易，将一些 ERC20 代币提取回 L1 链。

##### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 令牌的地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 令牌的地址。

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

提取金额。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

• **isEstimatingGas?**: `boolean`

##### Returns

`Promise`\<`TransactionRequest`\>

#### withdrawETH()

> **withdrawETH**: (`amount`,`opts`?,`isEstimatingGas`?) =>`Promise`\<`TransactionRequest`\>

生成一笔交易，将一些 ETH 提取回 L1 链。

##### Parameters

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

要提取的 ETH 数量。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

• **isEstimatingGas?**: `boolean`

##### Returns

`Promise`\<`TransactionRequest`\>

#### Source

src/cross-chain-messenger.ts:1304

## Accessors

### l1Provider

>`get` **l1Provider**(): `Provider`

连接到 L1 链的提供商。

#### Returns

`Provider`

#### Source

src/cross-chain-messenger.ts:193

***

### l1Signer

>`get` **l1Signer**(): `Signer`

连接到 L1 链的签名者。

#### Returns

`Signer`

#### Source

src/cross-chain-messenger.ts:215

***

### l2Provider

>`get` **l2Provider**(): `Provider`

连接到 L2 链的提供商。

#### Returns

`Provider`

#### Source

src/cross-chain-messenger.ts:204

***

### l2Signer

>`get` **l2Signer**(): `Signer`

连接到 L2 链的签名者。

#### Returns

`Signer`

#### Source

src/cross-chain-messenger.ts:226

## Methods

### approval()

> **批准**(`l1Token`,`l2Token`,`opts`?): `Promise`\<`BigNumber`\>

查询账户对给定 L1 代币的批准金额。

#### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 代币地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 代币地址。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

#### Returns

`Promise`\<`BigNumber`\>

批准从账户存款的代币数量。

#### Source

src/cross-chain-messenger.ts:1214

***

### approveERC20()

> **批准ERC20**(`l1Token`,`l2Token`,`amount`,`opts`?): `Promise`\<`TransactionResponse`\>

批准存入 L2 链。

#### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 代币地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 代币地址。

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

要批准的代币数量。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

#### Returns

`Promise`\<`TransactionResponse`\>

批准交易的交易响应。

#### Source

src/cross-chain-messenger.ts:1233

***

### depositERC20()

> **充值ERC20**(`l1Token`,`l2Token`,`amount`,`opts`?): `Promise`\<`TransactionResponse`\>

将一些 ERC20 代币存入 L2 链。

#### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 令牌的地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 令牌的地址。

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

存入金额。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

#### Returns

`Promise`\<`TransactionResponse`\>

存款交易的交易响应。

#### Source

src/cross-chain-messenger.ts:1256

***

### depositETH()

> **存入ETH**(`amount`,`opts`?): `Promise`\<`TransactionResponse`\>

将一些 ETH 存入 L2 链。

#### Parameters

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

存入的 ETH 数量（以 wei 为单位）。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

#### Returns

`Promise`\<`TransactionResponse`\>

存款交易的交易响应。

#### Source

src/cross-chain-messenger.ts:1183

***

### encodeFunctionMessage()

> **编码函数消息**(`options`): `string`

L2CrossDomainMessenger合约编码消息，例如hashCrossDomainMessagev1

#### Parameters

• **选项**

• **options.message**: `string`

消息随跨域消息一起传递

• **options.messageNonce**: `BigNumber`

跨域消息随机数

• **options.sender**: `string`

跨域消息的发送者

• **options.target**: `string`

跨域消息的目标

• **options.value**: `BigNumber`

与跨域消息一起发送的值

#### Returns

`string`

#### Source

src/cross-chain-messenger.ts:972

***

### estimateL2MessageGasLimit()

> **估计L2MessageGasLimit**(`message`,`opts`?): `Promise`\<`BigNumber`\>

估计在 L2 上完全执行给定消息所需的 Gas 量。仅适用于
L1 => L2 消息。您可以在向 L2 发送消息时提供此 Gas 限制。

#### Parameters

• **message**: [`MessageRequestLike`](../type-aliases/MessageRequestLike.md)

消息获取气体估计。

• **选择？**

选项对象。

• **opts.bufferPercent?**: `number`

添加到估计值中的气体百分比。默认为 20。

• **opts.from?**: `string`

用作发件人的地址。

#### Returns

`Promise`\<`BigNumber`\>

估计 L2 气体限制。

#### Source

src/cross-chain-messenger.ts:918

***

### getBackendTreeSyncIndex()

> **getBackendTreeSyncIndex**(): `Promise`\<`number`\>

#### Returns

`Promise`\<`number`\>

#### Source

src/cross-chain-messenger.ts:1122

***

### getBridgeForTokenPair()

> **getBridgeForTokenPair**(`l1Token`,`l2Token`): `Promise`\<[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md)\>

为给定的 L1 - L2 令牌对查找适当的桥接适配器。如果没有桥梁就会抛出
支持令牌对，或者如果多个网桥支持令牌对。

#### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1代币地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 代币地址。

#### Returns

`Promise`\<[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md)\>

适用于给定令牌对的桥接适配器。

#### Source

src/cross-chain-messenger.ts:378

***

### getCommittedL2BlockNumber()

> **getCommittedL2BlockNumber**(): `Promise`\<`any`\>

#### Returns

`Promise`\<`any`\>

#### Source

src/cross-chain-messenger.ts:995

***

### getDepositsByAddress()

> **通过地址获取存款**(`address`,`opts`): `Promise`\<[`TokenBridgeMessage`](../interfaces/TokenBridgeMessage.md)[]\>

获取给定地址的所有存款。

#### Parameters

• **address**: [`AddressLike`](../type-aliases/AddressLike.md)

从中搜索消息的地址。

• **选择**=`{}`

选项对象。

• **opts.fromBlock?**: `BlockTag`

阻止开始搜索消息。如果未提供，将启动
从第一个块（块#0).

• **opts.toBlock?**: `BlockTag`

阻止停止搜索消息。如果未提供，将停止在
最新已知块（“最新”）。

#### Returns

`Promise`\<[`TokenBridgeMessage`](../interfaces/TokenBridgeMessage.md)[]\>

由给定地址发送的所有存款代币桥接消息。

#### Source

src/cross-chain-messenger.ts:424

***

### getFinalizedL2BlockNumber()

> **getFinalizedL2BlockNumber**(): `Promise`\<`any`\>

#### Returns

`Promise`\<`any`\>

#### Source

src/cross-chain-messenger.ts:1017

***

### getMessageReceipt()

> **获取消息收据**(`message`,`opts`): `Promise`\<[`MessageReceipt`](../interfaces/MessageReceipt.md)\>

查找执行特定跨链消息的交易的收据。

#### Parameters

• **message**: [`MessageLike`](../type-aliases/MessageLike.md)

消息查找收据。

• **选择**=`{}`

• **opts.direction?**: [`MessageDirection`](../enumerations/MessageDirection.md)

#### Returns

`Promise`\<[`MessageReceipt`](../interfaces/MessageReceipt.md)\>

CrossChainMessage 收据包括中继交易的收据
给出的消息。

#### Source

src/cross-chain-messenger.ts:757

***

### getMessageStatus()

> **获取消息状态**(`message`,`opts`): `Promise`\<[`MessageStatus`](../enumerations/MessageStatus.md)\>

以枚举形式检索特定消息的状态。

#### Parameters

• **message**: [`MessageLike`](../type-aliases/MessageLike.md)

跨链消息检查状态。

• **选择**=`{}`

• **opts.direction?**: [`MessageDirection`](../enumerations/MessageDirection.md)

#### Returns

`Promise`\<[`MessageStatus`](../enumerations/MessageStatus.md)\>

消息的状态。

#### Source

src/cross-chain-messenger.ts:634

***

### getMessagesByTransaction()

> **通过交易获取消息**(`transaction`,`opts`): `Promise`\<[`CrossChainMessage`](../interfaces/CrossChainMessage.md)[]\>

检索给定交易中发送的所有跨链消息。

#### Parameters

• **transaction**: [`TransactionLike`](../type-aliases/TransactionLike.md)

用于查找消息的交易哈希或收据。

• **选择**=`{}`

选项对象。

• **opts.direction?**: [`MessageDirection`](../enumerations/MessageDirection.md)

搜索消息的方向。如果未提供，将尝试
假设交易哈希只会自动搜索两个方向
存在于一条链上。如果哈希值在两条链上都存在，则会抛出错误。

#### Returns

`Promise`\<[`CrossChainMessage`](../interfaces/CrossChainMessage.md)[]\>

交易内发送的所有跨链消息。

#### Source

src/cross-chain-messenger.ts:244

***

### getProvenWithdrawal()

> **getProvenWithdrawal**(`withdrawalHash`): `Promise`\<[`ProvenWithdrawal`](../interfaces/ProvenWithdrawal.md)\>

查询L1CrossDomainMessenger合约的`provenWithdrawals`映射
对于与传递的withdrawalHash相匹配的ProvenWithdrawal

#### Parameters

• **withdrawalHash**: `string`

#### Returns

`Promise`\<[`ProvenWithdrawal`](../interfaces/ProvenWithdrawal.md)\>

ProvenWithdrawal 对象

#### Source

src/cross-chain-messenger.ts:957

***

### getWithdrawMessageProof()

> **getWithdrawMessageProof**(`message`): `Promise`\<[`WithdrawMessageProof`](../interfaces/WithdrawMessageProof.md)\>

生成完成 L2 到 L1 消息所需的证明。

#### Parameters

• **message**: [`MessageLike`](../type-aliases/MessageLike.md)

用于生成证明的消息。

#### Returns

`Promise`\<[`WithdrawMessageProof`](../interfaces/WithdrawMessageProof.md)\>

可用于最终确定消息的证明。

#### Source

src/cross-chain-messenger.ts:1042

***

### getWithdrawalsByAddress()

> **按地址获取提款**(`address`,`opts`): `Promise`\<[`TokenBridgeMessage`](../interfaces/TokenBridgeMessage.md)[]\>

获取给定地址的所有提款。

#### Parameters

• **address**: [`AddressLike`](../type-aliases/AddressLike.md)

从中搜索消息的地址。

• **选择**=`{}`

选项对象。

• **opts.fromBlock?**: `BlockTag`

阻止开始搜索消息。如果未提供，将启动
从第一个块（块#0).

• **opts.toBlock?**: `BlockTag`

阻止停止搜索消息。如果未提供，将停止在
最新已知块（“最新”）。

#### Returns

`Promise`\<[`TokenBridgeMessage`](../interfaces/TokenBridgeMessage.md)[]\>

由给定地址发送的所有提款令牌桥消息。

#### Source

src/cross-chain-messenger.ts:458

***

### proveAndRelayMessage()

> **证明并中继消息**(`message`,`opts`?): `Promise`\<`TransactionResponse`\>

证明并中继从 L2 发送到 L1 的跨链消息。仅适用于L2至L1
消息。

#### Parameters

• **message**: [`MessageLike`](../type-aliases/MessageLike.md)

消息最终确定。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

#### Returns

`Promise`\<`TransactionResponse`\>

完成交易的交易响应。

#### Source

src/cross-chain-messenger.ts:1163

***

### sendMessage()

> **发送消息**(`message`,`opts`?): `Promise`\<`TransactionResponse`\>

发送给定的跨链消息。消息发送到哪里取决于所附的指示
到消息本身。

#### Parameters

• **message**: [`CrossChainMessageRequest`](../interfaces/CrossChainMessageRequest.md)

跨链消息发送。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

#### Returns

`Promise`\<`TransactionResponse`\>

消息发送事务的事务响应。

#### Source

src/cross-chain-messenger.ts:1143

***

### toCrossChainMessage()

> **toCrossChainMessage**(`message`,`opts`?): `Promise`\<[`CrossChainMessage`](../interfaces/CrossChainMessage.md)\>

将 MessageLike 解析为 CrossChainMessage 对象。
与其他强制函数不同，此函数是有状态的，需要额外进行
请求。现在我将把这个函数保留在这里，但我们可以考虑放一个
如果人们想使用它而不必使用 utils/coercion.ts 中的类似功能
创建一个完整的 CrossChainProvider 对象。

#### Parameters

• **message**: [`MessageLike`](../type-aliases/MessageLike.md)

MessageLike 解析为 CrossChainMessage。

• **选择？**

• **opts.direction?**: [`MessageDirection`](../enumerations/MessageDirection.md)

#### Returns

`Promise`\<[`CrossChainMessage`](../interfaces/CrossChainMessage.md)\>

消息被强制转换为 CrossChainMessage。

#### Source

src/cross-chain-messenger.ts:491

***

### toLowLevelMessage()

> **到低级消息**(`message`,`opts`?): `Promise`\<[`LowLevelMessage`](../type-aliases/LowLevelMessage.md)\>

将 CrossChainMessenger 消息转换为其内部的低级表示
L2 上的 L2ToL1MessagePasser 合约。

#### Parameters

• **message**: [`MessageLike`](../type-aliases/MessageLike.md)

消息要转变。

• **选择？**

• **opts.direction?**: [`MessageDirection`](../enumerations/MessageDirection.md)

#### Returns

`Promise`\<[`LowLevelMessage`](../type-aliases/LowLevelMessage.md)\>

转换后的消息。

#### Source

src/cross-chain-messenger.ts:326

***

### waitBatchFinalize()

> **等待BatchFinalize**(`transactionHash`): `Promise`\<`void`\>

#### Parameters

• **transactionHash**: `string`

#### Returns

`Promise`\<`void`\>

#### Source

src/cross-chain-messenger.ts:600

***

### waitForMessageReceipt()

> **等待消息接收**(`message`,`opts`): `Promise`\<[`MessageReceipt`](../interfaces/MessageReceipt.md)\>

等待消息执行并返回已执行交易的收据
给定的消息。

#### Parameters

• **message**: [`MessageLike`](../type-aliases/MessageLike.md)

等待消息。

• **选择**=`{}`

传递给等待函数的选项。

• **opts.confirmations?**: `number`

返回之前等待的交易确认数。

• **opts.pollIntervalMs?**: `number`

轮询收据之间等待的毫秒数。

• **opts.timeoutMs?**: `number`

超时前等待的毫秒数。

#### Returns

`Promise`\<[`MessageReceipt`](../interfaces/MessageReceipt.md)\>

CrossChainMessage 收据包括中继交易的收据
给出的消息。

#### Source

src/cross-chain-messenger.ts:802

***

### waitForMessageStatus()

> **等待消息状态**(`message`,`status`,`opts`): `Promise`\<`void`\>

等待，直到给定消息的状态更改为预期状态。请注意，如果
给定消息的状态更改为暗示预期状态的状态，这将
还是回来。如果消息的状态更改为排除预期的状态
状态，这将引发错误。

#### Parameters

• **message**: [`MessageLike`](../type-aliases/MessageLike.md)

等待消息。

• **status**: [`MessageStatus`](../enumerations/MessageStatus.md)

消息的预期状态。

• **选择**=`{}`

传递给等待函数的选项。

• **opts.direction?**: [`MessageDirection`](../enumerations/MessageDirection.md)

• **opts.pollIntervalMs?**: `number`

轮询时等待的毫秒数。

• **opts.timeoutMs?**: `number`

超时前等待的毫秒数。

#### Returns

`Promise`\<`void`\>

#### Source

src/cross-chain-messenger.ts:840

***

### waitRollupSuccess()

> **等待Rollup成功**(`transactionHash`): `Promise`\<`void`\>

#### Parameters

• **transactionHash**: `string`

#### Returns

`Promise`\<`void`\>

#### Source

src/cross-chain-messenger.ts:552

***

### waitSyncSuccess()

> **等待同步成功**(`transactionHash`): `Promise`\<`void`\>

#### Parameters

• **transactionHash**: `string`

#### Returns

`Promise`\<`void`\>

#### Source

src/cross-chain-messenger.ts:576

***

### withdrawERC20()

> **提取ERC20**(`l1Token`,`l2Token`,`amount`,`opts`?): `Promise`\<`TransactionResponse`\>

将一些 ERC20 代币撤回 L1 链。

#### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 令牌的地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 令牌的地址。

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

提取金额。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

#### Returns

`Promise`\<`TransactionResponse`\>

提款交易的交易响应。

#### Source

src/cross-chain-messenger.ts:1282

***

### withdrawETH()

> **提取ETH**(`amount`,`opts`?): `Promise`\<`TransactionResponse`\>

将一些 ETH 提取回 L1 链。

#### Parameters

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

要提取的 ETH 数量。

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

#### Returns

`Promise`\<`TransactionResponse`\>

提款交易的交易响应。

#### Source

src/cross-chain-messenger.ts:1198
