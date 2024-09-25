[**@morph-l2/sdk**](../globals.md)• **文档**

***

[@morph-l2/sdk](../globals.md)/ ETHBridge适配器

# Class: ETHBridgeAdapter

ETH 桥接器的桥接适配器。

## Extends

-[`StandardBridgeAdapter`](StandardBridgeAdapter.md)

## Constructors

### new ETHBridgeAdapter()

> **新的 ETHBridgeAdapter**(`opts`): [`ETHBridgeAdapter`](ETHBridgeAdapter.md)

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

[`ETHBridgeAdapter`](ETHBridgeAdapter.md)

#### Inherited from

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`constructor`](StandardBridgeAdapter.md#constructors)

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

#### Inherited from

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`estimateGas`](StandardBridgeAdapter.md#estimategas)

#### Source

src/adapters/standard-bridge.ts:405

***

### l1Bridge

> **l1Bridge**: `Contract`

L1桥梁合同。

#### Inherited from

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`l1Bridge`](StandardBridgeAdapter.md#l1bridge)

#### Source

src/adapters/standard-bridge.ts:41

***

### l2Bridge

> **l2Bridge**: `Contract`

L2桥合同。

#### Inherited from

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`l2Bridge`](StandardBridgeAdapter.md#l2bridge)

#### Source

src/adapters/standard-bridge.ts:42

***

### messenger

> **messenger**: [`CrossChainMessenger`](CrossChainMessenger.md)

Provider 用于进行与跨链交互相关的查询。

#### Inherited from

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`messenger`](StandardBridgeAdapter.md#messenger)

#### Source

src/adapters/standard-bridge.ts:40

***

### populateTransaction

> **populateTransaction**: `object`

包含生成由用户签名的交易的函数的对象。
遵循 ethers.js 使用的模式。

#### approve()

> **approve**: (`l1Token`,`l2Token`,`amount`,`opts`?) =>`Promise`\<`never`\>

##### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

##### Returns

`Promise`\<`never`\>

#### deposit()

> **deposit**: (`l1Token`,`l2Token`,`amount`,`opts`) =>`Promise`\<`TransactionRequest`\>

##### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

• **opts**: [`IActionOptions`](../interfaces/IActionOptions.md)

##### Returns

`Promise`\<`TransactionRequest`\>

#### withdraw()

> **withdraw**: (`l1Token`,`l2Token`,`amount`,`opts`) =>`Promise`\<`TransactionRequest`\>

##### Parameters

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

• **opts**: [`IActionOptions`](../interfaces/IActionOptions.md)

##### Returns

`Promise`\<`TransactionRequest`\>

#### Overrides

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`populateTransaction`](StandardBridgeAdapter.md#populatetransaction)

#### Source

src/adapters/eth-bridge.ts:116

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

#### Overrides

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`approval`](StandardBridgeAdapter.md#approval)

#### Source

src/adapters/eth-bridge.ts:22

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

#### Inherited from

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`approve`](StandardBridgeAdapter.md#approve-2)

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

#### Inherited from

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`deposit`](StandardBridgeAdapter.md#deposit-2)

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

#### Overrides

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`getDepositsByAddress`](StandardBridgeAdapter.md#getdepositsbyaddress)

#### Source

src/adapters/eth-bridge.ts:30

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

#### Overrides

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`getWithdrawalsByAddress`](StandardBridgeAdapter.md#getwithdrawalsbyaddress)

#### Source

src/adapters/eth-bridge.ts:64

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

#### Overrides

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`supportsTokenPair`](StandardBridgeAdapter.md#supportstokenpair)

#### Source

src/adapters/eth-bridge.ts:105

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

#### Inherited from

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`withdraw`](StandardBridgeAdapter.md#withdraw-2)

#### Source

src/adapters/standard-bridge.ts:274
