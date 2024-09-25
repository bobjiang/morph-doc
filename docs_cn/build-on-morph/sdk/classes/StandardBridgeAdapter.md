[**@morph-l2/sdk**](../globals.md)• **文档**

***

[@morph-l2/sdk](../globals.md)/ 标准桥接适配器

# Class: StandardBridgeAdapter

适用于任何使用标准令牌桥接口的令牌桥的桥适配器。

## Extended by

-[`ETHBridgeAdapter`](ETHBridgeAdapter.md)

## Implements

-[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md)

## Constructors

### new StandardBridgeAdapter()

> **新的标准桥适配器**(`opts`): [`StandardBridgeAdapter`](StandardBridgeAdapter.md)

创建一个 StandardBridgeAdapter 实例。

#### Parameters

• **选择**

适配器的选项。

• **opts.l1Bridge**: [`AddressLike`](../type-aliases/AddressLike.md)

L1桥梁合同。

• **opts.l2Bridge**: [`AddressLike`](../type-aliases/AddressLike.md)

L2桥合同。

• **opts.messenger**: [`CrossChainMessenger`](CrossChainMessenger.md)

Provider 用于进行与跨链交互相关的查询。

#### Returns

[`StandardBridgeAdapter`](StandardBridgeAdapter.md)

#### Source

src/adapters/standard-bridge.ts:52

## Properties

### estimateGas

> **estimateGas**: `object`

包含估计给定交易所需气体的函数的对象。
遵循 ethers.js 使用的模式。

#### approve()

> **approve**: (`l1Token`,`l2Token`,`amount`,`opts`?) =>`Promise`\<`BigNumber`\>

##### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

##### Returns

`Promise`\<`BigNumber`\>

#### deposit()

> **deposit**: (`l1Token`,`l2Token`,`amount`,`opts`?) =>`Promise`\<`BigNumber`\>

##### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

##### Returns

`Promise`\<`BigNumber`\>

#### withdraw()

> **withdraw**: (`l1Token`,`l2Token`,`amount`,`opts`?) =>`Promise`\<`BigNumber`\>

##### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

##### Returns

`Promise`\<`BigNumber`\>

#### Implementation of

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`estimateGas`](../interfaces/IBridgeAdapter.md#estimategas)

#### Source

src/adapters/standard-bridge.ts:405

***

### l1Bridge

> **l1Bridge**: `Contract`

L1桥梁合同。

#### Implementation of

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`l1Bridge`](../interfaces/IBridgeAdapter.md#l1bridge)

#### Source

src/adapters/standard-bridge.ts:41

***

### l2Bridge

> **l2Bridge**: `Contract`

L2桥合同。

#### Implementation of

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`l2Bridge`](../interfaces/IBridgeAdapter.md#l2bridge)

#### Source

src/adapters/standard-bridge.ts:42

***

### messenger

> **messenger**: [`CrossChainMessenger`](CrossChainMessenger.md)

Provider 用于进行与跨链交互相关的查询。

#### Implementation of

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`messenger`](../interfaces/IBridgeAdapter.md#messenger)

#### Source

src/adapters/standard-bridge.ts:40

***

### populateTransaction

> **populateTransaction**: `object`

包含生成由用户签名的交易的函数的对象。
遵循 ethers.js 使用的模式。

#### approve()

> **approve**: (`l1Token`,`l2Token`,`amount`,`opts`?) =>`Promise`\<`TransactionRequest`\>

##### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

##### Returns

`Promise`\<`TransactionRequest`\>

#### deposit()

> **deposit**: (`l1Token`,`l2Token`,`amount`,`opts`?) =>`Promise`\<`TransactionRequest`\>

##### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

##### Returns

`Promise`\<`TransactionRequest`\>

#### withdraw()

> **withdraw**: (`l1Token`,`l2Token`,`amount`,`opts`?) =>`Promise`\<`TransactionRequest`\>

##### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

##### Returns

`Promise`\<`TransactionRequest`\>

#### Implementation of

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`populateTransaction`](../interfaces/IBridgeAdapter.md#populatetransaction)

#### Source

src/adapters/standard-bridge.ts:286

## Methods

### approval()

> **批准**(`l1Token`,`l2Token`,`opts`): `Promise`\<`BigNumber`\>

查询账户对给定 L1 代币的批准金额。

#### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L1 代币地址。

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L2 代币地址。

• **opts**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

#### Returns

`Promise`\<`BigNumber`\>

批准从账户存款的代币数量。

#### Implementation of

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`approval`](../interfaces/IBridgeAdapter.md#approval)

#### Source

src/adapters/standard-bridge.ts:209

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

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

#### Returns

`Promise`\<`TransactionResponse`\>

批准交易的交易响应。

#### Implementation of

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`approve`](../interfaces/IBridgeAdapter.md#approve-2)

#### Source

src/adapters/standard-bridge.ts:250

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

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

#### Returns

`Promise`\<`TransactionResponse`\>

存款交易的交易响应。

#### Implementation of

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`deposit`](../interfaces/IBridgeAdapter.md#deposit-2)

#### Source

src/adapters/standard-bridge.ts:262

***

### getDepositsByAddress()

> **通过地址获取存款**(`address`,`opts`?): `Promise`\<[`TokenBridgeMessage`](../interfaces/TokenBridgeMessage.md)[]\>

获取给定地址的所有存款。

#### Parameters

• **address**: [`AddressLike`](../type-aliases/AddressLike.md)

从中搜索消息的地址。

• **选择？**

选项对象。

• **opts.fromBlock?**: `BlockTag`

• **opts.toBlock?**: `BlockTag`

#### Returns

`Promise`\<[`TokenBridgeMessage`](../interfaces/TokenBridgeMessage.md)[]\>

由给定地址发送的所有存款代币桥接消息。

#### Implementation of

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`getDepositsByAddress`](../interfaces/IBridgeAdapter.md#getdepositsbyaddress)

#### Source

src/adapters/standard-bridge.ts:75

***

### getWithdrawalsByAddress()

> **按地址获取提款**(`address`,`opts`?): `Promise`\<[`TokenBridgeMessage`](../interfaces/TokenBridgeMessage.md)[]\>

获取给定地址的所有提款。

#### Parameters

• **address**: [`AddressLike`](../type-aliases/AddressLike.md)

从中搜索消息的地址。

• **选择？**

选项对象。

• **opts.fromBlock?**: `BlockTag`

• **opts.toBlock?**: `BlockTag`

#### Returns

`Promise`\<[`TokenBridgeMessage`](../interfaces/TokenBridgeMessage.md)[]\>

由给定地址发送的所有提款令牌桥消息。

#### Implementation of

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`getWithdrawalsByAddress`](../interfaces/IBridgeAdapter.md#getwithdrawalsbyaddress)

#### Source

src/adapters/standard-bridge.ts:122

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

#### Implementation of

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`supportsTokenPair`](../interfaces/IBridgeAdapter.md#supportstokenpair)

#### Source

src/adapters/standard-bridge.ts:165

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

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

附加选项。

#### Returns

`Promise`\<`TransactionResponse`\>

提款交易的交易响应。

#### Implementation of

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`withdraw`](../interfaces/IBridgeAdapter.md#withdraw-2)

#### Source

src/adapters/standard-bridge.ts:274
