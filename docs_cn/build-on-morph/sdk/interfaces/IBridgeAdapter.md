[**@morph-l2/sdk**](../globals.md)• **文档**

***

[@morph-l2/sdk](../globals.md)/ IBridge适配器

# Interface: IBridgeAdapter

表示 L1 - L2 令牌桥的适配器。每个定制桥目前都需要自己的
适配器，因为桥接口不是标准化的。这在未来可能会改变。

## Properties

### estimateGas

> **estimateGas**: `object`

包含估计给定交易所需气体的函数的对象。
遵循 ethers.js 使用的模式。

#### approve()

估计批准一些代币存入 L2 链所需的天然气。

##### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 代币地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 代币地址。

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

要批准的代币数量。

• **opts?**: [`IActionOptions`](IActionOptions.md)

附加选项。

##### Returns

`Promise`\<`BigNumber`\>

交易的 Gas 估算。

#### deposit()

估计将一些代币存入 L2 链所需的天然气。

##### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 代币地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 代币地址。

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

要存入的代币金额。

• **opts?**: [`IActionOptions`](IActionOptions.md)

附加选项。

##### Returns

`Promise`\<`BigNumber`\>

交易的 Gas 估算。

#### withdraw()

估计将一些代币提取回 L1 链所需的天然气。

##### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 代币地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 代币地址。

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

要提取的代币数量。

• **opts?**: [`IActionOptions`](IActionOptions.md)

附加选项。

##### Returns

`Promise`\<`BigNumber`\>

交易的 Gas 估算。

#### Source

src/interfaces/bridge-adapter.ts:221

***

### l1Bridge

> **l1Bridge**: `Contract`

L1桥梁合同。

#### Source

src/interfaces/bridge-adapter.ts:38

***

### l2Bridge

> **l2Bridge**: `Contract`

L2桥合同。

#### Source

src/interfaces/bridge-adapter.ts:43

***

### messenger

> **messenger**: [`CrossChainMessenger`](../classes/CrossChainMessenger.md)

Provider 用于进行与跨链交互相关的查询。

#### Source

src/interfaces/bridge-adapter.ts:33

***

### populateTransaction

> **populateTransaction**: `object`

包含生成由用户签名的交易的函数的对象。
遵循 ethers.js 使用的模式。

#### approve()

生成一个交易，用于批准一些代币存入 L2 链。

##### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 代币地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 代币地址。

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

要批准的代币数量。

• **opts?**: [`IActionOptions`](IActionOptions.md)

附加选项。

##### Returns

`Promise`\<`TransactionRequest`\>

可以签署并执行以存入代币的交易。

#### deposit()

生成一个交易，将一些代币存入 L2 链。

##### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 代币地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 代币地址。

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

要存入的代币金额。

• **opts?**: [`IActionOptions`](IActionOptions.md)

附加选项。

##### Returns

`Promise`\<`TransactionRequest`\>

可以签署并执行以存入代币的交易。

#### withdraw()

生成一笔交易，将一些代币提取回 L1 链。

##### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 代币地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 代币地址。

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

要提取的代币数量。

• **opts?**: [`IActionOptions`](IActionOptions.md)

附加选项。

##### Returns

`Promise`\<`TransactionRequest`\>

可以签署并执行以提取代币的交易。

#### Source

src/interfaces/bridge-adapter.ts:167

## Methods

### approval()

> **批准**(`l1Token`,`l2Token`,`opts`?): `Promise`\<`BigNumber`\>

查询账户对给定 L1 代币的批准金额。

#### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 代币地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 代币地址。

• **opts?**: [`IActionOptions`](IActionOptions.md)

附加选项。

#### Returns

`Promise`\<`BigNumber`\>

批准从账户存款的代币数量。

#### Source

src/interfaces/bridge-adapter.ts:103

***

### approve()

> **批准**(`l1Token`,`l2Token`,`amount`,`signer`,`opts`?): `Promise`\<`TransactionResponse`\>

批准存入 L2 链。

#### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 代币地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 代币地址。

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

要批准的代币数量。

• **signer**: `Signer`

签名者用于签名并发送交易。

• **opts?**: [`IActionOptions`](IActionOptions.md)

附加选项。

#### Returns

`Promise`\<`TransactionResponse`\>

批准交易的交易响应。

#### Source

src/interfaces/bridge-adapter.ts:119

***

### deposit()

> **存款**(`l1Token`,`l2Token`,`amount`,`signer`,`opts`?): `Promise`\<`TransactionResponse`\>

将一些代币存入 L2 链。

#### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 代币地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 代币地址。

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

要存入的代币金额。

• **signer**: `Signer`

签名者用于签名并发送交易。

• **opts?**: [`IActionOptions`](IActionOptions.md)

附加选项。

#### Returns

`Promise`\<`TransactionResponse`\>

存款交易的交易响应。

#### Source

src/interfaces/bridge-adapter.ts:137

***

### getDepositsByAddress()

> **通过地址获取存款**(`address`,`opts`?): `Promise`\<[`TokenBridgeMessage`](TokenBridgeMessage.md)[]\>

获取给定地址的所有存款。

#### Parameters

• **address**: [`AddressLike`](../type-aliases/AddressLike.md)

从中搜索消息的地址。

• **选择？**

选项对象。

• **opts.fromBlock?**: `BlockTag`

阻止开始搜索消息。如果未提供，将启动
从第一个块（块#0).

• **opts.toBlock?**: `BlockTag`

阻止停止搜索消息。如果未提供，将停止在
最新已知块（“最新”）。

#### Returns

`Promise`\<[`TokenBridgeMessage`](TokenBridgeMessage.md)[]\>

由给定地址发送的所有存款代币桥接消息。

#### Source

src/interfaces/bridge-adapter.ts:56

***

### getWithdrawalsByAddress()

> **按地址获取提款**(`address`,`opts`?): `Promise`\<[`TokenBridgeMessage`](TokenBridgeMessage.md)[]\>

获取给定地址的所有提款。

#### Parameters

• **address**: [`AddressLike`](../type-aliases/AddressLike.md)

从中搜索消息的地址。

• **选择？**

选项对象。

• **opts.fromBlock?**: `BlockTag`

阻止开始搜索消息。如果未提供，将启动
从第一个块（块#0).

• **opts.toBlock?**: `BlockTag`

阻止停止搜索消息。如果未提供，将停止在
最新已知块（“最新”）。

#### Returns

`Promise`\<[`TokenBridgeMessage`](TokenBridgeMessage.md)[]\>

由给定地址发送的所有提款令牌桥消息。

#### Source

src/interfaces/bridge-adapter.ts:75

***

### supportsTokenPair()

> **支持TokenPair**(`l1Token`,`l2Token`): `Promise`\<`boolean`\>

检查桥是否支持给定的令牌对。

#### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 代币地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 代币地址。

#### Returns

`Promise`\<`boolean`\>

桥是否支持给定的令牌对。

#### Source

src/interfaces/bridge-adapter.ts:90

***

### withdraw()

> **撤回**(`l1Token`,`l2Token`,`amount`,`signer`,`opts`?): `Promise`\<`TransactionResponse`\>

将一些代币撤回到L1链。

#### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 代币地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 代币地址。

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

要提取的代币数量。

• **signer**: `Signer`

签名者用于签名并发送交易。

• **opts?**: [`IActionOptions`](IActionOptions.md)

附加选项。

#### Returns

`Promise`\<`TransactionResponse`\>

提款交易的交易响应。

#### Source

src/interfaces/bridge-adapter.ts:155
